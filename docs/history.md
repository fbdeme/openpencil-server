# History

프로젝트 진행 과정을 시간순으로 기록합니다.

## 2026-04-06

### 프로젝트 초기 세팅
- `CLAUDE.md`, `.env.example`, `.gitignore` 기존 파일 확인
- `docker-compose.yml` 작성 (openpencil 서비스, 포트 3000)
- `README.md` 작성 (한국어, ngrok 기반 가이드)

### Docker 설치 및 테스트
- 서버에 Docker 미설치 상태 확인
- 사용자가 직접 Docker 설치 (sudo 권한 필요)
- Docker v29.3.1, Compose v5.1.1 설치 완료
- `docker compose up -d` → 컨테이너 정상 실행
- `localhost:3000` HTTP 200 확인

### 터널 방식 변경: ngrok → Cloudflare Tunnel
- 원래 목표가 Cloudflare였음을 확인
- Cloudflare Quick Tunnel은 도메인 없이 사용 가능하다는 점 확인
- `docker-compose.yml`에 `cloudflare/cloudflared` 서비스 추가
- Quick Tunnel URL 생성 확인: `https://cartridges-bare-fold-modem.trycloudflare.com`
- ngrok 대비 장점: 경고 페이지 없음, docker-compose에 통합

### 문서 체계화
- `docs/` 디렉토리 생성
- `current_state.md`, `history.md`, `todo.md`, `issues.md`, `product_concepts.md` 작성
- `CLAUDE.md`에 docs 관리 패턴 추가

### OpenPencil AI Agent 테스트
- 컨테이너 내 Claude CLI 확인 (`/usr/local/bin/claude`)
- `docker compose exec -it openpencil claude /login`으로 OAuth 인증 완료
- AI Agent 채팅 동작 확인
- 채팅 기록 UI가 없는 점 확인 (Claude/Gemini 웹처럼 히스토리 표시 안됨)

### 실시간 협업 검증 → 미지원 확인
- OpenPencil GitHub 로드맵에서 "Collaborative editing"이 미구현 항목임을 확인
- 소스코드에 Yjs, CRDT, WebSocket 등 실시간 동기화 코드 전혀 없음
- "concurrent Agent Teams"는 AI 에이전트 병렬 작업이지, 사람 간 협업 아님
- 여러 사용자 접속 시 각자 독립된 세션, 변경사항 실시간 공유 불가

### 방향 전환 결정: Figma + Figma MCP
- 실시간 협업이 핵심 요구사항이므로 Figma로 메인 도구 전환
- 각 팀원이 로컬 Claude Code + Figma MCP로 Figma 디자인 AI 조작
- OpenPencil은 보조 도구(AI Agent, 오프라인 작업)로 유지

### AI Agent 동작 분석 및 커스텀 스킬 조사
- 이미지를 주면 웹사이트로 변환하는 이유 분석: AI 시스템 프롬프트가 UI/웹 디자인 전용
- 주요 역할: "frontend designer", "design assistant", "design system architect" 등
- `design.md` (Design System 패널): 스타일 제약만 변경 가능, 동작 방식 변경 불가
- 스킬 파일: AI의 사고/행동 방식 자체를 변경 가능하나 소스 리빌드 필요

### OpenPencil 스킬 구조 파악
- 소스 클론하여 `packages/pen-ai-skills/skills/` 구조 확인
- 스킬 = YAML 프론트매터 + 마크다운 프롬프트 (.md 파일)
- 카테고리: domains, knowledge, phases (planning/generation/validation/maintenance), style-guides
- 빌드 파이프라인: .md → vite-plugin-skills.ts → _generated/skill-registry.ts
- Docker 이미지에는 빌드 결과물만 포함, 런타임 스킬 추가 불가

### OpenPencil 소스 포크 및 커스텀 빌드 착수
- 목표: 이미지 충실 재현 스킬 추가 + Docker 이미지 리빌드
- 포크 → 스킬 .md 추가 → Docker 빌드 → docker-compose.yml 교체
