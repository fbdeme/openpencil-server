# CLAUDE.md

## Project Overview

OpenPencil 디자인 에디터를 Docker + Cloudflare Tunnel로 배포하여, 4인 팀이 웹 브라우저로 접속해 디자인 협업하고 각자 Claude Code MCP로 디자인 파일을 조작할 수 있는 환경 구축.

## Architecture

```
[Team Members' Browsers] → https://xxxx.trycloudflare.com
                                    ↓
                          [Docker: cloudflared tunnel]
                                    ↓
                          [Docker: OpenPencil :3000]

[Each Developer's Claude Code] → MCP (stdio) → @open-pencil/mcp → .fig files
```

## Tech Stack

- **OpenPencil**: ZSeven-W/openpencil (Docker image)
- **Tunnel**: Cloudflare Tunnel (Quick Tunnel, 도메인 불필요)
- **MCP**: @open-pencil/mcp (for Claude Code integration)
- **Container**: Docker + Docker Compose

## Key Commands

```bash
# Start all services (OpenPencil + Cloudflare Tunnel)
docker compose up -d

# Check tunnel URL
docker compose logs tunnel | grep trycloudflare.com

# Stop
docker compose down

# MCP setup (each developer's local machine)
bun add -g @open-pencil/mcp
claude mcp add --transport stdio open-pencil -- openpencil-mcp
```

## Ports

| Service | Port | Purpose |
|---------|------|---------|
| OpenPencil | 3000 | Web UI (Nitro server) |

## File Structure

```
openpencil-server/
├── docker-compose.yml      # OpenPencil + Cloudflare Tunnel 서비스 정의
├── .env.example             # 환경변수 템플릿
├── .gitignore               # .env, node_modules/, *.fig 제외
├── README.md                # 팀원용 세팅 가이드 (한국어)
├── CLAUDE.md                # Claude Code 작업 지침 (이 파일)
└── docs/                    # 프로젝트 문서
    ├── current_state.md     # 현재 인프라/파일 상태
    ├── history.md           # 작업 이력 (시간순)
    ├── todo.md              # 해야 할 일 / 완료된 일
    ├── issues.md            # 알려진 이슈 및 제약 사항
    └── product_concepts.md  # 프로젝트 목표, 핵심 컨셉, 기술 선택 이유
```

## docs/ 관리 규칙

새로운 Claude Code 세션에서 작업을 이어갈 때 반드시 `docs/` 아래 문서를 먼저 읽고 현재 상태를 파악한 뒤 작업을 시작할 것.

### 각 문서의 역할과 업데이트 시점

| 문서 | 역할 | 언제 업데이트 |
|------|------|--------------|
| `current_state.md` | 현재 인프라/파일 상태 스냅샷 | 인프라 변경, 파일 추가/삭제, 서비스 상태 변경 시 |
| `history.md` | 작업 이력 (시간순) | 작업 완료 시 해당 날짜에 항목 추가 |
| `todo.md` | 할 일 목록 (미완료/완료) | 새 작업 식별 시 추가, 완료 시 체크 |
| `issues.md` | 알려진 이슈/제약 사항 | 이슈 발견 시 추가, 해결 시 "해결됨"으로 이동 |
| `product_concepts.md` | 프로젝트 목표/컨셉/기술 선택 | 방향 변경이나 새로운 의사결정 시 |

### 작업 흐름

1. **작업 시작 전**: `docs/` 전체를 읽고 현재 상태, 미완료 TODO, 활성 이슈 파악
2. **작업 중**: 의미 있는 변경이 생기면 관련 문서 즉시 업데이트
3. **작업 완료 후**: `current_state.md` 갱신, `history.md`에 기록 추가, `todo.md` 체크
