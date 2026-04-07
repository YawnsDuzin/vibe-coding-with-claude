# vibe-coding-with-claude

**1인 바이브코딩 개발자를 위한 개발 문서 체계 가이드**

> Claude Code를 주력 코딩 에이전트로 사용하는 1인 개발자가, 최소한의 문서로 최대의 바이브코딩 효율을 내기 위한 실전 가이드

---

## 이 가이드가 다루는 것

- 1인 바이브코딩에 **실질적으로 필요한 문서 종류** (필수 4종 / 권장 3종 / 불필요 5종)
- 코딩 에이전트가 잘 이해하는 **문서 포맷 비교** (Markdown, Mermaid, PlantUML, draw.io 등)
- 각 문서의 **복붙 가능한 템플릿**과 작성 팁/안티패턴
- **기술스택별** (WPF, 웹 풀스택, HTMX, Flutter, IoT) 문서 작성 전략 및 CLAUDE.md 예시
- 작업 유형별 (Feature, Bugfix, 리팩토링, DB 변경, UI) **바이브코딩 프롬프트 패턴**

---

## 가이드 목차

| # | 문서 | 내용 |
|---|------|------|
| 00 | [목차 & Quick Start](./docs/00-index.md) | 전체 구조, 빠른 시작 가이드, 문서 체계 다이어그램 |
| 01 | [개발 문서 종류 정리](./docs/01-document-types.md) | 필수/권장/불필요 문서 분류, 목적, 에이전트 활용도 |
| 02 | [에이전트 친화적 문서 포맷](./docs/02-agent-friendly-formats.md) | 포맷별 비교, 문서 종류별 최적 포맷 매칭 |
| 03 | [실전 작성 가이드](./docs/03-practical-writing-guide.md) | CLAUDE.md, PRD, 아키텍처, ERD 템플릿 및 안티패턴 |
| 04 | [문서 작성 생산성 도구](./docs/04-productivity-tools.md) | VS Code 확장, Claude Code 활용법, AI 문서 생성 도구 |
| 05 | [기술스택별 문서 전략](./docs/05-tech-stack-strategies.md) | WPF/웹/모바일/IoT 스택별 차이점 및 CLAUDE.md 예시 |
| 06 | [바이브코딩 작업 요청 패턴](./docs/06-vibe-coding-patterns.md) | 프롬프트 템플릿, 문서→코드 워크플로우 |

---

## 빠른 시작

```
1. CLAUDE.md를 프로젝트 루트에 생성 → 03번 문서의 템플릿 복붙
2. docs/PRD.md 작성 → 기능 목록 + P0/P1/P2 우선순위
3. docs/architecture.md 작성 → Mermaid 다이어그램 포함
4. docs/erd.md 작성 → Mermaid erDiagram 포함
5. 에이전트에게 문서 참조시키며 바이브코딩 시작!
```

## 핵심 원칙

- **Markdown + Mermaid** 조합이면 모든 문서를 커버할 수 있다
- 에이전트가 읽고/생성/수정할 수 있는 포맷만 사용한다
- 문서는 **사람이 읽는 용도 + 에이전트 컨텍스트** 겸용이다
- 엔터프라이즈 오버스펙은 배제하고, **최소 문서 최대 효과**를 추구한다
