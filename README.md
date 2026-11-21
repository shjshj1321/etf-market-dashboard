# NASDAQ 투자 대시보드 (GitHub Pages 전용)

기존 `etf-signals` 저장소는 수정하지 않습니다. 이 프로젝트는 **새 GitHub 저장소**에 올리세요.

## 포함된 지표

- QLD/TQQQ: 완료 주봉 RSI(14, Wilder), 일봉 200일 이동평균선 괴리율, 유튜버 공개 1~3차 신호
- 나스닥100(`^NDX`): 최근 252거래일 일봉 **종가** 최고점 대비 하락률, 200일 이동평균선 위/아래
- VIX(`^VIX`): 최근 수치와 참고 구간(20, 30)
- 단계별 매수 예산 계산기: 입력값은 서버로 전송하지 않음

Yahoo Finance의 비공식 차트 경로를 사용하므로 조회 실패·차단·시세 지연 가능성이 있습니다. 실시간 시세가 아닙니다. 장중에는 일봉 마지막 값이 미확정일 수 있습니다. 신호는 투자 권유가 아닙니다.

## 설치 (GitHub 웹에서)

1. GitHub에서 **새 공개 저장소** `etf-market-dashboard`를 만듭니다. **기존 `etf-signals` 저장소는 건드리지 마세요.**
2. ZIP 압축을 풀고 그 안의 `docs`, `scripts`, `README.md`를 새 저장소의 최상위에 업로드합니다. ZIP 자체를 올리지 않습니다.
3. `.github` 폴더가 숨김 처리되어 업로드되지 않는다면 GitHub의 **Add file → Create new file**에서 파일 이름을 `.github/workflows/update.yml`로 입력하고, 압축을 푼 동일 경로의 YAML 파일 내용을 붙여넣은 뒤 Commit합니다.
4. **Settings → Actions → General → Workflow permissions → Read and write permissions** 선택 후 저장합니다.
5. **Actions → Update market dashboard → Run workflow** 실행. 녹색 체크가 뜨는지 확인합니다. 이 단계에서 실제 시세 조회가 실패하면 Actions 실행 로그를 확인하세요.
6. **Settings → Pages → Source: Deploy from a branch → Branch: main → Folder: /docs → Save**.
7. 몇 분 뒤 `https://깃허브아이디.github.io/etf-market-dashboard/`에서 확인합니다.

예약 실행은 UTC 월~금 22:30(한국시간 화~토 오전 7:30)이며 지연될 수 있습니다. 미국 휴장일에는 마지막 제공 데이터를 유지할 수 있습니다.

## 계산 주의점

- 나스닥100 52주 고점은 **장중 고점이 아닌 최근 252거래일 종가 최고점**입니다.
- ETF 200일선은 각 ETF의 일봉 종가로 계산합니다. 주봉 RSI는 뉴욕 시간 기준 주간 마지막 종가로 계산하며 진행 중인 주는 확정 RSI에서 제외합니다.
- 종목 분할 및 배당 조정 방식에 따라 다른 차트 서비스와 지표가 차이 날 수 있습니다.
- ETF 신호는 RSI 또는 괴리율 중 하나만 임계값에 닿아도 해당 단계입니다. 나스닥100/VIX는 ETF 신호 단계에 영향을 주지 않습니다.
- 가격 데이터 날짜는 제공업체의 일봉 타임스탬프에 기반하며, 장 마감 확정 여부를 별도 검증하지 않습니다.
