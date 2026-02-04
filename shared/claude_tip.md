# 사용 tool

## intellij

- intellij - plugin 설치 claude code 있음
- intellij 내에 터미널로 연결됨
- @로 검색 가능

## terminal
- 터미널 실행
- project에서 claude 명령어 실행해서 만들기
- drag & drop 으로 파일이나 이미지 첨부 가능

# 사용 방법

## 실행 방법

- /init
    - claude init 실행 시 다음 파일/폴더가 자동 생성됨:    
```
.claude/
 ├── claude.json         (프로젝트 메타 정보)
 ├── project/
 │    └── {projectId}/   (프로젝트별 히스토리 정보)
 ├── mcp/                (연결된 MCP 서버 목록)
 └── logs/               (세션별 히스토리)
claude.md                (메인 프로젝트 문서)
```
`
    - 해당 프로젝트를 분석하고 CLAUDE 파일을 생성해줌
    - user home에 .claude 메타 정보를 생성한다.
    - ~/.claude/projects 에는 프로젝트 메타 데이터가 저장된다
    - ~/.claude.json 파일을 보면 설정 내용을 확인해볼 수 있다.
        

## 명령어

- /terminal-setup
    - 줄바꿈 설정
    - shift + enter로 줄바꿈이 됨
    - 안되면 \ + enter 쓰면 됨
        
- /ide 명령어
    - intellij를 연결해줄 수 있다.
    - tab 으로 thinking 모드를 키고 끄고 할수 있다.
        - Thinking Mode ON:
            - 깊은 분석, 설계, 시퀀스 작성 필요 시
            - 아키텍처 설계, 도메인 분석, MSA 흐름 분석
            - Tech Spec 생성
        - Thinking Mode OFF:
            - 코드 수정, 스몰 리팩토링, 단순 질의응답
    - ultra thinking 모드는 깊게 커맨드에서 생각해줘, 생각하고 답변해줘 등 으로 처리해야 한다.
        
- /model 명령어
    - 모델 변경 가능
        
- /agents 명령어
    - built-in agents 가 있음
    - 더 적은 토큰으로 최적의 아웃풋을 기대할 수 있음
    - agent 없이 클코를 쓰는건 비효율적이라 생각이 든다
    - 내가 명령을 내리는 ai가 main이고 agent 들이 병렬로 실행될 수 있다.
    - agent 는 md 파일로 작성해서 템플릿으로 만들어둘 수 있다.
        
- /mcp 명령어
    - mcp 서버와 연동하여 작업이 가능
    - 단점으로는 mcp가 너무 많으면 토큰을 많이 사용하게 됨
        
- /commands 폴더
    - / 를 했을때 나오는 기본 커맨드를 커스텀해서 사용할 수 있다.
    - 예를 들어 위에서 생성한 agent에서 고정해서 사용하고 싶은 경우 command로 만들어서 사용할 수 있다.
    - 위 명령어를 사용하지 않는 다면 /agents 명령어를 사용해서 선택해서 사용할 수 있는데 복잡하다.
        
- claude -c
    - 만약 중간에 실수 or 컴퓨터 문제로 터미널이 꺼진 경우 이전 세션에 이어서 작업을 진행할 수 있다.
        

## 클로드 코드 효율을 올리는 방법

- Plan Mode: Claude Code의 핵심 기능
    - 이 모드를 활성화하면 Claude는 아래 로직으로 동작합니다:
        - 먼저 전체 구조 분석
        - 필요한 단계들을 순서대로 목록화
        - 파일별 영향도 분석
        - 리스크 및 테스트 전략 제시
        - 최종적으로 ‘승인(accept)’ 전에는 코드를 절대 수정하지 않음
            
    - 활용 시나리오:
        - 신규 기능 개발 (PRD → Tech Spec)
        - 레거시 코드 리팩토링
        - MSA 서비스 연동 분석
        - CI/CD 설계 변경
            
    - 권장 모델: **Opus**

- shift + tab    
    - 모드 변경
    - accept edits on
        - claude 에게 모든 권한
    - plan mode on
        - 계획을 세우는 모드
        - plan mode에서는 opus 모델을 함께 사용하는게 좋음
            
- agent 생성
    - inherit 모델을 고정해놔라
    - description을 잘 짜야 한다
    - agentId 값을 공유해서 context를 이어갈 수 있다.
        
- opcode (외부 프로그램)
    - claude code dashboard 볼 수 있다.
    - think mode나 model을 설정할 수 있다.
        
- plugin
    - 로컬에서 사용시 marketplace.json 을 생성해서 플러그인을 등록해서 사용할 수 있음
    - 플러그인 내부에 command를 정의해두는데 해당 command를 플러그인 설정으로 커맨드를 가져다 쓸 수 있다.
    - 플러그인 사용 예시
    - 코드리뷰 플러그인을 만들 수 있다.
    - 테스트 코드 작성 플로그인을 만들 수 있다.
        
- hook
    - 명령에 대한 처리가 끝거나 추가 명령이 필요한 경우 hook을 통해 응답을 받을 수 있다.
        
- 프롬프트를 잘못 입력했을 때
    - esc 키를 1번 누르면 현재 실행중인 프롬프트가 취소된다. 잘못 입력한 경우엔 바로 esc로 취소하자.
        

## Skills Tip

> [https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices)
> 
> 권고하는 공식 베스트 프랙티스가 존재 하기 때문에, 직접 읽어보시는걸 추천

### 1. 간결하게 작성

- **SKILL.md는 500줄 이하 (이상적: 50-150줄)**
- Claude가 이미 아는 내용 제외
- 간결하게 작성한다고 최소 컨텍스트를 작성하지 않으면 안됨
    

### 2. 참조가 깊으면 안됨

- **참조는 1단계만**
    - SKILL.md → 참조 파일 (직접)
        
- 나쁜 예:
    - SKILL.md → 참조1 → 참조2 → 참조3

### 3. **Description**

- 무엇을 하는지와 언제 사용하는지를 포함 하여 작성 해야 함
- 좋은 예:
    - description: PDF 파일에서 텍스트 및 표 추출, 양식 작성, 문서 병합. PDF 파일로 작업하거나 사용자가 PDF, 양식 또는 문서 추출을 언급할 때 사용합니다.
        
- 나쁜 예:
    - description: 문서 작업을 도와줍니다

### 4. skills는 모든 모델로 테스트

- skills가 완성되면 사용 가능한 모델들로 테스트 하는게 좋다.
    - output을 비교하며 모델별로 해당 skill에 가장 적합한 모델 선택