# Current State

> 마지막 업데이트: 2026-04-06

## 방향 전환 결정

OpenPencil은 실시간 멀티유저 협업을 지원하지 않음이 확인됨 (GitHub 로드맵에 미구현 항목). 따라서 **Figma + Figma MCP** 기반 협업으로 전환 예정.

- **OpenPencil**: 서버에 Docker로 유지 (로컬/오프라인 작업, AI Agent 활용)
- **Figma**: 메인 실시간 협업 도구 (팀원 각자 로컬 Claude Code + Figma MCP)

## 인프라 상태

| 구성 요소 | 상태 | 비고 |
|-----------|------|------|
| Docker | 설치 완료 | v29.3.1, Compose v5.1.1 |
| OpenPencil 컨테이너 | 실행 중 | ghcr.io/zseven-w/openpencil:latest, 포트 3000 |
| Cloudflare Tunnel | 실행 중 | Quick Tunnel (도메인 없이 사용) |
| localhost:3000 | 접속 확인 | HTTP 200 |
| 터널 URL | 활성 | `https://cartridges-bare-fold-modem.trycloudflare.com` (재시작 시 변경됨) |
| OpenPencil AI Agent | 동작 확인 | 컨테이너 내 `claude /login` 완료 |
| Figma MCP 연동 | 미착수 | 다음 작업으로 예정 |

## 파일 현황

| 파일 | 상태 | 설명 |
|------|------|------|
| `docker-compose.yml` | 완료 | openpencil + cloudflared tunnel 서비스 |
| `README.md` | 완료 | Cloudflare Tunnel 기준 가이드 (Figma 전환 반영 필요) |
| `CLAUDE.md` | 완료 | Cloudflare 반영 + docs 관리 패턴 포함 |
| `.env.example` | 완료 | Cloudflare Tunnel token 템플릿 |
| `.gitignore` | 완료 | `.env`, `node_modules/`, `*.fig` |
| `docs/` | 완료 | 프로젝트 문서 디렉토리 |

## Docker Compose 구성

```yaml
services:
  openpencil:    # 디자인 에디터 웹 서버 (포트 3000)
  tunnel:        # Cloudflare Quick Tunnel (openpencil:3000으로 프록시)
```
