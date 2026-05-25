---
title: 홈
layout: default
nav_order: 1
permalink: /
description: 로컬 마크다운 + 노션식 UX + AI Copilot을 한 곳에. OV의 공식 문서.
---

<section class="hero" markdown="0">
  <div class="hero__logo" aria-hidden="true"></div>
  <div class="hero__eyebrow">OV Documentation</div>
  <h1 class="hero__title">로컬 마크다운을<br>노션처럼 쓰는 방법.</h1>
  <p class="hero__lede">
    OV는 데이터를 당신 컴퓨터에 두면서, 노션식 블록 에디터와 vault를 이해하는 AI Copilot을 더한 데스크탑 노트 앱이에요. 이 사이트는 처음 사용자를 위한 공식 가이드입니다.
  </p>

  <div class="cta-row">
    <a class="cta-btn cta-btn-primary" href="https://github.com/ouomoxo/ov-releases/releases/latest">
      {% include icon.html name="download" size="16" %}
      OV 다운로드
    </a>
    <a class="cta-btn cta-btn-secondary" href="./install/">설치 가이드</a>
    <a class="cta-btn cta-btn-secondary" href="./guide/">사용자 가이드</a>
  </div>
</section>

<div class="pill-row">
  <span class="pill">{% include icon.html name="folder" size="14" %} 로컬 마크다운</span>
  <span class="pill">{% include icon.html name="file-text" size="14" %} 블록 에디터</span>
  <span class="pill">{% include icon.html name="database" size="14" %} 데이터베이스 뷰</span>
  <span class="pill">{% include icon.html name="sparkles" size="14" %} AI Copilot</span>
  <span class="pill">{% include icon.html name="lock" size="14" %} 키체인 암호화</span>
  <span class="pill">{% include icon.html name="palette" size="14" %} Light · Dark</span>
</div>

<div class="screenshot editor-mock" aria-label="OV 에디터 화면 미리보기" role="img" markdown="0">
  <div class="screenshot__caption">에디터 미리보기</div>
  <div class="editor-mock__body">
    <div class="editor-mock__rail">
      <span></span><span></span><span></span><span></span><span></span>
    </div>
    <div class="editor-mock__sidebar">
      <div class="editor-mock__folder"></div>
      <div class="editor-mock__file"></div>
      <div class="editor-mock__file editor-mock__file--active"></div>
      <div class="editor-mock__file"></div>
      <div class="editor-mock__folder"></div>
      <div class="editor-mock__file"></div>
      <div class="editor-mock__file"></div>
    </div>
    <div class="editor-mock__main">
      <div class="editor-mock__h1"></div>
      <div class="editor-mock__meta"></div>
      <div class="editor-mock__line editor-mock__line--90"></div>
      <div class="editor-mock__line editor-mock__line--80"></div>
      <div class="editor-mock__line editor-mock__line--65"></div>
      <div class="editor-mock__bullet"><i></i></div>
      <div class="editor-mock__bullet"><i></i></div>
      <div class="editor-mock__bullet"><i></i></div>
      <div class="editor-mock__line editor-mock__line--40"></div>
    </div>
    <div class="editor-mock__props">
      <div class="editor-mock__prop"><i></i></div>
      <div class="editor-mock__prop"><i></i></div>
      <div class="editor-mock__prop"><i></i></div>
      <div class="editor-mock__prop"><i></i></div>
    </div>
  </div>
</div>

## 핵심 기능
{: .section-head }

<div class="feature-grid" markdown="0">
  <a class="feature-card" href="./guide/#1-vault--노트를-저장하는-폴더">
    <div class="feature-card__icon">{% include icon.html name="folder" size="22" %}</div>
    <div class="feature-card__title">로컬 우선</div>
    <div class="feature-card__body">모든 노트는 평범한 <code>.md</code> 파일. Obsidian / iA Writer / VS Code와 그대로 호환. 데이터 잠금 없음.</div>
  </a>

  <a class="feature-card" href="./guide/#2-마크다운-작성">
    <div class="feature-card__icon">{% include icon.html name="file-text" size="22" %}</div>
    <div class="feature-card__title">블록 에디터</div>
    <div class="feature-card__body">TipTap 기반. 슬래시(<code>/</code>) 메뉴, 콜아웃, 토글, 임베드, 위키링크가 자연스럽게 흐름에 녹아듭니다.</div>
  </a>

  <a class="feature-card" href="./guide/#4-데이터베이스-뷰-2">
    <div class="feature-card__icon">{% include icon.html name="database" size="22" %}</div>
    <div class="feature-card__title">데이터베이스 뷰</div>
    <div class="feature-card__body">frontmatter 속성이 자동으로 컬럼이 돼요. Table · Kanban · Calendar 세 가지 뷰로 전환.</div>
  </a>

  <a class="feature-card" href="./guide/#5-캘린더--일정">
    <div class="feature-card__icon">{% include icon.html name="calendar" size="22" %}</div>
    <div class="feature-card__title">캘린더 + Day view</div>
    <div class="feature-card__body"><code>date</code> 필드를 가진 노트들이 캘린더로. 시간 슬롯 Day view에 NOW 라인까지.</div>
  </a>

  <a class="feature-card" href="./guide/#6-ai-copilot-j">
    <div class="feature-card__icon">{% include icon.html name="sparkles" size="22" %}</div>
    <div class="feature-card__title">AI Copilot</div>
    <div class="feature-card__body">vault를 읽고 변경을 <strong>제안</strong>. 모든 적용은 diff 확인 후 사용자 승인. 자동 수정 없음.</div>
  </a>

  <a class="feature-card" href="./guide/#7-보안">
    <div class="feature-card__icon">{% include icon.html name="shield" size="22" %}</div>
    <div class="feature-card__title">프라이버시 우선</div>
    <div class="feature-card__body">Telemetry 없음. API 키는 OS 키체인 암호화. 자세한 건 <a href="./privacy/">Privacy</a>.</div>
  </a>
</div>

## 시작하기
{: .section-head }

<div class="feature-grid" markdown="0">
  <a class="feature-card feature-card--compact" href="./install/">
    <div class="feature-card__icon">{% include icon.html name="download" size="18" %}</div>
    <div class="feature-card__text">
      <div class="feature-card__title">1. 설치 & 첫 실행</div>
      <div class="feature-card__body">macOS / Windows / Linux 단계별 가이드.</div>
    </div>
  </a>
  <a class="feature-card feature-card--compact" href="./guide/">
    <div class="feature-card__icon">{% include icon.html name="file-text" size="18" %}</div>
    <div class="feature-card__text">
      <div class="feature-card__title">2. 사용자 가이드</div>
      <div class="feature-card__body">vault부터 Copilot까지 10 섹션.</div>
    </div>
  </a>
  <a class="feature-card feature-card--compact" href="./shortcuts/">
    <div class="feature-card__icon">{% include icon.html name="keyboard" size="18" %}</div>
    <div class="feature-card__text">
      <div class="feature-card__title">3. 단축키 외우기</div>
      <div class="feature-card__body">⌘K · ⌘P · ⌘J · ⌘/ 부터.</div>
    </div>
  </a>
</div>

## 자주 찾는 페이지
{: .section-head }

<div class="feature-grid" markdown="0">
  <a class="feature-card feature-card--compact" href="./faq/">
    <div class="feature-card__icon">{% include icon.html name="help-circle" size="18" %}</div>
    <div class="feature-card__text">
      <div class="feature-card__title">자주 묻는 질문</div>
      <div class="feature-card__body">설치·보안·Copilot Q&amp;A.</div>
    </div>
  </a>
  <a class="feature-card feature-card--compact" href="./troubleshooting/">
    <div class="feature-card__icon">{% include icon.html name="alert-triangle" size="18" %}</div>
    <div class="feature-card__text">
      <div class="feature-card__title">문제 해결</div>
      <div class="feature-card__body">잘 안 될 때 확인할 것들.</div>
    </div>
  </a>
  <a class="feature-card feature-card--compact" href="./colors/">
    <div class="feature-card__icon">{% include icon.html name="palette" size="18" %}</div>
    <div class="feature-card__text">
      <div class="feature-card__title">색상 도감</div>
      <div class="feature-card__body">Callout 5색의 의미.</div>
    </div>
  </a>
  <a class="feature-card feature-card--compact" href="./changelog/">
    <div class="feature-card__icon">{% include icon.html name="git-branch" size="18" %}</div>
    <div class="feature-card__text">
      <div class="feature-card__title">릴리스 노트</div>
      <div class="feature-card__body">v1.0 → v1.1 → v1.2.</div>
    </div>
  </a>
  <a class="feature-card feature-card--compact" href="./privacy/">
    <div class="feature-card__icon">{% include icon.html name="lock" size="18" %}</div>
    <div class="feature-card__text">
      <div class="feature-card__title">프라이버시</div>
      <div class="feature-card__body">데이터가 어디로 가는지, 안 가는지.</div>
    </div>
  </a>
  <a class="feature-card feature-card--compact" href="https://github.com/ouomoxo/ov-releases/issues">
    <div class="feature-card__icon">{% include icon.html name="git-branch" size="18" %}</div>
    <div class="feature-card__text">
      <div class="feature-card__title">버그 신고 / 토론</div>
      <div class="feature-card__body">GitHub Issues로 알려주세요.</div>
    </div>
  </a>
</div>

---

OV는 로컬 우선, 오픈 데이터, telemetry 없는 노트 앱이에요. 좋은 글쓰기 되세요.
