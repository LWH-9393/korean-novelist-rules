# korean-novelist-rules

한국 소설 작법 **21계명**을 기준으로 원고를 진단하고 다듬는 **범용 에이전트 스킬**입니다.

> "위반된 룰만 골라서 짚는다." — 21개 룰을 기계적으로 모두 적용하지 않습니다.

이 스킬은 [Threads @korgeek82](https://www.threads.com/@korgeek82?hl=ko) 님의 아이디어를 바탕으로 만들어졌습니다.

---

## 지원 에이전트

각 에이전트가 인식하는 표준 파일을 모두 제공합니다.

| 사용 파일 | 사용처 | 적용 방식 |
|---|---|---|
| `SKILL.md` | **Skills 표준** (frontmatter 기반 자동 트리거) — Claude Code, Cowork, Codex, Antigravity 등 다수의 에이전트가 채택한 공용 스킬 포맷 | 각 에이전트의 스킬 디렉토리에 두면 `description` 매칭으로 자동 트리거 |
| `CLAUDE.md` | Claude Code의 디렉토리 컨텍스트 | 소설 작업 폴더에 복사하면 그 폴더 안에서 Claude Code가 자동으로 컨텍스트 로드 |
| `AGENTS.md` | Codex CLI · OpenAI Codex · opencode · Aider 등 `AGENTS.md` 컨벤션을 따르는 코딩/글쓰기 에이전트 | 프로젝트 루트 또는 글로벌 지침 경로에 배치 |
| `AGENTS.md` 또는 `PROMPT.md` | Cursor | `.cursorrules` / `.cursor/rules/*.mdc`로 복사 |
| `PROMPT.md` | ChatGPT · Claude.ai · Gemini · 기타 챗 LLM, 자체 에이전트 | `=== PROMPT START ===` ~ `=== PROMPT END ===` 구간을 시스템/커스텀 프롬프트에 붙여넣기 |

---

## 무엇을 하는 스킬인가요

소설 원고를 가져오면 에이전트가 편집자가 되어 다음을 수행합니다.

- **진단 모드 (기본)**: 원문은 건드리지 않고, 위반된 룰만 골라 지적·조언
- **반영 모드 (요청 시)**: "고쳐줘", "다시 써줘"라고 하면 그제야 수정본을 만듭니다

진단 우선순위: 룰 1·8·9 > 룰 5·6·7 > 룰 10·21 > 나머지. 발견된 위반이 많아도 가장 중요한 5~7개만 짚습니다.

---

## 21계명 한눈에

| 번호 | 이름 | 핵심 |
|---|---|---|
| 1 | 구체성 | 수치·감각·행동으로 |
| 2 | 장식 빼기 | 부사→형용사→동사 |
| 3 | 토씨·중복 | 조사·단어 반복 제거 |
| 4 | 단어 선택 | 한복-김칫국물 원리 |
| 5 | "있다" 지우기 | ~고 있다 남용 금지 |
| 6 | "것" 지우기 | 의존명사 남용 금지 |
| 7 | "수" 지우기 | ~ㄹ 수도 있다 남용 금지 |
| 8 | 무개념 문장 | 개념 없으면 삭제 |
| 9 | 끝맺음 | 할 말 끝나면 바로 멈춰라 |
| 10 | 접속사 지우기 | 그리고/그래서/하지만 제거 |
| 11 | 핍진성 | 9 진실로 1 거짓을 믿게 |
| 12 | 복선 | 노루 꼬리처럼 미세하게 |
| 13 | 절제된 문장 | 기름 짜내듯 |
| 14 | 작가의 거리 | 유리처럼 차갑게 |
| 15 | 인물 묘사 절제 | 약 올리며 옷 벗기기 |
| 16 | 인물별 말투 | 누가 말했는지 표시 없이 구분 |
| 17 | 주제 노출 금지 | 독자가 스스로 깨닫게 |
| 18 | 다듬은 대화 | 실제 말 그대로 쓰면 부자연스럽다 |
| 19 | 충돌 인물 말투 | 갈등 장면에서 말투 대비 |
| 20 | 대화로 입체화 | 서술을 대화로 활성화 |
| 21 | 죽은 어휘 | 감각으로 살아 있는 단어로 |

---

## 설치

### Skills 표준 (Claude Code, Cowork, Codex, Antigravity 등)

`SKILL.md`의 frontmatter(`name` + `description`)를 보고 자동 트리거하는 모든 스킬 호환 에이전트에서 사용할 수 있습니다. 각 에이전트의 스킬 디렉토리에 폴더째로 두면 됩니다.

**Claude Code**

```bash
mkdir -p ~/.claude/skills
cd ~/.claude/skills
git clone https://github.com/LWH-9393/korean-novelist-rules.git
```

**Codex / Antigravity / 그 외 스킬 호환 에이전트**

각 에이전트의 사용자 스킬 디렉토리(예: `~/.codex/skills/`, Antigravity의 스킬 폴더 등) 아래에 동일하게 클론합니다. 정확한 경로는 해당 에이전트의 스킬 문서를 확인하세요.

설치 후 에이전트를 새로 켜면 스킬 목록에 `korean-novelist-rules`가 등록되고, 트리거 문장(예: "내 소설 봐줘")을 말하면 발동합니다.

### Claude Code — 디렉토리 컨텍스트 (특정 소설 폴더에서만 적용)

소설 작업 폴더에 `CLAUDE.md`만 복사해두면, 그 폴더에서 Claude Code를 켤 때 자동으로 21계명 지침이 컨텍스트로 로드됩니다.

```bash
# 소설 작업 폴더에서
curl -O https://raw.githubusercontent.com/LWH-9393/korean-novelist-rules/main/CLAUDE.md
```

작품마다 다른 룰셋을 쓰고 싶을 때, 또는 스킬 시스템을 쓰지 않고 폴더 단위로 적용하고 싶을 때 유용합니다.

### Codex CLI · opencode · Aider 등 (AGENTS.md 인식 에이전트)

방법 A — **프로젝트 단위로 사용:**

```bash
git clone https://github.com/LWH-9393/korean-novelist-rules.git
cp korean-novelist-rules/AGENTS.md ./AGENTS.md   # 작업할 소설 디렉토리에 복사
```

방법 B — **글로벌 지침으로 사용** (Codex CLI):

`AGENTS.md` 내용을 `~/.codex/instructions.md`(또는 사용 중인 에이전트의 글로벌 지침 경로)에 추가합니다.

### Cursor

`AGENTS.md` 또는 `PROMPT.md`의 본문을 프로젝트 루트의 `.cursorrules`로 복사하거나, `.cursor/rules/korean-novelist-rules.mdc`로 저장합니다.

```bash
cp korean-novelist-rules/AGENTS.md .cursorrules
```

### ChatGPT · Claude.ai · Gemini 등 챗 LLM

`PROMPT.md`를 열어 `=== PROMPT START ===` 부터 `=== PROMPT END ===` 사이의 내용을 복사한 뒤:

- **ChatGPT**: Custom Instructions 또는 Custom GPT의 시스템 프롬프트에 붙여넣기
- **Claude.ai**: Project의 Custom instructions에 붙여넣기
- **Gemini**: Gem의 instructions에 붙여넣기

이후 소설 원고를 붙여넣고 "내 소설 봐줘"처럼 요청하면 됩니다.

---

## 사용 방법

설치 후, 소설 원고를 에이전트에게 주고 아래와 같이 요청합니다.

- "내 소설 봐줘"
- "21계명으로 진단해줘"
- "소설가 룰로 봐줘"
- "이 문장 어때"
- "탈고해줘", "수정 제안해줘", "소설 진단해줘"

진단 후 수정을 원하면:

- "고쳐줘", "다 고쳐줘" → 진단에서 짚은 위반 사항 전체 반영
- "룰 5만 적용해줘" → 해당 룰만 반영
- "이 부분만 다시 써줘" → 해당 부분만 반영

---

## 작가의 의도 보호

룰은 룰일 뿐입니다. 작가가 의도적으로 룰을 어겼다고 판단되는 경우 — 캐릭터 말투 안의 룰 위반, 1인칭 화자의 의식의 흐름, 시적 반복, 리듬을 위한 부사 — 짚지 않거나 "의도하신 것이라면 유지하시는 게 좋습니다"라고 덧붙입니다.

---

## 파일 구조

```
korean-novelist-rules/
├── README.md      # 이 파일
├── SKILL.md       # Skills 표준 (frontmatter 포함, name+description 자동 매칭). Claude Code · Cowork · Codex · Antigravity 등에서 공용
├── CLAUDE.md      # Claude Code 디렉토리 컨텍스트
├── AGENTS.md      # Codex CLI · OpenAI Codex · opencode · Aider · Cursor 등
└── PROMPT.md      # 챗 LLM 시스템 프롬프트용
```

네 파일의 21계명 본문은 동일합니다. 각 에이전트의 컨벤션(frontmatter 유무, 헤더 톤, 트리거 표현)에 맞춰 도입부와 메타 정보만 다릅니다.

---

## 출처 / Credits

소설 작법 21계명의 원래 아이디어와 정리는 [Threads @korgeek82](https://www.threads.com/@korgeek82?hl=ko) 님에게서 비롯되었습니다. 이 저장소는 그 내용을 다양한 에이전트에서 쓸 수 있는 형태로 옮긴 것입니다.

---

## 라이선스

자유롭게 사용·수정·배포 가능합니다.
