<div align="center">

<img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/291aefa4-072f-4aaa-9a33-4f17613424a7" />

# TradingView 웹훅 고잉봇

**TradingView 알림 → 자동 주문 실행 데스크톱 애플리케이션**

[![Version](https://img.shields.io/badge/version-0.3.0-00d4aa?style=for-the-badge)](https://github.com/trader-going/tradingview-webhook-bot)
[![License](https://img.shields.io/badge/license-Personal_Use-blue?style=for-the-badge)](#-라이센스)
[![Python](https://img.shields.io/badge/python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![PyQt5](https://img.shields.io/badge/PyQt5-Desktop_GUI-41CD52?style=for-the-badge&logo=qt&logoColor=white)](https://riverbankcomputing.com/software/pyqt/)

<br/>

<img alt="GoingBot Screenshot" src="https://github.com/user-attachments/assets/cfafb0c4-d879-4a39-9161-4fbba0797064" width="800" />

<br/>

[**고잉봇 다운로드**](https://drive.google.com/drive/folders/1-eWL55uQGM83Eqm5irc-tMh6J-QYOVss) · [**설치 가이드**](https://github.com/trader-going/tradingview-webhook-bot/wiki/%EA%B3%A0%EC%9E%89%EB%B4%87-%EC%84%B8%ED%8C%85-%EB%B0%A9%EB%B2%95)   

<br/>

<table>
<tr>
<td align="center">
<a href="https://open.kakao.com/o/g6UiEPei"><img src="https://github.com/user-attachments/assets/ba7cb89e-54da-4c0b-85df-e90c60b4b726" width="140" /></a><br/>
<sub><b><a href='https://open.kakao.com/o/g6UiEPei'>고잉봇 커뮤니티</a></b></sub>
</td>
<td align="center">
<a href="https://open.kakao.com/me/trader_going"><img src="https://github.com/user-attachments/assets/e4d85c5d-1f6b-438b-885b-1c28a0ec26ab" width="140" /></a><br/>
<sub><b><a href='https://open.kakao.com/me/trader_going'>개발자 문의</a></b></sub>
</td>
<td align="center">
<a href="https://open.kakao.com/o/gYMmhcYg"><img src="https://github.com/user-attachments/assets/ab41b9b2-ec17-4243-bbdc-1f50d6ce3a58" width="140" /></a><br/>
<sub><b><a href='https://open.kakao.com/o/gYMmhcYg'>트레이딩뷰 유저 코리아</a></b></sub>
</td>
</tr>
</table>

</div>

<br/>

---

<br/>

## 📋 목차

- [지원 거래소](#-지원-거래소)
- [주요 기능](#-주요-기능)
- [빠른 시작](#-빠른-시작)
- [화면 구성](#️-화면-구성)
- [TradingView 웹훅 설정](#-tradingview-웹훅-설정)
- [기능별 사용법](#-기능별-사용법)
- [설정 옵션](#️-설정-옵션)
- [문제 해결](#-문제-해결)
- [주의사항](#-주의사항)
- [라이센스](#-라이센스)

<br/>

## 🏦 지원 거래소

| 거래소 | 현물 | 선물 | 비고 |
|:------:|:----:|:----:|:----:|
| <img src="https://cdn.jsdelivr.net/gh/nicehash/cryptocurrency-icons/32/color/krw.png" width="16"/> **업비트** | ✅ | — | 국내 최대 거래소 |
| <img src="https://cdn.jsdelivr.net/gh/nicehash/cryptocurrency-icons/32/color/krw.png" width="16"/> **빗썸** | ✅ | — | 국내 거래소 |
| <img src="https://cdn.jsdelivr.net/gh/nicehash/cryptocurrency-icons/32/color/bnb.png" width="16"/> **바이낸스** | — | ✅ | 세계 최대 거래소 (선물 전용) |
| <img src="https://cdn.jsdelivr.net/gh/nicehash/cryptocurrency-icons/32/color/usdt.png" width="16"/> **바이비트** | — | ✅ | 파생상품 거래소 |
| <img src="https://cdn.jsdelivr.net/gh/nicehash/cryptocurrency-icons/32/color/usdt.png" width="16"/> **OKX** | — | 🚧 | 개발 중 |

<br/>

## ✨ 주요 기능

<table>
<tr>
<td width="50%">

### 🤖 자동 매매
TradingView 전략 알림 → 자동 주문 실행

### 📊 실시간 차트
캔들 차트 + 주문 타점 마커 표시

### 💰 잔고 조회
거래소별 잔고 및 수익률 실시간 확인

### 🔔 토스트 알림
웹훅 수신, 주문 체결 시 데스크톱 알림

</td>
<td width="50%">

### 📐 유연한 수량 표현
`100USDT` · `50000KRW` · `25%` · `0.01`

### 🔥 선물 거래 지원
레버리지, 마진모드(격리/교차), 포지션 사이드

### ⚡ 일괄 청산
종목 선택 후 한 번에 청산 (선물 포지션 포함)

### 🔒 보안
IP 화이트리스트 + 프라이버시 모드

</td>
</tr>
</table>

<br/>

## 🚀 빠른 시작

### 필수 준비물

> **거래소 API 키** + **TradingView Pro 이상** + **포트 포워딩 가능한 환경**

### Step 1 — API 키 발급

<details>
<summary><b>🟡 업비트 API 키</b></summary>
<br/>

1. [업비트](https://upbit.com) 로그인 → 마이페이지 → Open API 관리
2. **Open API Key 발급하기** 클릭
3. 권한 설정:
   - ✅ 자산조회 · ✅ 주문조회 · ✅ 주문하기
   - ❌ 출금하기 (보안상 비활성화 권장)
4. **IP 주소 등록** (중요!)
5. API Key와 Secret Key 복사

</details>

<details>
<summary><b>🟡 빗썸 API 키</b></summary>
<br/>

1. [빗썸](https://www.bithumb.com) 로그인 → 마이페이지 → API 관리
2. **API 생성** 클릭
3. 권한 설정:
   - ✅ 거래정보조회 · ✅ 주문
   - ❌ 출금 (비활성화 권장)
4. API Key와 Secret Key 복사

</details>

<details>
<summary><b>🟠 바이낸스 API 키</b></summary>
<br/>

1. [바이낸스](https://www.binance.com) 로그인 → 프로필 → API Management
2. **Create API** 클릭
3. 권한 설정:
   - ✅ Enable Reading · ✅ Enable Futures (선물 거래)
4. IP 접근 제한 설정 권장
5. API Key와 Secret Key 복사

</details>

<details>
<summary><b>🟠 바이비트 API 키</b></summary>
<br/>

1. [바이비트](https://www.bybit.com) 로그인 → 계정 및 보안 → API 관리
2. **새 키 만들기** 클릭
3. 권한 설정:
   - ✅ 거래 읽기/쓰기 · ✅ 포지션 읽기/쓰기
4. API Key와 Secret Key 복사

</details>

### Step 2 — 설정 파일 구성

`config.yml.example` → `config.yml`로 복사 후 API 키 입력:

```yaml
webhook:
  port: 8000

exchanges:
  upbit:
    api_key: "업비트_API_KEY"
    secret_key: "업비트_SECRET_KEY"
  bithumb:
    api_key: "빗썸_API_KEY"
    secret_key: "빗썸_SECRET_KEY"
  binance:
    api_key: "바이낸스_API_KEY"
    secret_key: "바이낸스_SECRET_KEY"
  bybit:
    api_key: "바이비트_API_KEY"
    secret_key: "바이비트_SECRET_KEY"
```

### Step 3 — 프로그램 실행

1. `TradingView_Webhook_GoingBot.exe` 실행
2. 면책조항 동의 (최초 1회)
3. 상단에서 서버 상태 확인 (초록색 **"실행 중"**)
4. 상태바에서 거래소 연결 확인

### Step 4 — 포트 포워딩

TradingView에서 웹훅을 보내려면 외부에서 접근 가능해야 합니다.

<details>
<summary><b>공유기 포트 포워딩</b></summary>
<br/>

1. 공유기 관리 페이지 접속 (보통 `192.168.0.1`)
2. 포트 포워딩 설정 메뉴
3. 설정 추가:

| 항목 | 값 |
|------|-----|
| 외부 포트 | `8000` |
| 내부 IP | 프로그램 실행 PC의 내부 IP |
| 내부 포트 | `8000` |
| 프로토콜 | TCP |

</details>

<details>
<summary><b>ngrok 사용 (대안)</b></summary>
<br/>

포트 포워딩이 어려운 경우:

```bash
ngrok http 8000
```

ngrok에서 제공하는 URL을 TradingView 웹훅 URL로 사용합니다.

</details>

<br/>

## 🖥️ 화면 구성

```
┌──────────────────────────────────────────────────────────────────┐
│  📅 날짜/시간   🌐 IP   💻 CPU/MEM   💱 환율   📈 김프          │  ← 시스템 바
│  UPBIT BTC ₩xxx (±x.xx%)  │  BINANCE BTC $xxx (±x.xx%)        │  ← 실시간 시세
├──────────┬───────────────────────────────────┬───────────────────┤
│ 연결 상태  │  📋 웹훅 로그  📦 주문 내역  ⚠ Warning  │   잔고 현황      │
│          │                                   │  ┌─────────────┐ │
│ 수동 주문  │        💹 실시간 차트              │  │ 업비트│빗썸│…│ │
│          │                                   │  │ BTC 0.5     │ │
│          │                                   │  │ ETH 2.0     │ │
│          │                                   │  └─────────────┘ │
│          │                                   │  [⚡ 일괄청산]    │
├──────────┴───────────────────────────────────┴───────────────────┤
│  🟢 서버: 8000  │  🟢 업비트  │  🟢 바이낸스  │  🟢 바이비트     │  ← 상태바
└──────────────────────────────────────────────────────────────────┘
```

| 영역 | 구성 요소 |
|:----:|----------|
| **상단** | 날짜/시간, IP, CPU/MEM, USD/KRW 환율, 김치프리미엄, BTC/ETH 실시간 시세 |
| **좌측** | 거래소 연결 상태, 수동 주문 패널 |
| **중앙** | 웹훅 로그 · 주문 내역 · Warning 탭, 실시간 캔들 차트 |
| **우측** | 거래소별 잔고 탭 (업비트/빗썸/바이낸스/바이비트), 일괄청산 |
| **하단** | 웹훅 서버 포트, 각 거래소 연결 상태 |

<br/>

## 📡 TradingView 웹훅 설정

### Pine Script 설정

프로그램의 **"트레이딩뷰 예제 전략 복사"** 버튼을 클릭하거나, 아래 함수를 사용:

```pine
// 메시지 생성 함수
build_msg(string action, string qtyStr) =>
     '{"action":"' + action + '"' +
     ',"exchange":"{{exchange}}"' +
     ',"symbol":"{{ticker}}"' +
     ',"price":"{{strategy.order.price}}"' +
     ',"qty":"' + qtyStr + '"' +
     ',"leverage":' + str.tostring(leverage) +
     ',"time":"{{time}}"' +
     '}'

// 진입/청산 시 사용
if longEntry
    strategy.entry("L", strategy.long, qty=btQty, alert_message=build_msg("LONG_ENTRY", "100USDT"))

if longClose
    strategy.close("L", qty=btQty, alert_message=build_msg("LONG_CLOSE", "100%"))
```

### TradingView Alert 설정

1. 차트에서 전략 적용 → **알림(Alerts)** 탭 → **+ 알림 만들기**
2. 조건: `[전략 이름]` / 옵션: `Order fills only`
3. **웹훅 URL** 체크 → `http://[공인IP]:8000/webhook`
4. **메시지**란에 아래 입력:
   ```
   {{strategy.order.alert_message}}
   ```

### 웹훅 JSON 필드

| 필드 | 설명 | 예시 |
|:----:|------|------|
| `action` | 주문 액션 | `LONG_ENTRY`, `LONG_CLOSE`, `SHORT_ENTRY`, `SHORT_CLOSE`, `BUY`, `SELL` |
| `exchange` | 거래소 | `BINANCE`, `UPBIT`, `BITHUMB`, `BYBIT` |
| `symbol` | 심볼 | `BTCUSDT`, `BTC/KRW` |
| `qty` | 수량 | `100USDT`, `50000KRW`, `25%`, `0.01` |
| `leverage` | 레버리지 | `1`, `5`, `10` |
| `price` | 주문 가격 | `43123.4` |

### 수량(qty) 표현 방식

| 형식 | 설명 | 예시 |
|:----:|------|------|
| `{금액}USDT` | USDT 금액 | `100USDT` = 100 USDT 어치 |
| `{금액}KRW` | 원화 금액 | `50000KRW` = 5만원 어치 |
| `{비율}%` | 잔고 비율 | `25%` = 잔고의 25% |
| `{수량}` | 코인 수량 | `0.01` = 0.01개 |

### 거래소 자동 매핑

> [!NOTE]
> 웹훅에서 `BINANCE`로 보내면 자동으로 **바이낸스 선물(BINANCE_FUTURES)**로 처리됩니다.

| 웹훅 exchange | 실제 처리 |
|:-------------:|----------|
| `BINANCE` | 바이낸스 선물 |
| `UPBIT` | 업비트 현물 |
| `BITHUMB` | 빗썸 현물 |
| `BYBIT` | 바이비트 선물 |

<br/>

## 📖 기능별 사용법

<details>
<summary><h3>💰 잔고 조회</h3></summary>
<br/>

1. 우측 패널에서 거래소 탭 선택 (업비트/빗썸/바이낸스/바이비트)
2. 자동으로 잔고 표시 (자동 새로고침 지원)
3. 수동 새로고침: 상단 **새로고침** 버튼

**표시 정보:** 자산명(심볼) · 보유 수량 · 평가 금액 · 수익률(%) · 평균 매수가 · 총 자산

> [!TIP]
> 잔고 행을 클릭하면 해당 심볼의 차트로 자동 전환됩니다.

</details>

<details>
<summary><h3>🛒 수동 주문</h3></summary>
<br/>

좌측 **수동 주문** 패널에서:

1. **거래소 선택** — 업비트(현물) · 빗썸(현물) · 바이낸스(선물) · 바이비트(선물)
2. **심볼 입력** — `BTC` 입력 시 자동 완성: `BTC/KRW`(국내) 또는 `BTC/USDT:USDT`(해외 선물)
3. **주문 유형** — MARKET(시장가) / LIMIT(지정가)
4. **수량 입력** — 단위 선택: KRW/USDT 또는 코인수량
5. **선물 옵션** (바이낸스/바이비트)
   - 레버리지: 1x ~ 125x (빠른 선택 버튼)
   - 마진모드: ISOLATED(격리) / CROSS(교차)
   - 포지션 사이드: BOTH / LONG / SHORT
6. **매수/매도** 버튼 클릭 → 확인 다이얼로그

> [!IMPORTANT]
> **업비트/빗썸 시장가 주의사항**
> - 매수: 수량 = 원화 금액 (예: `10000` = 1만원어치)
> - 매도: 수량 = 코인 수량 (예: `0.001` = 0.001 BTC)

</details>

<details>
<summary><h3>⚡ 일괄 청산</h3></summary>
<br/>

1. 우측 잔고 패널 하단의 **일괄청산** 버튼 클릭
2. 청산할 종목을 선택 (전체 선택 / 개별 선택 가능)
3. **청산 실행** 클릭
4. 종목별 성공/실패 결과 확인

> [!CAUTION]
> 일괄 청산은 되돌릴 수 없습니다. 선물 포지션은 반대 방향 시장가 주문으로 청산됩니다.

</details>

<details>
<summary><h3>📋 웹훅 로그 & 주문 내역</h3></summary>
<br/>

**웹훅 로그 탭** — 날짜, 시간, 거래소, 심볼, 방향, 수량, 상태(SUCCESS/FAILED) 표시
- **더블클릭**: 상세 정보 팝업 (원본 웹훅 JSON 확인)

**주문 내역 탭** — 날짜, 시간, 거래소, 심볼, 방향, 체결수량, 단위, 체결가, 출처, 주문ID
- 출처: `webhook`(웹훅) / `manual`(수동) — 색상 구분

**하단 컨트롤** — 자동 스크롤 · DB 새로고침 · 로그 지우기

</details>

<details>
<summary><h3>📊 차트</h3></summary>
<br/>

| 기능 | 설명 |
|------|------|
| 캔들 차트 | lightweight-charts 기반 실시간 |
| 타임프레임 | 1m · 5m · 15m · 1h · 4h · 1d · 1w |
| 거래소 | 업비트 · 빗썸 · 바이낸스 · 바이비트 |
| 주문 마커 | 매수 초록 ▲ · 매도 빨강 ▼ |
| 보조지표 | SMA · EMA · 볼린저밴드 |

</details>

<details>
<summary><h3>🔔 토스트 알림</h3></summary>
<br/>

웹훅 수신 · 주문 체결 시 화면 우측 하단에 토스트 알림이 표시됩니다.

설정 (설정 다이얼로그 → UI 설정):
- 토스트 알림 활성화/비활성화
- 표시 시간 조절 (1~30초)
- 알림음 On/Off

</details>

<details>
<summary><h3>🔒 프라이버시 모드</h3></summary>
<br/>

상단 **프라이버시** 토글을 켜면:
- IP 주소 → `***.***.***.***`
- 잔고 금액 → `****`
- 웹훅 로그 상세 정보 숨김

> [!TIP]
> 방송이나 화면 공유 시 유용합니다.

</details>

<br/>

## ⚙️ 설정 옵션

상단 **설정** 버튼 클릭하여 접근

<details>
<summary><b>서버 탭</b></summary>
<br/>

| 항목 | 설명 | 기본값 |
|------|------|:------:|
| 포트 | 웹훅 서버 포트 | `8000` |

</details>

<details>
<summary><b>API 탭</b></summary>
<br/>

각 거래소별 API 키 설정:
- 업비트: API Key, Secret Key
- 빗썸: API Key, Secret Key
- 바이낸스: API Key, Secret Key
- 바이비트: API Key, Secret Key
- OKX: API Key, Secret Key, Passphrase

</details>

<details>
<summary><b>UI 설정 탭</b></summary>
<br/>

| 카테고리 | 항목 |
|----------|------|
| **폰트** | 기본 폰트 크기, 폰트 종류 |
| **잔고** | 자동 새로고침, 새로고침 간격(초) |
| **시세 티커** | 업비트/바이낸스 시세 표시, 가격 변경 시 깜빡임 |
| **토스트** | 활성화/비활성화, 표시 시간(1~30초), 알림음 |
| **차트** | 주문 마커 표시 On/Off |
| **색상 테마** | 액센트, 매수/매도, 배경, 카드 배경, 텍스트 색상 |

> [!WARNING]
> 색상 변경은 **프로그램 재시작 후** 적용됩니다.

</details>

<details>
<summary><b>보안 탭</b></summary>
<br/>

**IP 화이트리스트:**
- TradingView 공식 IP 자동 허용
- 내부 IP 대역 (`127.x`, `192.168.x` 등) 자동 허용
- 추가 IP 등록/삭제 가능

</details>

<br/>

## 🔧 문제 해결

<details>
<summary><b>서버가 시작되지 않음</b> — 서버 상태가 빨간색 "오류"로 표시</summary>
<br/>

1. 포트 충돌 확인 (다른 프로그램이 8000 포트 사용 중인지)
2. 설정에서 다른 포트로 변경 (예: `8080`)
3. 방화벽에서 해당 포트 허용

</details>

<details>
<summary><b>거래소 연결 실패</b> — 상태바에서 빨간색 "연결 실패" 표시</summary>
<br/>

1. API 키가 올바르게 입력되었는지 확인
2. API 키의 권한 설정 확인
3. **IP 허용 목록**에 현재 IP가 등록되었는지 확인
4. 거래소 서버 상태 확인

</details>

<details>
<summary><b>웹훅이 수신되지 않음</b> — TradingView에서 알림 발송했으나 로그에 미표시</summary>
<br/>

1. 웹훅 URL 확인 (`http://공인IP:포트/webhook`)
2. 포트 포워딩 설정 확인
3. 방화벽에서 포트 허용 확인
4. TradingView 알림 설정에서 웹훅 URL 체크 확인
5. Alert 메시지가 `{{strategy.order.alert_message}}`인지 확인
6. ngrok 사용 시 URL이 만료되지 않았는지 확인

</details>

<details>
<summary><b>주문이 실패함</b> — 상태가 FAILED로 표시</summary>
<br/>

웹훅 로그에서 해당 항목 **더블클릭** → 상세 정보 팝업에서 에러 메시지를 확인하세요.

**일반적인 원인:**
- 잔고 부족
- 최소 주문 수량 미달
- 심볼 형식 오류
- API 권한 부족
- 레버리지/마진모드 설정 오류 (선물)

</details>

<details>
<summary><b>김치프리미엄이 표시되지 않음</b> — 김프가 <code>---</code>로 표시</summary>
<br/>

1. 업비트와 바이낸스 모두 BTC 가격이 표시되는지 확인
2. 환율 데이터 수신 확인 (USD/KRW 값)
3. 인터넷 연결 확인

</details>

<details>
<summary><b>차트가 표시되지 않음</b></summary>
<br/>

1. 거래소 API 연결 확인
2. 심볼 형식 확인 (예: `BTC/KRW`, `BTC/USDT`)
3. 타임프레임 변경 시도
4. 프로그램 재시작

</details>

<br/>

## ⚠ 주의사항

### 🔐 보안

> [!CAUTION]
> **API 키를 절대 타인과 공유하지 마세요.** `config.yml`에 API 키가 저장됩니다.

- 출금 권한은 비활성화 권장
- IP 제한 설정 필수
- 화면 공유 시 프라이버시 모드 활성화

### 📈 거래

- **테스트 우선** — 처음에는 소액으로 테스트, 전략 검증 후 금액 증가
- **시장가 주문** — 슬리피지 발생 가능, 유동성 낮은 코인 주의
- **선물 거래** — 레버리지 사용 시 손실 위험 증가, 마진모드 설정 확인, 청산 가격 주의
- **일괄 청산** — 되돌릴 수 없는 작업, 신중하게 사용
- **24시간 운영 시** — 안정적인 인터넷 연결, UPS(무정전전원장치) 권장

### ⚖️ 법적 고지

- 이 프로그램은 거래 도구일 뿐, 투자 조언을 제공하지 않습니다
- 암호화폐 거래는 높은 위험을 수반합니다
- 투자 손실에 대한 책임은 사용자에게 있습니다
- 거주 국가의 관련 법규를 준수하세요

<br/>

## 📄 라이센스

```
Copyright (c) 2025, 고잉 All rights reserved.
```

본 소프트웨어는 **개인적, 교육적, 연구 목적에 한하여** 사용이 허용됩니다.

다음 행위는 **명시적으로 금지**됩니다:
- 상업적 사용, 판매, 재판매, 임대, 서비스 제공
- 본 소프트웨어를 이용한 수익 창출 행위
- 사전 서면 허가 없는 재배포

> 상업적 사용을 원할 경우, 저작권자의 사전 서면 허가를 받아야 합니다.

<br/>

---

<div align="center">

**[트레이딩뷰 유저 코리아](https://open.kakao.com/o/gYMmhcYg)** · **[고잉봇 커뮤니티](https://open.kakao.com/o/g6UiEPei)** · **[개발자 문의](https://open.kakao.com/me/trader_going)**

*마지막 업데이트: 2026년 2월*

</div>
