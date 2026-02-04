# Claude Code Cheat Sheet

> v1.0 (2026-01-08)

---

## Key Commands

```bash
/init            # 프로젝트 시작, CLAUDE.md 생성
/help (or ?)     # 도움말
/model           # 모델 변경 (Opus / Sonnet / Haiku)
/clear           # 대화 초기화
/exit            # 종료
Shift + Tab      # 응답 모드 전환 (Normal / Auto / Plan)
opt + p          # 프롬프트 작성 중 model 전환
```

### Prefix

```text
#   : CLAUDE.md 노트 저장
>   : 즉시 커맨드 실행
!   : Bash 명령 직접 실행
?   : 파일/경로 참조
```

---

## Project Management

```bash
/init                # CLAUDE.md 초기화
/memory              # CLAUDE.md 편집
/add-dir             # 작업 디렉토리 추가
/export file         # 대화 내보내기 (txt, md, log)
```

---

## Session & Context

```bash
/resume (session)    # 이전 세션 복원
/rename (name)       # 현재 세션 이름 변경
/context             # 컨텍스트 사용량 시각화
/compact [inst]      # 컨텍스트 압축
```

---

## Model & AI

```bash
/model               # 대화 모델 변경
/agents              # 커스텀 서브에이전트 관리
/plan                # 플랜 모드 전환 (Opus 추천)
```

---

## Code Quality

```bash
/review              # 코드 리뷰 요청
/security_review     # 보안 취약점 점검
/pr-comments         # GitHub PR 코멘트 확인
```

---

## Monitoring

```bash
/cost                # 토큰 사용량
/usage               # 월별 사용량 & Rate Limit
/stats               # 일일 사용량, 세션 히스토리
/todos               # TODO 목록
```

---

## Settings

```bash
/config              # 설정 (Config 탭)
/status              # 상태 확인
/permissions         # 권한 관리
```

---

## MCP (Model Context Protocol)

```bash
/mcp                 # MCP 서버 관리 대시보드
```

```bash
ex) mcp github_list_prs
# github MCP 서버에서 PR 목록 조회
```

---

## Claude Skills

### 기본 구조

```text
.claude/skills/skill_name/
 ├─ skill.md        # 필수: 개요 및 네비게이션
 ├─ reference.md    # 선택: 상세 문서
 ├─ example.md      # 선택: 사용 예시
 ├─ scripts/        # 선택: 유틸리티 스크립트
 └─ helper.py       # 선택: 보조 로직

SKILL.md
 ├─ name
 ├─ description
 ├─ allowed_tools
 └─ model
```

- **skill.md / SKILL.md 필수**
    
- description은 짧고 명확하게
    
- allowed_tools: Bash, Read, Write 등
    
- model 예시: `claude-sonnet-4.5-20250209`
    

---

## Hooks (Events Automation)

```text
Pre/PostToolUse
PostToolUseFailure
Notification
UserPromptSubmit
SessionStart / SessionEnd
SubagentStart
PreCompact
Stop
PermissionRequest
```

- 툴 실행 전/후
    
- 실패 시 알림
    
- 세션 시작/종료 시
    
- 서브에이전트 실행 전
    
- 컨텍스트 압축 전
    
- 중단 요청 시
    
- 권한 요청 시
    

---

## Plugins (Expansion)

```bash
/plugin                          # 플러그인 관리 대시보드
/plugin name command args        # 플러그인 실행
```

예시:

```bash
/plugin document_skills.pdf      # PDF 생성/파싱
```

---

## Agents (Subagents)

```bash
/agents                          # 에이전트 관리
```

```text
~/.claude/agents/*.y             # 에이전트 정의 파일
```

---

## Custom Commands

```text
.claude/commands/**.md           # 프로젝트 공통 커맨드
~/.claude/commands/**.md         # 글로벌 커맨드
```

---

## Conventions

### 1. File Path

```text
single-file
@file.py
@src/model.py
@file.py:10-20
```

```text
Pattern matching
*.py
**/*.py
src/**/test.py
```

### 2. File Coverage Rank

```text
~/.claude/settings.json          # 전역
.claude/settings.json            # 프로젝트
.claude/settings.local.json      # 로컬 (git ignore)
```

---

## Models

### Opus 4.5

- 복잡한 작업에 가장 적합
    
- 약 $5 / $25 per Mtok
    

### Sonnet 4.5

- 일상적인 개발 작업에 적합
    
- 약 $3 / $15 per Mtok
    

### Haiku 4.5

- 빠른 응답, 단순 작업
    
- 약 $1 / $5 per Mtok
    