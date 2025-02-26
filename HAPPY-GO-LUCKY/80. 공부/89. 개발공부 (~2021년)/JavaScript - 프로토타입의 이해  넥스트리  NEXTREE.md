---
Created: Invalid date
Updated: Invalid date
URL: http://www.nextree.co.kr/p7323/
---
- [Home](http://www.nextree.co.kr/)
- [About](http://www.nextree.co.kr/about/)
- [Login](http://www.nextree.co.kr/login-2/)

# JavaScript : 프로토타입(prototype) 이해

**Posted by** [**권 혁준**](http://www.nextree.co.kr/author/hjkwonnextree-co-kr/) **in** [**배움터 - 열공**](http://www.nextree.co.kr/category/study/)

on Mar 25th, 2014

![[untitled 14.jpg|untitled 14.jpg]]

JavaScript는 클래스라는 개념이 없습니다. 그래서 기존의 객체를 복사하여(cloning) 새로운 객체를 생성하는 프로토타입 기반의 언어입니다. 프로토타입 기반 언어는 객체 원형인 프로토타입을 이용하여 새로운 객체를 만들어냅니다. 이렇게 생성된 객체 역시 또 다른 객체의 원형이 될 수 있습니다. 프로토타입은 객체를 확장하고 객체 지향적인 프로그래밍을 할 수 있게 해줍니다. 프로토타입은 크게 두 가지로 해석됩니다. 프로토타입 객체를 참조하는 prototype 속성과 객체 멤버인 __proto__ 속성이 참조하는 숨은 링크가 있습니다. 이 둘의 차이점을 이해하기 위해서는 JavaScript 함수와 객체의 내부적인 구조를 이해 해야합니다. 이번 글에서는 JavaScript의 함수와 객체 내부 구조부터 시작하여 프로토타입에 대해 알아보겠습니다.

**1. 함수와 객체의 내부 구조**

JavaScript에서는 함수를 정의하고, 파싱단계에 들어가면, 내부적으로 수행되는 작업이 있습니다. 함수 멤버로 prototype 속성이 있습니다. 이 속성은 다른 곳에 생성된 함수이름의 프로토타입 객체를 참조합니다. 프로토타입 객체의 멤버인 constructor 속성은 함수를 참조하는 내부구조를 가집니다. 아래의 그림 1과 같이 표현합니다.

![[untitled 1 6.jpg|untitled 1 6.jpg]]

< 그림 1 >

**1function Person(){}**

< 소스 1 >

속성이 하나도 없는 Person이라는 함수가 정의되고, 파싱단계에 들어가면, Person 함수 Prototype 속성은 프로토타입 객체를 참조합니다. 프로토타입 객체 멤버인 constructor 속성은 Person 함수를 참조하는 구조를 가집니다. 여기서 알아야 하는 부분은 Person 함수의 prototype 속성이 참조하는 프로토타입 객체는 new라는 연산자와 Person 함수를 통해 생성된 모든 객체의 원형이 되는 객체입니다. 생성된 모든 객체가 참조한다는 것을 기억해야 합니다. 아래의 그림 2와 같이 표현합니다.

![[untitled 2 4.jpg|untitled 2 4.jpg]]

< 그림 2 >

**1234function Person(){} var joon = new Person();var jisoo = new Person();**

< 소스 2 >

JavaScript에서는 기본 데이터 타입인 boolean, number, string, 그리고 특별한 값인 null, undefined 빼고는 모두 객체입니다. 사용자가 정의한 함수도 객체이고, new라는 연산자를 통해 생성된 것도 객체입니다. 객체 안에는 __proto__(비표준) 속성이 있습니다. 이 속성은 객체가 만들어지기 위해 사용된 원형인 프로토타입 객체를 숨은 링크로 참조하는 역할을 합니다.

**2. 프로토타입 객체란?**

함수를 정의하면 다른 곳에 생성되는 프로토타입 객체는 자신이 다른 객체의 원형이 되는 객체입니다. 모든 객체는 프로토타입 객체에 접근할 수 있습니다. 프로토타입 객체도 동적으로 런타임에 멤버를 추가할 수 있습니다. 같은 원형을 복사로 생성된 모든 객체는 추가된 멤버를 사용할 수 있습니다.

![[untitled 3 4.jpg|untitled 3 4.jpg]]

< 그림 3 >

**1234567891011function Person(){} var joon = new Person();var jisoo = new Person(); Person.prototype.getType = function (){  return "인간"; }; console.log(joon.getType()); // 인간console.log(jisoo.getType()); // 인간**

< 소스 3 >

위 소스 3 6라인은 함수 안의 prototype 속성을 이용하여 멤버를 추가하였습니다. 프로토타입 객체에 getType()이라는 함수를 추가하면 멤버를 추가하기 전에 생성된 객체에서도 추가된 멤버를 사용할 수 있습니다. 같은 프로토타입을 이용하여 생성된 joon과 jisoo 객체는 getType()을 사용할 수 있습니다.

여기서 알아두어야 할 것은 프로토타입 객체에 멤버를 추가, 수정, 삭제할 때는 함수 안의 prototype 속성을 사용해야 합니다. 하지만 프로토타입 멤버를 읽을 때는 함수 안의 prototype 속성 또는 객체 이름으로 접근합니다.

![[untitled 4 3.jpg|untitled 4 3.jpg]]

< 그림 4 >

**1234567891011joon.getType = function (){  return "사람"; }; console.log(joon.getType()); // 사람console.log(jisoo.getType()); // 인간 jisoo.age = 25; console.log(joon.age); // undefinedconsole.log(jisoo.age); // 25**

< 소스 4 >

위 소스 4 1라인은 joon 객체를 이용하여 getType() 리턴 값을 사람으로 수정하였습니다. 그리고 joon과 jisoo에서 각각 getType()을 호출하면 joon 객체를 이용하여 호출한 결과는 사람으로 출력되고, jisoo로 호출한 결과는 인간이 출력됩니다. 생성된 객체를 이용하여 프로토타입 객체의 멤버를 수정하면 프로토타입 객체에 있는 멤버를 수정하는 것이 아니라 자신의 객체에 멤버를 추가하는 것입니다. joon 객체를 사용하여 getType()을 호출하면 프로토타입 객체의 getType()을 호출한 것이 아닙니다. joon 객체에 추가된 getType()을 호출한 것입니다. 프로토타입 객체의 멤버를 수정할 경우는 멤버 추가와 같이 함수의 prototype 속성을 이용하여 수정합니다.

![[untitled 4 3.jpg|untitled 4 3.jpg]]

< 그림 5 >

**12345Person.prototype.getType = function (){ return "사람"; }; console.log(jisoo.getType()); // 사람**

< 소스 5 >

소스 5를 보게 되면 함수의 prototype 속성을 이용하여 getType() 리턴 값을 사람으로 수정합니다. 그리고 jisoo 객체를 이용하여 호출한 결과 사람이 나옵니다.

결론을 내리면, 프로토타입 객체는 새로운 객체가 생성되기 위한 원형이 되는 객체입니다. 같은 원형으로 생성된 객체가 공통으로 참조하는 공간입니다. 프로토타입 객체의 멤버를 읽는 경우에는 객체 또는 함수의 prototype 속성을 통해 접근할 수 있습니다. 하지만 추가, 수정, 삭제는 함수의 prototype 속성을 통해 접근해야 합니다.

**3. 프로토타입이란?**

JavaScript에서 기본 데이터 타입을 제외한 모든 것이 객체입니다. 객체가 만들어지기 위해서는 자신을 만드는 데 사용된 원형인 프로토타입 객체를 이용하여 객체를 만듭니다. 이때 만들어진 객체 안에 __proto__ (비표준) 속성이 자신을 만들어낸 원형을 의미하는 프로토타입 객체를 참조하는 숨겨진 링크가 있습니다. 이 숨겨진 링크를 프로토타입이라고 정의합니다.

![[untitled 5 3.jpg|untitled 5 3.jpg]]

< 그림 6 >

**123function Person(){} var joon = new Person();**

< 소스 6 >

위 그림 6 joon 객체의 멤버인 __proto__ (비표준) 속성이 프로토타입 객체를 가리키는 숨은 링크가 프로토타입이라고 합니다. 프로토타입을 크게 두 가지로 해석된다 했습니다. 함수의 멤버인 prototype 속성은 프로토타입 객체를 참조하는 속성입니다. 그리고 함수와 new 연산자가 만나 생성한 객체의 프로토타입 객체를 지정해주는 역할을 합니다. 객체 안의 __proto__(비표준) 속성은 자신을 만들어낸 원형인 프로토타입 객체를 참조하는 숨겨진 링크로써 프로토타입을 의미합니다.

JavaScript에서는 숨겨진 링크가 있어 프로토타입 객체 멤버에 접근할 수 있습니다. 그래서 이 프로토타입 링크를 사용자가 정의한 객체에 링크가 참조되도록 설정하면 코드의 재사용과 객체 지향적인 프로그래밍을 할 수 있습니다.

**4. 코드의 재사용**

코드의 재사용 하면 떠오르는 단어는 바로 상속입니다. 클래스라는 개념이 있는 Java에서는 중복된 코드를 상속받아 코드 재활용을 할 수 있습니다. 하지만 JavaScript에서는 클래스가 없는, 프로토타입 기반 언어입니다. 그래서 프로토타입을 이용하여 코드 재사용을 할 수 있습니다.

이 방법에도 크게 두 가지로 분류할 수 있습니다. classical 방식과 prototypal 방식이 있습니다. classical 방식은 new 연산자를 통해 생성한 객체를 사용하여 코드를 재사용 하는 방법입니다. 마치 Java에서 객체를 생성하는 방법과 유사하여 classical 방식이라고 합니다. prototypal 방식은 리터럴 또는 Object.create()를 이용하여 객체를 생성하고 확장해 가는 방식입니다. 두 가지 방법 중 JavaScript에서는 prototypal 방식을 더 선호합니다. 그 이유는 classical 방식보다 간결하게 구현할 수 있기 때문입니다. 밑의 예제 1 ~ 4번까지는 classical 방식의 코드 재사용 방법이고, 5번은 prototypal 방식인 Object.create()를 사용하여 코드의 재사용을 보여줍니다.

**(1) 기본 방법**

부모에 해당하는 함수를 이용하여 객체를 생성합니다. 자식에 해당하는 함수의 prototype 속성을 부모 함수를 이용하여 생성한 객체를 참조하는 방법입니다.

![[untitled 6]]

< 그림 7 >

**12345678910111213141516function Person(name) { this.name = name || "혁준"; } Person.prototype.getName = function(){ return this.name;}; function Korean(name){}Korean.prototype = new Person(); var kor1 = new Korean();console.log(kor1.getName()); // 혁준 var kor2 = new Korean("지수");console.log(kor2.getName()); // 혁준**

< 소스 7 >

위 소스 7을 보면 부모에 해당하는 함수는 Person입니다. 10라인에서 자식 함수인 Korean 함수 안의 prototype 속성을 부모 함수로 생성된 객체로 바꿨습니다. 이제 Korean 함수와 new 연산자를 이용하여 생성된 kor 객체의 __proto__속성이 부모 함수를 이용하여 생성된 객체를 참조합니다. 이 객체가 Korean 함수를 이용하여 생성된 모든 객체의 프로토타입 객체가 됩니다. kor1에는 name과 getName() 이라는 속성이 없지만, 부모에 해당하는 프로토타입객체에 name이 있습니다. 이 프로토타입객체의 부모에 getName()을 가지고 있어 kor1에서 사용할 수 있습니다. 이 방법에도 단점이 있습니다. 부모 객체의 속성과 부모 객체의 프로토타입 속성을 모두 물려받게 됩니다. 대부분의 경우 객체 자신의 속성은 특정 인스턴스에 한정되어 재사용할 수 없어 필요가 없습니다. 또한, 자식 객체를 생성할 때 인자를 넘겨도 부모 객체를 생성할 때 인자를 넘겨주지 못합니다. 그림 7 소스 하단 두 번째 줄에서 kor2 객체를 생성할 때 Korean 함수의 인자로 지수라고 주었습니다. 객체를 생성한 후 getName()을 호출하면 지수라고 출력될 거 같지만, 부모 생성자에 인자를 넘겨주지 않았기 때문에 name에는 default 값인 혁준이 들어있습니다. 객체를 생성할 때마다 부모의 함수를 호출할 수도 있습니다. 하지만 매우 비효율적입니다. 그래서 다음 방법은 이 방법의 문제점을 해결하는 방법을 알아보겠습니다.

**(2) 생성자 빌려 쓰기**

이 방법은 기본 방법의 문제점인 자식 함수에서 받은 인자를 부모 함수로 인자를 전달하지 못했던 부분을 해결합니다. 부모 함수의 this에 자식 객체를 바인딩하는 방식입니다.

![[untitled 7]]

< 그림 8 >

**1234567891011121314function Person(name) { this.name = name || "혁준";} Person.prototype.getName = function(){ return this.name;}; function Korean(name){ Person.apply(this, arguments);} var kor1 = new Korean("지수");console.log(kor1.name); // 지수**

< 소스 8 >

위 소스 8 10라인을 보면 Korean 함수 내부에서 apply 함수를 이용합니다. 부모객체인 Person 함수 영역의 this를 Korean 함수 안의 this로 바인딩합니다. 이것은 부모의 속성을 자식 함수 안에 모두 복사합니다. 객체를 생성하고, name을 출력합니다. 객체를 생성할 때 넘겨준 인자를 출력하는 것을 볼 수 있습니다. 기본 방법에서는 부모객체의 멤버를 참조를 통해 물려받았습니다. 하지만 생성자 빌려 쓰기는 부모객체 멤버를 복사하여 자신의 것으로 만들어 버린다는 차이점이 있습니다. 하지만 이 방법은 부모객체의 this로 된 멤버들만 물려받게 되는 단점이 있습니다. 그래서 부모객체의 프로토타입 객체의 멤버들을 물려받지 못합니다. 위 그림 8 그림을 보시면 kor1 객체에서 부모객체의 프로토타입 객체에 대한 링크가 없다는 것을 볼 수 있습니다.

**(3) 생성자 빌려 쓰고 프로토타입 지정해주기**

이 방법은 방법 1과 방법 2 문제점들을 보완하면서 Java에서 예상할 수 있는 동작 방식과 유사합니다.

![[untitled 8]]

< 그림 9 >

**1234567891011121314function Person(name) { this.name = name || "혁준"; } Person.prototype.getName = function(){ return this.name;}; function Korean(name){ Person.apply(this, arguments);}Korean.prototype = new Person(); var kor1 = new Korean("지수");console.log(kor1.getName()); // 지수**

< 소스 9 >

위 소스 9 9라인에서 부모 함수 this를 자식 함수 this로 바인딩합니다. 11라인에서 자식 함수 prototype 속성을 부모 함수를 사용하여 생성된 객체로 지정했습니다. 부모객체 속성에 대한 참조를 가지는 것이 아닌 복사본을 통해 내 것으로 만듭니다. 동시에 부모객체의 프로토타입 객체에 대한 링크도 참조됩니다. 부모객체의 프로토타입 객체 멤버도 사용할 수 있습니다. 그림 7과 비교했을 때 kor1 객체에 name 멤버가 없는 반면 그림 9에서는 name 멤버를 가지고 있는 것을 확인할 수 있습니다. 그림 8과 비교했을 때는 프로토타입 링크가 부모 함수로 생성한 객체에 대해 참조도 하고 있습니다. 그리고 부모 객체의 프로토타입 객체도 링크로 연결된 것을 볼 수 있습니다. 이 방법에도 문제점이 있습니다. 부모 생성자를 두 번 호출합니다. 생성자 빌려 쓰기 방법과 달리 getName()은 제대로 상속되었지만, name에 대해서는 kor1 객체와 부모 함수를 이용하여 생성한 객체에도 있는 것을 볼 수 있습니다.

**(4) 프로토타입공유**

이번 방법은 부모 생성자를 한 번도 호출하지 않으면서 프로토타입 객체를 공유하는 방법입니다.

![[untitled 9]]

< 그림 10 >

**123456789101112131415function Person(name) { this.name = name || "혁준";} Person.prototype.getName = function(){ return this.name;}; function Korean(name){ this.name = name;} Korean.prototype = Person.prototype; var kor1 = new Korean("지수");console.log(kor1.getName()); // 지수**

< 소스 10 >

위 소스 10 12라인에서 자식 함수의 prototype 속성을 부모 함수의 prototype 속성이 참조하는 객체로 설정했습니다. 자식 함수를 통해 생성된 객체는 부모 함수를 통해 생성된 객체를 거치지 않고 부모 함수의 프로토타입 객체를 부모로 지정하여 객체를 생성합니다. 부모 함수의 내용을 상속받지 못하므로 상속받으려는 부분을 부모 함수의 프로토타입 객체에 작성해야 사용자가 원하는 결과를 얻게 됩니다. 그림 9와 비교했을 때 중간에 부모 함수로 생성한 객체가 없고 부모 함수의 프로토타입 객체로 링크가 참조되는 것을 볼 수 있습니다.

**(5) prototypal한 방식의 재사용**

이 방법은 Object.create()를 사용하여 객체를 생성과 동시에 프로토타입객체를 지정합니다. 이 함수는 첫 번째 매개변수는 부모객체로 사용할 객체를 넘겨주고, 두 번째 매개변수는 선택적 매개변수로써 반환되는 자식객체의 속성에 추가되는 부분입니다. 이 함수를 사용함으로 써 객체 생성과 동시에 부모객체를 지정하여 코드의 재활용을 간단하게 구현할 수 있습니다.

**123456789101112131415var person = { type : "인간", getType : function(){ return this.type; }, getName : function(){ return this.name; }}; var joon = Object.create(person);joon.name = "혁준"; console.log(joon.getType()); // 인간console.log(joon.getName()); // 혁준**

< 소스 11 >

위 소스 1라인에서 부모 객체에 해당하는 person을 객체 리터럴 방식으로 생성했습니다. 그리고 11라인에서 자식 객체 joon은 Object.create() 함수를 이용하여 첫 번째 매개변수로 person을 넘겨받아 joon 객체를 생성하였습니다. 한 줄로 객체를 생성함과 동시에 부모객체의 속성도 모두 물려받았습니다. 위의 1 ~ 4번에 해당하는 classical 방식보다 간단하면서 여러 가지 상황을 생각할 필요도 없습니다. JavaScript에서는 new 연산자와 함수를 통해 생성한 객체를 사용하는 classical 방식보다 prototypal 방식을 더 선호합니다.

**5. 마치며**

지금까지 JavaScript 프로토타입에 대해 정리했습니다. 처음 프로토타입을 공부할 땐, 자바 OOP 관점에서 접근하여 혼란스러웠습니다. 하지만 함수의 내부구조부터 차근차근 접근하였더니 쉽게 이해할 수 있었습니다. 그리고 코드의 재사용 방식에 대해 공부하였던 것도 JavaScript 언어 자체를 이해하는 데 많은 도움이 되었습니다.  
이 글이 JavaScript를 처음 접하거나 프로토타입에 대해 공부하는 분들에게 많은 도움이 되었으면 합니다.  

**참조 도서 및 사이트**

- 황인균 저, 자바스크립트 객체지향 프로그래밍
- 스토얀 스테파노프 저, JavaScript Patterns
- 송형주 고원주 저, 인사이드 자바스크립트
- 블로그 – Javascript : 함수(function) 다시 보기 by 이 재 욱 [http://www.nextree.co.kr/p4150/](http://www.nextree.co.kr/p4150/)
- 웹문서 - [http://insanehong.kr/post/javascript-prototype/](http://insanehong.kr/post/javascript-prototype/)

Rating: 5.0/**5** (6 votes cast)

JavaScript : 프로토타입(prototype) 이해, 5.0 out of 5 based on 6 ratings

- [Facebook21](http://www.nextree.co.kr/p7323/?share=facebook&nb=1)
- [Twitter](http://www.nextree.co.kr/p7323/?share=twitter&nb=1)
- [Google](http://www.nextree.co.kr/p7323/?share=google-plus-1&nb=1)
- [Print](http://www.nextree.co.kr/p7323/#print)
- [Email](http://www.nextree.co.kr/p7323/?share=email&nb=1)

# 7 Responses to “ “JavaScript : 프로토타입(prototype) 이해”

1. **hanmomhanda**[  
    **2014/03/30 at 8:29 pm**  
    ](http://www.nextree.co.kr/p7323/\#comment-12817)**그림 설명이 너무 좋네요. 3번에서 나오는 숨겨진 링크를 ‘프로토타입’이라고 하는 것 보다 스펙에 있는대로 [[Prototype]]이라고 하면 더 명확할 것 같습니다.프로토타입은 그 자체가 어렵다기 보다는 우리말로 ‘프로토타입’이라고 쓰면서, 쓰는 사람에 따라 prototype 속성을 가리키기도 하고, 프로토타입 객체를 가리키기도 하고, [[Prototype]]을 가리키기도 하기 때문인 것 같습니다.**[**Reply**](http://www.nextree.co.kr/p7323/?replytocom=12817#respond) **권 혁준**[  
    **2014/04/01 at 11:50 am**  
    ](http://www.nextree.co.kr/p7323/\#comment-12860)**네 저도 프로토타입을 처음 접할 때 프로토타입 객체를 프로토타입이라고 이해하고 공부한 거 같습니다. 하지만 프로토타입 의미를 정확히 이해한다면 쉽게 접근할 수 있습니다. ECMAScript에서 [[Prototype]]정의하는 것을 알고 있지만, 프로토타입을 처음 접하시는 분들이 [[Prototype]]와 프로토타입, prototype 프로퍼티에 대해 혼란스러울까 봐 프로토타입이라고 정의했습니다. 글쓴이도 조금 더 생각해보고 어떤 것이 사람들에게 혼동을 안 주는지 생각해보고 수정하겠습니다. 좋은 의견 감사드립니다.**[**Reply**](http://www.nextree.co.kr/p7323/?replytocom=12860#respond)
2. **김상균**[  
    **2014/04/04 at 12:03 pm**  
    ](http://www.nextree.co.kr/p7323/\#comment-13018)**자바스크립트는 정말 재밋는 언어 이면서도 어려운 언어 인거 같습니다공부를 많이 했는데 또 까먹고 하네요 다시 처음 읽는다고 생각하고 읽었습니다.좋은 정보 감사합니다~**[**Reply**](http://www.nextree.co.kr/p7323/?replytocom=13018#respond) **권 혁준**[  
    **2014/04/04 at 1:49 pm**  
    ](http://www.nextree.co.kr/p7323/\#comment-13021)**감사합니다~!**[**Reply**](http://www.nextree.co.kr/p7323/?replytocom=13021#respond)
3. **말썽쩡**[  
    **2014/04/16 at 7:06 pm**  
    ](http://www.nextree.co.kr/p7323/\#comment-13504)**어려워요 잘 보고 갑니다 ㅠㅠ**[**Reply**](http://www.nextree.co.kr/p7323/?replytocom=13504#respond)
4. [**이재환**](http://jhlee8379.cafe24.com/)[  
    **2014/05/05 at 12:52 pm**  
    ](http://www.nextree.co.kr/p7323/\#comment-14986)**아 잘보고 갑니다~^^ 저도 인사이드 자바스크립트보고 어느정도 이해했는데 여기서도 잘 설명해놓았네요~ㅎㅎ**[**Reply**](http://www.nextree.co.kr/p7323/?replytocom=14986#respond)
5. **몽쉘통통**[  
    **2014/10/23 at 5:44 pm**  
    ](http://www.nextree.co.kr/p7323/\#comment-26406)**그림과 소스코드를 상세하게 설명해주셔서 이해가 잘 되네요감사합니다.**[**Reply**](http://www.nextree.co.kr/p7323/?replytocom=26406#respond)

# Leave a Reply

Your email address will not be published. Required fields are marked *

Name *

Email *

Website

TextVisual

p



You may use these HTML tags and attributes: `<a href="" title=""> <abbr title=""> <acronym title=""> <b> <blockquote cite=""> <cite> <code class="" title="" data-url=""> <del datetime=""> <em> <i> <q cite=""> <strike> <strong> <pre class="" title="" data-url=""> <span class="" title="" data-url="">`

![[untitled 10]]

## ^_^

- [일터 – 경험과 노하우](http://www.nextree.co.kr/category/knowhow/) (82)
- [쉼터 – 따뜻한 공감](http://www.nextree.co.kr/category/nextrian/) (19)
- [알림터 – 회사 소식](http://www.nextree.co.kr/category/notice/) (10)
- [로드맵 – SW 엔지니어](http://www.nextree.co.kr/category/roadmap/) (4)
- [배움터 – 열공](http://www.nextree.co.kr/category/study/) (45)

## ^_^

[ajax](http://www.nextree.co.kr/tag/ajax/)[AngularJs](http://www.nextree.co.kr/tag/angularjs/)[Axure RP](http://www.nextree.co.kr/tag/axure-rp/)[CSS](http://www.nextree.co.kr/tag/css/)[CXF](http://www.nextree.co.kr/tag/cxf/)[eclipse](http://www.nextree.co.kr/tag/eclipse/)[fit](http://www.nextree.co.kr/tag/fit/)[fitnesse](http://www.nextree.co.kr/tag/fitnesse/)[graph](http://www.nextree.co.kr/tag/graph/)[hadoop](http://www.nextree.co.kr/tag/hadoop/)[IT 운영](http://www.nextree.co.kr/tag/it-%ec%9a%b4%ec%98%81/)[java](http://www.nextree.co.kr/tag/java/)[JavaScript](http://www.nextree.co.kr/tag/javascript-2/)[jet](http://www.nextree.co.kr/tag/jet/)[jq-plot](http://www.nextree.co.kr/tag/jq-plot/)[jqplot](http://www.nextree.co.kr/tag/jqplot/)[jQuery](http://www.nextree.co.kr/tag/jquery/)[jquery graph](http://www.nextree.co.kr/tag/jquery-graph/)[jUnit](http://www.nextree.co.kr/tag/junit/)[LBS](http://www.nextree.co.kr/tag/lbs/)[mapreduce](http://www.nextree.co.kr/tag/mapreduce/)[maven](http://www.nextree.co.kr/tag/maven/)[nodejs](http://www.nextree.co.kr/tag/nodejs/)[oozie](http://www.nextree.co.kr/tag/oozie/)[RAP](http://www.nextree.co.kr/tag/rap/)[RCP](http://www.nextree.co.kr/tag/rcp/)[reflection](http://www.nextree.co.kr/tag/reflection/)[REST](http://www.nextree.co.kr/tag/rest/)[SOAP](http://www.nextree.co.kr/tag/soap/)[square model](http://www.nextree.co.kr/tag/square-model/)[test process](http://www.nextree.co.kr/tag/test-process/)[Type Object](http://www.nextree.co.kr/tag/type-object/)[Unit Test](http://www.nextree.co.kr/tag/unit-test/)[WebService](http://www.nextree.co.kr/tag/webservice/)[Web Service](http://www.nextree.co.kr/tag/web-service/)[XML](http://www.nextree.co.kr/tag/xml/)[로드맵](http://www.nextree.co.kr/tag/%eb%a1%9c%eb%93%9c%eb%a7%b5/)[릴리스](http://www.nextree.co.kr/tag/%eb%a6%b4%eb%a6%ac%ec%8a%a4/)[빅데이터](http://www.nextree.co.kr/tag/%eb%b9%85%eb%8d%b0%ec%9d%b4%ed%84%b0/)[서비스접근제어](http://www.nextree.co.kr/tag/%ec%84%9c%eb%b9%84%ec%8a%a4%ec%a0%91%ea%b7%bc%ec%a0%9c%ec%96%b4/)[스토리보드](http://www.nextree.co.kr/tag/%ec%8a%a4%ed%86%a0%eb%a6%ac%eb%b3%b4%eb%93%9c/)[자료구조](http://www.nextree.co.kr/tag/%ec%9e%90%eb%a3%8c%ea%b5%ac%ec%a1%b0/)[트래킹](http://www.nextree.co.kr/tag/%ed%8a%b8%eb%9e%98%ed%82%b9/)[패턴](http://www.nextree.co.kr/tag/%ed%8c%a8%ed%84%b4/)[프로젝트이야기](http://www.nextree.co.kr/tag/%ed%94%84%eb%a1%9c%ec%a0%9d%ed%8a%b8%ec%9d%b4%ec%95%bc%ea%b8%b0/)

## ^_^

![[untitled 11]]

![[bitkookmin_bn1.gif]]

## ^_^

- 넥스트리소프트(주)  
- 넥스트리컨설팅(주)  
- 전화번호: 02 - 6344 - 5050  
- 이 메 일: tsong@nextree.co.kr  
- 우편번호:153-792  
- 서울 금천구 가산디지털1로 186  
- 제이플라츠 702호  
- 가산디지털단지역 6,7번출구  

## ^_^

Powered by [WordPress](http://www.wordpress.com/) | Designed by [Elegant Themes](http://www.elegantthemes.com/)

![[www.google.co.kr.gif]]