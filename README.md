<div align="center">

<img width="160" height="160" alt="GoingBot" src="https://github.com/user-attachments/assets/291aefa4-072f-4aaa-9a33-4f17613424a7" />

# GoingBot

**TradingView 웹훅 자동매매 데스크톱 앱**

[![Latest Release](https://img.shields.io/github/v/release/trader-going/tradingview-webhook-bot?style=for-the-badge&label=release)](https://github.com/trader-going/tradingview-webhook-bot/releases/latest)
[![Platform](https://img.shields.io/badge/platform-Windows%20(macOS%20%EC%A4%80%EB%B9%84%20%EC%A4%91)-111?style=for-the-badge)](#다운로드)
[![License](https://img.shields.io/badge/license-Personal_Use-blue?style=for-the-badge)](#라이선스)

<br/>

[최신 버전 다운로드](https://github.com/trader-going/tradingview-webhook-bot/releases/latest) · [Pine Script 예제](./example.pinescript) · [고잉봇 커뮤니티](https://open.kakao.com/o/g6UiEPei)

</div>

---

## 처음 사용 순서

1. 이 페이지의 **다운로드**에서 앱을 설치합니다.
2. 앱 설정에서 거래소 API 키를 입력합니다.
3. 앱 설정의 **웹훅 Secret**을 복사합니다.
4. ngrok, Tailscale Funnel, 직접 포트포워딩 중 하나로 **공개 웹훅 URL**을 만듭니다.
5. TradingView Alert에 공개 웹훅 URL과 Pine Script 메시지를 연결합니다.
6. 앱에서 테스트 웹훅을 먼저 확인한 뒤 소액으로 실거래를 검증합니다.

## 다운로드

최신 설치 파일은 [GitHub Releases](https://github.com/trader-going/tradingview-webhook-bot/releases/latest)에서 받습니다.

현재 최신 릴리스(`v0.1.0`)는 **Windows 전용**입니다. macOS 빌드는 준비 중이며, 게시되면 이 표가 갱신됩니다.

| 운영체제 | 권장 파일 | 비고 |
|---|---|---|
| Windows | `GoingBot-Setup-x.y.z.exe` | 설치형(NSIS). 자동 업데이트 대상 |
| Windows | `GoingBot-Portable-x.y.z.exe` | 무설치 수동 실행용. 자동 업데이트 대상 아님 |
| macOS | (준비 중) | 현재 미게시. 추후 `.dmg`/`.zip` 제공 예정 |

> **코드 서명 안내**: 현재 빌드는 코드 서명이 되어 있지 않습니다. Windows에서는 첫 설치 시 **SmartScreen 경고**가 뜰 수 있습니다. 공식 GitHub Releases에서 받은 파일이 맞다면 `추가 정보 → 실행`으로 진행하세요. macOS 빌드가 게시되더라도 무서명 상태에서는 **Gatekeeper**가 실행을 막으므로 `우클릭 → 열기`로 직접 허용해야 합니다.

## 지원 거래소

주문이 가능한 거래소는 **5개**입니다. 바이낸스는 **선물(USDT)만 주문**할 수 있고, 바이낸스 현물은 시세 표시(전광판) 용도로만 쓰입니다.

| 거래소 | 현물 | 선물 | 비고 |
|---|:---:|:---:|---|
| 업비트 | 지원 | - | KRW 현물 |
| 빗썸 | 지원 | - | KRW 현물 |
| 바이낸스 | - | 지원 | USDT 선물. 현물은 시세 표시 전용(주문 불가) |
| 바이비트 | - | 지원 | USDT 선물 |
| OKX | - | 지원 | USDT 선물, passphrase 필요 |

웹훅에서 `exchange`를 `BINANCE`로 보내도 앱이 자동으로 **바이낸스 선물**로 처리합니다.

## 주요 기능

- TradingView Alert 웹훅 수신 후 자동 주문 실행
- 수동 주문, 잔고/포지션 조회, 일괄 청산
- 실시간 차트, 호가, 체결 스트림, 시세 전광판
- `100USDT`, `50000KRW`, `25%`, `100%`, `0.01` 같은 수량 표현
- 웹훅 Secret 필수 검증, IP 화이트리스트, 민감 로그 마스킹
- API 키와 웹훅 Secret을 OS 보안 저장소 기반으로 암호화 저장
- 자동 업데이트(상단바 업데이트 알약, 자동 확인 기본 ON) — 단, **Windows 설치형 한정**

## 빠른 시작

### 1. 앱 설치

1. [Releases](https://github.com/trader-going/tradingview-webhook-bot/releases/latest)에서 `GoingBot-Setup-x.y.z.exe`를 다운로드합니다.
2. 설치 파일을 실행합니다. SmartScreen 경고가 보이면 `추가 정보 → 실행`으로 진행합니다.
3. 앱을 실행한 뒤 설정 화면을 엽니다.

### 2. 거래소 API 키 입력

앱의 **설정 → 거래소 API**에서 사용할 거래소의 API Key, Secret Key를 입력하고 저장합니다. OKX는 추가로 **Passphrase**가 필요합니다.

| 거래소 | 필요 권한 | 비활성화 권장 |
|---|---|---|
| 업비트 | 자산조회, 주문조회, 주문하기 | 출금 |
| 빗썸 | 잔액조회, 주문 | 출금 |
| 바이낸스 | Reading, Futures | 출금 |
| 바이비트 | Read-Write, Contract Orders/Positions | 출금 |
| OKX | Read, Trade, Passphrase | 출금 |

API 키는 앱 설정 저장 시 OS 보안 저장소(Windows DPAPI / macOS Keychain) 기반으로 암호화되어 로컬 설정 파일에 기록됩니다. 설정 파일에 `enc:v1:`로 시작하는 값이 보이면 정상입니다.

### 3. 웹훅 Secret 확인 (필수)

앱의 **설정 → 웹훅 서버**에서 자동 생성된 **웹훅 Secret**을 확인합니다.

GoingBot은 **Secret이 설정되어야만 실거래 웹훅을 받습니다.** Secret이 비어 있으면 서버가 웹훅을 `503`으로 거부합니다. TradingView는 커스텀 헤더를 넣기 어렵기 때문에 Pine Script 메시지 JSON의 `secret` 필드에 이 값을 넣습니다. 직접 호출하는 클라이언트는 `X-Webhook-Secret` 헤더를 사용할 수도 있습니다. Secret 비교는 타이밍-세이프 방식으로 검증됩니다.

### 4. 공개 웹훅 URL 준비

GoingBot의 기본 로컬 웹훅 주소:

```text
http://127.0.0.1:47821/webhook
```

TradingView에서 PC로 웹훅을 보내려면 이 로컬 주소를 외부에서 접근 가능한 URL로 연결해야 합니다. 앱이 터널을 직접 실행하지는 않으므로, 아래 도구 중 하나를 별도로 사용합니다.

| 방식 | 사용 예 | 비고 |
|---|---|---|
| ngrok | `ngrok http 47821` | 가장 간단한 테스트용 |
| Tailscale Funnel | `tailscale funnel --https=443 47821` | 개인 장비 고정 URL 운영에 적합 |
| 직접 포트포워딩 | 외부 `443` → PC `47821` | host를 `0.0.0.0` 또는 PC LAN IP로 변경 필요 |

**Tailscale Funnel 사용 예**

1. PC에 Tailscale을 설치하고 로그인합니다.
2. Tailnet 관리자에서 Funnel 기능을 활성화합니다.
3. 앱이 실행 중인 상태에서 `tailscale funnel --https=443 47821`을 실행합니다.
4. 출력되는 `https://<머신이름>.<테일넷>.ts.net/webhook`을 TradingView Alert의 Webhook URL로 사용합니다.

**직접 포트포워딩 사용 시**

앱 설정의 웹훅 **호스트**를 `0.0.0.0` 또는 PC의 LAN IP로 변경한 뒤 앱을 재시작합니다(호스트/포트 변경은 재시작이 필요합니다). 공유기/방화벽에서 외부 포트를 앱이 실행 중인 PC의 `47821`로 전달하고, 가능하면 HTTPS reverse proxy를 앞에 두고 `https://내도메인/webhook` 형태로 사용하세요.

공개 URL이 준비되면 앱 설정의 **공개 웹훅 URL**에 저장합니다. 이 값은 상태바에서 클릭해 복사할 수 있는 메모용 정보이며, 서버 동작 자체를 바꾸지는 않습니다(실제 바인딩은 호스트/포트 설정으로 결정됩니다).

### 5. 테스트 웹훅 실행

1. 앱에서 웹훅 테스트 버튼을 누릅니다.
2. 웹훅 로그에 테스트 수신 내역이 남는지 확인합니다.
3. 그 다음 TradingView Alert를 연결합니다.

## TradingView 설정

### Pine Script

이 저장소의 [example.pinescript](./example.pinescript)를 TradingView Pine Editor에 붙여넣습니다.

스크립트 입력값:

- `Webhook Secret`: 앱에서 복사한 웹훅 Secret
- `Exchange`: 주문을 보낼 거래소. 예: `UPBIT`, `BITHUMB`, `BINANCE`, `BYBIT`, `OKX`
- `Symbol Override`: 앱에 보낼 심볼을 직접 지정할 때 사용. 비워두면 차트 심볼을 사용합니다.
- `Entry Qty`: 진입 수량 문자열. 예: `100USDT`, `50000KRW`, `0.01`
- `Close Qty`: 청산 수량 문자열. 예: `100%`, `50%`, `0.01`
- `Leverage`: 선물 주문 레버리지(1~125)
- `Hedge Mode`: 거래소 계정이 hedge mode일 때 켭니다.

### Alert 만들기

1. 차트에 전략을 적용합니다.
2. Alert 생성 화면에서 조건을 해당 전략으로 선택합니다.
3. 옵션은 `Order fills only`를 사용합니다.
4. Webhook URL에 앞에서 만든 공개 웹훅 URL을 입력합니다.
5. Message에는 아래 한 줄만 넣습니다.

```text
{{strategy.order.alert_message}}
```

### 웹훅 payload 예시

```json
{
  "secret": "앱에서_복사한_웹훅_Secret",
  "id": "L-2026-06-27T12:00:00Z",
  "action": "LONG_ENTRY",
  "exchange": "BINANCE",
  "symbol": "BTCUSDT",
  "price": "65000",
  "qty": "100USDT",
  "leverage": 3,
  "hedgeMode": false,
  "time": "2026-06-27T12:00:00Z"
}
```

| 필드 | 설명 |
|---|---|
| `secret` | 앱의 웹훅 Secret. **필수** |
| `id` | 중복 웹훅 방지용 ID(30초 내 같은 ID/본문은 무시) |
| `action` | `LONG_ENTRY`, `LONG_CLOSE`, `SHORT_ENTRY`, `SHORT_CLOSE` |
| `exchange` | `UPBIT`, `BITHUMB`, `BINANCE`, `BYBIT`, `OKX` |
| `symbol` | `BTCUSDT`, `BTC/KRW` 등 |
| `qty` | 주문 수량 문자열 |
| `leverage` | 선물 레버리지 |
| `hedgeMode` | hedge mode 사용 여부 |
| `price` | TradingView 체결 가격 또는 현재가 |

`BINANCE`는 앱에서 Binance futures로 자동 처리됩니다.

### action 값

| action | 동작 |
|---|---|
| `LONG_ENTRY` | 롱 진입(매수) |
| `LONG_CLOSE` | 롱 청산(reduce-only) |
| `SHORT_ENTRY` | 숏 진입(매도) |
| `SHORT_CLOSE` | 숏 청산(reduce-only) |

위 4가지 외의 값은 오류로 처리됩니다.

## 수량 표현

| 예시 | 의미 |
|---|---|
| `100USDT` | 100 USDT 어치 주문(현재가로 수량 환산) |
| `50000KRW` | 50,000원 어치 주문(해외 거래소는 환율로 USDT 환산) |
| `25%` | **close 주문에서만** 현재 포지션/잔고의 25% 청산 |
| `100%` | **close 주문에서만** 현재 포지션/잔고 전량 청산 |
| `0.01` | 코인/계약 수량 직접 입력 |

`%` 수량은 **청산(`LONG_CLOSE`/`SHORT_CLOSE`) 액션에서만** 허용됩니다. 진입 액션에 `%`를 쓰면 오류가 납니다.

`LONG_CLOSE`, `SHORT_CLOSE`, 앱의 일괄 청산은 reduce-only 성격으로 실행됩니다. 포지션이 없으면 청산 주문을 막고, 요청 수량이 현재 포지션보다 크면 실제 포지션 수량으로 제한합니다.

## 자동 업데이트

- 앱은 시작 시 자동으로 새 버전을 확인하며(자동 확인 기본 **ON**), 새 버전이 있으면 상단바에 **업데이트 알약**이 표시됩니다.
- 다운로드와 설치는 알약을 눌러 직접 진행합니다(자동 다운로드/자동 설치는 꺼져 있습니다).
- **Windows 설치형(NSIS)**: 자동 업데이트가 동작합니다. 무서명이라 새 버전 설치 시에도 SmartScreen 경고가 보일 수 있습니다.
- **Windows Portable**: 자동 업데이트 대상이 아닙니다. 새 버전을 직접 받아 교체하세요.
- **macOS**: 무서명/공증 미적용 상태에서는 Gatekeeper 때문에 자동 업데이트가 동작하지 않습니다. 새 버전을 수동으로 다시 받아야 합니다(macOS 빌드 게시 후 적용).

## PyQt 버전 대비 달라진 점

GoingBot은 기존 PyQt(Python + FastAPI + PyQt5) 버전을 Electron/React 단일 앱으로 다시 만든 버전입니다. 사용자 입장에서 달라진 주요 사항은 다음과 같습니다.

- **설치/실행이 단순해졌습니다.** 예전에는 Python 백엔드 프로세스가 별도로 떠야 했지만, 이제 하나의 데스크톱 앱으로 모든 것이 동작합니다. Python·conda 설치가 필요 없습니다.
- **웹훅 Secret이 필수가 되었습니다.** 예전에는 IP 화이트리스트만으로 웹훅을 받았지만, 이제는 Secret이 설정되어야만(미설정 시 `503`) 웹훅이 동작하며, Secret 불일치는 `401`로 거부됩니다.
- **IP 자동 허용 범위가 좁아졌습니다.** 예전에는 사설 대역(10/172.16~31/192.168)을 자동 허용했지만, 이제는 루프백과 TradingView 공식 IP, 그리고 사용자가 직접 등록한 IP만 자동 허용됩니다. 같은 LAN의 다른 PC에서 보낸다면 해당 IP를 화이트리스트에 추가해야 합니다.
- **기본 포트가 8000 → 47821로 바뀌었습니다.** 기존 `8000` 설정은 자동으로 47821로 마이그레이션됩니다.
- **API 키/Secret이 암호화 저장됩니다.** 예전 평문 `config.yml` 대신, OS 보안 저장소 기반으로 암호화해 `enc:v1:` 형태로 저장합니다.
- **자동 업데이트가 추가되었습니다.** 상단바 업데이트 알약과 자동 확인(기본 ON)을 제공합니다(PyQt 버전에는 자동 업데이트가 없었습니다).
- **공개 URL 운영 안내와 호스트/공개 URL 설정이 추가되었습니다.** ngrok / Tailscale Funnel / 직접 포트포워딩 흐름을 정식 지원합니다.
- **거래소 주문 대상이 명확해졌습니다.** 주문은 업비트·빗썸·바이낸스선물·바이비트·OKX 5개로 정리되었고, 바이낸스 현물은 시세 표시 전용으로 분리, OKX passphrase 설정이 정식화되었습니다.
- **터미널형 UI로 강화되었습니다.** 호가 10단 + 체결 테이프, 실시간 차트, 시세 전광판 등 실시간 화면이 모두 웹소켓 기반으로 동작합니다.
- 보안 측면에서 민감 로그 마스킹, 30초 중복 웹훅 무시, 본문 크기 제한, CORS Origin 제한이 추가되었습니다.
- action/수량 파싱 규칙(4종 action, `%`는 청산만, `100USDT`/`50000KRW`/`0.01` 등)은 PyQt 버전과 동일하게 유지됩니다.

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
| `503` 응답(웹훅 거부) | 앱 설정에서 **웹훅 Secret이 설정되어 있는지** 확인 |
| `401 Invalid webhook secret` | Pine Script의 `Webhook Secret` 값이 앱 설정과 같은지 확인 |
| `403 Access denied` | IP 화이트리스트 설정 확인(보내는 IP 등록 필요) |
| `415` 응답 | 요청 Content-Type이 `application/json`인지 확인 |
| `% quantity is allowed only for close actions` | 진입 액션에 `%` 수량을 쓰지 않았는지 확인 |
| 주문 실패 | 거래소 API 권한, 잔고, 최소 주문 수량, 심볼 표기, 선물 레버리지/포지션 모드 확인 |
| 앱 업데이트가 안 보임 | 상단바 업데이트 알약 또는 앱 설정에서 `업데이트 확인`을 누르고, 새 버전이 있는지 확인 |
| 설정 파일에 `enc:v1:` 값이 보임 | 정상입니다. 앱이 민감 정보를 암호화해 저장한 값입니다. |

## 주의사항

이 앱은 투자 조언을 제공하지 않습니다. 모든 주문과 손익 책임은 사용자에게 있습니다. 암호화폐와 선물 거래는 원금 손실 위험이 크므로 충분히 검증한 뒤 사용하세요.

## 라이선스

```text
Copyright (c) 2026 Going. All rights reserved.
```

본 소프트웨어는 개인 사용 목적에 한해 사용할 수 있습니다. 상업적 이용, 재판매, 재배포, 서비스 제공은 사전 서면 허가 없이 금지됩니다.
