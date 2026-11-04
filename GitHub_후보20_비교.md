# GitHub 추가 후보 20개 비교와 채택 근거

검토일: 2026-11-05(한국시간). 기존 분석의 완료 조사는 재사용했다. 기존 참조 25개·추가 참고 12개를 식별한 후 신규 저장소를 우선 골랐다. Kiwi의 Python wrapper는 기존 본체와 관련된 별도 후보임을 명시했다. 별 개수는 채택 기준으로 사용하지 않았다.

최종 교차검토에서 write-good의 일반 참고 링크가 기존 자료에 있었음을 확인했다. 따라서 이 후보는 기존 언급에 대한 실제 구현·테스트 추가 검토로 구별한다. 다른 후보도 단순 링크 존재와 기능 도입을 동일하게 세지 않았다.

공개 조사 경로는 ego-browser CLI/nodejs와 ego lite TaskSpace 13이다. 실제 검색·저장소 페이지를 연 뒤 문서화된 ego Node fetch로 공개 HTML과 고정 커밋의 원문을 확보했다. 공개 GitHub API 403 한도 오류와 초기 잘못된 경로의 404는 원문 기록에 남겼다. 오류를 다른 웹 도구나 계정 권한 확대의 근거로 삼지 않았다.

**설계 채택은 외부 코드 복제·패키지 설치가 아니다.** 채택한 구조를 참고해 표준 라이브러리로 독자 구현했다. 각 저장소의 테스트는 원문을 읽었으며 직접 실행하지 않았다. 외부 저장소의 성능 주장을 이 패키지의 실측 결과로 옮기지 않았다.

|후보|판단|실제 적용/보류 이유|
|---|---|---|
|[hyunwoongko/kss](https://github.com/hyunwoongko/kss/tree/d7e26bd565569e816268a838a3816b3ed84d8034)|보류|기존 Kiwi·한국어 지침과 일부 중복. 우선 필요한 보존 검사에는 필수 아님; 큰 입력의 문장 정렬 수요가 생길 때 별도 측정.|
|[bab2min/kiwipiepy](https://github.com/bab2min/kiwipiepy/tree/0254a0162840e844d349f406299e5d60ee561aff)|보류|기존 bab2min/Kiwi 원문과 같은 생태계의 별도 wrapper 저장소. 원문 그대로 보존하는 오프라인 경량 도구를 우선해 의존성 도입 보류.|
|[haven-jeon/PyKoSpacing](https://github.com/haven-jeon/PyKoSpacing/tree/a44b09f339797433853a6e741a8bb7182795d8f3)|보류|기존 한국어 편집 지침을 자동 추천으로 확장하나 설치 비용 큼. 모델 없이 가능한 문자·보호 구역 검사를 먼저 구현.|
|[ssut/py-hanspell](https://github.com/ssut/py-hanspell/tree/fdc6ca50c19f1c85971437a072d89d4e5ce024b8)|기본 도입 기각|새 서비스 연결을 기본 조건으로 만들지 않는 요청과 맞지 않는다. 외부 전송 없는 독자 검사로 대체.|
|[lovit/soynlp](https://github.com/lovit/soynlp/tree/503eaee28799e9a3baf01483c6fc59e0db524fa3)|정규화 기본 도입 기각|기존 검색·의도적 반복 보존 지침과 겹친다. 자동 정규화 대신 원형을 두고 위험 변화만 보고하도록 채택 방향 결정.|
|[toss/es-hangul](https://github.com/toss/es-hangul/tree/0ecc91ee2e3f130824d726595ad246c859f88656)|보류|단어 삽입 양식이 주 목적일 때 효과가 높다. 현재 자유로운 윤문에는 새 JS 런타임 연결보다 의미·제약 검수가 우선.|
|[e-/Josa.js](https://github.com/e-/Josa.js/tree/1805eb348be8783e529cc4505ff49686828ebe76)|보류|es-hangul과 중복. 실제 템플릿 수요가 생기면 더 넓은 예외와 테스트를 가진 후보를 비교; 지금은 도입 보류.|
|[jdongian/python-jamo](https://github.com/jdongian/python-jamo/tree/7f3f407c7951b54f5c0ed922cf01c01e462a641b)|보류|기존 자모 처리·Kiwi와 일부 겹친다. 필요한 Unicode 표현 차이 경고는 표준 unicodedata로 독자 구현해 추가 의존성 생략.|
|[remarkjs/remark](https://github.com/remarkjs/remark/tree/1146b3a274fc1f4607111e5d6607a3a769a0e89a)|구조 구분 설계 채택·런타임 보류|기존 unified 참조와 인접하지만 별도 Markdown parser 구현 검토. 이번에는 제한된 보호 구역 스캐너만 독자 구현; 완전한 AST 기능이 필요하면 재검토.|
|[markdown-it/markdown-it](https://github.com/markdown-it/markdown-it/tree/a8c00d474ec9b304fad9b71c16d6fa8b4909279e)|보호 구역 설계 채택·런타임 보류|기존 textlint·unified의 범용 안내와 다르게 실제 코드/인용 보호 검사의 공백에 직접 연결. 새 패키지 없이 필요한 구분만 구현.|

## 앞 10개: 한국어 처리와 문서 구조

### 1. hyunwoongko/kss

- 검토 커밋: `d7e26bd565569e816268a838a3816b3ed84d8034`. [README](https://github.com/hyunwoongko/kss/blob/d7e26bd565569e816268a838a3816b3ed84d8034/README.md) · [관련 코드](https://github.com/hyunwoongko/kss/blob/d7e26bd565569e816268a838a3816b3ed84d8034/kss/_modules/sentences/split_sentences.py) · [예시/테스트](https://github.com/hyunwoongko/kss/blob/d7e26bd565569e816268a838a3816b3ed84d8034/tests/test_sentences.py) · [라이선스](https://github.com/hyunwoongko/kss/blob/d7e26bd565569e816268a838a3816b3ed84d8034/LICENSE)
- 해결 문제·구체 적용: 한국어 문장 경계·띄어쓰기를 찾아 문장별 비교 단위를 만들 수 있다. split_sentences의 ignores·backend와 인용 처리 단계를 확인했다.
- 한국어 적용·제약: 구어체 문장 분리에 맞지만 모델·분석기와 띄어쓰기 선택은 저자 의도를 바꿀 수 있다. 현 도구는 완전한 한국어 문장 분리를 주장하지 않는다.
- 권리·의존성·환경: BSD-3-Clause; 복제 시 저작권·조건·면책 고지와 추천 금지 조항 보존. Python, C/C++ 확장·여러 NLP 의존성. 현재 setup.py의 자동 mecab 설치는 비활성화되어 있다.
- 중복·비용·효과·판단: **보류**. 기존 Kiwi·한국어 지침과 일부 중복. 우선 필요한 보존 검사에는 필수 아님; 큰 입력의 문장 정렬 수요가 생길 때 별도 측정.

### 2. bab2min/kiwipiepy

- 검토 커밋: `0254a0162840e844d349f406299e5d60ee561aff`. [README](https://github.com/bab2min/kiwipiepy/blob/0254a0162840e844d349f406299e5d60ee561aff/README.md) · [관련 코드](https://github.com/bab2min/kiwipiepy/blob/0254a0162840e844d349f406299e5d60ee561aff/kiwipiepy/_wrap.py) · [예시/테스트](https://github.com/bab2min/kiwipiepy/blob/0254a0162840e844d349f406299e5d60ee561aff/test/test_kiwipiepy.py) · [라이선스](https://github.com/bab2min/kiwipiepy/blob/0254a0162840e844d349f406299e5d60ee561aff/LICENSE.txt)
- 해결 문제·구체 적용: Python에서 형태소·문장 경계·오탈자 후보를 구한다. _wrap.py의 split_into_sents·space 계열과 테스트를 확인했다.
- 한국어 적용·제약: 한국어에 직접 유용하나 모델 사전과 고유명사·말투 예외 관리 필요. 형태소 점수를 문장 의미 판정으로 쓰지 않는다.
- 권리·의존성·환경: Apache-2.0; 복제·배포 시 LICENSE·NOTICE와 해당 제3자 고지를 보존하고 수정 표시. Python>=3.9, kiwipiepy_model, numpy, tqdm. 소스 빌드는 C++17/CMake.
- 중복·비용·효과·판단: **보류**. 기존 bab2min/Kiwi 원문과 같은 생태계의 별도 wrapper 저장소. 원문 그대로 보존하는 오프라인 경량 도구를 우선해 의존성 도입 보류.

### 3. haven-jeon/PyKoSpacing

- 검토 커밋: `a44b09f339797433853a6e741a8bb7182795d8f3`. [README](https://github.com/haven-jeon/PyKoSpacing/blob/a44b09f339797433853a6e741a8bb7182795d8f3/README.md) · [관련 코드](https://github.com/haven-jeon/PyKoSpacing/blob/a44b09f339797433853a6e741a8bb7182795d8f3/pykospacing/kospacing.py) · [예시/테스트](https://github.com/haven-jeon/PyKoSpacing/blob/a44b09f339797433853a6e741a8bb7182795d8f3/tests/test_v2.py) · [라이선스](https://github.com/haven-jeon/PyKoSpacing/blob/a44b09f339797433853a6e741a8bb7182795d8f3/LICENSE)
- 해결 문제·구체 적용: 띄어쓰기 제안 전용 후보. Spacing의 ignore/규칙과 v2 테스트의 공백 제거 전후 문자 보존 조건을 확인했다.
- 한국어 적용·제약: 한국어 띄어쓰기를 직접 다루지만 띄어쓰기가 의미를 바꾸는 경우 수동 판단 필요. v2는 별도 모델.
- 권리·의존성·환경: GPL-3.0; 결합·배포 방식의 의무 검토가 필요하므로 코드 복제·번들링하지 않는다. 기본 TensorFlow>=2.16.2·h5py, 선택 v2는 torch·transformers·모델 체크포인트.
- 중복·비용·효과·판단: **보류**. 기존 한국어 편집 지침을 자동 추천으로 확장하나 설치 비용 큼. 모델 없이 가능한 문자·보호 구역 검사를 먼저 구현.

### 4. ssut/py-hanspell

- 검토 커밋: `fdc6ca50c19f1c85971437a072d89d4e5ce024b8`. [README](https://github.com/ssut/py-hanspell/blob/fdc6ca50c19f1c85971437a072d89d4e5ce024b8/README.md) · [관련 코드](https://github.com/ssut/py-hanspell/blob/fdc6ca50c19f1c85971437a072d89d4e5ce024b8/hanspell/spell_checker.py) · [예시/테스트](https://github.com/ssut/py-hanspell/blob/fdc6ca50c19f1c85971437a072d89d4e5ce024b8/tests.py) · [라이선스](https://github.com/ssut/py-hanspell/blob/fdc6ca50c19f1c85971437a072d89d4e5ce024b8/LICENSE)
- 해결 문제·구체 적용: 네이버 맞춤법 API 응답을 파싱해 오류·수정문을 제공한다. check()와 테스트가 실제 외부 응답에 의존함을 확인했다.
- 한국어 적용·제약: 한국어 교정에 맞지만 외부 전송·비공식 서비스·응답 형식 변화에 의존하며 의미 검수는 별도다.
- 권리·의존성·환경: MIT; 복제 시 저작권·허가문 보존. 원격 서비스 이용 조건은 코드 라이선스와 별개. Python+requests, 네트워크 필요. requirements의 구형 pin과 setup의 unpin을 구분.
- 중복·비용·효과·판단: **기본 도입 기각**. 새 서비스 연결을 기본 조건으로 만들지 않는 요청과 맞지 않는다. 외부 전송 없는 독자 검사로 대체.

### 5. lovit/soynlp

- 검토 커밋: `503eaee28799e9a3baf01483c6fc59e0db524fa3`. [README](https://github.com/lovit/soynlp/blob/503eaee28799e9a3baf01483c6fc59e0db524fa3/README.md) · [관련 코드](https://github.com/lovit/soynlp/blob/503eaee28799e9a3baf01483c6fc59e0db524fa3/soynlp/normalizer/_normalizer.py) · [예시/테스트](https://github.com/lovit/soynlp/blob/503eaee28799e9a3baf01483c6fc59e0db524fa3/test/basic_test.py) · [라이선스](https://github.com/lovit/soynlp/blob/503eaee28799e9a3baf01483c6fc59e0db524fa3/LICENSE)
- 해결 문제·구체 적용: 반복 문자·기호 정리, 토큰화·키워드 추출 후보. normalizer와 basic_test의 숫자·영문 제거 예를 확인했다.
- 한국어 적용·제약: SNS 반복은 감정·저자 말투일 수 있다. 정규화가 숫자·영문·기호를 제거하면 원문 보존 실패.
- 권리·의존성·환경: LGPL-3.0; 배포 시 적용 라이선스·고지와 수정·연결 방식 의무 확인. 코드 복제 없음. Python, numpy·psutil·scipy.
- 중복·비용·효과·판단: **정규화 기본 도입 기각**. 기존 검색·의도적 반복 보존 지침과 겹친다. 자동 정규화 대신 원형을 두고 위험 변화만 보고하도록 채택 방향 결정.

### 6. toss/es-hangul

- 검토 커밋: `0ecc91ee2e3f130824d726595ad246c859f88656`. [README](https://github.com/toss/es-hangul/blob/0ecc91ee2e3f130824d726595ad246c859f88656/README-en_us.md) · [관련 코드](https://github.com/toss/es-hangul/blob/0ecc91ee2e3f130824d726595ad246c859f88656/src/core/josa/josa.ts) · [예시/테스트](https://github.com/toss/es-hangul/blob/0ecc91ee2e3f130824d726595ad246c859f88656/src/core/josa/josa.spec.ts) · [라이선스](https://github.com/toss/es-hangul/blob/0ecc91ee2e3f130824d726595ad246c859f88656/LICENSE)
- 해결 문제·구체 적용: 한글 조사 선택과 자모 도구. josa의 받침·종성 ㄹ 예외·영문 마지막 문자 처리와 표본 테스트를 확인했다.
- 한국어 적용·제약: 제품명 삽입 템플릿에는 유용하나 영문 약어·숫자의 실제 읽기와 예외가 남고 문맥 의미는 판단하지 않는다.
- 권리·의존성·환경: MIT; 복제 시 저작권·허가문 보존. JavaScript/TypeScript, ESM·CJS 빌드. 개발 검사는 Vitest.
- 중복·비용·효과·판단: **보류**. 단어 삽입 양식이 주 목적일 때 효과가 높다. 현재 자유로운 윤문에는 새 JS 런타임 연결보다 의미·제약 검수가 우선.

### 7. e-/Josa.js

- 검토 커밋: `1805eb348be8783e529cc4505ff49686828ebe76`. [README](https://github.com/e-/Josa.js/blob/1805eb348be8783e529cc4505ff49686828ebe76/README.md) · [관련 코드](https://github.com/e-/Josa.js/blob/1805eb348be8783e529cc4505ff49686828ebe76/josa.js) · [예시/테스트](https://github.com/e-/Josa.js/blob/1805eb348be8783e529cc4505ff49686828ebe76/test/index.js) · [라이선스](https://github.com/e-/Josa.js/blob/1805eb348be8783e529cc4505ff49686828ebe76/LICENSE)
- 해결 문제·구체 적용: 한글 받침에 따른 이/가·은/는·을/를·와/과 선택. 마지막 문자 코드 분기와 QUnit 표본을 확인했다.
- 한국어 적용·제약: 짧은 한글 명사 템플릿용. 숫자·영문·발음 예외와 더 넓은 조사 지원은 별도 확인 필요.
- 권리·의존성·환경: MIT; 복제 시 고지 보존. 의존성 없는 JS 본체. 브라우저 QUnit 테스트는 있으나 npm test는 실패 placeholder.
- 중복·비용·효과·판단: **보류**. es-hangul과 중복. 실제 템플릿 수요가 생기면 더 넓은 예외와 테스트를 가진 후보를 비교; 지금은 도입 보류.

### 8. jdongian/python-jamo

- 검토 커밋: `7f3f407c7951b54f5c0ed922cf01c01e462a641b`. [README](https://github.com/jdongian/python-jamo/blob/7f3f407c7951b54f5c0ed922cf01c01e462a641b/README.rst) · [관련 코드](https://github.com/jdongian/python-jamo/blob/7f3f407c7951b54f5c0ed922cf01c01e462a641b/jamo/jamo.py) · [예시/테스트](https://github.com/jdongian/python-jamo/blob/7f3f407c7951b54f5c0ed922cf01c01e462a641b/tests/test_jamo.py) · [라이선스](https://github.com/jdongian/python-jamo/blob/7f3f407c7951b54f5c0ed922cf01c01e462a641b/LICENSE)
- 해결 문제·구체 적용: 완성형 한글과 자모 분해·조합, Unicode 문자 종류 검사. 변환 함수와 임의 한글 표본 테스트를 확인했다.
- 한국어 적용·제약: 분해형·완성형이 화면상 같아도 코드 포인트·글자 수가 다름을 구별하는 데 유용하다. 모든 입력을 정규화하면 엄격 원문 보존에 어긋날 수 있다.
- 권리·의존성·환경: Apache-2.0; 복제 시 라이선스·고지·수정 표시를 보존. Python3와 Unicode 데이터 파일.
- 중복·비용·효과·판단: **보류**. 기존 자모 처리·Kiwi와 일부 겹친다. 필요한 Unicode 표현 차이 경고는 표준 unicodedata로 독자 구현해 추가 의존성 생략.

### 9. remarkjs/remark

- 검토 커밋: `1146b3a274fc1f4607111e5d6607a3a769a0e89a`. [README](https://github.com/remarkjs/remark/blob/1146b3a274fc1f4607111e5d6607a3a769a0e89a/readme.md) · [관련 코드](https://github.com/remarkjs/remark/blob/1146b3a274fc1f4607111e5d6607a3a769a0e89a/packages/remark-parse/lib/index.js) · [예시/테스트](https://github.com/remarkjs/remark/blob/1146b3a274fc1f4607111e5d6607a3a769a0e89a/test.js) · [라이선스](https://github.com/remarkjs/remark/blob/1146b3a274fc1f4607111e5d6607a3a769a0e89a/license)
- 해결 문제·구체 적용: Markdown을 AST(구문 트리)로 나눠 코드·본문을 구별하는 설계. remark-parse가 fromMarkdown과 확장을 연결하고 테스트가 트리·왕복 변환을 검사한다.
- 한국어 적용·제약: 문법 구조는 언어와 무관하므로 한국어에도 적용 가능. 한국어 문장 의미·말투 평가는 제공하지 않는다.
- 권리·의존성·환경: MIT; 복제 시 저작권·허가문 보존. 코드 복제 없음. Node ESM, unified·mdast-util 계열.
- 중복·비용·효과·판단: **구조 구분 설계 채택·런타임 보류**. 기존 unified 참조와 인접하지만 별도 Markdown parser 구현 검토. 이번에는 제한된 보호 구역 스캐너만 독자 구현; 완전한 AST 기능이 필요하면 재검토.

### 10. markdown-it/markdown-it

- 검토 커밋: `a8c00d474ec9b304fad9b71c16d6fa8b4909279e`. [README](https://github.com/markdown-it/markdown-it/blob/a8c00d474ec9b304fad9b71c16d6fa8b4909279e/README.md) · [관련 코드](https://github.com/markdown-it/markdown-it/blob/a8c00d474ec9b304fad9b71c16d6fa8b4909279e/src/rules_block/fence.ts) · [예시/테스트](https://github.com/markdown-it/markdown-it/blob/a8c00d474ec9b304fad9b71c16d6fa8b4909279e/test/markdown-it/markdown-it.test.mjs) · [라이선스](https://github.com/markdown-it/markdown-it/blob/a8c00d474ec9b304fad9b71c16d6fa8b4909279e/LICENSE)
- 해결 문제·구체 적용: 펜스 길이·백틱 개수를 구분하는 실제 파싱과 테스트를 확인했다. 문체 진단이 코드에 개입하지 않도록 구역을 분리하는 근거.
- 한국어 적용·제약: 한국어 Markdown에도 적용 가능. 완전한 CommonMark 파서와 이번 제한 스캐너를 구분해야 한다.
- 권리·의존성·환경: MIT; 복제 시 저작권·허가문 보존. 코드 복제 없음. Node·브라우저 JS/TS, 링크·문자 엔티티 등 의존성.
- 중복·비용·효과·판단: **보호 구역 설계 채택·런타임 보류**. 기존 textlint·unified의 범용 안내와 다르게 실제 코드/인용 보호 검사의 공백에 직접 연결. 새 패키지 없이 필요한 구분만 구현.

### 저장소 자체 성능 주장과 직접 검증의 구분

PyKoSpacing README의 v1 성능은 세종 구어체·별도 문어체 자료에서 공백이 맞은 문자 비율을 측정한 값이다. 일반 윤문의 의미·자연스러움 점수가 아니다. v2 비교도 같은 저장소가 제시한 데이터·백엔드 조건의 주장이고 재실행하지 않았다. KSS·remark·markdown-it의 정확도·속도 문구 역시 이 환경에서 재현하지 않았다. 이번 직접 검증 대상은 새 보존 검사·색인 완전성·계약 평가기와 현재 Codex의 고정 생성문 표본이다.

# GitHub 추가 후보 10개: 편집·평가·탐지

검토일: 2026-11-05(한국시간). 공개 자료는 ego-browser CLI/nodejs로 조사했다. 같은 TaskSpace 13의 p2에서 실제 GitHub 페이지를 열었고, 이후 설치본 가이드가 허용하는 Node `fetch`로 공개 HTML과 고정 커밋의 원문을 수집했다.

**우선 적용할 것은 문서 구역을 나눠 검사하고, 문제가 된 위치와 이유를 남기는 방식이다.** 유사도·가독성·AI 탐지 점수를 의미 보존의 합격 기준으로 삼지 않는다. 아래 ‘설계 채택’은 코드 복제나 패키지 설치가 아닌, 확인한 구조를 참고한 독자 구현 제안이다. 실제 반영·실행 여부는 통합 결과에서 따로 확인해야 한다.

기존 참조와 중복된 `retextjs/retext`, `wooorm/franc`와 비슷한 영어 기본 처리 후보인 `retextjs/retext-english` 대신 `textstat/textstat`, `redpen-cc/redpen`, `btford/write-good`를 조사했다. `rhysd/redpen`은 404여서 실제 저장소 `redpen-cc/redpen`으로 정정했다. `UKPLab/sentence-transformers`는 현재 소스가 Hugging Face 조직 경로를 안내한다. 아래 링크는 실제 검토에 사용한 GitHub 경로와 고정 커밋이다.

| 후보 | 판단 | 글쓰기기에 유용한 부분 | 도입 비용·핵심 한계 |
|---|---|---|---|
| markdownlint | 설계 채택 | 본문·코드·표·링크의 검사 범위 구분 | 작은 독자 구현 가능. Markdown 구조 검사이며 문장 의미 평가는 아님 |
| textstat | 한국어 주평가 도입 기각 | 영문 전용 가독성의 선택 보조 지표 | 한국어용 검증식 확인 안 됨. 언어 구분 없이 점수화하면 오판 위험 |
| RedPen | 보류 | 문서 단위와 문장 단위의 진단 구분 | JVM·Maven 및 한국어 규칙 제작 비용. 기존 textlint류와 중복 |
| write-good | 설계 일부 채택 | 위치·사유가 있는 경고, 규칙별 중지, 예외 구역 | 영어 규칙 일괄 도입 기각. 예외 처리 구현도 그대로 복제하지 않음 |
| jellyfish | 보류 | 오탈자 후보와 문자열 변경량 확인 | 문자 유사도가 사실 보존·자연스러움을 설명하지 못함 |
| RapidFuzz | 보류 | 대량 자료의 유사 제목·중복 후보 찾기 | 집합 기반 유사도는 내용 추가를 놓칠 수 있음. 현재 소규모 검색에는 과한 의존성 |
| Sentence Transformers | 보류 | 관련 자료 검색·유사 문단 후보 찾기 | PyTorch와 모델 다운로드 필요. 한국어 모델별 성능·라이선스 확인 필요 |
| COMET | 보류 | 번역의 원문·번역문·참조문 대조 설계 | 무거운 모델, 일부 모델의 제한 라이선스·동의·로그인 조건 |
| BLEURT | 보류 | 번역 평가의 보조 점수·오류 표본 설계 | TensorFlow·체크포인트 필요. 단일 문장 점수로 합격 판정 곤란 |
| Fast-DetectGPT | 기본 도입 기각 | 탐지 점수의 실험 조건·한계를 확인하는 자료 | 자연스러움 개선기가 아님. 한국어 집필·윤문 효과의 직접 검증 없음 |

## 11. DavidAnson/markdownlint

- 검토판: `5dd44fe44481cfbc8c6fee955719773fa17dc5d5`. [README](https://github.com/DavidAnson/markdownlint/blob/5dd44fe44481cfbc8c6fee955719773fa17dc5d5/README.md), [관련 코드 MD013](https://github.com/DavidAnson/markdownlint/blob/5dd44fe44481cfbc8c6fee955719773fa17dc5d5/lib/md013.mjs), [테스트](https://github.com/DavidAnson/markdownlint/blob/5dd44fe44481cfbc8c6fee955719773fa17dc5d5/test/markdownlint-test.mjs)를 확인했다.
- 해결 문제와 적용: 긴 줄 규칙도 코드 블록·표·제목·링크만 있는 줄을 구분한다. 글쓰기기에서도 본문에만 문체 진단을 적용하고, 코드·URL·원문 인용은 보존 여부를 별도로 확인하는 구역 분리로 연결할 수 있다. 한국어의 논리나 자연스러움은 검사하지 않는다.
- 코드 근거: MD013 29–49행에서 코드·표·제목 포함 설정과 구역의 줄 번호를 수집하고, 74–81행에서 해당 설정 및 링크 구역을 조건으로 검사한다. 고정 글자 수를 한국어 문장 품질 점수로 바꾸는 방식은 채택하지 않는다.
- 환경·권리: 현재 [package.json](https://github.com/DavidAnson/markdownlint/blob/5dd44fe44481cfbc8c6fee955719773fa17dc5d5/package.json)은 Node.js 22 이상과 micromark·re2js 등 의존성을 선언한다. [MIT](https://github.com/DavidAnson/markdownlint/blob/5dd44fe44481cfbc8c6fee955719773fa17dc5d5/LICENSE); 코드를 복제·배포하면 저작권·허가문 보존이 필요하다.
- 판단: **구역 분리 설계 채택, 런타임 패키지 도입 보류.** 기존 textlint 안내는 선택 도구 소개이고, 독자적인 보존 검사의 실행 구역 분리와는 공백이 다르다. 외부 패키지 없이 필요한 범위만 구현하면 설치 비용이 낮다.

## 12. textstat/textstat

- 검토판: `5679e7ccc0c2627bca1c0506eae1a7feb802a163`. [README](https://github.com/textstat/textstat/blob/5679e7ccc0c2627bca1c0506eae1a7feb802a163/README.md), [구현](https://github.com/textstat/textstat/blob/5679e7ccc0c2627bca1c0506eae1a7feb802a163/textstat/textstat.py), [언어 설정 테스트](https://github.com/textstat/textstat/blob/5679e7ccc0c2627bca1c0506eae1a7feb802a163/tests/textstat/test_set_lang.py), [등급 조합 테스트](https://github.com/textstat/textstat/blob/5679e7ccc0c2627bca1c0506eae1a7feb802a163/tests/textstat/test_text_standard.py)를 확인했다.
- 해결 문제와 적용: 음절 수·어휘 수·문장 길이 등을 바탕으로 영문 독해 난이도를 추정한다. 영어 장문의 과밀한 문장을 찾는 선택 진단에는 쓸 수 있다. 의미 보존·독자 적합성·한국어 자연스러움의 합격 점수로는 쓰지 않는다.
- 한국어 제약: README는 기본 영어 알고리즘과 일부 유럽 언어 변형을 명시한다. 언어 테스트에도 한국어 표본이 없다. 한국어를 지원하지 않는다고 모든 함수에 대해 단정하지 않되, 한국어 가독성 추정의 검증 근거를 확인하지 못했다.
- 환경·권리: [setup.py](https://github.com/textstat/textstat/blob/5679e7ccc0c2627bca1c0506eae1a7feb802a163/setup.py)는 Python 3.6 이상과 pyphen·nltk·setuptools를 선언한다. 같은 판의 코드에는 더 최신 Python 구문도 있어 선언값만으로 오래된 환경 실행을 보장할 수 없다. [MIT](https://github.com/textstat/textstat/blob/5679e7ccc0c2627bca1c0506eae1a7feb802a163/LICENSE), 복제 시 고지 보존.
- 판단: **한국어 주평가 도입 기각, 영문 보조 기능 보류.** 기존 수동 독자 적합성 검수를 수치로 대체할 근거가 부족하고, 의존성 대비 현재 목적의 효과가 낮다.

## 13. redpen-cc/redpen

- 검토판: `875029898b36d9dd4a053a0f925cf7c1a726c6af`. [README](https://github.com/redpen-cc/redpen/blob/875029898b36d9dd4a053a0f925cf7c1a726c6af/README.md), [InvalidExpressionValidator](https://github.com/redpen-cc/redpen/blob/875029898b36d9dd4a053a0f925cf7c1a726c6af/redpen-core/src/main/java/cc/redpen/validator/sentence/InvalidExpressionValidator.java), [해당 테스트](https://github.com/redpen-cc/redpen/blob/875029898b36d9dd4a053a0f925cf7c1a726c6af/redpen-core/src/test/java/cc/redpen/validator/sentence/InvalidExpressionValidatorTest.java)를 확인했다.
- 해결 문제와 적용: 기술 문서를 문장·문서의 여러 검사기로 나눠 검사한다. 진단에 위치를 붙이고, 조직별 금칙 표현을 별도 사전으로 관리하는 방식은 참고할 수 있다. 실제 읽은 구현은 사전 문자열이 문장에 있는지 검사하므로, 문맥·인용·부정의 의도까지 판정하지 않는다.
- 한국어 제약: 현재 읽은 사전 기반 검사기는 사용자 한국어 사전을 넣는 독자 확장 가능성이 있으나 한국어 지원 품질을 검증하지 않았다. 서술어·조사 변화·인용 예외를 단순 일치로 처리하면 과잉 수정 위험이 있다.
- 환경·권리: [pom.xml](https://github.com/redpen-cc/redpen/blob/875029898b36d9dd4a053a0f925cf7c1a726c6af/pom.xml)의 Java/Maven 모듈 프로젝트(버전 1.10.4). JVM·문서 파서·별도 규칙 관리가 필요하다. [Apache-2.0](https://github.com/redpen-cc/redpen/blob/875029898b36d9dd4a053a0f925cf7c1a726c6af/LICENSE.txt), [NOTICE](https://github.com/redpen-cc/redpen/blob/875029898b36d9dd4a053a0f925cf7c1a726c6af/NOTICE.md)도 확인했다. 복제·배포 시 라이선스·관련 고지와 수정 표시를 보존해야 한다.
- 판단: **런타임 도입 보류.** 기존 textlint·Vale 안내와 겹치며 한국어 규칙을 새로 만들 비용이 높다. 문장별 위치 진단 개념만 더 작은 독자 도구에 반영하는 편이 적절하다.

## 14. btford/write-good

- 검토판: `6940b034c6f5a7e101c01a24d651a778fc3fe435`. [README](https://github.com/btford/write-good/blob/6940b034c6f5a7e101c01a24d651a778fc3fe435/README.md), [실제 코드](https://github.com/btford/write-good/blob/6940b034c6f5a7e101c01a24d651a778fc3fe435/write-good.js), [테스트](https://github.com/btford/write-good/blob/6940b034c6f5a7e101c01a24d651a778fc3fe435/test/basic.spec.js)를 확인했다.
- 해결 문제와 적용: 영어 문장에서 반복·상투 표현·수동태 등의 후보를 위치와 사유로 돌려준다. 글쓰기기에는 ‘규칙 ID·위치·근거·검토 필요’ 형태의 진단, 사용자별 제외 표현, 규칙별 중지의 설계를 일부 채택할 수 있다. 영어 수동태·부사 규칙을 한국어에 그대로 적용하지 않는다.
- 주의할 실제 구현: whitelist 위치 수집은 `index > 0` 조건이라 맨 앞에서 시작하는 예외 표현을 놓칠 수 있다(31–35행). 이 코드를 복제하지 않고, 위치 0·반복·중첩 예외 구역을 따로 시험해야 한다. 기존 ‘AI 말투’ 금지어 치환을 확대하는 근거로 쓰지 않는다.
- 환경·권리: [package.json](https://github.com/btford/write-good/blob/6940b034c6f5a7e101c01a24d651a778fc3fe435/package.json)은 Node.js 6 이상, npm 5 이상과 여러 영어 규칙 패키지를 선언한다. 현재 운영 지원성을 실행으로 검증한 것은 아니다. [MIT](https://github.com/btford/write-good/blob/6940b034c6f5a7e101c01a24d651a778fc3fe435/LICENSE), 복제 시 고지 보존.
- 판단: **위치 진단·제외 구역 설계 일부 채택, 영어 규칙 일괄 도입 기각.** 한국어에 필요한 최소 경고를 독자 구현하면 가볍고, 과잉 수정을 줄일 수 있다. 경고 개수는 글의 품질 점수가 아니다.

## 15. jamesturk/jellyfish

- 검토판: `922a6395d02bc1f405bcd6466252dfdb58225c3f`. [README와 사용 예](https://github.com/jamesturk/jellyfish/blob/922a6395d02bc1f405bcd6466252dfdb58225c3f/README.md), [Python 구현](https://github.com/jamesturk/jellyfish/blob/922a6395d02bc1f405bcd6466252dfdb58225c3f/python/jellyfish/_jellyfish.py), [파라미터화 테스트](https://github.com/jamesturk/jellyfish/blob/922a6395d02bc1f405bcd6466252dfdb58225c3f/tests/test_jellyfish.py)를 확인했다.
- 해결 문제와 적용: 편집 거리·Jaro 계열 유사도와 발음 기반 매칭을 제공한다. 유사 고유명사·오탈자 후보를 띄우거나 원문 변경량을 참고할 수 있다. 한국어에서는 유니코드 정규화 방식과 자모·완성형 차이를 별도로 정의해야 하며 영문 발음 알고리즘을 한글 발음 검사로 취급할 수 없다.
- 의미 한계: 숫자 한 자리나 부정 표현이 바뀌어도 문자열 대부분은 같다. 높은 유사도는 사실·조건 보존을 입증하지 않는다. 기존 Python 표준 `difflib`로 작은 변경량을 보여줄 수 있어 현재 목적에서는 중복이 크다.
- 환경·권리: [pyproject.toml](https://github.com/jamesturk/jellyfish/blob/922a6395d02bc1f405bcd6466252dfdb58225c3f/pyproject.toml)은 Python 3.11 이상, maturin/PyO3 기반 Rust 확장 빌드를 선언한다. 휠 사용 여부에 따라 빌드 부담이 달라진다. [MIT](https://github.com/jamesturk/jellyfish/blob/922a6395d02bc1f405bcd6466252dfdb58225c3f/LICENSE), 복제 시 고지 보존.
- 판단: **보류.** 대량 오탈자 후보 기능이 필요해졌을 때 재검토한다. 현재는 숫자·단위·인용·조건을 별도로 확인하는 기능이 더 직접적이다.

## 16. rapidfuzz/RapidFuzz

- 검토판: `1d7d2f071c30f376bf47b76e06815f870ac420f8`. [README와 예](https://github.com/rapidfuzz/RapidFuzz/blob/1d7d2f071c30f376bf47b76e06815f870ac420f8/README.md), [fuzz_py 구현](https://github.com/rapidfuzz/RapidFuzz/blob/1d7d2f071c30f376bf47b76e06815f870ac420f8/src/rapidfuzz/fuzz_py.py), [테스트](https://github.com/rapidfuzz/RapidFuzz/blob/1d7d2f071c30f376bf47b76e06815f870ac420f8/tests/test_fuzz.py)를 확인했다.
- 해결 문제와 적용: 대량 문자열 유사 검색에 적합하다. 자료 제목의 오타 허용 검색·중복 문단 후보·유사 파일명 탐지에는 쓸 수 있다. 한국어 문장의 논리나 말투를 판정하는 도구는 아니다.
- 중요 한계: `token_set_ratio`는 한쪽 토큰 집합이 다른 쪽의 부분집합이면 추가 내용이 있어도 최고 점수를 줄 수 있다. README 예시와 실제 집합 연산 구현이 이를 보여준다. 따라서 새 사실 추가·누락의 합격 판정에는 부적합하다. README의 속도 우위 주장은 저장소 자체 벤치마크이며 이 작업에서 재현하지 않았다.
- 환경·권리: [pyproject.toml](https://github.com/rapidfuzz/RapidFuzz/blob/1d7d2f071c30f376bf47b76e06815f870ac420f8/pyproject.toml)은 Python 3.11 이상. README는 Windows C++ 재배포 패키지, 소스 빌드 시 C++17 환경을 안내한다. [MIT](https://github.com/rapidfuzz/RapidFuzz/blob/1d7d2f071c30f376bf47b76e06815f870ac420f8/LICENSE), 복제 시 고지 보존.
- 판단: **보류.** 기존 색인 검색의 대량 유사 검색 공백이 실제로 커질 때 효과를 측정한 뒤 도입한다. 색인 누락 탐지는 집합 비교로 해결할 수 있으므로 이 의존성이 필요하지 않다.

## 17. UKPLab/sentence-transformers

- 검토판: `3eeec5b5a912809e1034847f9d6d3d4a2d0a5f62`. [README와 인코딩 예](https://github.com/UKPLab/sentence-transformers/blob/3eeec5b5a912809e1034847f9d6d3d4a2d0a5f62/README.md), [현재 model.py](https://github.com/UKPLab/sentence-transformers/blob/3eeec5b5a912809e1034847f9d6d3d4a2d0a5f62/sentence_transformers/sentence_transformer/model.py), [임베딩 테스트](https://github.com/UKPLab/sentence-transformers/blob/3eeec5b5a912809e1034847f9d6d3d4a2d0a5f62/tests/sentence_transformer/test_compute_embeddings.py)를 확인했다. 예전 `SentenceTransformer.py` 경로는 현재 판에서 404여서 실제 파일 경로를 찾아 수정했다.
- 해결 문제와 적용: 문장을 벡터로 만들어 관련 참고 자료를 찾거나 유사 문단 후보를 묶을 수 있다. 한국어 지원은 프레임워크 이름이 아닌 선택 모델의 학습·평가 범위에 달려 있다. 부정·수치 차이가 작은 문장에 대한 의미 보존 합격기로 바로 쓰지 않는다.
- 코드 근거: 현재 구현에는 모델별 인코딩·정규화·차원 축소·정밀도 선택이 있고, 테스트는 출력 크기와 배치·단일 인코딩 및 정규화를 비교한다. 이 테스트 통과가 한국어 사실 보존을 입증하는 것은 아니다.
- 환경·권리: [pyproject.toml](https://github.com/UKPLab/sentence-transformers/blob/3eeec5b5a912809e1034847f9d6d3d4a2d0a5f62/pyproject.toml)의 개발판 6.3.0.dev0은 Python 3.10 이상, torch 2.2 이상, transformers 5 계열 등과 모델 파일이 필요하다. [Apache-2.0](https://github.com/UKPLab/sentence-transformers/blob/3eeec5b5a912809e1034847f9d6d3d4a2d0a5f62/LICENSE), [NOTICE](https://github.com/UKPLab/sentence-transformers/blob/3eeec5b5a912809e1034847f9d6d3d4a2d0a5f62/NOTICE.txt); 모델별 라이선스는 별도 확인해야 한다.
- 판단: **보류.** 기존 경량 자료 검색과 겹치는 부분에 비해 설치·모델 관리 비용이 크다. 이번 작업의 외부 모델 비필수 조건을 유지한다.

## 18. Unbabel/COMET

- 검토판: `da61b810ea06f67bbd5d96031f55082167a16e80`. [README](https://github.com/Unbabel/COMET/blob/da61b810ea06f67bbd5d96031f55082167a16e80/README.md), [회귀 평가 구현](https://github.com/Unbabel/COMET/blob/da61b810ea06f67bbd5d96031f55082167a16e80/comet/models/regression/regression_metric.py), [실제 예측 테스트](https://github.com/Unbabel/COMET/blob/da61b810ea06f67bbd5d96031f55082167a16e80/tests/unit/test_models_predict.py)를 확인했다.
- 해결 문제와 적용: 원문·번역문·참조문을 나란히 평가하는 구조다. XCOMET 테스트에는 고유명사가 바뀐 번역과 오류 구역·심각도 표본이 있어, 글쓰기기의 번역 평가 사례 설계에 참고할 수 있다. 자연스러워 보여도 사실이 바뀌면 실패시키는 독자 평가와 연결된다.
- 한국어 제약: README는 기반 다국어 모델 언어에 한국어를 포함하지만, 모든 한국어 장르·저자 말투에서 성능을 보장하지 않는다. 점수는 모델·학습 자료·참조문에 의존한다. 저장소의 성능·상관 주장과 이 작업의 실제 검증은 구별한다.
- 환경·권리: [pyproject.toml](https://github.com/Unbabel/COMET/blob/da61b810ea06f67bbd5d96031f55082167a16e80/pyproject.toml)은 Python 3.8 계열 이상 범위, torch·transformers·pytorch-lightning 등과 모델을 요구한다. 코드 [Apache-2.0](https://github.com/Unbabel/COMET/blob/da61b810ea06f67bbd5d96031f55082167a16e80/LICENSE). [모델 라이선스 표](https://github.com/Unbabel/COMET/blob/da61b810ea06f67bbd5d96031f55082167a16e80/LICENSE.models.md)는 Apache와 CC-BY-NC-SA 모델을 구별한다. 일부 모델은 Hugging Face 동의·로그인도 필요하다.
- 판단: **런타임 도입 보류, 원문·출력·참조문 및 오류 구역 평가 설계 참고.** 기본 글쓰기 기능에 모델·권한·다른 계정을 필수로 추가하지 않는다. 공개 모델 체크포인트도 이 작업에서는 다운로드·실행하지 않았다.

## 19. google-research/bleurt

- 검토판: `cebe7e6f996b40910cfaa520a63db47807e3bf5c`. [README](https://github.com/google-research/bleurt/blob/cebe7e6f996b40910cfaa520a63db47807e3bf5c/README.md), [score.py](https://github.com/google-research/bleurt/blob/cebe7e6f996b40910cfaa520a63db47807e3bf5c/bleurt/score.py), [실제 테스트](https://github.com/google-research/bleurt/blob/cebe7e6f996b40910cfaa520a63db47807e3bf5c/bleurt/score_test.py), [체크포인트 안내](https://github.com/google-research/bleurt/blob/cebe7e6f996b40910cfaa520a63db47807e3bf5c/checkpoints.md)를 확인했다.
- 해결 문제와 적용: 참조문과 생성문의 적합성을 학습된 모델로 점수화한다. 번역 평가의 선택 보조 점수나 오류가 주입된 평가 세트 설계에 참고할 수 있다. README는 BLEURT-20이 한국어를 포함한 13개 언어의 보류 평가 자료로 시험됐다고 설명하지만, 이는 글쓰기기의 한국어 실제 성능 검증이 아니다.
- 제약: README도 단일 문장의 점수 변동과 집합 평균을 설명하며, 기본 시험용 체크포인트의 정확도가 낮다고 알린다. 높은 점수로 숫자·부정·인용 오류를 상쇄하지 않는다. 장르·독자 적합성·개인 말투는 따로 평가해야 한다.
- 환경·권리: [setup.py](https://github.com/google-research/bleurt/blob/cebe7e6f996b40910cfaa520a63db47807e3bf5c/setup.py)는 TensorFlow·tf-slim·sentencepiece·numpy·scipy·pandas를 요구한다. CPU 실행도 안내하지만 GPU가 유리하며 별도 체크포인트가 필요하다. [Apache-2.0](https://github.com/google-research/bleurt/blob/cebe7e6f996b40910cfaa520a63db47807e3bf5c/LICENSE); 배포 체크포인트의 조건도 별도 확인 대상이다.
- 판단: **보류.** 직접 읽고 확인하는 사실 보존 필수 기준을 먼저 갖춘다. 무거운 모델 점수와 한국어 장르별 보정은 이번 경량 업데이트의 필요조건이 아니다.

## 20. baoguangsheng/fast-detect-gpt

- 검토판: `971b05202bac2bb504d60c0ac0812fea7a8f7c82`. [README](https://github.com/baoguangsheng/fast-detect-gpt/blob/971b05202bac2bb504d60c0ac0812fea7a8f7c82/README.md), [곡률 계산 코드](https://github.com/baoguangsheng/fast-detect-gpt/blob/971b05202bac2bb504d60c0ac0812fea7a8f7c82/scripts/fast_detect_gpt.py), [로컬 예](https://github.com/baoguangsheng/fast-detect-gpt/blob/971b05202bac2bb504d60c0ac0812fea7a8f7c82/scripts/local_infer.py), [실험 설정](https://github.com/baoguangsheng/fast-detect-gpt/blob/971b05202bac2bb504d60c0ac0812fea7a8f7c82/main.sh), [자료 구성](https://github.com/baoguangsheng/fast-detect-gpt/blob/971b05202bac2bb504d60c0ac0812fea7a8f7c82/scripts/custom_datasets.py)을 확인했다.
- 해결 문제: 생성 텍스트의 모델 확률 곡률을 이용한 탐지 연구다. 문장 품질·의도 구현을 직접 개선하는 도구는 아니다. 한국어 탐지 회피를 보장하는 기능으로 사용할 근거를 확인하지 못했다.
- 실험 조건: README의 AUROC·속도 주장은 소스 모델을 이용하는 조건과 대리 모델 조건이 다르며, 데이터·모델 평균과 A100 환경을 사용했다. `main.sh`는 xsum·squad·writing 자료를 지정한다. 한국어 사용자 원고의 탐지 성능·오탐률·윤문 효과를 이 작업에서 시험하지 않았다.
- 환경·권리: [requirements](https://github.com/baoguangsheng/fast-detect-gpt/blob/971b05202bac2bb504d60c0ac0812fea7a8f7c82/requirements.txt)는 torch·transformers 4.28.1·datasets 2.12.0 등을 요구한다. [MIT](https://github.com/baoguangsheng/fast-detect-gpt/blob/971b05202bac2bb504d60c0ac0812fea7a8f7c82/LICENSE), 모델별 권리는 별도다. README의 데모 기본 모델 설명은 gpt-neo-2.7B지만, 현재 코드 기본은 falcon-7b/falcon-7b-instruct여서 문서만으로 재현 조건을 정하면 안 된다.
- 판단: **기본 도입 기각.** 탐지 회피 점수 최적화는 사실·말투·자연스러움 보존의 증거가 되지 않는다. 글쓰기기에서는 문맥 없는 상투 표현·의미 없는 수식·일률적인 문장 리듬을 실제 대목에서 고치고 원문 의미를 대조하는 경로를 유지한다. 외부 모델·유료 API·계정 조건도 추가하지 않는다.

## 검증 범위와 기록

- 10개 모두 고정 커밋의 README·관련 구현·예 또는 테스트·라이선스·의존성 선언을 실제로 수집하고 검토했다. 저장소 전체를 전수 검토한 것은 아니다.
- 외부 저장소의 테스트 실행·패키지 설치·모델 다운로드·한국어 성능 벤치마크는 수행하지 않았다. ‘테스트 확인’은 테스트 원문을 읽었다는 뜻이다. 해당 저장소의 성능 수치를 이 환경의 측정 결과로 제시하지 않았다.
- 초기에 GitHub 비인증 API가 한도 초과 403을 반환했다. API 호출을 중단하고 같은 ego 실행 경로의 공개 HTML·raw 원문으로 조사했다. 인증·권한을 추가하거나 다른 브라우저로 전환하지 않았다.
- 404가 난 초기 추정 파일 경로와 성공한 실제 경로는 저장소별 `meta.json`에 구분해 남겼다. 원문·URL·수집 시각·일부 SHA256은 `work/github-text-eval/<owner>--<repo>/`에 보존했다. 저장소 코드는 조사용 작업 자료이며 글쓰기기 패키지에 복제하지 않는다.
- 최종 구현의 수락 기준은 별도다. 사실·조건·인용 오류는 문체·유사도 점수와 무관하게 실패시키고, 보호 구역 맨 앞·반복·중첩, 정상 표현 유지, 한국어·영어 혼합 문장을 회귀 사례에 포함해야 한다.

