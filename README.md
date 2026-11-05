# 글쓰기기 2.6.0

요청한 의도·분량·문체에 맞춰 지원동기·자기소개·에세이·설명문을 작성하고, 기존 글의 흐름과 표현을 다듬는 플러그인입니다.

일반 집필의 첫 경로에서 소재와 문단 구성, Humanizer를 참고한 문맥 편집, 의미와 길이 대조를 연결했습니다. 기존 9개 스킬·자료·라이선스·플러그인 ID·기본 프롬프트를 보존했습니다.

## 현재 배포

[v2.6.0 릴리스](https://github.com/rosususu/writing-design-research-toolkit/releases/tag/v2.6.0)의 첨부 파일을 사용하세요.

- `writing-toolkit-2.6.0-marketplace.tar.xz`: 공개 로컬 설치용 전체 패키지
- `writing-toolkit-2.6.0-full.tar.xz`: 플러그인 단독 전체 소스 1,939개 파일
- `writing-toolkit-2.6.0-update.zip`: 기존 2.5.0용 변경 파일 40개
- `SHA256SUMS-2.6.0.txt`: 세 배포 파일의 SHA256
- 품질 비교 보고서: 실제 생성문과 버전 가림 판독의 근거·한계

GitHub가 자동 생성하는 Source code ZIP은 이전 저장소 스냅샷을 포함할 수 있습니다. 최신 전체 소스는 위 첨부 압축 파일 안에 있습니다.

기존 개인 계정 설치와 공개 로컬 설치는 한 경로를 선택하세요. 공개 로컬 설치는 다음과 같습니다.

```powershell
New-Item -ItemType Directory -Force .\geulsseugi-2.6.0
tar -xf .\writing-toolkit-2.6.0-marketplace.tar.xz -C .\geulsseugi-2.6.0
codex plugin marketplace add .\geulsseugi-2.6.0
codex plugin add writing-design-research-toolkit@rosususu-writing-tools
```

## 이번 검증

기존 검사 204개가 통과했습니다. 가상 입력 12개에서 실제 생성문 24개를 비교한 Codex 평가자의 버전 가림 선호는 후보 3·기준선 1·동률 8입니다. 후보 선호 1건은 줄바꿈 준수 차이이며, 일반적인 문장 품질 우월성의 증거로 쓰지 않습니다.

의미·요청 준수 검토는 후보 12개가 수락됐습니다. 표본이 작고 정확한 backend ID·seed·temperature가 확인되지 않았습니다. 사람 독자 연구, 모든 장르의 품질 향상, 자동 스킬 선택, Office 화면 렌더, AI 탐지 통과를 입증하지 않습니다.

Humanizer는 고정 커밋 `0ef9fe5bc3572734fd3ae6c448fe00a30cd5dcf0`의 SKILL 3.1.0과 MIT 고지를 확인해 한국어 적용 기준을 독립 작성했습니다. 영어 규칙의 일괄 이식, 새 경험·감정·의견 추가, 탐지 회피는 적용하지 않았습니다. 새 유료 API·모델·계정·필수 의존성은 추가하지 않았습니다.

## 이전 2.4.0 기록

아래는 이전 배포의 기록이며 현재 배포는 위 2.6.0을 기준으로 합니다.

원문의 사실·숫자·인용·조건·확신도·저자 말투를 보존하면서 한국어·영어 글의 논리와 자연스러움을 다듬는 Codex 플러그인입니다. 기존 스킬 9개와 자료·템플릿·개별 라이선스를 유지했습니다.

## 다운로드와 설치

[v2.4.0 공개 배포](https://github.com/rosususu/writing-design-research-toolkit/releases/tag/v2.4.0)에서 공개 설치용 `writing-design-research-toolkit-2.4.0-marketplace.zip`을 받으세요. 기존 자료를 포함한 전체 소스가 ZIP 안에 들어 있습니다. 압축을 푼 폴더를 로컬 마켓플레이스로 등록합니다.

```powershell
Expand-Archive -LiteralPath .\writing-design-research-toolkit-2.4.0-marketplace.zip -DestinationPath .\geulsseugi-2.4.0
codex plugin marketplace add .\geulsseugi-2.4.0
codex plugin add writing-design-research-toolkit@rosususu-writing-tools
```

기존 개인 계정에 글쓰기기가 설치되어 있다면 계정 설치와 공개 설치 중 한 경로를 선택하세요. 동명 스킬의 중복 설치를 피하세요. `writing-design-research-toolkit-2.4.0.zip`은 플러그인 단독 전체 패키지, `-update.zip`은 기존 2.3.6에 덧씌우는 변경 파일 패키지입니다. `SHA256SUMS.txt`로 다운로드 파일을 대조할 수 있습니다.

## 달라진 점

- 수치·단위·인용·코드·URL, 글자 수와 수정 범위를 오프라인으로 검사합니다.
- 부정·조건·확신도·인과 단서 변화는 위치와 이유를 보여 주고 원문을 읽어 판단하도록 합니다. 자동 치환·AI 탐지 점수로 합격시키지 않습니다.
- 요청 의도·편집 강도·표본 말투·문단 근거를 검수하고, 신규 집필·번역·말투·분량을 포함한 18개 입력과 실제 출력 평가기를 제공합니다.
- 자료 색인의 새 파일 누락·중복·오래된 경로를 탐지하고 오래된 Gemini·Reason Network 실행 절차를 정리했습니다.

## 검증과 범위

로컬 검사 83개가 통과했습니다. 실제 출력 36개를 버전명을 가려 원문과 대조한 소규모 합성 평가에서는 기준판 17/18개, 후보 18/18개가 수락됐습니다. 일부 문장의 연결은 기준판 선호도 있어 모든 글의 향상을 주장하지 않습니다. 모델 backend ID·seed·temperature는 확인되지 않았습니다.

개인 계정의 2.4.0 업데이트·공식 설치와 설치 파일 1,787개 대조, 설치된 검사기 실행을 확인했습니다. 호스트의 자동 스킬 선택·Office 화면 렌더·실제 독자 반응·AI 탐지 회피는 측정하지 않았습니다. 새 검사기는 Python 3.10 이상 표준 라이브러리만 사용합니다. DOCX는 기존 선택 기능이며 `python-docx>=1.1,<2`가 별도로 필요합니다. 새 유료 API·외부 모델·계정 권한을 요구하지 않습니다.

- [GitHub 후보 20개 비교](GitHub_후보20_비교.md): 고정 커밋의 README·관련 코드·예시/테스트·권리 자료를 확인했습니다. 원문 120개를 확보했고 외부 저장소의 테스트는 직접 실행하지 않았습니다.
- [대표 입력의 실제 전후 결과](대표_전후_결과.md)
- [변경 기록](RELEASE_NOTES.md) · [제3자 자료와 권리 고지](THIRD_PARTY_NOTICES.md)

전체 소스·스킬·평가 입력·검사 실행법·기존 출처 고지는 공개 설치 ZIP의 `plugins/writing-design-research-toolkit/` 안에 있습니다. 새 외부 코드를 복제하거나 필수 의존성으로 추가하지 않았습니다. 각 기존 자료의 권리는 해당 고지와 원출처를 따릅니다.

# 글쓰기기 2.4.0

원문의 사실·숫자·인용·조건·확신도·저자 말투를 보존하면서 한국어·영어 글의 논리와 자연스러움을 다듬는 Codex 플러그인입니다. 기존 스킬 9개와 자료·템플릿·개별 라이선스를 유지했습니다.

## 다운로드와 설치

[v2.4.0 공개 배포](https://github.com/rosususu/writing-design-research-toolkit/releases/tag/v2.4.0)에서 공개 설치용 `writing-design-research-toolkit-2.4.0-marketplace.zip`을 받으세요. 기존 자료를 포함한 전체 소스가 ZIP 안에 들어 있습니다. 압축을 푼 폴더를 로컬 마켓플레이스로 등록합니다.

```powershell
Expand-Archive -LiteralPath .\writing-design-research-toolkit-2.4.0-marketplace.zip -DestinationPath .\geulsseugi-2.4.0
codex plugin marketplace add .\geulsseugi-2.4.0
codex plugin add writing-design-research-toolkit@rosususu-writing-tools
```

기존 개인 계정에 글쓰기기가 설치되어 있다면 계정 설치와 공개 설치 중 한 경로를 선택하세요. 동명 스킬의 중복 설치를 피하세요. `writing-design-research-toolkit-2.4.0.zip`은 플러그인 단독 전체 패키지, `-update.zip`은 기존 2.3.6에 덧씌우는 변경 파일 패키지입니다. `SHA256SUMS.txt`로 다운로드 파일을 대조할 수 있습니다.

## 달라진 점

- 수치·단위·인용·코드·URL, 글자 수와 수정 범위를 오프라인으로 검사합니다.
- 부정·조건·확신도·인과 단서 변화는 위치와 이유를 보여 주고 원문을 읽어 판단하도록 합니다. 자동 치환·AI 탐지 점수로 합격시키지 않습니다.
- 요청 의도·편집 강도·표본 말투·문단 근거를 검수하고, 신규 집필·번역·말투·분량을 포함한 18개 입력과 실제 출력 평가기를 제공합니다.
- 자료 색인의 새 파일 누락·중복·오래된 경로를 탐지하고 오래된 Gemini·Reason Network 실행 절차를 정리했습니다.

## 검증과 범위

로컬 검사 83개가 통과했습니다. 실제 출력 36개를 버전명을 가려 원문과 대조한 소규모 합성 평가에서는 기준판 17/18개, 후보 18/18개가 수락됐습니다. 일부 문장의 연결은 기준판 선호도 있어 모든 글의 향상을 주장하지 않습니다. 모델 backend ID·seed·temperature는 확인되지 않았습니다.

개인 계정의 2.4.0 업데이트·공식 설치와 설치 파일 1,787개 대조, 설치된 검사기 실행을 확인했습니다. 호스트의 자동 스킬 선택·Office 화면 렌더·실제 독자 반응·AI 탐지 회피는 측정하지 않았습니다. 새 검사기는 Python 3.10 이상 표준 라이브러리만 사용합니다. DOCX는 기존 선택 기능이며 `python-docx>=1.1,<2`가 별도로 필요합니다. 새 유료 API·외부 모델·계정 권한을 요구하지 않습니다.

- [GitHub 후보 20개 비교](GitHub_후보20_비교.md): 고정 커밋의 README·관련 코드·예시/테스트·권리 자료를 확인했습니다. 원문 120개를 확보했고 외부 저장소의 테스트는 직접 실행하지 않았습니다.
- [대표 입력의 실제 전후 결과](대표_전후_결과.md)
- [변경 기록](RELEASE_NOTES.md) · [제3자 자료와 권리 고지](THIRD_PARTY_NOTICES.md)

전체 소스·스킬·평가 입력·검사 실행법·기존 출처 고지는 공개 설치 ZIP의 `plugins/writing-design-research-toolkit/` 안에 있습니다. 새 외부 코드를 복제하거나 필수 의존성으로 추가하지 않았습니다. 각 기존 자료의 권리는 해당 고지와 원출처를 따릅니다.
