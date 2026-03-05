# oh-my-scone

Claude Code를 위한 개인 skill 모음 저장소.

[oh-my-codex](https://github.com/Yeachan-Heo/oh-my-codex)에서 영감을 받아, 반복적으로 사용하는 작업 패턴을 skill로 정리하고 발전시켜 나가는 harness 체계입니다.

## Skills

| Skill | 설명 | 출처 |
|-------|------|------|
| **simtalk** | Siemens Plant Simulation의 SimTalk 2.0 레퍼런스. 문법, 함수, 데이터 타입, 코드 예제, 1.0→2.0 마이그레이션 가이드 포함. | Custom ([AT-704](https://ignitecorp.atlassian.net/browse/AT-704)) |
| **deepeval-best-practices** | `deepeval` / `deepteam` 기반 LLM 평가 가이드. RAG 평가, 에이전트 테스트, 커스텀 메트릭, 합성 데이터, 레드팀, 벤치마크, CI/CD 통합. | Custom |
| **langchain-langgraph-best-practices** | `langchain-core`, `langchain`, `langgraph`, `deepagents` 코드 가이드. 에이전트 구축, 상태 관리, 스트리밍, 멀티에이전트 패턴. | Custom |
| **handoff** | 다음 에이전트가 이어서 작업할 수 있도록 HANDOFF.md 인수인계 문서를 작성/업데이트. | Forked from [ykdojo/claude-code-tips](https://github.com/ykdojo/claude-code-tips/blob/main/skills/handoff/SKILL.md) |

## 구조

```
.claude/skills/
├── simtalk/                              # SimTalk 2.0 레퍼런스
│   ├── SKILL.md
│   ├── assets/                           # 코드 예제 템플릿
│   └── references/                       # 함수·문법 레퍼런스
├── deepeval-best-practices/              # LLM 평가 가이드
│   ├── SKILL.md
│   ├── assets/                           # 평가 코드 예제
│   └── references/                       # API 레퍼런스
├── langchain-langgraph-best-practices/   # LangChain/LangGraph 가이드
│   ├── SKILL.md
│   └── assets/                           # 패턴별 코드 예제
└── handoff/                              # 인수인계 문서 생성
    └── SKILL.md
```
