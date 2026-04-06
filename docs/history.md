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
