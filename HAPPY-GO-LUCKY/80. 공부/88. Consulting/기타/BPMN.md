BPMN은 오늘날 비즈니스 프로세스를 모델링할 때에 가장 널리 쓰이는 언어 중 하나이다. 이번 포스팅에서는 이 BPMN이 무엇인지에 대해 알아보겠다.

[![](https://blog.kakaocdn.net/dn/dil1oL/btqAjmBoLmD/r1fvzspDlkn4Lt5P3AGfmK/img.png)](https://blog.kakaocdn.net/dn/dil1oL/btqAjmBoLmD/r1fvzspDlkn4Lt5P3AGfmK/img.png)

BPMN을 이용해 나타낸 프로세스 모델

BPMN은 위 그림과 같은 형태를 가진다. BPMN의 구성 요소를 하나하나 살펴 보면 다음과 같다.

- task / activity: 하나의 행동을 나타낸다. 위 그림에서 register request, decide 등이 이에 해당된다.
- event: 토큰이 이동하는 자리를 표시하는 역할을 한다. 이는 일정 시간이 지나면 / 메일이 오면 등의 조건이 될 수도 있고 start와 end처럼 시작과 끝을 의미하기도 한다. 각 event마다 input과 output arc가 각각 하나씩만 있다. (start, end event 제외)

[![](https://blog.kakaocdn.net/dn/o9cP2/btqAiWJUk7g/Ke8iwYxVLpr9GvDNyQ9h6k/img.png)](https://blog.kakaocdn.net/dn/o9cP2/btqAiWJUk7g/Ke8iwYxVLpr9GvDNyQ9h6k/img.png)

BPMN의 이벤트 예시

- gateway: 하나의 task 이후에 어떤 선택을 할 것인지(split) 혹은 하나의 task 전에 어떤 조건이 필요한지(join)를 나타내는 것을 말한다. 위 그림에서는 X, +로 표현된 것들이 이에 해당된다. 이 gateway에는 다음과 같이 6개의 종류가 있다.

[![](https://blog.kakaocdn.net/dn/yNBvs/btqAkT56vPu/BUr4KDUx2kBRiCcPl9BOd0/img.png)](https://blog.kakaocdn.net/dn/yNBvs/btqAkT56vPu/BUr4KDUx2kBRiCcPl9BOd0/img.png)

BPMN의 gateway

각 gateway들을 설명하면 다음과 같다.

- AND-split: 뒤에 오는 화살표들이 모두 실행된다.
- AND-join: 앞에 오는 화살표가 모두 실행되고 나서 뒤가 실행된다.
- XOR-split: 뒤에 오는 화살표 중 하나가 실행된다.
- XOR-join: 앞에 오는 화살표 중 하나가 실행되면 뒤가 실행된다.
- OR-split: 뒤에 오는 화살표 중 하나 이상이 실행된다.
- OR-join: 앞에 오는 화살표 중 하나 이상이 실행되면 뒤가 실행된다.