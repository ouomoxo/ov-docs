---
title: 자주 묻는 질문
layout: default
nav_order: 5
permalink: /faq/
---

# 자주 묻는 질문
{: .no_toc }

<details open markdown="block">
  <summary>카테고리</summary>

* TOC
{:toc}
</details>

---

## 일반

### OV는 무료인가요?

네, 완전 무료에 오픈소스입니다. MIT 라이선스로 [GitHub](https://github.com/ouomoxo/ov-releases)에서 받을 수 있어요. 소스 코드는 현재 비공개(`ouomoxo/ov`)지만 릴리스 아티팩트와 문서는 공개입니다.

### Obsidian / Notion과 뭐가 달라요?

- **vs Obsidian**: OV는 Notion식 슬래시 메뉴, 데이터베이스 뷰(Table/Kanban/Calendar), 그리고 AI Copilot이 기본 포함. Obsidian은 강력한 플러그인 생태계가 강점.
- **vs Notion**: OV는 로컬 마크다운 파일 — 데이터가 당신 컴퓨터에 있고, Obsidian 같은 다른 도구로도 열 수 있어요. Notion은 클라우드 강점 + 협업.
- **공통**: 셋 다 "블록 기반 글쓰기" 패러다임.

### Telemetry 보내나요?

**없습니다.** OV는 어떤 사용 데이터도 외부로 보내지 않아요. 유일한 외부 네트워크 활동:
1. AI Copilot 사용 시 OpenAI API에 직접 호출 (당신의 키로)
2. 시작 시 GitHub Releases에서 새 버전 확인 (auto-update — 끌 수 있어요)

자세한 건 [Privacy](./privacy/) 참고.

---

## Vault & 데이터

### 노트는 어디에 저장되나요?

기본값: `~/Documents/OV/` (macOS/Linux) 또는 `C:\Users\<you>\Documents\OV\` (Windows). 모든 노트는 그 폴더 안의 평범한 `.md` 파일이에요. Finder/Explorer에서 직접 열어볼 수도 있어요.

### 여러 vault를 동시에 쓸 수 있나요?

지금은 한 번에 하나의 vault만 열 수 있어요. 다른 vault로 바꾸려면 사이드바의 "Vault 열기" 버튼. 최근 vault 목록은 명령 팔레트(`⌘K`)에서 빠르게 전환할 수 있어요.

### Obsidian / iCloud 폴더와 같이 써도 되나요?

**네.** 같은 폴더를 Obsidian과 OV에서 열어도 됩니다. OV는 외부 변경을 chokidar로 감지해서 자동 새로고침해요. iCloud Drive 같은 동기화 폴더도 가능 — 다만 두 기기에서 동시 편집 시 conflict 다이얼로그가 뜰 수 있어요 (안전하게 보호됩니다).

### 첨부파일(이미지/동영상)은 어디에?

vault 안의 `.attachments/` 폴더. 이미지/영상/파일을 에디터에 드래그-드롭/붙여넣기/슬래시 메뉴로 삽입하면 그 폴더에 복사되고 노트 본문엔 `ov-asset://` URL 또는 `[file](path)` 형식으로 저장됩니다.

### 백업은 어떻게?

vault 폴더가 곧 백업 단위입니다. Time Machine, Dropbox, Git 등 어떤 도구를 써도 되고, 별도 백업 기능은 일부러 만들지 않았어요 — 평범한 파일이라 OS 도구가 더 잘합니다.

---

## 마크다운 & 에디터

### 마크다운 문법을 외워야 하나요?

아니요. 빈 줄에서 `/`만 누르면 슬래시 메뉴가 떠서 모든 블록 타입을 고를 수 있어요. `#`/`##`/`-`/`>` 같은 자주 쓰는 건 자동 변환되긴 해요.

### 위키링크는 어떻게 쓰나요?

본문에서 `[[`를 누르면 자동완성 팝업이 뜹니다. 노트 이름을 입력하고 Enter. 예: `[[Welcome]]`. 백링크는 우측 정보 패널에서 확인할 수 있어요.

### Frontmatter는 뭔가요?

노트 맨 위의 YAML 블록입니다:

```yaml
---
status: in-progress
date: 2026-01-15
tags: [work, urgent]
---
```

이게 있으면 데이터베이스 뷰(`⌘2`)에서 자동으로 컬럼이 되고, `date` 필드가 있으면 캘린더에 표시됩니다. 노트 상단의 회색 영역(PropertyBar)에서 GUI로도 추가/편집할 수 있어요.

### 표 (Table) 삽입은?

슬래시 메뉴(`/`) → "표" 선택. 또는 `|` 셀 구분자로 직접 작성도 가능.

---

## AI Copilot

### 어떤 모델을 쓰나요?

기본 OpenAI `gpt-5.4-mini`. 설정에서 다른 모델로 바꿀 수 있어요. 향후 Anthropic Claude도 지원 예정.

### API 키는 어디에 저장되나요?

OS 키체인(macOS Keychain / Windows DPAPI / Linux libsecret)에 암호화되어 저장됩니다. `localStorage` 같은 평문 위치에는 절대 두지 않아요. 자세한 건 [보안 가이드](./security/) 참고.

### Copilot이 vault 파일을 수정해요?

직접 수정하지 않습니다. AI는 "이렇게 바꾸자"라는 *제안*만 만들고, 당신이 diff를 확인 후 직접 **Approve**를 눌러야 적용됩니다. 13개 도구 중 6개가 *propose* 도구(create/edit/rename/delete) — 모두 승인 게이트가 있어요.

### Copilot에 무엇을 보내나요?

- 시스템 프롬프트 (OV 사용법)
- vault 요약 (파일 목록, 폴더 구조 — 본문 X)
- 활성 노트의 메타데이터 (이름, 크기 — 본문 X)
- 당신이 채팅창에 입력한 텍스트
- AI가 `read_note` 도구를 호출하면 그때만 본문 일부

기본적으로 **노트 본문은 절대 자동 첨부되지 않아요**. AI가 명시적으로 요청해야 합니다.

### Copilot 없이 OV 쓸 수 있나요?

물론이죠. API 키를 안 넣으면 Copilot 패널은 그냥 "키 없음" 상태로 닫혀있고, 나머지 모든 기능은 정상 작동합니다.

---

## 보안 & 프라이버시

### App password와 File password 차이는?

- **App password**: 앱을 켤 때마다 한 번 입력. 잠금 해제 후엔 vault 안 모든 노트가 평소처럼 보임.
- **File password**: 노트 *개별*로 잠금. 사이드바에서 우클릭 → "잠금" → 그 노트만 AES-GCM-256으로 암호화. 같은 비밀번호로 모두 잠금/해제.

둘은 독립적입니다. 둘 다 켜면 — 앱 시작 시 App password, 잠긴 노트 열 때 File password.

### 비밀번호를 잊으면?

**복구 불가능합니다.** OV는 비밀번호를 어디에도 저장하지 않아요 (PBKDF2 해시만 가지고 있어요). File password로 잠긴 노트는 비밀번호 없이는 평문을 절대 볼 수 없습니다. 힌트(hint)를 미리 등록해두는 걸 권장합니다.

### Crash dump엔 뭐가 들어가요?

Electron이 만드는 minidump 파일은 OS 표준 형식의 *프로세스 상태 덤프*예요. 자동으로 어디에도 전송하지 않습니다. 위치는 [Privacy](./privacy/) 참고.

---

## 트러블슈팅

### 첫 실행에서 앱이 안 켜져요

- macOS: [설치 가이드](./install/#1-dmg-열기)의 "Apple에서 확인할 수 없는 개발자" 섹션 참고
- Windows: SmartScreen "추가 정보 → 실행"
- Linux: `chmod +x` 실행 권한 확인

자세한 트러블슈팅은 [문제 해결](./troubleshooting/) 페이지를 보세요.

### 외부 편집기와 동시 편집 시 충돌

OV는 같은 파일이 외부에서 변경되면 mtime 충돌 모달을 띄워요:
- **내 변경사항으로 덮어쓰기** — OV에서 입력한 게 우선
- **외부 변경 불러오기** — 외부 편집기 결과로 덮어씀
- **취소** — 일단 두고 결정 미루기

silent 데이터 손실은 절대 없습니다.

### 더 많은 질문

- [문제 해결](./troubleshooting/) — 흔한 이슈와 해결법
- [GitHub Issues](https://github.com/ouomoxo/ov-releases/issues) — 버그 신고
- [Discussions](https://github.com/ouomoxo/ov-releases/discussions) — 일반 질문
