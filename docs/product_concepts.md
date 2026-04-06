# Product Concepts

## 프로젝트 목표

4인 디자인 팀이 OpenPencil로 실시간 협업하면서, 각 개발자가 Claude Code MCP를 통해 프로그래밍 방식으로 디자인 파일(.fig)을 조작할 수 있는 환경 구축.

## 핵심 컨셉

### 1. 웹 기반 디자인 협업
- OpenPencil 에디터를 서버에 호스팅
- 팀원들은 브라우저로 접속하여 실시간 P2P 협업
- 별도 소프트웨어 설치 불필요 (브라우저만 있으면 됨)

### 2. 터널을 통한 외부 접속
- 서버가 내부 네트워크에 있어도 외부에서 접속 가능
- Cloudflare Tunnel 사용 (1차), ngrok은 fallback 옵션
- 향후 도메인 연결로 고정 URL 확보 가능

### 3. Claude Code MCP 연동
- `@open-pencil/mcp`를 통해 Claude Code에서 .fig 파일 직접 조작
- 90개 이상의 도구: 도형 생성, 스타일 변경, 노드 탐색, 파일 입출력, 내보내기
- 각 개발자의 로컬 Claude Code에서 독립적으로 MCP 연결

### 4. Git 기반 파일 관리
- .fig 파일은 바이너리이므로 Git merge 충돌 시 수동 해결 필요
- feature 브랜치 전략으로 충돌 최소화
- 동시 수정이 필요한 경우 웹 UI P2P 협업 후 한 명이 commit

## 사용 시나리오

```
1. 관리자가 서버에서 docker compose up -d 실행
2. Cloudflare Tunnel URL을 팀원에게 공유
3. 팀원 A, B: 브라우저에서 URL 접속 → OpenPencil에서 디자인 작업
4. 팀원 C, D: Claude Code MCP로 .fig 파일 프로그래밍 조작
5. 작업 완료 후 Git으로 .fig 파일 버전 관리
```

## 기술 선택 이유

| 선택 | 이유 |
|------|------|
| OpenPencil | 오픈소스 Figma 대안, 셀프호스팅 가능, MCP 지원 |
| Docker | 환경 일관성, 한 줄로 실행 가능 |
| Cloudflare Tunnel | 무료, 도메인 불필요(Quick Tunnel), 경고 페이지 없음 |
| Claude Code MCP | AI 기반 디자인 자동화, 90개 도구로 프로그래밍 방식 조작 |
