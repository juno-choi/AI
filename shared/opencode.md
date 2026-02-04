## 1. opencode란?

**opencode**는 한마디로 말해 _여러 AI 모델을 하나의 CLI에서 사용할 수 있게 해주는 오픈소스 AI CLI 도구_입니다.

개발자들 사이에서 많이 쓰이는 **Claude Code**가 좋은 평가를 받는 이유는 단순히 모델 성능 때문만이 아니라,

개발자 친화적인 CLI 환경에서 다양한 작업을 편리하게 처리할 수 있기 때문입니다.

opencode는 이 장점을 확장해서, 특정 모델(Claude)에 묶이지 않고 아래와 같은 다양한 AI를 자유롭게 사용할 수 있도록 해줍니다.

- GPT 계열    
- Gemini
- Claude
- DeepSeek
- Local AI 모델

즉, **하나의 CLI에서 상황에 맞게 AI 모델을 바꿔가며 사용할 수 있는 오픈소스 도구**라고 이해하면 됩니다.

---

## 2. opencode가 최근 다시 주목받는 이유

opencode 자체는 사실 예전부터 존재하던 프로젝트입니다.

하지만 최근 들어 **oh my opencode**라는 플러그인이 등장하면서 생산성이 매우 좋다는 소문이 퍼졌고, 그로 인해 다시 많은 개발자들의 관심을 받기 시작했습니다.

물론 oh my opencode 플러그인을 사용하지 않더라도,

- 여러 AI 모델을 하나의 CLI에서 관리
- 작업 성격에 따라 모델을 빠르게 전환

이런 용도로 opencode 자체만으로도 충분히 매력적인 도구입니다.

---

## 3. oh my opencode(OMO)란?

**oh my opencode**는 한국인 개발자([https://github.com/code-yeongyu](https://github.com/code-yeongyu) )가 만든 opencode 플러그인입니다.

이 플러그인을 설치하면 opencode의 기본 모드인

- planning
- build mode

가 아래와 같이 변경됩니다.

- **Sisyphus planning**
- **Sisyphus mode**

### 핵심 개념: 작업별 AI 분업

OMO의 핵심은 **작업 유형에 따라 가장 적합한 AI 모델을 자동으로 선택**해준다는 점입니다.

아래는 OMO에서 사용하는 대표적인 에이전트 구성입니다.

|   |   |   |   |
|---|---|---|---|
|에이전트|역할|모델|호출 방법|
|Sisyphus|메인 오케스트레이터|Claude Opus 4.5 (32k)|기본 활성화|
|Oracle|아키텍처 설계, 디버깅 어드바이저|GPT-5.2 Medium|@oracle|
|Librarian|공식 문서 탐색, 코드 리서치|Claude Sonnet 4.5 / Gemini 3 Flash|@librarian|
|Explore|코드베이스 초고속 탐색|Grok Code / Gemini 3 Flash / Claude Haiku 4.5|@explore|
|Frontend UI/UX|프론트엔드 개발|Gemini 3 Pro|자동 호출|
|Document-Writer|README, API 문서 작성|Gemini 3 Flash|자동 호출|
|Multimodal-Looker|PDF, 이미지, 다이어그램 분석|Gemini 3 Flash|자동 호출|

OMO 개발자는 실제로 **약 2,400만 원 상당의 토큰 비용**을 사용하며,

"업무별로 가장 잘하는 AI를 붙여두는 조합"을 실험해서 이 구성을 만들었다고 합니다.

---

## 4. OMO는 어떻게 동작할까?

OMO(oh my opencode)는 사용자가 하나의 작업 요청을 하면,

1. 작업 유형을 자동으로 분류
2. 해당 작업을 가장 잘 처리할 수 있는 AI를 선택
3. 여러 AI를 내부적으로 조합해서 작업을 끝까지 수행
    

하도록 설계되어 있습니다.

### 예시: 코드 리팩토링 작업

- 코드베이스 탐색 → **Grok Code**
- 전체 리팩토링 계획 수립 → **Claude Opus**
- 관련 문서/레퍼런스 탐색 → **Claude Sonnet**
- 프론트엔드 작업 → **Gemini**

OMO 없이 직접 한다면,

- Grok에게 코드 분석 요청
- 결과를 MD 파일로 정리
- Opus로 계획 수립
- Opus가 던진 질문을 Sonnet으로 조사
- UI 작업은 다시 Gemini에게 요청

이런 식으로 **개발자가 모델을 직접 나눠서 관리**해야 합니다.

OMO를 사용하면 이런 과정을 **하나의 프롬프트**로 처리할 수 있습니다.

---

## 5. Ultrawork 모드

OMO에는 **ultrawork**라는 강력한 기능도 있습니다.

작업 명령 시 ult 또는 ultrawork 키워드를 붙이면,

- 작업이 끝날 때까지 모든 판단과 실행을 OMO에게 위임
- 중간 개입 없이 자동으로 끝까지 처리

하도록 동작합니다.

⚠️ 단점도 분명합니다.

- 토큰 사용량이 매우 큼
- 말 그대로 **돈으로 성능을 찍어누르는 방식**
- 실험·프로토타이핑이나 개인 프로젝트에는 강력하지만, 비용 통제가 필요한 팀 환경에서는 신중한 사용이 필요

---

## 6. 지금 OMO를 써도 될까?

### 1) Anthropic(Claude) 이슈

- OMO에서 Claude를 **구독 계정 기반**으로 사용할 경우
- Anthropic이 계정 정지를 시키는 사례가 발생 중

이를 피하기 위해 opencode의 **zen 기능**을 통한 우회 방법이 공유되고 있지만,

리스크는 인지하고 사용하는 것이 필요합니다.

반면 OpenAI는 오히려 opencode 사용을 장려하는 분위기입니다.

---

### 2) 비용 문제

- 생산성은 매우 높다는 평가가 많음
- 동시에 토큰 소모도 매우 큼

개인 사용이나 실험 목적이 아니라면,

**업무 범위와 비용에 대한 고려는 필수**입니다.

---

## 7. 개인적인 정리

- opencode / OMO를 지금 당장 쓰지 않는다고 해서 뒤처지는 것은 아님
- 다만, **AI 모델별 강점이 분업되는 흐름**은 분명히 가속 중
- openrouter, opencode 같은 도구는 이 흐름의 자연스러운 결과

👉 지금은 각 AI의 특성을 이해하고 업무에 선택적으로 활용하는 단계

👉 opencode 계열 도구가 더 대중화되면, 그때 도입해도 충분히 따라갈 수 있음

**관심 있는 분들은 실험용으로 한 번쯤 써볼 만한 도구**라고 생각합니다.