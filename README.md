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
