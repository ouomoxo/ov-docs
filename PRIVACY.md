---
title: 프라이버시
layout: default
nav_order: 10
permalink: /privacy/
---

# 프라이버시

OV는 **local-first** 노트 앱입니다. Telemetry 없음, analytics 없음, 광고 없음. 이 문서는 OV가 무엇을, 언제, 어디로 보내는지(혹은 안 보내는지)에 대한 단일 진실 소스예요.

---

## 한줄 요약

> OV가 외부와 통신하는 경우는 단 두 가지: **(1) 당신이 AI Copilot을 사용할 때 OpenAI API에 직접 호출**, **(2) 시작 시 GitHub에서 새 버전 확인**. 그 외엔 어떤 데이터도 외부로 나가지 않습니다.

---

## 외부 네트워크 활동

### 1. AI Copilot (당신이 활성화한 경우만)

- 호출 대상: `https://api.openai.com/v1/chat/completions`
- 호출 주체: OV의 main 프로세스 (renderer가 직접 API에 안 닿음)
- 보내는 데이터: 시스템 프롬프트 + vault 요약(파일 목록) + 활성 노트 메타데이터(이름, 크기, **본문 X**) + 당신의 채팅 입력 + AI가 `read_note` 도구 호출 시 그 시점에만 본문
- 인증: 당신의 OpenAI API 키 (OS 키체인에 암호화 저장)
- OV 서버 경유 안 함 — OpenAI로 직접

**Copilot을 끄려면**: 설정에서 API 키 입력 안 하거나 제거. Copilot 패널 자체는 "키 없음" 상태로 비활성.

### 2. Auto-update 체크

- 호출 대상: `https://api.github.com/repos/ouomoxo/ov-releases/releases/latest`
- 빈도: 앱 시작 시 1회 + 그 후 6시간마다
- 보내는 데이터: GitHub API 요청 헤더(User-Agent: `OV/{version}`) — 사용자 식별 정보 없음
- 새 버전이 있으면 백그라운드 다운로드 → 다음 종료 시 적용

**자동 업데이트를 끄려면**: 설정 → General → "Check for updates automatically" 토글 OFF (v1.3 예정).

### 3. 외부 링크 클릭

본문의 `http://` / `https://` 링크를 클릭하면 OS 기본 브라우저로 엽니다(`shell.openExternal`). OV가 직접 fetch하지 않아요.

---

## 로컬에만 저장되는 것

### Vault (`~/Documents/OV/` 또는 사용자 지정)
- 모든 `.md` 노트 파일
- 노트 본문, frontmatter, 첨부파일
- 평범한 마크다운 — 다른 도구로도 열림

### 앱 데이터 (`~/Library/Application Support/OV/` 또는 OS 동등 위치)
- `state.json` — 마지막 vault 경로, 최근 vault 목록
- `secure/ai.apiKey.enc` — OpenAI API 키 (OS 키체인으로 암호화)
- `secure/ov.copilot.enc` — Copilot 채팅 히스토리 (암호화)
- `Crashpad/` — 크래시 minidump (자동 전송 안 함)

### Renderer 로컬스토리지
- `ov.settings` — UI 설정 (테마, daily folder 경로 등 — *비밀이 아닌* 환경 설정)
- `ov.ui` — 사이드바 너비, 펼침 폴더 등

---

## 보내지 *않는* 것

- ❌ 사용 통계 (어떤 기능을 썼는지)
- ❌ 오류 보고 (crash dump는 로컬 보관만, 자동 전송 X)
- ❌ 노트 내용 (Copilot read_note 외)
- ❌ vault 위치
- ❌ IP / 디바이스 식별자
- ❌ 광고/마케팅용 데이터 일체

---

## 데이터 삭제

- **OV 제거**: macOS는 휴지통으로 드래그. Windows는 제어판/설정에서 제거. Linux는 AppImage 파일 삭제.
- **앱 데이터까지 완전 삭제**: 위 "앱 데이터" 경로의 폴더를 직접 삭제. vault는 별도 삭제 필요.
- **vault 삭제**: 그냥 vault 폴더를 지우면 됩니다. OV가 만든 hidden 메타데이터 같은 건 없어요.

---

## 오픈소스

OV의 모든 외부 통신 코드는 [GitHub](https://github.com/ouomoxo/ov-releases) (릴리스 + 문서)에서 공개되어 있습니다. 메인 소스 코드는 현재 비공개지만 향후 공개 예정. 보안 우려가 있다면 직접 확인하거나 보안 리뷰 issue를 열어주세요.

---

## 변경사항

이 정책의 변경은 [CHANGELOG](./changelog/)에 명시됩니다. *마지막 갱신: 2026-05-25 (v1.2.0)*.
