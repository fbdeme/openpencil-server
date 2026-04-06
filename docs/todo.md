# TODO

## 미완료

### 문서 업데이트
- [ ] `README.md`를 Cloudflare Tunnel 기준으로 재작성
- [ ] `.env.example`에서 ngrok 관련 내용 제거 또는 Cloudflare 옵션 추가
- [ ] `CLAUDE.md` Architecture 섹션 Cloudflare 반영

### 인프라
- [ ] Cloudflare 계정 + 도메인 연결 시 Named Tunnel로 전환 (고정 URL)
- [ ] ngrok 관련 설정 완전 제거 여부 결정 (fallback으로 유지할지)

### MCP 연동
- [ ] `@open-pencil/mcp` 설치 및 연동 테스트
- [ ] MCP로 .fig 파일 생성/조작 테스트

### 팀 온보딩
- [ ] 팀원 4명에게 터널 URL 공유
- [ ] 각 팀원 Claude Code MCP 설정 가이드 제공
- [ ] 웹 브라우저 P2P 실시간 협업 테스트

## 완료

- [x] `docker-compose.yml` 작성
- [x] `README.md` 초안 작성 (ngrok 기준)
- [x] Docker 설치
- [x] OpenPencil 컨테이너 실행 및 접속 확인
- [x] Cloudflare Quick Tunnel 연동 및 URL 생성 확인
- [x] `docs/` 문서 체계 구축
