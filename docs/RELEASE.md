# GoingBot Public Release Guide

이 저장소는 GoingBot 사용자 배포 전용 저장소입니다. 소스코드는 이 저장소에 두지 않고, 사용자가 받는 설치 파일과 자동업데이트 메타데이터만 GitHub Releases에 올립니다.

## 저장소 역할

- 사용자 README와 TradingView Pine Script 예제를 제공합니다.
- Release asset으로 Windows/macOS 설치 파일을 제공합니다.
- Electron 자동업데이트가 읽는 `latest.yml`, `latest-mac.yml`을 제공합니다.
- `.exe`, `.dmg`, `.zip`, `.blockmap`, `latest.yml`, `latest-mac.yml`은 Git tree에 커밋하지 않습니다.

## 소스 레포에서 필요한 설정

빌드는 소스 레포에서 수행하고, Release 업로드만 이 저장소로 보냅니다.

필수 설정:

- Electron `build.publish.owner`: `trader-going`
- Electron `build.publish.repo`: `tradingview-webhook-bot`
- 소스 레포 Actions secret: `DISTRIBUTION_REPO_TOKEN`
- `DISTRIBUTION_REPO_TOKEN` 권한: 이 저장소의 `Contents: Read and write`

서명 빌드용 secret:

- Windows: `WINDOWS_CSC_LINK`, `WINDOWS_CSC_KEY_PASSWORD`
- macOS: `MACOS_CSC_LINK`, `MACOS_CSC_KEY_PASSWORD`, `APPLE_API_KEY_BASE64`, `APPLE_API_KEY_ID`, `APPLE_API_ISSUER`

## Release asset 체크리스트

Windows 자동업데이트에 필요한 파일:

- `GoingBot-Setup-x.y.z.exe`
- `GoingBot-Setup-x.y.z.exe.blockmap`
- `latest.yml`

Windows 수동 실행용 파일:

- `GoingBot-Portable-x.y.z.exe`

macOS 자동업데이트와 사용자 다운로드에 필요한 파일:

- `GoingBot-x.y.z-arm64.dmg`
- `GoingBot-x.y.z-arm64.dmg.blockmap`
- `GoingBot-x.y.z-arm64-mac.zip`
- `GoingBot-x.y.z-x64.dmg`
- `GoingBot-x.y.z-x64.dmg.blockmap`
- `GoingBot-x.y.z-x64-mac.zip`
- `latest-mac.yml`

파일명은 빌드 후 바꾸지 않습니다. `latest.yml`, `latest-mac.yml`은 실제 asset 파일명을 참조하므로 파일명을 바꾸면 자동업데이트가 실패합니다.

## 배포 순서

1. 소스 레포에서 `package.json`, `package-lock.json`, `VERSION`을 같은 새 버전으로 올립니다.
2. 소스 레포에서 릴리즈 워크플로를 실행하거나 `vX.Y.Z` 태그를 push합니다.
3. 워크플로가 이 저장소에 draft Release를 만들고 asset을 업로드합니다.
4. draft Release에서 asset 목록과 파일명을 확인합니다.
5. Windows/macOS 설치, 실행, 업데이트 확인을 검수합니다.
6. 문제가 없으면 draft Release를 publish합니다.

Release가 draft 상태이면 일반 사용자의 업데이트 확인에서 감지되지 않을 수 있습니다. 검수 후 반드시 publish하세요.

## 자동업데이트 검수

공개 전 최소 검수:

- 이전 버전 설치본에서 `업데이트 확인`을 눌렀을 때 새 버전을 감지하는지 확인
- 다운로드 진행률이 표시되는지 확인
- `재시작 설치` 후 앱 버전이 새 버전으로 바뀌는지 확인
- 설정 파일, API 키, 웹훅 Secret, 로그가 보존되는지 확인
- Windows 설치본 코드서명 상태 확인
- macOS dmg 실행, zip 자동업데이트, notarization 상태 확인

자동업데이트는 현재 설치된 앱보다 높은 버전만 감지합니다. 문제가 있는 릴리즈를 냈다면 같은 태그를 덮어쓰지 말고 더 높은 patch 버전을 새로 배포합니다.

## 기존 사용자 마이그레이션

예전 설치본이 다른 GitHub Release 저장소를 바라보도록 빌드되어 있었다면, 이 저장소에 새 Release를 올려도 그 설치본은 감지하지 못합니다.

기존 사용자가 있다면 아래 중 하나를 선택합니다.

- 예전 업데이트 저장소에 이 공개 배포 저장소를 바라보는 bridge 버전을 한 번 배포합니다.
- 사용자에게 이 저장소의 최신 설치본을 한 번 수동 재설치하도록 안내합니다.

신규 사용자는 이 저장소 Releases에서 받은 설치본부터 이 저장소 Releases를 자동업데이트 대상으로 사용합니다.

## 수동 업로드 fallback

워크플로가 실패했지만 빌드 산출물이 이미 준비되어 있으면 GitHub Releases에서 같은 태그로 draft Release를 만들고 위 asset을 직접 업로드할 수 있습니다.

수동 업로드 시에도 아래 규칙은 유지합니다.

- 파일명 변경 금지
- `latest.yml`, `latest-mac.yml` 포함
- draft 상태에서 검수 후 publish
- 실패한 Release asset 덮어쓰기 대신 새 patch 버전 배포
