# TODO

## 미완료

### Figma MCP 전환 (다음 작업)
- [ ] 팀원 각자 Figma 계정 생성/확인
- [ ] 공유 Figma 프로젝트/파일 생성
- [ ] 각 팀원 로컬 Claude Code에 Figma MCP 설정
- [ ] Figma MCP로 디자인 읽기/생성/수정 테스트
- [ ] 팀원 간 실시간 동시 편집 테스트

### 문서 업데이트
- [x] `README.md`를 Cloudflare Tunnel 기준으로 재작성
- [x] `.env.example`에서 ngrok 관련 내용 제거 → Cloudflare 옵션으로 변경
- [x] `CLAUDE.md` Architecture 섹션 Cloudflare 반영
- [ ] `README.md`에 Figma MCP 워크플로우 추가
- [ ] `CLAUDE.md` Architecture에 Figma 반영

### OpenPencil (보조)
- [ ] `@open-pencil/mcp` 설치 및 연동 테스트
- [ ] Cloudflare 계정 + 도메인 연결 시 Named Tunnel로 전환 (고정 URL)

### 팀 온보딩
- [ ] Figma 공유 파일 URL 팀원에게 공유
- [ ] 각 팀원 Figma MCP 설정 가이드 제공
- [ ] OpenPencil 터널 URL 공유 (보조 도구)

## 완료

- [x] `docker-compose.yml` 작성
- [x] `README.md` 초안 작성 (ngrok 기준) → Cloudflare로 업데이트
- [x] Docker 설치
- [x] OpenPencil 컨테이너 실행 및 접속 확인
- [x] Cloudflare Quick Tunnel 연동 및 URL 생성 확인
- [x] `docs/` 문서 체계 구축
- [x] OpenPencil AI Agent 로그인 (`claude /login`)
- [x] OpenPencil 실시간 협업 가능 여부 조사 → 미지원 확인
- [x] Figma + Figma MCP 전환 결정
