# OV Documentation

> Notes, todos & ideas — Obsidian-style local markdown with Notion-grade UX.

이 저장소는 **OV** 데스크탑 노트 앱의 공식 문서입니다. GitHub Pages로 발행된 사이트는 [**ouomoxo.github.io/ov-docs**](https://ouomoxo.github.io/ov-docs/)에서 볼 수 있어요.

## 무엇을 담고 있나요

| 파일 | 내용 |
|---|---|
| [`index.md`](index.md) | 사이트 홈 — 환영 + 다운로드 |
| [`INSTALL.md`](INSTALL.md) | 플랫폼별 설치 가이드 |
| [`GUIDE.md`](GUIDE.md) | 사용자 가이드 (10 섹션) |
| [`SHORTCUTS.md`](SHORTCUTS.md) | 키보드 단축키 모음 |
| [`FAQ.md`](FAQ.md) | 자주 묻는 질문 |
| [`TROUBLESHOOTING.md`](TROUBLESHOOTING.md) | 문제 해결 |
| [`COLORS.md`](COLORS.md) | 색상 의미 도감 |
| [`CHANGELOG.md`](CHANGELOG.md) | 릴리스 노트 |
| [`PRIVACY.md`](PRIVACY.md) | 프라이버시 정책 |
| [`RELEASE.md`](RELEASE.md) | 개발자용 릴리스 가이드 |

## 기여 (오타·번역·예시 추가)

1. 이 저장소 fork
2. 마크다운 수정
3. PR 보내기 — 짧은 변경이라도 환영합니다

각 페이지 하단의 "이 페이지 수정 제안" 링크를 누르면 GitHub 에디터로 바로 갈 수 있어요.

## 빌드 (로컬 미리보기)

GitHub Pages가 자동 빌드하므로 로컬 빌드는 필수가 아니지만, 미리 보고 싶다면:

```bash
# Ruby + Bundler 필요
gem install bundler
bundle init
echo 'source "https://rubygems.org"' >> Gemfile
echo 'gem "github-pages"' >> Gemfile
bundle install
bundle exec jekyll serve
# → http://localhost:4000/ov-docs/
```

## 라이선스

문서는 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). OV 앱 자체는 [MIT](https://github.com/ouomoxo/ov-releases/blob/main/LICENSE).

## 관련 저장소

- [`ouomoxo/ov-releases`](https://github.com/ouomoxo/ov-releases) — 빌드 아티팩트 (DMG / NSIS / AppImage)
- `ouomoxo/ov` — 메인 소스 (현재 비공개)
