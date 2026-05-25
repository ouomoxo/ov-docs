---
title: 릴리스 노트
layout: default
nav_order: 8
permalink: /changelog/
---

# 릴리스 노트

각 버전의 의미 있는 변경 사항. 형식은 [Keep a Changelog](https://keepachangelog.com/) 1.1을 따릅니다.

> 다운로드: [GitHub Releases](https://github.com/ouomoxo/ov-releases/releases)

---

## [1.2.0] — UX & 접근성 · FTUE 전면 강화

### Added
- **인터랙티브 투어** — 첫 실행 시 8단계 spotlight 투어가 실제 UI를 강조하며 사용자를 안내. 액션 자동 감지 + 1.5초 ✓ 셀러브레이션
- **공용 primitive 6종**: `Kbd`, `EmptyState`, `Tooltip`, `BaseModal`, `Toast`, `useFocusTrap` 훅
- **인앱 도움말 시스템**
  - `⌘/` 글로벌 단축키 시트 — Navigation/View/Editing/Copilot/Help 5개 카테고리
  - 우측 레일 `?` → 도움말 메뉴 (가이드 노트 5개 점프, 온보딩 재시작, 외부 docs 링크)
- **Toast 알림 시스템** — alert 5건을 우하단 toast로. info/success/error + 자동 dismiss + 액션 버튼
- **사이드바 가상화** — 1000+ 노트 vault에서 60fps. drag 중 가장자리 auto-scroll, 600ms hover로 폴더 자동 펼침
- **EmptyState 적용** — Sidebar / MainPanel / Table / Kanban
- **외부 문서 사이트** — [ouomoxo.github.io/ov-docs](https://ouomoxo.github.io/ov-docs/) (이 사이트!)

### Changed
- 모든 모달이 `BaseModal` 또는 `useFocusTrap` — aria-modal, focus trap, scroll lock, Esc 동작 통일
- 슬래시 메뉴 desc 한국어 확장 + Callout 색상 의미 명시
- inline `<kbd>` → `<Kbd>` 컴포넌트로 통일
- 에러 메시지 헬퍼 `formatErrorMessage` — `[무엇] · [왜] · [어떻게]` 한국어 템플릿

### Fixed
- `ChatMessage`에서 hook의 조건부 호출 (rules-of-hooks 위반)
- HelpMenu popover가 화면 하단에서 잘리던 문제 — viewport-aware positioning

---

## [1.1.0] — 보안 · 안정성 · 접근성 베이스라인

### Added
- **API 키 / Copilot 히스토리 OS 키체인 암호화** (Electron `safeStorage`)
- **전역 ErrorBoundary** + 패널별 inline 보호
- **mtime 충돌 모달** — 외부 편집기와 동시 수정 시 덮어쓰기 / 외부 변경 불러오기 / 취소
- **종료 시 unsaved 가드** — 저장 안 한 탭 있으면 native 확인 다이얼로그
- **atomic write** — tmp + fsync + rename 패턴
- **path traversal 방어** — `assertVaultRoot` + `safeJoin` (15곳)
- **`attachment:readExternal` 화이트리스트** — pickFiles 결과만 1회용 허용
- **autoUpdater** (`electron-updater`) + **GitHub Actions CI**
- **Playwright e2e smoke 테스트**
- **ESLint + Prettier + LICENSE (MIT)**

### Changed
- CSP 좁힘 — `script-src 'self'`, `connect-src 'self' ws: wss:`
- IframeEmbed `allow-popups` 제거
- 모든 vault IPC 핸들러가 atomic write + path 검증

### Removed
- 평문 `ai.apiKey` localStorage 저장
- `minisearch` deps (사용 안 됨)

---

## [1.0.0] — OV 첫 출시

### Added
- NewWorld → OV 브랜드
- 8단계 첫 진입 온보딩 (슬라이드쇼)
- AI Copilot + 13개 tool calling (read/propose 분리, 모든 변경 사용자 승인)
- 외부 링크 오버레이, 캘린더 Day view + Schedule → Todo 브릿지
- Light / Dark 테마
- 파일 비밀번호 / 앱 비밀번호 보안 (PBKDF2 + AES-GCM)
- 마크다운 입력 룰 + TipTap 블록 에디터 + 슬래시 메뉴 + 콜아웃/토글/임베드
