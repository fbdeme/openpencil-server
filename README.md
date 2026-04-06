# OpenPencil 팀 협업 서버

OpenPencil 디자인 에디터를 Docker + ngrok으로 띄워서, 팀원들이 웹 브라우저로 접속해 디자인 협업하고, 각자 Claude Code MCP로 .fig 파일을 조작할 수 있는 환경입니다.

## 서버 세팅 (관리자)

### 1. Docker 설치 확인

```bash
docker --version
docker compose version
```

### 2. OpenPencil 실행

```bash
docker compose up -d
```

`http://localhost:3000`으로 접속되는지 확인합니다.

### 3. ngrok 설치 및 설정

1. [ngrok 다운로드](https://ngrok.com/download)에서 설치
2. [ngrok 가입](https://dashboard.ngrok.com/signup) (무료)
3. authtoken 설정:

```bash
ngrok config add-authtoken <your-token>
```

### 4. 터널 실행

```bash
ngrok http 3000
```

터미널에 표시되는 `https://xxxx.ngrok-free.app` URL을 팀원에게 공유합니다.

> **주의:** 무료 플랜은 ngrok을 재시작할 때마다 URL이 변경됩니다.

### 5. 서버 종료

```bash
docker compose down
```

## 팀원 접속

1. 관리자에게 공유받은 URL(`https://xxxx.ngrok-free.app`)을 브라우저에서 접속
2. OpenPencil 에디터에서 디자인 작업 시작

## Claude Code MCP 연동 (각 개발자)

### 설치

```bash
bun add -g @open-pencil/mcp
claude mcp add --transport stdio open-pencil -- openpencil-mcp
```

### 사용 가능한 주요 도구 (90개)

| 카테고리 | 도구 예시 |
|----------|----------|
| 도형 생성/편집 | `create_shape`, `set_fill`, `set_stroke`, `set_layout` |
| 파일 입출력 | `open_file`, `save_file` (.fig 파일 읽기/쓰기) |
| 노드 탐색/조작 | `get_page_tree`, `find_nodes`, `group_nodes`, `clone_node` |
| 내보내기 | `export` (PNG, SVG) |

## Git 협업 워크플로우

- `.fig`는 바이너리 파일이므로 동시 수정 시 충돌이 불가피합니다.
- 각자 feature 브랜치에서 작업 후 main에 머지합니다.
- 같은 파일을 동시에 수정해야 할 경우: 웹 UI에서 P2P 실시간 협업 후 한 명이 commit합니다.

## 참고 링크

- [OpenPencil GitHub](https://github.com/ZSeven-W/openpencil)
- [OpenPencil MCP 문서](https://openpencil.dev/programmable/mcp-server)
- [ngrok](https://ngrok.com)
