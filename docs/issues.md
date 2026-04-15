# Issues

알려진 이슈와 제약 사항을 기록합니다.

## 활성 이슈

### 1. OpenPencil 실시간 멀티유저 협업 미지원 (치명적)
- **심각도:** 높음
- **설명:** OpenPencil은 실시간 협업(Collaborative editing)이 아직 미구현. GitHub 로드맵에 미체크 항목으로 남아있음.
- **영향:** 여러 팀원이 같은 캔버스를 동시에 편집/확인 불가. 각자 독립된 세션.
- **대응:** Figma + Figma MCP 기반으로 메인 협업 도구 전환 결정

### 2. 이미지 첨부 시 여전히 웹 디자인으로 변환됨
- **심각도:** 높음
- **설명:** chat.ts에 imageReproductionHint 추가, 커스텀 스킬 추가했으나, Claude Agent SDK 경로의 시스템 프롬프트가 UI 디자인 생성에 강하게 바인딩되어 있어 무시됨
- **영향:** 이미지를 주고 "그대로 그려줘"해도 웹사이트 디자인을 생성
- **원인 추정:** Agent SDK 내부 시스템 프롬프트 > 우리가 추가한 힌트. 소스 코드 깊이 분석 필요
- **다음 단계:** OpenPencil의 AI 파이프라인(generate.ts, chat.ts, agent SDK 호출부) 전체를 분석해서 시스템 프롬프트 우선순위 파악

### 3. OpenPencil 채팅 기록 UI 부재
- **심각도:** 중간
- **설명:** Agent 채팅이 Claude/Gemini 웹처럼 대화 히스토리를 보여주지 않음
- **영향:** 이전 대화 내용 확인 어려움
- **대응:** 당장 해결 어려움 (OpenPencil 소스 수정 필요)

### 3. Cloudflare Quick Tunnel URL이 재시작마다 변경됨
- **심각도:** 중간
- **설명:** Quick Tunnel(도메인 없이 사용)은 컨테이너 재시작 시 URL이 바뀜
- **영향:** 매번 팀원에게 새 URL 공유 필요
- **해결 방안:** Cloudflare 계정 + 도메인으로 Named Tunnel 설정 시 고정 URL 사용 가능

### 4. UDP 버퍼 크기 경고
- **심각도:** 낮음
- **설명:** cloudflared 로그에 `failed to sufficiently increase receive buffer size` 경고 출력
- **영향:** 기능에는 영향 없음, QUIC 성능이 약간 저하될 수 있음
- **해결 방안:** 호스트에서 `sudo sysctl -w net.core.rmem_max=7500000` 실행

## 해결됨

- ~~README.md가 ngrok 기준으로 작성됨~~ → 2026-04-06 Cloudflare 기준으로 업데이트 완료
- ~~Docker 미설치~~ → 2026-04-06 설치 완료
- ~~sudo 권한 없음~~ → 사용자가 직접 설치로 해결
