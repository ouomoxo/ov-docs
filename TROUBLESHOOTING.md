---
title: 문제 해결
layout: default
nav_order: 6
permalink: /troubleshooting/
---

# 문제 해결
{: .no_toc }

흔히 마주치는 문제와 해결 방법.

<details open markdown="block">
  <summary>이 페이지에서</summary>

* TOC
{:toc}
</details>

---

## 앱이 시작되지 않음

### macOS: "Apple에서 확인할 수 없는 개발자" 차단

OV 1.2 이상은 코드 서명 + notarization을 진행했지만 만약 그래도 차단된다면:

1. `시스템 환경설정 → 개인 정보 보호 및 보안` 열기
2. 스크롤해서 "OV.app이 차단되었습니다" 메시지 찾기
3. **이대로 열기** → 비밀번호 입력 → 확인

또는 터미널에서:

```bash
xattr -d com.apple.quarantine /Applications/OV.app
```

### Windows: SmartScreen 차단

"Microsoft Defender SmartScreen이 인식할 수 없는 앱을 실행하지 못하도록 했습니다" 화면이 나오면:

1. **추가 정보** 클릭
2. **실행** 버튼 표시됨 → 클릭

OV는 Authenticode 서명을 받았지만 EV 인증서가 아니라서 reputation이 쌓이기 전까지 이 경고가 나올 수 있어요.

### Linux: AppImage 실행 권한

```bash
chmod +x OV-{version}.AppImage
./OV-{version}.AppImage
```

만약 `fuse` 관련 에러:

```bash
sudo apt install fuse libfuse2     # Ubuntu / Debian
sudo dnf install fuse fuse-libs    # Fedora
```

---

## Vault 관련

### "No vault is currently open" 에러

Vault 폴더가 이동/삭제되었거나, 첫 실행 시 vault 선택을 안 한 경우. 사이드바(`⌘B`)에서 **Vault 열기** 클릭 → 폴더 선택.

### 외부에서 노트를 수정했는데 OV가 인식 못 함

chokidar(파일 워처)가 잠시 멈춘 경우. 사이드바 헤더에서 새로고침 또는 `⌘R` (앱 리로드 — 저장 안 된 변경 있으면 확인 뜸).

### vault 폴더 권한 거부

macOS의 "Full Disk Access"가 필요한 폴더(예: `~/Library`)에 vault를 두면 권한 거부 토스트가 뜹니다. `~/Documents/` 같은 일반 폴더로 옮기는 걸 권장.

### iCloud 동기화 vault에서 충돌

OV는 외부 변경(iCloud sync)을 mtime으로 감지하고 충돌 모달을 띄워요:
- **내 변경사항으로 덮어쓰기** — 다른 기기 변경 사라짐
- **외부 변경 불러오기** — 내 변경 사라짐
- **취소** — 결정 미루기, 그대로 두기

iCloud 충돌이 자주 발생하면 동기화 폴더가 아닌 일반 폴더 사용을 고려하세요.

---

## 에디터 관련

### 슬래시 메뉴 (`/`)가 안 열려요

- 빈 줄에서 `/`를 눌러야 합니다 (텍스트 중간에선 그냥 슬래시 문자 입력)
- 한글 IME 입력 중에는 글자 조합 중 — 한 번 ESC 또는 Enter 후 다시 시도

### 마크다운이 자동 변환 안 됨

빈 줄의 시작에서:
- `# ` 다음 띄어쓰기 → H1
- `- ` 다음 띄어쓰기 → 글머리 목록
- `> ` 다음 띄어쓰기 → 인용문
- ` ``` ` 3개 → 코드 블록

기존 텍스트가 있는 줄에서는 자동 변환되지 않아요. 슬래시 메뉴를 쓰세요.

### 위키링크 자동완성이 안 떠요

`[[`를 연속으로 두 번 입력해야 popup이 뜹니다. 한글 IME가 활성화된 경우, IME composition 끝난 후 시도하세요.

---

## AI Copilot

### "API 키가 설정되지 않았습니다"

설정(`⌘,`) → **AI Copilot** 탭 → API key 필드에 OpenAI API 키 입력 → **저장**.

키가 저장됐다면 "키체인에 저장됨" 표시가 떠요.

### "Bad Request" 또는 "401 Unauthorized"

- API 키가 잘못됐거나 만료됨 — OpenAI 대시보드에서 새 키 발급
- 결제 정보 미등록 — OpenAI는 free trial 종료 후 결제 정보 필요

### Copilot이 응답 도중 멈춤

채팅 입력창 오른쪽의 **■ 중단** 버튼으로 강제 중단. 다음 메시지 보내면 새로 시작됩니다.

### Copilot이 vault 정보를 잘못 가져옴

vault index가 stale일 수 있어요. 사이드바 새로고침 또는 `⌘R`로 앱 리로드.

---

## 보안 / 비밀번호

### App password를 잊어버렸어요

복구 불가능합니다. 다만 vault 폴더 자체는 평문 마크다운이라 데이터 손실 없이 *앱 재설치* 후 같은 vault를 다시 열 수 있어요:

1. OV 종료
2. `~/Library/Application Support/OV/` (macOS) 또는 `%APPDATA%/OV/` (Windows) 폴더 삭제 — 설정 초기화
3. OV 재실행 → 같은 vault 폴더 선택 → App password 다시 등록

### File password로 잠근 노트가 안 열려요

- 비밀번호가 정확한지 확인 (Caps Lock 등)
- 힌트가 등록되어 있다면 잠금 다이얼로그에서 힌트 표시 가능
- 비밀번호 모르면 **복구 불가능** (AES-GCM-256은 brute-force 안 됨)

자세한 건 [보안 가이드](./security/) 참고.

---

## 자동 업데이트

### 업데이트가 적용되지 않음

- 인터넷 연결 확인
- GitHub Releases에 새 버전이 실제 공개됐는지 확인
- macOS는 quarantine 속성이 새 버전에서 다시 붙을 수 있어요 — [위의 macOS 섹션](#macos-apple에서-확인할-수-없는-개발자-차단) 참고

### 수동 업데이트

[Releases 페이지](https://github.com/ouomoxo/ov-releases/releases/latest)에서 최신 버전 다운로드 → 기존 앱 위에 설치. Vault와 설정은 그대로 유지됩니다.

---

## 성능

### 큰 vault에서 사이드바가 느려요

1000+ 노트 vault는 사이드바 가상화로 60fps 유지. 만약 그래도 느리면:
- 외부 동기화 폴더(iCloud, Dropbox)가 너무 자주 변경 알림을 보내는지 확인
- `.attachments/`에 큰 파일이 많으면 vault 인덱싱이 느려질 수 있음 — 별도 폴더로 옮기기

### 에디터가 큰 노트에서 끊김

- 100KB 이상 단일 노트는 분할 권장 — 위키링크로 연결
- 이미지/영상 첨부가 많은 노트는 잘게 쪼개기

### Copilot 응답이 느림

- OpenAI API 자체 latency — 대화 history가 길수록 input tokens 많아짐
- 새 채팅(`+`)으로 시작하면 context가 짧아져 빨라짐

---

## 그 외

### 로그를 어디서 보나요?

Electron renderer 콘솔: 개발 빌드(`npm run dev`)에서는 자동 오픈, 프로덕션 빌드에서는 `Cmd+Opt+I` (macOS) / `Ctrl+Shift+I` (Win/Linux)로 열 수 있습니다.

Main process 로그는 터미널에서 OV를 실행하면 stdout에 표시:

```bash
# macOS
/Applications/OV.app/Contents/MacOS/OV
```

### Crash dump 위치

- macOS: `~/Library/Application Support/OV/Crashpad/completed/`
- Windows: `%APPDATA%/OV/Crashpad/completed/`
- Linux: `~/.config/OV/Crashpad/completed/`

OV는 dump를 자동으로 어디에도 보내지 않아요. 버그 신고 시 직접 첨부해주세요.

### 그래도 해결이 안 돼요

[GitHub Issues](https://github.com/ouomoxo/ov-releases/issues/new)에 다음 정보와 함께 신고해주세요:

- OS + 버전 (예: macOS 14.5, Apple Silicon)
- OV 버전 (설정 → About 또는 메뉴바)
- 재현 단계
- 콘솔 로그 (가능하면)
- 스크린샷
