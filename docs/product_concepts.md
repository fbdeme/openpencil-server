# Product Concepts

## 프로젝트 목표

4인 디자인 팀이 Figma로 실시간 협업하면서, 각 개발자가 Claude Code + Figma MCP를 통해 프로그래밍 방식으로 디자인을 조작할 수 있는 환경 구축. OpenPencil은 보조 도구(로컬/오프라인, AI Agent)로 활용.

## 방향 전환 경위 (2026-04-06)

초기에는 OpenPencil만으로 실시간 협업을 구상했으나, 검증 결과:
- OpenPencil의 "Collaborative editing"은 GitHub 로드맵에 **미구현 항목**
- 소스코드에 Yjs, CRDT, WebSocket 등 실시간 동기화 코드 없음
- "concurrent Agent Teams"는 AI 에이전트 병렬 작업이지, 사람 간 협업 아님

→ **Figma (실시간 협업) + Figma MCP (AI 연동)** 으로 메인 도구 전환 결정

## 핵심 컨셉

### 1. Figma 기반 실시간 디자인 협업
- Figma 클라우드에서 네이티브 멀티플레이어 지원
- 팀원 각자 Figma 계정으로 동일 파일 동시 편집 가능
- 커서 공유, 코멘트, 버전 히스토리 등 협업 기능 내장

### 2. Claude Code + Figma MCP
- 각 팀원이 로컬 Claude Code에 Figma MCP 연결
- Claude Code로 Figma 디자인을 읽고, 생성하고, 수정 가능
- 디자인 → 코드 변환, AI 기반 디자인 자동화

### 3. OpenPencil (보조 도구)
- Docker + Cloudflare Tunnel로 서버에 유지
- AI Agent 기능 활용 (텍스트 → 디자인 생성)
- 오프라인/로컬 작업 시 활용
- `@open-pencil/mcp`로 .fig 파일 프로그래밍 조작 가능

## 사용 시나리오 (전환 후)

```
[메인 워크플로우 - Figma]
1. 팀원 각자 Figma 계정으로 공유 파일 접속
2. 브라우저에서 실시간 동시 편집
3. 각자 로컬 Claude Code + Figma MCP로 AI 디자인 조작
4. Figma 자체 버전 관리 활용

[보조 워크플로우 - OpenPencil]
1. 서버에서 docker compose up -d 실행
2. Cloudflare Tunnel URL로 접속
3. AI Agent로 텍스트 → 디자인 생성
4. .fig 파일 로컬 작업 시 활용
```

## 기술 선택 이유

| 선택 | 이유 |
|------|------|
| Figma | 네이티브 실시간 협업, MCP 지원, 업계 표준 |
| Figma MCP | Claude Code에서 Figma 디자인 읽기/생성/수정 |
| OpenPencil | 오픈소스, AI Agent 내장, 셀프호스팅 가능 (보조) |
| Docker | 환경 일관성, 한 줄로 실행 가능 |
| Cloudflare Tunnel | 무료, 도메인 불필요(Quick Tunnel), 경고 페이지 없음 |
