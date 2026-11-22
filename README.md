# 아수라장 코치 (AramCoach)

롤 **무작위 총력전: 아수라장(ARAM: Mayhem)** 에서 증강과 아이템 고르는 걸 도와주는 프로그램 + MCP 서버입니다.

- **판단은 각자 PC에 로그인된 AI(Claude Code / Codex / Claude·ChatGPT 채팅)가 합니다.** 이 프로그램은 AI API를 직접 호출하지 않으므로 배포자에게 비용이 들지 않고, 각자 본인 구독을 씁니다.
- 증강 점수는 **AI만 정합니다.** AI 세팅이 끝나기 전에는 오버레이에 "AI 분석 중"만 표시해요.

## Windows에서 시작하기

[Windows 실행 파일 다운로드](https://github.com/limeknit-wq/aram-coach-public/releases/latest/download/AramCoach.exe)

Windows x64용입니다. 자동 추천을 사용하려면 본인 PC에 Claude Code 또는 Codex CLI를 설치하고 로그인하세요. 실행 파일에는 공통 게임 데이터와 화면 구성 리소스가 들어 있습니다. 선택 기록과 설정은 실행한 사람의 PC에서 생성됩니다.

## 설치 및 사용

1. `AramCoach.exe`를 실행하면 설치를 물어봐요. 설치 위치는 `%LOCALAPPDATA%\Programs\AramCoach`이고, 시작 메뉴에 "아수라장 코치"가 생겨요. 관리자 권한은 필요 없어요.
   - 서명이 없어서 처음에 Windows SmartScreen 경고가 뜰 수 있어요. **추가 정보 → 실행**을 누르세요.
2. 작업 표시줄 오른쪽에 **트레이 아이콘**이 생겨요. 롤만 하면 나머지는 자동이에요.
   - **픽창:** 내 챔피언이 3초 동안 그대로면 롤 클라이언트(읽기 전용)에서 읽어서, **Claude Code 또는 Codex를 백그라운드로 실행해 그 챔피언의 기본 점수표를 미리 만들어요**(측정 18초). 챔피언별로 저장해서, 같은 챔피언을 다시 하면 바로 써요. 패치로 증강 데이터가 바뀌면 새로 만들어요.
   - **로딩 화면:** 적 조합이 나오면 기본 점수표를 **즉시 적용**하고(첫 증강부터 점수 표시), 적 조합 보정만 AI가 해요(측정 19초).
   - **픽창 준비분이 없을 때:** 로딩 화면에서 한 번에 전체 세팅해요(측정 21초).
   - **속도를 낸 방법:** AI가 도구를 여러 번 부르지 않게 정보를 처음부터 한 번에 넣고, 증강 번호로 된 짧은 JSON만 받아요. AI 모델은 각자 Claude Code·Codex에 설정해 둔 기본 모델을 그대로 쓰고, 다른 MCP 연결을 불러오지 않아요. 아이템 추천은 칼바람 상점 목록(다른 모드 아이템 제외)에 있는 이름만 받아요.
   - **게임 중:** 증강 선택지가 뜨면 카드 위에 AI 등급·점수·이유가 바로 떠요.
   - 세팅이 끝나면 트레이 알림이 와요.
3. **트레이 메뉴:** 상태, 설정 열기, 오버레이 켜기/끄기, 다시 세팅(AI 다시 분석), 종료
4. **설정창:**
   - **이번 판:** 전략, 상위 증강, 고른 증강
   - **설정:** AI 엔진(자동/Claude Code/Codex/끄기), 오버레이 크기·세로 위치, 윈도우 시작 시 실행, 제거
   - **연결:** Claude 데스크톱·Claude Code·Codex에 MCP 연결 설정 복사

> **AI 엔진 준비:** [Claude Code](https://claude.com/claude-code) 또는 Codex CLI가 설치돼 있고 로그인돼 있어야 자동 세팅이 돼요. 둘 다 없으면 채팅에서 "세팅"이라고 하면 돼요(아래 MCP 연결).

> **이미 MCP를 연결해 둔 경우:** 프로그램을 켜면 화면 감시와 오버레이를 프로그램이 넘겨받아요. 예전 버전 MCP 서버가 켜져 있으면 넘겨받지 못하니, Claude 데스크톱을 한 번 다시 켜세요.

**직접 빌드:** `npm install` → `npm run build:exe` → `dist/AramCoach.exe`. Node 24에 내장된 단일 실행 파일 기능으로, 스크립트·데이터·글꼴이 exe 안에 들어가요.

**디자인:** 롤 클라이언트 색감(남색·금색)에 [Pretendard](https://github.com/orioncactus/pretendard)(SIL OFL 1.1) 글꼴을 썼어요. 카드는 등급 배지, 점수, 진행 막대, 빌드 태그, 시너지 박스로 구성했고, GitHub의 아수라장 도우미 [valkia/aramgg_client](https://github.com/valkia/aramgg_client), [ItzStorDz/mayhem-advisor](https://github.com/ItzStorDz/mayhem-advisor)의 구성을 참고했어요(코드는 직접 작성).

## 채팅에서 쓰기 (MCP) — 세팅을 직접 하거나 상황 변화를 물을 때

1. **게임 시작(로딩 화면이나 게임 시작 직후)에 채팅에 `세팅`이라고 한 번만 입력하세요.** 프로그램이 켜져 있으면 자동으로 되니 필요 없어요.
   - AI가 내 챔피언, 양 팀 조합, 이번 판 이벤트를 보고 증강 전체의 **점수표**를 만들어 저장합니다(`save_game_plan`). 1~2분쯤 걸려요.
   - 점수표에는 등급, 한 줄 이유, "A를 고르면 B 점수 +N" 같은 **시너지 규칙**, 아이템 빌드 순서가 들어갑니다.
2. **게임 중에는 아무것도 안 해도 됩니다.** 증강 선택지가 뜨면 1~2초 안에 **카드 바로 위에** 등급·점수·이유가 뜨고, 1순위 카드는 금색 테두리로 강조됩니다. 이때 AI는 호출하지 않아요.
   - **고른 증강 자동 기록:** 카드를 클릭하고 선택 화면이 닫히면 "고른 증강 기록됨"이 뜹니다. 다음 선택지부터 시너지 점수가 자동 반영됩니다.
   - **커맨드 라인 이벤트:** 가장 약한 카드에 "이 카드 먼저 새로고침"을 표시합니다.
   - **HEARTSTEEL 스티커:** 스티커가 붙은 카드는 점수 +8로 계산합니다.
   - 점수표에 없는 증강은 AI가 정한 기본 점수(defaultScore)로 표시하고 "점수표에 없음"이라고 알려줍니다.
3. **상황이 바뀌면** "아칼리가 너무 컸어, 다시 짜줘"처럼 말하세요. AI가 점수표를 고치고 오버레이에 바로 반영됩니다.

> 오버레이는 **테두리 없는 창 모드**에서만 게임 위에 보입니다. 전체 화면이면 오버레이가 가려지니, 그때는 Alt+Tab 해서 채팅에서 "뭐 고를까?"라고 물어보세요(점수표가 있으면 바로 답합니다).

오버레이 구조는 GitHub의 [czgreat/aramhex](https://github.com/czgreat/aramhex), [Nyx0ra/lol-aram-mayhem-hextech-helper](https://github.com/Nyx0ra/lol-aram-mayhem-hextech-helper)(둘 다 MIT), [valkia/aramgg_client](https://github.com/valkia/aramgg_client)의 방식(카드 위 표시, 화면 순서 유지, 테두리 없는 창)을 참고했고, 코드는 직접 작성했습니다.

**오버레이 동작 방식**
- 투명하고 항상 위에 있는 창입니다. 포커스를 뺏지 않고 마우스 클릭은 게임으로 그대로 통과합니다.
- 롤 게임 창이 맨 앞에 있고 선택지가 떠 있을 때만 보입니다.
- 프로그램과 MCP 서버(데스크톱 채팅, Claude Code 등)가 여러 개 켜져 있어도, 화면 감시와 오버레이는 **하나만** 돌아요. 127.0.0.1:47321을 잡은 쪽이 맡고(프로그램이 우선), 나머지는 그 상태를 공유합니다.
- 끄려면 환경 변수 `LOL_OVERLAY=0`.
- 화면이 작으면(1080p 등) 글자를 키워서 인식합니다. 1600×900 실제 게임 스크린샷으로 4장 모두 인식되는 것을 확인했습니다.

### 증강 선택지 자동 인식 (Windows)

- 서버가 켜져 있으면 **롤 게임 창이 맨 앞에 있을 때만** 1.5초마다 화면을 찍어 Windows 내장 한국어 OCR로 글자를 읽고, 증강 이름이 2개 이상 보이면 선택지로 기억합니다. 다시 돌리기로 선택지가 바뀌면 새 선택지로 갱신됩니다.
- 게임 메모리·파일은 건드리지 않고 화면 캡처만 합니다. 캡처는 `%TEMP%\lol-aram-mcp`에만 저장되고 외부로 보내지 않습니다. AI가 `includeImage`나 `capture_game_screen`을 쓸 때만 그 화면이 연결된 AI에 전달됩니다.
- **전체 화면 / 테두리 없는 창 / 창 모드 모두** 지원합니다. 캡처는 OBS '디스플레이 캡처'와 같은 DXGI Desktop Duplication 방식을 쓰고, 실패하면 일반 화면 캡처(GDI)로 넘어갑니다.
- 한국어·영어 클라이언트 모두 인식합니다.
- 끄려면 환경 변수 `LOL_SCREEN_WATCH=0`.
- 인식 시험: `node scripts/ocr-test.mjs 스크린샷.png`
- 캡처 진단: `powershell -ExecutionPolicy Bypass -File src/watcher.ps1 -TestCapture` (맨 앞 창을 한 번 찍어 캡처 방식과 평균 밝기만 출력. 밝기 0이면 검은 화면)
- HDR을 켠 모니터는 화면 형식이 달라 GDI 방식으로 넘어가며, 전체 화면에서는 검게 나올 수 있습니다.

> **"적이 AP 많은데 다음 템 뭐 사?"** / **"카타리나가 너무 컸어, 빌드 바꿔야 해?"**

현재 골드와 적의 실제 아이템(마법/물리 비중, 탱커, 성장한 적)을 보고 다음 구매를 추천합니다.

## 귀빈 이벤트 (판마다 바뀌는 규칙)

아수라장은 판마다 **귀빈(Guest of Honor) 이벤트**가 하나 붙어 규칙이 바뀝니다. 게임 데이터에서 현재 이벤트 9개를 뽑아 `data/events.json`에 넣었고, AI가 추천할 때 반영합니다.

| 이벤트 | 효과 | 추천에 주는 영향 |
|---|---|---|
| 커맨드 라인 | 각 선택에서 첫 새로고침 시 그 증강의 등급 상승 | 가장 약한 카드를 먼저 새로고침 |
| HEARTSTEEL | 일부 증강에 멤버 스티커 → 고르면 추가 효과 | 스티커 효과를 점수에 더함 (카드에 ★ 표시) |
| 열혈 팬 | 레벨 제한 21, 21레벨에 추가 증강 | 후반 스케일링 증강 가치 상승 |
| 펜타킬 | 기본 스킬 하나 강화 (18레벨에 하나 더) | 강화할 스킬도 추천 |
| K/DA | 포토카드 4장 모으면 추가 증강 | 운영 조언 |
| True Damage | 다중 킬·제압·포탑 파괴 시 모루 | 운영 조언 |
| 꿀벌 유랑단 | 꿀(골드·회복)과 벌(피해)이 맵을 가로지름 | 운영 조언 |
| 귀염둥이 카페 | 체력 회복 유물 강화 | 운영 조언 |
| 우주 그루브 | 무대에서 춤추면 모두 1,000골드 | 아이템 타이밍 |

- 경기 시작 안내 화면을 OCR로 **자동 인식**합니다. 킬 알림의 '펜타킬'로 잘못 잡지 않도록, 이벤트 이름과 소개 문구가 같은 화면에 있을 때만 인정합니다.
- 안내를 놓쳤으면 "이번 판 이벤트는 커맨드 라인이야"처럼 말하면 기록됩니다.
- HEARTSTEEL 스티커가 붙은 카드도 화면에서 읽어 해당 카드에 연결합니다.
- 화면 상단에 **🎤 이번 판: 이벤트명** 배지가 붙습니다.

> **증강 세트(특성)는 반영하지 않았습니다.** 세트는 26.3 패치에 추가됐다가, Riot이 26.12 패치에서 폐지한다고 발표했습니다([개발자 노트](https://www.leagueoflegends.com/en-us/news/dev/dev-augmentmaxxing-aram-mayhem)). 현재 게임 데이터에도 세트 정의(소속 증강, 보너스)가 없고 문자열과 이펙트만 남아 있습니다. AI에게도 세트 보너스를 근거로 추천하지 말라고 지시해 두었습니다.

## 화면 (채팅 안 UI)

Claude·ChatGPT처럼 **MCP Apps**를 지원하는 앱에서는 답변과 함께 화면이 채팅 안에 그려집니다. 구조는 GitHub의 아수라장 도우미 중 가장 많이 쓰이는 [valkia/aramgg_client](https://github.com/valkia/aramgg_client)(★690+)와 [ItzStorDz/mayhem-advisor](https://github.com/ItzStorDz/mayhem-advisor)를 참고했습니다.

- **증강 카드** (`show_augment_pick`): 게임 화면과 같은 **왼쪽/가운데/오른쪽 순서**로 3장을 보여줍니다. 카드마다 등급색(실버/골드/프리즘), AI 판단 점수(0~100)와 등급(S+~C), 빌드 방향, 한 줄 이유, 1순위 배지가 붙습니다. **이걸로 골랐어**를 누르면 고른 증강이 바로 기록됩니다.
- **게임 패널** (`show_game_panel`): 탭 4개.
  - **구매:** AI가 정한 구매 순서와 이유, 지금 골드로 살 수 있는지 또는 얼마가 부족한지.
  - **적응:** 적의 마법/물리 피해 비중 막대, 성장한 적 경고, 탱커, 코치 메모.
  - **증강:** 지금까지 고른 증강.
  - **팀:** 양 팀 챔피언, 레벨, KDA, 아이템.
- 점수는 AI의 판단 점수이며 승률 통계가 아닙니다(Riot 정책상 증강 승률 표시는 피함).
- MCP Apps를 지원하지 않는 앱에서는 같은 내용이 텍스트로 전달됩니다.
- 미리보기: `node scripts/ui-preview.mjs` → http://localhost:4321/augments , http://localhost:4321/panel

## 도구 목록

| 도구 | 하는 일 |
|---|---|
| `get_live_game` | 진행 중인 게임 상황 (롤 클라이언트의 공식 Live Client Data API, 읽기 전용) |
| `get_augment_offer` | 화면에서 자동으로 읽은 증강 선택지 + 효과 + HEARTSTEEL 스티커 (필요하면 당시 화면 이미지) |
| `get_augment_catalog` | 세팅용: 증강 전체를 한 줄씩 (이름·등급·분류·효과 요약) |
| `save_game_plan` | 이번 판 점수표·시너지·빌드 저장 → 오버레이가 즉시 사용 |
| `get_game_plan` | 저장된 세팅, 고른 증강, 지금 선택지 점수 보기 |
| `get_mayhem_event` | 이번 판 귀빈 이벤트와 효과, 전체 이벤트 목록 |
| `capture_game_screen` | 마지막 게임 화면 이미지 (상점·스코어보드 확인 등) |
| `show_augment_pick` | 증강 추천 카드 화면 |
| `show_game_panel` | 구매/적응/증강/팀 패널 화면 |
| `set_game_context` | 게임이 안 잡힐 때 조합 직접 입력, 고른 증강·메모 기록 |
| `analyze_matchup` | 양 팀 조합 분석 (역할, AD/AP, 앞라인, 원거리) |
| `find_augments` | 선택지로 뜬 증강 이름 → 정확한 효과·등급 |
| `search_augments` | 증강 키워드/등급/태그 검색 |
| `get_champion` | 챔피언 패시브·스킬·쿨타임·스탯 |
| `search_items` / `get_item` | 칼바람 구매 가능 아이템 검색 / 상세 |

## 설치

필요한 것: [Node.js](https://nodejs.org) 20 이상

```bash
cd lol-aram-mcp
npm install
npm test
```

`npm test` 가 모든 도구를 한 번씩 호출해 봅니다(게임 중이 아니면 `get_live_game`은 "게임을 찾지 못함"이 정상).

> 실시간 게임 정보는 **롤을 실행 중인 그 PC에서 서버를 돌릴 때만** 읽힙니다. 다른 기기(폰 등)에서 쓰면 조합을 말로 알려주면 됩니다.

### Claude Desktop

`%APPDATA%\Claude\claude_desktop_config.json` (macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`)에 추가 후 Claude 재시작:

```json
{
  "mcpServers": {
    "lol-aram": {
      "command": "node",
      "args": ["C:\\경로\\lol-aram-mcp\\src\\index.js"]
    }
  }
}
```

### Claude Code

```bash
claude mcp add lol-aram -- node "C:/경로/lol-aram-mcp/src/index.js"
```

### Codex (OpenAI CLI)

`~/.codex/config.toml`:

```toml
[mcp_servers.lol-aram]
command = "node"
args = ["C:/경로/lol-aram-mcp/src/index.js"]
```

### ChatGPT (웹/데스크톱)

ChatGPT는 인터넷에서 접속 가능한 https 주소의 MCP만 연결할 수 있습니다. 내 PC에서 HTTP 모드로 켜고 터널로 주소를 만듭니다.

1. 서버를 HTTP 모드로 실행 (토큰은 아무 긴 문자열로 직접 정하세요):
   ```powershell
   $env:MCP_TOKEN="여기에-긴-비밀값"; npm run start:http
   ```
2. 다른 창에서 터널 실행 (예: [cloudflared](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/)):
   ```bash
   cloudflared tunnel --url http://localhost:3939
   ```
3. ChatGPT 설정에서 개발자 모드를 켜고 커넥터(앱)를 추가, URL에 `https://<터널주소>/mcp?token=<정한 비밀값>` 입력.

토큰 없이 열면 주소를 아는 누구나 접속할 수 있으니 꼭 `MCP_TOKEN`을 설정하세요. (도구는 읽기 전용이지만 내 게임 정보가 보입니다.)

## 패치 후 증강 데이터 갱신

챔피언·아이템은 실행할 때 최신 패치 데이터(Data Dragon)를 자동으로 받습니다. 증강은 미리 만들어 둔 `data/augments.json`을 쓰므로, 새 증강이 나오면:

```bash
npm run build:augments
```

(CommunityDragon에서 문자열 데이터 약 36MB와 모드 데이터 약 13MB를 받아 `data/augments.json`, `data/events.json`을 만듭니다.)

Riot은 2027년 1월(시즌 1)에 아수라장 변경을 예고했습니다. 패치 후에는 이 명령으로 데이터를 꼭 갱신하세요.

## 알려진 한계

- 증강 데이터는 아수라장의 두 증강 풀(KIWI, KIWI_JADE)을 합친 287개입니다. 어느 풀이 지금 라이브인지는 데이터만으로 알 수 없어 둘 다 넣었습니다(각 증강의 `pools` 필드).
- 증강 선택지는 게임 API에 없어 **화면 OCR**로 읽습니다. 실제 게임 스크린샷(영어 클라이언트)으로 3개 모두 인식되는 것을 확인했지만, 한국어 클라이언트의 실제 화면과 실제 전체 화면 게임에서는 아직 검증 전이며, 못 읽으면 스크린샷이나 이름으로 알려주면 됩니다. 어떤 증강을 **골랐는지**는 자동으로 알 수 없어서 AI가 물어보고 기록합니다.
- 증강 중 약 100개는 설명의 일부 수치가 `?` 로 비어 있고, 13개는 설명이 없습니다(원본 데이터에 수치가 없음). AI가 아는 지식으로 보완합니다.
- 챔피언 AD/AP 구분은 Data Dragon 값으로 **추정**한 것입니다.
- 게임 내 오버레이가 아니라 별도 채팅에서 쓰는 도구이며, 롤 클라이언트의 공식 읽기 전용 API만 사용합니다. 그래도 Riot 서드파티 정책은 바뀔 수 있으니 본인 책임하에 사용하세요.

데이터 출처: Riot Data Dragon, CommunityDragon. 이 프로젝트는 Riot Games와 관련이 없습니다.
