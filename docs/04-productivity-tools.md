# 04. 문서 작성 생산성 도구

[← 목차로 돌아가기](./00-index.md) | [← 이전: 03. 실전 작성 가이드](./03-practical-writing-guide.md)

---

### 핵심 요약

```
VS Code + Markdown 확장 + Mermaid 프리뷰 = 문서 작성 최적 환경
Claude Code의 CLAUDE.md 자동 로드 + 문서 참조 = 에이전트 연동 최적화
```

---

## 4.1 VS Code 확장 (Extensions)

### Markdown 관련

| 확장 | 용도 | 추천도 |
|------|------|--------|
| **Markdown All in One** | TOC 자동 생성, 단축키, 리스트 자동 포맷 | ★★★★★ |
| **Markdown Preview Enhanced** | 고급 프리뷰 (Mermaid 렌더링 포함) | ★★★★★ |
| **markdownlint** | Markdown 문법 린팅 | ★★★★☆ |
| **Paste Image** | 클립보드 이미지 자동 저장 및 링크 삽입 | ★★★☆☆ |

### Mermaid 관련

| 확장 | 용도 | 추천도 |
|------|------|--------|
| **Mermaid Markdown Syntax Highlighting** | 코드블록 내 Mermaid 문법 하이라이팅 | ★★★★★ |
| **Mermaid Chart** | VS Code 내에서 Mermaid 실시간 프리뷰 | ★★★★☆ |

### 추천 VS Code 설정

```json
// .vscode/settings.json
{
    "markdown.preview.breaks": true,
    "markdown.mermaid.enabled": true,
    "editor.wordWrap": "on",
    "[markdown]": {
        "editor.defaultFormatter": "yzhang.markdown-all-in-one",
        "editor.quickSuggestions": {
            "other": true,
            "comments": false,
            "strings": false
        }
    }
}
```

---

## 4.2 Claude Code 활용

### CLAUDE.md 자동 로드
- 프로젝트 루트의 `CLAUDE.md`는 세션 시작 시 자동으로 읽힘
- 하위 디렉토리의 `CLAUDE.md`는 해당 디렉토리 작업 시 추가 로드
- `~/.claude/CLAUDE.md`에 전역 설정 (모든 프로젝트에 공통 적용)

### 에이전트에게 문서 참조시키기

```bash
# 방법 1: 파일 경로 직접 언급
"docs/erd.md를 읽고 User 테이블에 대한 CRUD API를 만들어줘"

# 방법 2: 프로젝트 문서 일괄 참조
"docs/ 폴더의 PRD.md와 architecture.md를 읽고 
P0-3 '상품 검색' 기능을 구현해줘"

# 방법 3: 문서 업데이트 요청
"현재 코드 구조를 분석해서 CLAUDE.md를 업데이트해줘"
```

### Claude Code의 유용한 기능

| 기능 | 활용법 |
|------|--------|
| **멀티파일 편집** | "PRD의 P0 기능 3개를 한번에 구현해줘" → 여러 파일을 동시에 생성/수정 |
| **Git 연동** | "이 변경사항을 커밋하고 PR 설명도 작성해줘" |
| **코드 → 문서** | "현재 API 엔드포인트를 분석해서 api-spec.md를 생성해줘" |
| **문서 → 코드** | "erd.md를 기반으로 SQLAlchemy 모델을 생성해줘" |

---

## 4.3 AI 기반 문서 자동생성

### 코드 → 문서 생성

| 도구 | 용도 | 특징 |
|------|------|------|
| **Claude Code** | 코드 분석 → 문서 생성 | CLAUDE.md, API 명세 자동 생성 가능 |
| **GitHub Copilot** | 코드 주석 → 문서 | 인라인 문서 생성에 강점 |
| **Mintlify Doc Writer** | VS Code에서 docstring 자동 생성 | 함수/클래스 문서화 |

### 실전 워크플로우: 코드에서 문서 자동 생성

```bash
# 1. ERD 자동 생성 요청
"현재 DB 모델(models/ 폴더)을 분석해서 Mermaid ERD를 생성해줘.
docs/erd.md에 저장해줘."

# 2. API 명세 자동 생성 요청
"현재 라우터(routes/ 폴더)를 분석해서 API 명세서를 생성해줘.
각 엔드포인트의 메서드, 경로, 요청/응답 예시를 포함해줘.
docs/api-spec.md에 저장해줘."

# 3. 아키텍처 문서 자동 생성 요청
"프로젝트 구조를 분석해서 architecture.md를 작성해줘.
Mermaid 다이어그램으로 레이어 구조와 주요 컴포넌트 관계를 표현해줘."
```

---

## 4.4 다이어그램 도구 비교

| 도구 | 유형 | 에이전트 친화성 | Git 친화성 | 비용 |
|------|------|:---:|:---:|------|
| **Mermaid Live Editor** (mermaid.live) | 웹 기반 | ★★★★★ | ★★★★★ | 무료 |
| **Excalidraw** | 웹/VS Code | ★★★☆☆ | ★★★★☆ | 무료 |
| **draw.io** (diagrams.net) | 웹/데스크톱 | ★★☆☆☆ | ★★★☆☆ | 무료 |
| **Eraser.io** | 웹 기반 | ★★☆☆☆ | ★☆☆☆☆ | Freemium |
| **tldraw** | 웹 기반 | ★★☆☆☆ | ★★★☆☆ | 무료 |

### 추천 워크플로우

```mermaid
graph LR
    A["Mermaid Live Editor<br/>(초안 작성/프리뷰)"] --> B["VS Code<br/>(편집 & 프리뷰)"]
    B --> C[".md 파일에 저장"]
    C --> D["Git으로 버전 관리"]
    D --> E["Claude Code에서<br/>읽기/수정"]
    
    style A fill:#ff6b6b,stroke:#333,color:#fff
    style E fill:#2ed573,stroke:#333,color:#fff
```

---

## 4.5 문서 관리 팁

### 폴더 구조 권장안

```
프로젝트 루트/
├── CLAUDE.md                  ← 에이전트 컨텍스트 (루트 필수)
├── docs/
│   ├── PRD.md                 ← 제품 요구사항
│   ├── architecture.md        ← 아키텍처 개요
│   ├── erd.md                 ← 데이터 모델
│   ├── api-spec.md            ← API 명세 (권장)
│   ├── ui-wireframe.md        ← 화면 설계 (권장)
│   └── decisions.md           ← 결정 이력 (권장)
├── src/
│   └── CLAUDE.md              ← 소스 코드 관련 추가 컨텍스트 (선택)
└── ...
```

### 문서 업데이트 주기

| 문서 | 업데이트 트리거 |
|------|----------------|
| CLAUDE.md | 패키지 추가/제거, 디렉토리 구조 변경, 컨벤션 변경 시 |
| PRD | 기능 추가/제거, 우선순위 변경 시 |
| 아키텍처 | 새 레이어/모듈 추가, 기술 스택 변경 시 |
| ERD | 테이블 추가/변경, 관계 변경 시 |

---

[다음: 05. 기술스택별 문서 작성 전략 →](./05-tech-stack-strategies.md)
