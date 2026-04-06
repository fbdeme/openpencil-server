# Issues

알려진 이슈와 제약 사항을 기록합니다.

## 활성 이슈

### 1. Cloudflare Quick Tunnel URL이 재시작마다 변경됨
- **심각도:** 중간
- **설명:** Quick Tunnel(도메인 없이 사용)은 컨테이너 재시작 시 URL이 바뀜
- **영향:** 매번 팀원에게 새 URL 공유 필요
- **해결 방안:** Cloudflare 계정 + 도메인으로 Named Tunnel 설정 시 고정 URL 사용 가능

### 2. UDP 버퍼 크기 경고
- **심각도:** 낮음
- **설명:** cloudflared 로그에 `failed to sufficiently increase receive buffer size` 경고 출력
- **영향:** 기능에는 영향 없음, QUIC 성능이 약간 저하될 수 있음
- **해결 방안:** 호스트에서 `sudo sysctl -w net.core.rmem_max=7500000` 실행

## 해결됨

- ~~README.md가 ngrok 기준으로 작성됨~~ → 2026-04-06 Cloudflare 기준으로 업데이트 완료
- ~~Docker 미설치~~ → 2026-04-06 설치 완료
- ~~sudo 권한 없음~~ → 사용자가 직접 설치로 해결
