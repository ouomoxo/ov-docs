---
title: 설치 & 첫 실행
layout: default
nav_order: 2
permalink: /install/
---

# 설치 & 첫 실행
{: .no_toc }

다운로드부터 첫 노트까지 5분.

<details open markdown="block">
  <summary>이 페이지에서</summary>

* TOC
{:toc}
</details>

---

## 다운로드

최신 릴리스는 [GitHub Releases](https://github.com/ouomoxo/ov-releases/releases/latest)에서 받을 수 있어요.

| 플랫폼 | 파일 | 비고 |
|---|---|---|
| **macOS (Apple Silicon)** | `OV-{version}-arm64.dmg` | M1/M2/M3/M4 |
| **macOS (Intel)** | `OV-{version}-x64.dmg` | Intel Mac |
| **Windows** | `OV-Setup-{version}.exe` | NSIS 설치 마법사 |
| **Linux** | `OV-{version}.AppImage` | 실행 권한 부여 후 더블클릭 |

> 💡 macOS는 Apple Silicon과 Intel용이 분리되어 있습니다. About this Mac에서 칩 정보를 확인하세요.

---

## macOS

### 1. DMG 열기

다운로드한 `.dmg` 파일을 더블클릭 → Finder 창에 OV.app이 나타나면 **Applications 폴더로 드래그**.

### 2. 첫 실행

Applications에서 OV.app 더블클릭. 첫 실행 시 **"Apple에서 확인할 수 없는 개발자"** 경고가 나올 수 있어요:

1. `시스템 환경설정 → 개인 정보 보호 및 보안` 열기
2. 아래쪽 "OV.app이 차단되었습니다" → **이대로 열기** 클릭
3. 한 번 허용하면 다음부터는 그냥 더블클릭으로 열림

{: .note }
> v1.2 이상은 Apple Developer ID로 코드 서명 + notarization을 진행했으니 위 경고가 없을 거예요.

### 3. 권한

OV는 vault 폴더(기본 `~/Documents/OV`)에 읽기/쓰기 권한이 필요합니다. macOS가 권한을 묻는 다이얼로그가 뜨면 **허용**.

---

## Windows

### 1. 설치

`OV-Setup-{version}.exe` 더블클릭 → 설치 마법사 따라가기. 설치 위치는 기본값(`C:\Users\<당신>\AppData\Local\Programs\OV`) 권장.

{: .warning }
> Windows SmartScreen이 "PC 보호" 화면을 띄울 수 있어요. **추가 정보 → 실행** 클릭하면 진행됩니다. (Authenticode 서명이 EV 인증서가 아니라서 그렇습니다 — 안전한 빌드입니다.)

### 2. 시작 메뉴

설치 후 시작 메뉴에서 "OV" 검색 → 실행. 또는 바탕화면 바로가기.

---

## Linux

### 1. AppImage

```bash
chmod +x OV-{version}.AppImage
./OV-{version}.AppImage
```

### 2. 데스크탑 통합 (선택)

[AppImageLauncher](https://github.com/TheAssassin/AppImageLauncher) 설치하면 자동으로 메뉴에 등록되고 업데이트도 수월합니다.

{: .note }
> Linux에서는 OS keychain(libsecret)이 없으면 `safeStorage` 암호화가 plain XOR로 fallback. GNOME Keyring 또는 KWallet 사용을 권장합니다.

---

## 첫 실행 후

앱이 처음 켜지면 **인터랙티브 투어**가 자동 시작됩니다. 8단계로:

1. 환영 → 다음
2. 사이드바 열기 (`⌘B`)
3. 새 노트 만들기 (사이드바 + 버튼)
4. 마크다운 / 슬래시 메뉴 (`/`)
5. 명령 팔레트 (`⌘K`)
6. AI Copilot (`⌘J`)
7. 도움말 (`?` 버튼)

투어를 건너뛰어도 우측 레일의 `?` → "온보딩 다시 보기"로 언제든 재실행할 수 있어요.

### Vault 위치

기본 vault는 `~/Documents/OV`에 생깁니다. 다른 폴더를 쓰고 싶으면:

1. 사이드바(`⌘B`) 열기
2. 사이드바 헤더의 **Vault 열기** 버튼
3. 원하는 폴더 선택

기존 Obsidian vault 폴더를 그대로 열어도 호환됩니다.

### 자동 업데이트

OV는 켜질 때 [GitHub Releases](https://github.com/ouomoxo/ov-releases/releases)에서 새 버전을 확인합니다. 있으면 백그라운드 다운로드 → 다음 종료 시 적용. 강제 종료 없이 안전합니다.

업데이트를 끄려면 설정에서 *Auto Update* 토글을 끄세요 (v1.3 예정).

---

## 다음 단계

- **[사용자 가이드](../guide/)** — 모든 기능 한 페이지에
- **[단축키](../shortcuts/)** — 핵심 단축키
- **[자주 묻는 질문](../faq/)** — FAQ
