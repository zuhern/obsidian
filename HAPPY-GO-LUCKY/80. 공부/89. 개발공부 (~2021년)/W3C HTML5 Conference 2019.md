---
Created: Invalid date
Updated: Invalid date
---
1. 기조연설 1.project Fugu “closing the app gap”

Google chrome 엔지니어

Documents -> (html5) -> Application

media consumption (youtube, netflix) —> media production (google docs...)

사례1:

Fugu???

Soundation 의 역사 flash (2010) -> chrome 기반 -> html5 (2018)

8년이나 걸림

원인: 웹 표준화의 속도가 느림

사례2:

PWA 웹을 앱처럼 사용할 수 있게 하는..

Spotify desktop app uses

chromium Enbedded Framework(CEF)

웹앱이 지원하지 않는 부분 때문에 앱을 포기하지 못한다. (노티,툴바,컴터시작시 자동 실행 등..)

사례3:

web audio api (2010-2019)

원인: 웹 개발자와의 소통 부족으로 인해 쓸데없는것을 만듦

위 사례들을 통해 fugu 를 하게 됌

웹 플랫폼과 네이티브와의 기능 차이를 줄이고 웹의 장점은 그대로 보존하면서

개발자들이 웹에서 새로운 기능을 사용할 수 있게 한다. -> 웹장점 + 앱장점

- ***

1. 의견 수집

2. 의견을 가지고 요구사항 정리 (write explainer)

3. Solicit feedback

4. 2-3 반복으로 정리가 되면 formal spec 정리

5. spec 구현

w3ctag.github.io/explainers

- > 사용자들이 격고있는 문제점의 분명한 정의

문제 접근 방법과 해결책 제안

해결책과 제안된 디자인에 기반한 코드 제의

github.com/googlechrome/origintrials

새로운 웹 기능을 안전하게 실험

새 기능 사용한 앱으로 직접 유저 테스트 가능

의미있는 피드백을 얻을 수 있다.

- > chrome api 가 꼭 거치는 ..

권한/허가 & 개인정보 보호 & 보안 이 세가지를 충실히 고민하여 강력한 사용자 보호..해야한다.

예시)

- 웹앱에서 블루투스 사용
- web Share & web Share Target 사용 가능
- media session api 웹에서 안드로이드의 media api 를 사용 가능
- shape detection api 사용 가능 (QR 코드 사용)
- badging api 뱃지 사용
- native file system: 웹앱이 로컬 파일에 접근 가능
- web serial api.. 아두이노 지원이 가능
- web HID API (human interface Driver(?)) 해드셋 버튼을 웹에서 사용하고 싶다. 할때

우왕

fugu API Tracker 에서 확인 가능

goo.gle/fugu-api-tracker

2. Naver whale

클린 웹: 광고 규정에 어긋나는 과도한 광고를 제거, 막음

웹 인증서 2.0

오픈소스의 무게 rebase

3. 플러그인 제거 현황

4. svelte

스벨트가 리엑트 보다 빠르다

메모리를 더 적게 쓴다

문법이 쉬워

html 문법 그대로

단점이 있는데.. TypeStript 를 완전히 지원하지는 않는다.

5. 웹개발자가 seo를 위해 알아두어야 할 구조화 데이터

search engine optimization

마케팅과 seo: 검색해서 방문하는 트래픽이 제일 많아

normal sniippet,

rich sniippet(이미지 포함하는 검색 결과),

featured snippet(박스로 영역이 따로 있는 검색 결과)

구글이 이해할 수 있는 구조화 데이터 문법, 샘플..을 찾으면 있음.

종류:

microdata: 데이터를 구조화하면 끝나는 것

json-ld: 기존 싸이트 변경 없이 추가할 수 있다., 구글이 이것을 적극 지지 (추천한다)

구글 developer 사이트에서 구조화 데이터 뭐.. 검색하면

관련 툴 많음

6. 디자이너가 코딩

- html, css, javascript, canvas, pixiJs*, threeJs(webGL)
- svg, snap.svg
- Animation library: GSAP (green sock 좋다)
- 수학(삼각함수 벡터 행렬: 게임 개발 책들을 보면 수학을 알려주면서 예제까지 들어줌, 게임개발자를 위한 수학...등)

7. 웹 브라우저

각 박스의 넓이는 viewport: 윈도우 사이즈 기준

각 박스의 높이는 contens( fonts ) 를 기준으로 함으로

이둘을 바꾸는 일이 있으면 layout 이 전체적으로 변경되어 성능이 느려질 것을 고려해야 한다.

paint 는 픽셀하나하나씩 그려야해서 겁나 느린데

layer tree 로 화면을 그리면 괜찮다 (update layer tree)

layer 생성 조건

Root object

Css position ..

Css 3d transform

Will-change...

등.......

composite layer -> 레이어 합침

7-2 신상 브라우저

8. V8

옛날 꺼

Fullcode generator:  최적화 되지 않은 코드 생성

Crankshaft : es6 전 js 최적화 : 최적화 하는 시점은 런타임 시점

turbofan: es6 이후 js 최적화 : 최적화 하는 시점은 런타임 시점

V8

Parser -> ast(abstract syntax tree) -> ignition -> byte code -> turbo fan -> turbo fan optimier -> byte code -> turbo fan...... 반복

SSA (Static single assignment form) 을 활용한 최적화

ignition 작동 과정