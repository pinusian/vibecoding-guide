# 바이브코딩 가이드 (vibecoding-guide)

> 바른 AI 아카데미 바이브코딩 과정 공식 자료

프로그래밍 초보자가 AI(Claude)와 함께 앱·웹서비스를 만들 때, 다음 3가지 함정에 빠지지 않도록 절차를 잡아주는 Claude Code 스킬입니다.

- 애매하게 요청하면 → AI도 애매하게 만든다
- 완성된 결과물이 제대로 동작하는지 확인할 방법이 없다
- 왜 이렇게 만들어졌는지 기록이 남지 않는다

설치하면 "앱 만들고 싶어"라고만 말해도 Claude가 **헌장 → 명세 → 명확화 → 계획 → 점검표 → 작업분해 → 모순점검 → TDD 구현**의 8단계 절차로 이끌어줍니다. GitHub [Spec Kit](https://github.com/github/spec-kit)이 설치되어 있으면 `/speckit.*` 명령을 활용하고(A코스), 없으면 스킬에 내장된 경량 워크플로로 같은 규율을 지킵니다(B코스) — **하이브리드 방식**입니다.

이 스킬의 내용은 실제로 완주한 프로젝트 기록인 『바이브코딩 실전 교육교재 — SpecKit로 기획부터 구현까지』에서 추출했습니다. 모든 절차·프롬프트·트러블슈팅 사례는 실제 사례입니다.

## 설치 방법 (3가지 중 하나 선택)

### 방법 1 — 플러그인 설치 (Claude Code CLI/데스크톱 사용자, 권장)

이 저장소가 GitHub에 올라가 있다면, Claude Code에서 두 명령이면 끝납니다:

```
/plugin marketplace add <계정명>/<저장소명>
/plugin install vibecoding-guide@vibecoding-marketplace
```

업데이트도 `/plugin` 메뉴에서 관리됩니다.

### 방법 2 — 프로젝트 폴더에 직접 넣기 (claude.ai 웹/클라우드 세션 포함, 가장 간단)

`plugins/vibecoding-guide/skills/vibecoding-guide/` 폴더를 통째로 복사해서, 내 프로젝트의 `.claude/skills/` 아래에 넣습니다:

```
내프로젝트/
└── .claude/
    └── skills/
        └── vibecoding-guide/
            ├── SKILL.md
            └── references/...
```

이 방법은 프로젝트 저장소에 스킬이 포함되므로, **claude.ai/code 클라우드 세션에서도 별도 설치 없이 그대로 작동**합니다. 교육용 시작 템플릿 저장소를 만들어 두고 수강생이 fork/clone하게 하면 진입장벽이 가장 낮습니다.

### 방법 3 — 개인 스킬로 설치 (모든 내 프로젝트에서 사용)

같은 폴더를 사용자 홈의 `~/.claude/skills/`(Windows: `C:\Users\<이름>\.claude\skills\`)에 넣으면 모든 프로젝트에서 사용할 수 있습니다. claude.ai 채팅만 쓰는 경우에는 스킬 폴더를 zip으로 압축해 claude.ai 설정 → 기능(Capabilities)에서 업로드할 수 있습니다.

## 사용법

설치 후 Claude에게 그냥 만들고 싶은 것을 말하면 됩니다:

> "가계부 웹앱 만들고 싶어"

Claude가 스킬을 자동으로 발동해 절차를 시작합니다. Spec Kit 설치 여부를 확인한 뒤 A코스(Spec Kit 코치) 또는 B코스(경량 워크플로)를 제안합니다.

## 폴더 구조

```
vibecoding-guide/                       ← 이 저장소 (마켓플레이스)
├── README.md
├── .claude-plugin/marketplace.json     ← 마켓플레이스 매니페스트
└── plugins/vibecoding-guide/           ← 플러그인
    ├── .claude-plugin/plugin.json
    └── skills/vibecoding-guide/        ← 스킬 본체 (방법 2·3에서는 이 폴더만 복사)
        ├── SKILL.md                    ← 핵심 절차 (항상 로딩됨)
        └── references/                 ← 상세 자료 (필요할 때만 Claude가 읽음)
            ├── 01-why-sdd.md                    왜 절차가 필요한가
            ├── 02-speckit-8steps.md             A코스: Spec Kit 8단계 실전 가이드
            ├── 03-lite-workflow.md              B코스: Spec Kit 없이 진행하는 경량 절차
            ├── 04-tdd-vertical-slice.md         TDD + 버티컬 슬라이스 규율
            ├── 05-troubleshooting.md            실전 트러블슈팅 사례집
            └── 06-collaboration-and-security.md AI 협업 원칙 · API 키 보안
```

## Spec Kit 설치 (A코스를 쓰려면)

```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
```

프로젝트 폴더에서 `specify init .` 실행 (uv가 없다면 https://docs.astral.sh/uv/ 참고). 설치하지 않아도 B코스로 동일한 절차를 진행할 수 있습니다.
