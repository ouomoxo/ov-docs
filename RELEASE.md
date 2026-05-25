---
title: 릴리스 (개발자)
layout: default
nav_order: 9
permalink: /release/
---

# Release Guide

OV ships from the private `ouomoxo/ov` repo. Build artifacts (DMG / NSIS /
AppImage + `latest.yml`) are published to the **public** `ouomoxo/ov-releases`
repo, which is what the in-app autoUpdater fetches from.

This split lets us keep source private without breaking auto-update.

---

## One-time setup

### 1. GitHub PAT for cross-repo publishing

The default `GITHUB_TOKEN` granted to Actions in the private repo cannot write
to a different (public) repo. Create a fine-grained Personal Access Token with
**write access to `ouomoxo/ov-releases` only**, then add it as the
`RELEASE_TOKEN` secret on the private `ov` repo.

GitHub → Settings → Developer settings → Personal access tokens →
Fine-grained tokens → Generate new token:

- Repository access: only `ouomoxo/ov-releases`
- Permissions → Repository → **Contents: Read and write**
- Expiration: 1 year (rotate before expiry)

Add to `ov` repo: Settings → Secrets and variables → Actions → New secret →
`RELEASE_TOKEN` = `<token>`.

### 2. Apple Developer ID secrets (macOS signing + notarization)

| Secret | Source | Notes |
|---|---|---|
| `APPLE_ID` | Apple developer email | The Apple ID enrolled in Developer Program |
| `APPLE_APP_SPECIFIC_PASSWORD` | <https://appleid.apple.com> → Sign-In and Security → App-Specific Passwords | NEVER use account password |
| `APPLE_TEAM_ID` | <https://developer.apple.com/account> (10-char ID) | |
| `CSC_LINK` | `base64 < DeveloperID.p12` | The exported `Developer ID Application` cert |
| `CSC_KEY_PASSWORD` | password for the .p12 | Set on export |

Export the cert from Keychain Access on a machine that already has it:

```bash
# In Keychain Access → My Certificates → "Developer ID Application: <name> (TEAMID)"
# → File → Export Items → format: Personal Information Exchange (.p12)
base64 -i DeveloperID.p12 | pbcopy   # paste into GH secret CSC_LINK
```

### 3. Windows EV cert (optional)

| Secret | Source |
|---|---|
| `WIN_CSC_LINK` | base64-encoded `.pfx` |
| `WIN_CSC_KEY_PASSWORD` | `.pfx` password |

Without these, the NSIS installer still builds but Windows SmartScreen shows
"unknown publisher" on first install. README has a one-line user note about
clicking "More info → Run anyway".

---

## Cutting a release

```bash
# from the private ov repo
npm version 1.2.0        # bumps package.json + creates tag v1.2.0
git push --follow-tags   # triggers .github/workflows/release.yml
```

The Actions run:
1. Typecheck + lint + build on macOS / Windows / Linux runners in parallel
2. Signs + notarizes the Mac builds (uploads to Apple, waits, staples)
3. Uploads DMG / zip / NSIS / AppImage + `latest.yml` to a **draft** release
   on `ouomoxo/ov-releases`

### Publishing the release

The release lands as a **draft** by default. autoUpdater only sees published
non-prerelease tags, so:

1. Go to `https://github.com/ouomoxo/ov-releases/releases`
2. Edit the new draft → add changelog → uncheck "Set as a pre-release" → click
   **Publish release**

Within a few hours, existing installs will detect the new `latest.yml` and
prompt to install.

---

## Manual smoke test before publish

```bash
# Locally, after CI uploads the draft assets:
# 1. Download the .dmg from the draft release
# 2. On a Mac that does NOT have your dev cert:
#    - Double-click the .dmg, drag OV to /Applications, open it
#    - Confirm NO "developer cannot be verified" Gatekeeper warning
spctl -a -t exec -vv /Applications/OV.app   # expect: accepted, source=Notarized Developer ID
codesign -dv --verbose=4 /Applications/OV.app   # expect: Authority=Developer ID Application: …
```

If either fails, hold the release. Re-check the signing log in the Actions
run, especially the `Package (macOS)` step.

---

## Troubleshooting

**autoUpdater not finding new release**
- Check the release is **Published** (not draft, not prerelease) on `ov-releases`
- Check `latest.yml` is present among the assets
- Check `electron-builder.yml`: `publish.owner: ouomoxo`, `publish.repo: ov-releases`, `releaseType: release`

**Notarization upload fails with `Invalid credentials`**
- Re-issue the app-specific password (the one from `appleid.apple.com`)
- Confirm `APPLE_TEAM_ID` matches the Team your cert was issued under

**`unable to spawn osascript` or similar codesign errors on CI**
- Ensure `CSC_LINK` is base64 of the `.p12` (no `data:` prefix)
- Ensure `CSC_KEY_PASSWORD` is set and matches the export password

**`The release has not been published` from autoUpdater**
- The release is still a draft — publish it from the ov-releases UI

---

## Pre-release / beta builds

For a beta channel, tag with a prerelease suffix:

```bash
npm version 1.3.0-beta.1
git push --follow-tags
```

In `electron-builder.yml`, temporarily switch `publish.releaseType: prerelease`
(or maintain a separate yml). Public installs won't receive beta tags unless
they opt in via the autoUpdater channel (not yet wired — v1.3 work).
