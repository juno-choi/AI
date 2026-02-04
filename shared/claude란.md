# claude란?

- AI 코딩 자동화 도구이다. 
- cursor, antigravity와는 다르게 ide가 따로 없고 러닝커브가 존재한다.
- 정해진 token만큼 사용 처리가 가능하여 token을 아끼는 방법을 연구해야한다.

## claude code를 어떻게 대해야할까?
- MIT 출신 모든 개발 doc을 마스터한 신입 입사자
    - 그 외에는 아무것도 모르는 신입 개발자
    - 우리 프로젝트에 대해 자세히 설명해주어야 한다.        
    - 개발 방향에 대해서도 자세히 설명해주어야 한다.

## Claude를 사용하며 알아야 할 부분

### model

- opus
    - 제일 고도화된 모델, 플랜을 짜거나 깊게 생각해야할 경우 유용하다.
        - 사용 예: 복잡한 설계 리뷰, 정책/규격 문서 작성, 코드 베스트 프랙티스 설계, 긴 레거시 코드 이해
    - 토큰 비용이 가장 비싸다.
    - 제일 느리다.
        
- sonnet
    - opus보다 빠르고 코딩에 있어 가장 효율이 좋다고 알려져 있다.
        - 사용 예: 일반적인 코드 작성/리팩터링, 테스트 코드 생성, API 명세/에러 메시지 설계
            
- haiku
    - 가장 빠르다.
    - 가볍게 질문을 하거나 에러를 찾아내는 등 쉬운 업무에 있어 유용하다.
        - 사용 예: 로그/에러 메세지 해석, 간단한 스크립트 생성, 요약, 간단 Q&A

### session

- 1개의 세션은 총 5시간 유효하다.
    - 세션에는 다음 정보들이 포함됩니다:
        - 현재 대화 콘텍스트
        - 선택된 모델 (Sonnet / Opus)
        - 로드된 MCP 서버 목록
        - 허용된/금지된 명령어 설정 (allow/deny)
        - 이전 코드 변경 히스토리
            
- 세션이 유지되는 동안 context를 유지하며 개발을 진행할 수 있다.
    - ‘/clear’ 또는 초기화(MCP 서버 재등록 등)를 하면 세션 콘텍스트 메모리가 모두 사라짐
    - ‘compact’는 오래된 대화를 압축하지만, 일부 세부 맥락이 소실될 수 있음
        
- 5시간 이후에 새로운 session이 열린다. 토큰 사용량은 5시간 기준으로 롤링되고 있기 때문에 세션 기준으로 잡으면 편하다.
    

### session 최적 활용법

- 회사원 기준(9-18)
    - 8시 기상하여 클로드에게 안녕? or 오늘 날씨 어때? 와 같은 의미 없는 대화를 시작한다.
        - 8~13 세션 유지 가능
    - 9시 출근
        - 출근하여 점심시간 전까지 열심히 토큰을 사용한다.
    - 13시 (점심 식사 이후) 이후에 새로운 세션으로 토큰이 초기화된다.
        - 퇴근까지 열심히 토큰을 사용한다.
            
- 위 방법으로 세션을 사용한다면 출근하여 퇴근까지 토큰을 최대치로 활용할 수 있다.
- 단, 최근 1일 기준이 아닌 1주일 기준 토큰 제한이 생겼다. 해당 토큰 값까지 잘 계산해서 활용하는게 필요하다.
    
### Token

- claude는 요청마다 토큰이 소모된다. 결제 타입에 따라 토큰이 많이 모자를 수 있다.
- ai와 함께하는 개발자는 이 토큰을 어떻게 줄일 수 있을까 많은 고민이 필요하다.
    - 이후에 사용하는 skill, agent 등 모두 토큰을 적게 사용하면서 더 좋은 결과를 얻기 위한 과정들이다.

### agent

- 예시
    - backend-architect: 백엔드 MSA 구조 분석 전용    
        - Spring Boot / Kafka / SQS / SNS / RDS 패턴 학습됨
        - ‘use proactively’ 키워드를 description에 포함하면 자동 트리거 활성화
    - code-reader: 대규모 파일 분석 시 사용
        - 성능 향상을 위해 Sonnet 4.5 권장
    - error-detective: 장애 트러블슈팅 전용
        - 로그 분석, 예측 원인, 재현 절차, 개선책 자동 생성
            

```
---
name: backend-architect
description: Backend system architecture and API design specialist. Use PROACTIVELY for RESTful APIs, microservice boundaries, database schemas, scalability planning, and performance optimization.
tools: Read, Write, Edit, Bash
model: inherit
color: red
---

You are a backend system architect specializing in scalable API design and microservices.

## Focus Areas
- RESTful API design with proper versioning and error handling
- Service boundary definition and inter-service communication
- Database schema design (normalization, indexes, sharding)
- Caching strategies and performance optimization
- Basic security patterns (auth, rate limiting)

## Approach
1. Start with clear service boundaries
2. Design APIs contract-first
3. Consider data consistency requirements
4. Plan for horizontal scaling from day one
5. Keep it simple - avoid premature optimization

## Output
- API endpoint definitions with example requests/responses
- Service architecture diagram (mermaid or ASCII)
- Database schema with key relationships
- List of technology recommendations with brief rationale
- Potential bottlenecks and scaling considerations

Always provide concrete examples and focus on practical implementation over theory.

```

- 특정 일을 맡는 전문가
- 역할, 설명, 도구, 행동 패턴들을 미리 정의해두고 필요에 따라 전문가를 통해 문제를 해결하는데 도움이 된다.
    

### skill
- 에이전트가 쓸 수 있는 능력    
- claude에게 장착 시켜주면 그 기능을 자동으로 활용할 수 있게 된다.
    - git commit convention을 미리 skill로 등록해주면 해당 컨벤션에 따라 작성
        

### command
- 매크로
- 프롬프트를 매번 작성해서 여러 과정을 진행해야하는 부분을 command를 통해 한번에 처리할 수 있다.
    - git diff 명령어를 통해 내가 지금까지 작업한 내용에 대해 git commit을 작성해줘 같은 부분을 프롬프트를 작성할때마다 고민하면서 쓰지 않고 /review-commit 과 같은 커맨드를 생성해두고 반복 사용 가능
        

### hook
- 정해진 순간에 자동으로 실행되는 규칙
    - claude가 파일을 수정하기 직전에 항상 git branch를 새롭게 생성해라
    - 업무가 종료된 경우엔 항상 테스트 코드를 실행하고, 실패한다면 알림을 보내라

### mcp

- ai가 사용하는 외부 도구
    - 예를 들어 github mcp를 사용하면 git issue, git pr 등 여러가지 기능을 활용할 수 있다.
- smithery 사이트에서 여러 mcp를 찾아보고 적용할 수 있다.
- mcp를 사용하는 것도 모두 토큰이기 때문에 정말 필요한 mcp만 상황에 맞춰 active 하는 것이 좋다.
- 외부 mcp 사용시 우리의 코드가 외부로 유출되어질 수 있기 때문에 보안에 신경을 쓰면서 사용해야 한다.
    

#### MCP 서버 사용 전략

- MCP 서버는 3가지 방식이 존재한다:
    1. Local MCP Server (내 개발환경에서 실행)
    2. Remote MCP Server (회사 내 특정 URL에 배포)
    3. Polling-Based Legacy MCP (deprecated)
        
- 보안 고려사항:
    - 회사 소스 코드가 원격 MCP로 전송되지 않는 구조이며, MCP 요청은 ‘문서 읽기 요청’ 수준임.
    - 단, MCP를 여러 개 등록하면 대화 시작 시 모두 로드되어 토큰이 **급격히** 소모됨 → 사용하지 않는 MCP는 disable 권장
        
- Spring AI 기반 MCP 서버:
    - Spring Boot 도큐먼트나 DB 스키마 등을 MCP로 등록 가능
    - 내부 프레임워크 업그레이드(Spring 3.1 → 3.4 등) 자동화 가능