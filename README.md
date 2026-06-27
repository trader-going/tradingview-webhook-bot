<div align="center">

<img width="160" height="160" alt="GoingBot" src="https://github.com/user-attachments/assets/291aefa4-072f-4aaa-9a33-4f17613424a7" />

# GoingBot

**TradingView 웹훅 자동매매 데스크톱 앱**

[![Latest Release](https://img.shields.io/github/v/release/trader-going/tradingview-webhook-bot?style=for-the-badge&label=release)](https://github.com/trader-going/tradingview-webhook-bot/releases/latest)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS-111?style=for-the-badge)](#다운로드)
[![License](https://img.shields.io/badge/license-Personal_Use-blue?style=for-the-badge)](#라이선스)

<br/>

[최신 버전 다운로드](https://github.com/trader-going/tradingview-webhook-bot/releases/latest) · [Pine Script 예제](./example.pinescript) · [고잉봇 커뮤니티](https://open.kakao.com/o/g6UiEPei)

</div>

---

## 처음 사용 순서

1. 이 페이지의 **다운로드**에서 앱을 설치합니다.
2. 앱 설정에서 거래소 API 키를 입력합니다.
3. 앱 설정의 **웹훅 Secret**을 복사합니다. 이 값이 TradingView 메시지에 없으면 웹훅이 거부됩니다.
4. ngrok, Tailscale Funnel, 직접 포트포워딩 중 하나로 **공개 웹훅 URL**을 만듭니다.
5. TradingView Alert에 공개 웹훅 URL과 Pine Script 메시지를 연결합니다.
6. 앱에서 테스트 웹훅을 먼저 확인한 뒤 소액으로 실거래를 검증합니다.

## 다운로드

최신 설치 파일은 [GitHub Releases](https://github.com/trader-going/tradingview-webhook-bot/releases/latest)에서 받습니다.

| 운영체제 | 권장 파일 | 비고 |
|---|---|---|
| Windows | `GoingBot-Setup-x.y.z.exe` | 설치형. 자동 업데이트 대상 |
| Windows | `GoingBot-Portable-x.y.z.exe` | 무설치 수동 실행용. 자동 업데이트 대상 아님 |
| macOS Apple Silicon | `GoingBot-x.y.z-arm64.dmg` | M1/M2/M3/M4 Mac |
| macOS Intel | `GoingBot-x.y.z-x64.dmg` | Intel Mac |

Windows SmartScreen 또는 macOS Gatekeeper 경고가 보이면 파일을 공식 GitHub Releases에서 받았는지 먼저 확인하세요.

## 지원 거래소

| 거래소 | 현물 | 선물 | 비고 |
|---|:---:|:---:|---|
| 업비트 | 지원 | - | KRW 현물 |
| 빗썸 | 지원 | - | KRW 현물 |
| 바이낸스 | - | 지원 | USDT 선물 |
| 바이비트 | - | 지원 | USDT 선물 |
| OKX | - | 지원 | USDT 선물, passphrase 필요 |

## 주요 기능

- TradingView Alert 웹훅 수신 후 자동 주문 실행
- 수동 주문, 잔고/포지션 조회, 일괄 청산
- 실시간 차트, 호가, 체결 스트림
- `100USDT`, `50000KRW`, `25%`, `100%`, `0.01` 같은 수량 표현
- 웹훅 Secret, IP 화이트리스트, 민감 로그 마스킹
- API 키와 웹훅 Secret 암호화 저장
- 앱 안에서 업데이트 확인, 다운로드, 재시작 설치

## 빠른 시작

### 1. 앱 설치

1. [Releases](https://github.com/trader-going/tradingview-webhook-bot/releases/latest)에서 설치 파일을 다운로드합니다.
2. Windows는 `GoingBot-Setup-x.y.z.exe`, macOS는 본인 CPU에 맞는 `.dmg`를 실행합니다.
3. 앱을 실행한 뒤 설정 화면을 엽니다.

### 2. 거래소 API 키 입력

앱의 **설정 → 거래소 API**에서 사용할 거래소의 API Key, Secret Key를 입력하고 저장합니다.

| 거래소 | 필요 권한 | 비활성화 권장 |
|---|---|---|
| 업비트 | 자산조회, 주문조회, 주문하기 | 출금 |
| 빗썸 | 잔액조회, 주문 | 출금 |
| 바이낸스 | Reading, Futures | 출금 |
| 바이비트 | Read-Write, Contract Orders/Positions | 출금 |
| OKX | Read, Trade, Passphrase | 출금 |

API 키는 앱 설정 저장 시 OS 보안 저장소 기반으로 암호화되어 로컬 설정 파일에 기록됩니다. 설정 파일에 `enc:v1:`로 시작하는 값이 보이면 정상입니다.

### 3. 웹훅 Secret 복사

앱의 **설정 → 웹훅 서버**에서 자동 생성된 **웹훅 Secret**을 확인합니다.

복사 순서:

1. 앱에서 **설정**을 엽니다.
2. **웹훅 서버** 섹션의 **웹훅 Secret** 값을 확인합니다.
3. `Secret 복사` 버튼을 누르거나, `키 표시`를 켠 뒤 값을 직접 복사합니다.
4. 이 값을 TradingView Pine Script 설정의 `Webhook Secret` 입력칸에 붙여넣습니다.

GoingBot은 Secret이 없는 웹훅을 거부합니다. TradingView는 커스텀 헤더를 넣기 어렵기 때문에 Pine Script 메시지 JSON의 `secret` 필드에 이 값을 넣습니다. 직접 호출하는 클라이언트는 `X-Webhook-Secret` 헤더를 사용할 수도 있습니다.

### 4. 공개 웹훅 URL 준비

GoingBot의 기본 로컬 웹훅 주소:

```text
http://127.0.0.1:47821/webhook
```

TradingView에서 PC로 웹훅을 보내려면 이 로컬 주소를 외부에서 접근 가능한 URL로 연결해야 합니다.

| 방식 | 사용 예 | 비고 |
|---|---|---|
| ngrok | `ngrok http 47821` | 가장 간단한 테스트용. 표시된 HTTPS 주소 뒤에 `/webhook`을 붙입니다. |
| Tailscale Funnel | `tailscale funnel --https=443 47821` | 개인 장비 운영에 적합 |
| 직접 포트포워딩 | 외부 포트 → PC `47821` | host를 `0.0.0.0` 또는 PC LAN IP로 변경 필요 |

ngrok 예시:

```text
ngrok 화면의 Forwarding: https://abc-123.ngrok-free.app
TradingView에 넣을 URL: https://abc-123.ngrok-free.app/webhook
```

직접 포트포워딩을 사용해도 됩니다. 이 경우 앱 설정의 웹훅 **호스트**를 `0.0.0.0` 또는 PC의 LAN IP로 변경한 뒤 앱을 재시작합니다. 공유기/방화벽에서 외부 포트를 앱이 실행 중인 PC의 `47821`로 전달합니다.

주의: `443` 포트를 포워딩한다고 자동으로 HTTPS가 되는 것은 아닙니다. HTTPS 주소를 쓰려면 Caddy, Nginx, Cloudflare Tunnel 같은 HTTPS reverse proxy가 앞에 있어야 합니다. 처음 사용자는 ngrok을 먼저 권장합니다.

공개 URL이 준비되면 앱 설정의 **공개 웹훅 URL**에 저장합니다. 상태바에서 클릭해 TradingView에 붙여넣을 URL을 복사할 수 있습니다.

### 5. 테스트 웹훅 실행

1. 먼저 `웹훅 테스트 URL`을 비워둔 상태로 앱의 테스트 버튼을 누릅니다. 이 테스트는 내 PC 안에서 서버가 켜져 있는지만 확인합니다.
2. 웹훅 로그에 테스트 수신 내역이 남는지 확인합니다.
3. 앱 설정의 `웹훅 테스트 URL`에 공개 웹훅 URL을 넣고 다시 테스트합니다. 예: `https://abc-123.ngrok-free.app/webhook`
4. 공개 URL 테스트까지 성공한 뒤 TradingView Alert를 연결합니다.

## TradingView 설정

### Pine Script

이 저장소의 [example.pinescript](./example.pinescript)를 TradingView Pine Editor에 붙여넣습니다.

주의: 이 예제는 웹훅 연결 테스트용입니다. `bar_index`를 기준으로 진입과 청산을 번갈아 발생시키므로, 그대로 실거래 Alert에 연결하면 주문이 계속 나갈 수 있습니다. 실사용 전 `longEntry`, `longClose` 조건을 본인 전략 조건으로 바꿔야 합니다.

스크립트 입력값:

- `Webhook Secret`: 앱에서 복사한 웹훅 Secret
- `Exchange`: 주문을 보낼 거래소. 예: `UPBIT`, `BITHUMB`, `BINANCE`, `BYBIT`, `OKX`
- `Symbol Override`: 앱에 보낼 심볼을 직접 지정할 때 사용. 비워두면 차트 심볼을 사용합니다.
- `Entry Qty`: 진입 수량 문자열. 예: `100USDT`, `50000KRW`, `0.01`
- `Close Qty`: 청산 수량 문자열. 예: `100%`, `50%`, `0.01`
- `Leverage`: 선물 주문 레버리지
- `Hedge Mode`: 거래소 계정이 hedge mode일 때 켭니다.

### Alert 만들기

1. 차트에 전략을 적용합니다.
2. Alert 생성 화면에서 조건을 해당 전략으로 선택합니다.
3. 옵션은 `Order fills only`를 사용합니다.
4. Webhook URL에 앱에서 복사한 공개 웹훅 URL을 입력합니다.
5. Message에는 아래 한 줄만 넣습니다.

```text
{{strategy.order.alert_message}}
```

### 웹훅 payload 예시

```json
{
  "secret": "앱에서_복사한_웹훅_Secret",
  "id": "L_ENTRY-1710000000000",
  "action": "LONG_ENTRY",
  "exchange": "BINANCE",
  "symbol": "BTCUSDT",
  "price": "65000",
  "qty": "100USDT",
  "leverage": 3,
  "hedgeMode": false,
  "time": "1710000000000"
}
```

| 필드 | 설명 |
|---|---|
| `secret` | 앱의 웹훅 Secret. 필수 |
| `id` | 중복 웹훅 방지용 ID |
| `action` | `LONG_ENTRY`, `LONG_CLOSE`, `SHORT_ENTRY`, `SHORT_CLOSE` |
| `exchange` | `UPBIT`, `BITHUMB`, `BINANCE`, `BYBIT`, `OKX` |
| `symbol` | `BTCUSDT`, `BTC/KRW` 등 |
| `qty` | 주문 수량 문자열 |
| `leverage` | 선물 레버리지 |
| `hedgeMode` | hedge mode 사용 여부 |
| `price` | TradingView 체결 가격 또는 현재가 |

`BINANCE`는 앱에서 Binance futures로 자동 처리됩니다.

## 수량 표현

| 예시 | 의미 |
|---|---|
| `100USDT` | 100 USDT 어치 주문 |
| `50000KRW` | 50,000원 어치 주문 |
| `25%` | close 주문에서 현재 포지션의 25% 청산 |
| `100%` | close 주문에서 현재 포지션 전량 청산 |
| `0.01` | 코인/계약 수량 직접 입력 |

`LONG_CLOSE`, `SHORT_CLOSE`, 앱의 일괄 청산은 reduce-only 성격으로 실행됩니다. 포지션이 없으면 청산 주문을 막고, 요청 수량이 현재 포지션보다 크면 실제 포지션 수량으로 제한합니다.

## 운영 팁

- 자동매매 PC는 절전 모드와 자동 재부팅을 꺼두세요.
- 출금 권한은 API 키에서 제외하세요.
- 거래소 API 키에는 IP 제한을 거는 것을 권장합니다.
- 첫 연결은 반드시 소액으로 테스트하세요.
- ngrok 무료 URL은 바뀔 수 있습니다. URL이 바뀌면 TradingView Alert의 Webhook URL도 바꿔야 합니다.
- Tailscale Funnel이나 직접 포트포워딩을 쓰면 고정 URL 운영이 쉬워집니다.
- 직접 포트포워딩은 방화벽과 공유기 설정이 공개 노출 범위를 결정하므로 Secret, IP 제한, HTTPS 구성을 함께 확인하세요.

## 문제 해결

| 증상 | 확인할 것 |
|---|---|
| 웹훅 로그가 비어 있음 | TradingView Webhook URL, ngrok/Tailscale/포트포워딩 상태, 앱 웹훅 서버 실행 여부 |
| `401 Invalid webhook secret` | Pine Script의 `Webhook Secret` 값이 앱 설정과 같은지 확인 |
| `403 Forbidden` | IP 화이트리스트 설정 확인 |
| 주문 실패 | 거래소 API 권한, 잔고, 최소 주문 수량, 심볼 표기, 선물 레버리지/포지션 모드 확인 |
| 앱 업데이트가 안 보임 | 앱 설정에서 `업데이트 확인`을 누르고, 현재 버전보다 새 버전이 있는지 확인 |
| 설정 파일에 `enc:v1:` 값이 보임 | 정상입니다. 앱이 민감 정보를 암호화해 저장한 값입니다. |

## 주의사항

이 앱은 투자 조언을 제공하지 않습니다. 모든 주문과 손익 책임은 사용자에게 있습니다. 암호화폐와 선물 거래는 원금 손실 위험이 크므로 충분히 검증한 뒤 사용하세요.

## 라이선스

```text
Copyright (c) 2026 Going. All rights reserved.
```

본 소프트웨어는 개인 사용 목적에 한해 사용할 수 있습니다. 상업적 이용, 재판매, 재배포, 서비스 제공은 사전 서면 허가 없이 금지됩니다.
