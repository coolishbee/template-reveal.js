# AGENTS.md

## 프로젝트 개요

순수 정적(static) HTML/CSS 기반의 reveal.js v5.2.1 프레젠테이션. 빌드 과정 없음.
커맨드(Command) & 옵저버(Observer) 디자인 패턴 게임 실무 적용 소개용 한국어 발표 자료.

## 핵심 명령어

```bash
# 개발 서버 실행 (로컬 HTTP 서버 필수 — file:// 직접 열기 불가)
npm start        # → npx serve .  (http://localhost:3000)

# 의존성 설치
npm install      # reveal.js v5.2.1 설치
```

> `yarn.lock`과 `package-lock.json` 둘 다 존재. npm을 기본으로 사용.

## 파일 구조

```
index.html          ← 유일한 앱 진입점 + 모든 슬라이드 내용
styles.css          ← 커스텀 스타일 (FHD 1920×1080 최적화)
design pattern.md   ← 슬라이드 원본 콘텐츠 초안 (참고용)
public/             ← 이미지 에셋
  command/
    command-bg.png  ← 커맨드 패턴 커버 슬라이드 전체 화면 배경 (data-background-image)
    command-01.png  ← ICommand→Command object→Stack→Invoker 흐름도 (정의 슬라이드 보조)
    command-02.png  ← Command Queue 구조 (Undo/Redo index 설명)
    command-03.png  ← Undo stack / Redo stack Push·Pop 구조 (장단점 슬라이드 보조)
    command-04.png  ← UML: InputManager→CommandInvoker→ICommand→MoveCommand→PlayerMover
    command-05.png  ← (미사용) UML 단순화 버전
  observer/
    observer-bg.png ← 옵저버 패턴 커버 슬라이드 전체 화면 배경 (data-background-image)
    observer-01.png ← Subject→Observer 3개 개념도 (정의·장단점 슬라이드 보조)
    observer-02.png ← UML: Subject ↔ Observer1, Observer2 (C# 이벤트 방식)
  logo_*.webp       ← 회사 로고 4종
node_modules/reveal.js/  ← 로컬에서 직접 참조 (CDN 아님)
```

## 아키텍처 주의사항

- **별도 JS/TS 파일 없음.** 모든 슬라이드 내용은 `index.html` 단일 파일에 포함.
- reveal.js를 CDN이 아닌 `node_modules/`에서 직접 참조 → `node_modules/` 삭제 시 동작 안 함.
- 이미지 경로는 `public/` 기준 (`public/command/command-bg.png` 등). `design pattern.md` 초안의 경로(`command/...`)는 그대로 쓰면 404 — 반드시 `public/` 접두어 붙일 것.
- **mermaid 미사용.** UML은 모두 `public/` 폴더 내 이미지로 표현. CDN 스크립트 없음.
- 커버 슬라이드(`page-cover`)는 `data-background-image` / `data-background-size="cover"` 속성으로 전체 화면 배경 처리. 내부 콘텐츠 없음.

## 슬라이드 구성 (총 12장)

| # | CSS 클래스 | 내용 |
|---|---|---|
| 1 | `.page-1` | 인트로 — 부정적 시각 3가지 + 목차 5항목 |
| 2 | `.page-cover` | 커맨드 패턴 커버 — `command-bg.png` 전체 화면 |
| 3 | `.page-definition` | 커맨드 패턴 — 정의 + `command-01.png` 보조 |
| 4 | `.page-components` | 커맨드 패턴 — 구성요소 (Command / ConcreteCommand / Receiver / Invoker) |
| 5 | `.page-uml` | 커맨드 패턴 — UML (`command-04.png`) |
| 6 | `.page-pros-cons` | 커맨드 패턴 — 장단점 + `command-02.png` / `command-03.png` 보조 |
| 7 | `.page-cover` | 옵저버 패턴 커버 — `observer-bg.png` 전체 화면 |
| 8 | `.page-definition` | 옵저버 패턴 — 정의 + `observer-01.png` 보조 |
| 9 | `.page-components` | 옵저버 패턴 — 구성요소 (Subject / Observer / Notification) |
| 10 | `.page-uml` | 옵저버 패턴 — UML (`observer-02.png`) |
| 11 | `.page-pros-cons` | 옵저버 패턴 — 장단점 + `observer-01.png` 보조 |
| 12 | `.page-guide` | 선택 가이드 + Builder·State FSM 언급 + Q&A |

## reveal.js 운용

- 발표자 노트: `S` 키로 발표자 뷰 열기 (`<aside class="notes">` 태그)
- 플러그인: `RevealNotes`, `RevealHighlight`만 사용
- 전환 효과: `slide` (배경: `fade`), autoAnimate 0.8초

## 환경

- Node.js: `v24.12.0` (`.nvmrc` 참조)
- 테스트/린트/타입체크 없음. 빌드 아티팩트 없음.
- 한국어 프레젠테이션 (`lang="ko"`, Pretendard Variable 폰트 CDN 사용)
- FHD(1920×1080) 해상도 전용 스타일 — 다른 해상도에서는 레이아웃 어긋날 수 있음.
- 인터넷 연결 필요: Pretendard 폰트(CDN) 사용 중.
