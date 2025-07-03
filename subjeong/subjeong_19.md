[모던 자바스크립트 Deep Dive]
[19장] 프로토타입

---

- 클래스

	- ES6에서 도입, 함수이며 기존 프로토타입 기반 패턴의 새로운 객체 생성 매커니즘
	
	- 클래스, 생성자 함수는 모두 프로토타입 기반의 인스턴스를 생성하지만 정확히 동일하게 동작하지는 않음 (클래스 > 생성자)

- 자바스크립트는 객체 기반의 프로그래밍 언어로, 거의 모든 것이 객체임

---

### 1. 객체지향 프로그래밍

- 명령형 프로그래밍

	- 프로그램을 명령어 또는 함수의 목록으로 보는 전통적인 프로그래밍

- 객체 지향 프로그래밍

	- 명령형 프로그래밍의 절차지향적 관점에서 벗어나 여러 개의 독립적 단위인 객체의 집합으로 프로그램을 표현하려는 프로그래밍 패러다임

	- 실체(상태, 속성)를 인식 + 프로그래밍(동작) -> 필요 속성만 간추려 추상화


- 객체

	- 상태 데이터와 동작을 하나의 논리적인 단위로 묶은 복합적인 자료구조

---

### 2. 상속과 프로토타입

- 상속

	- 객체지향 프로그래밍의 핵심 개념
	
	- 어떤 객체의 프로퍼티 또는 메서드를 다른 객체가 상속 받아 그대로 사용 가능한 것
	
- 자바스크립트는 프로토타입을 기반으로 상속을 구현하여 불필요한 중복을 제거함

	- 생성자 함수로 인스턴스 생성 시 부모 객체(프로토타입)로부터 메서드를 상속 받아 하나의 메서드를 공유함(코드 재활용)
	
	- Circle.prototype.getArea = function () { return this.radius; };
	
	- circle1.getArea === circle2.getArea -> true

---

### 3. 프로토타입 객체

- 프로토타입 객체(프로토타입)

	- 객체지향 프로그래밍의 근간을 이루는 객체 간 상속을 구현하기 위해 사용
	
	- 어떤 객체의 상위(부모) 객체의 역할을 하는 객체로서, 다른 객체에 공유 프로퍼티(메서드 포함)을 제공함
	
		- 프로토타입을 상속 받은 하위(자식) 객체는 상위 객체의 프로퍼티를 자유롭게 사용 가능함

- 모든 객체는 [[Prototype]]이라는 내부 슬롯을 가지며, 이 값은 프로토타입의 참조(또는 null)

	- 객체 생성 시 객체 생성 방식에 따라 프로토타입이 결정, [[Prototype]]에 저장됨

- 모든 객체는 하나의 프로토타입을 가지며, 이는 생성자 함수와 연결됨

	- __proto__ 접근자 프로퍼티를 통해 [[Prototype]] 내부 슬롯이 가리키는 프로토타입에 간접 접근 가능함
	
	- 프로토타입은 자신의 constructor 프로퍼티를 통해 생성자 함수에 접근 가능함
	
	- 생성자 함수는 자신의 prototype 프로퍼티를 통해 프로토타입에 접근 가능함

#### **proto** 접근자 프로퍼티

- Object.prototype

	- 프로토타입 체인의 최상위 객체, 모든 객체에 상속됨

		- 모든 객체는 프로토타입의 계층 구조인 프로토타입 체인에 묶여 있음
	
	- 자바스크립트 엔진은 객체의 프로퍼티(+메서드)에 접근 시, 해당 객체에 접근하려는 프로퍼티가 없다면 __proto__ 접근자 프로퍼티가 가리키는 참조를 따라 부모 프로토타입의 프로퍼티를 순차적으로 검색함
	
- __proto__ 접근자 프로퍼티

	- 자체적으로는 값([[Value]] 프로퍼티 어트리뷰트)을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수
	
	- [[Get]], [[Set]] 프로퍼티 어트리뷰트로 구성된 프로퍼티

- __proto__는 접근자 프로퍼티임

	- 모든 객체가 자신의 프로토타입([[Prototype]] 내부 슬롯)에 간접 접근 가능하도록 해 줌
	
		- __proto__로 프로토타입에 접근 시 내부적으로 getter [[Get]]이 호출됨
	
		- __proto__로 새로운 프로토타입을 할당 시 setter [[Set]]이 호출

- __proto__ 접근자 프로퍼티는 상속을 통해 사용됨

	- __proto__ 접근자 프로퍼티는 객체 직접 소유 프로퍼티가 아니라 Object.prototype의 프로퍼티임
	
		- 모든 객체는 상속을 통해 Object.prototype.__proto__ 접근자 프로퍼티를 사용 가능함
		
		- {}.__proto__ === Object.prototype -> true

- __proto__ 접근자 프로퍼티를 통해 프로토타입에 접근하는 이유

	- 상호 참조(순환 참조)에 의해 프로토타입 체인이 생성되는 것을 방지하기 위함
	
		- 프로토타입 체인은 단방향 링크드 리스트로 구현되어야 함

- __proto__ 접근자 프로퍼티를 코드 내에서 직접 사용하는 것은 비권장함

	- ES6에서 표준이지만, 모든 객체가 __proto__ 접근자 프로퍼티를 사용할 수 없기 때문임
	
		- obj는 프로토타입 체인의 종점이므로, Object.__proto__를 상속 받을 수 없음
	
			- const obj = Object.create(null); obj.__proto__ (X) Object.getPrototypeOf(obj) (O)
	
	- 프로토타입의 참조 취득을 위해 Object.getPrototypeOf 메서드를 사용
	
		- Object.getPrototypeOf(obj); == obj.__proto__;
	
	- 프로토타입의 교체를 위해 Object.setPrototypeOf 메서드를 사용
	
		- Object.setPrototypeOf(obj, parent); == obj.__proto__ = parent;

#### 함수 객체의 prototype 프로퍼티

- 함수 객체의 prototype 프로퍼티

	- 함수 객체만이 소유
	
	- 생성자 함수가 생성할 인스턴스의 프로토타입을 가리킴
	
		- 생성자 함수로서 호출 불가능한 non-constructor는 prototype 프로퍼티를 소유 X, 프로토타입 생성 X
		
			- 화살표 함수 ex. const Person = name => { this.name = name; };
			
			- ES6 메서드 축약 표현 ex. const obj = { foo() {} };
			
			- 일반 함수(함수 선언문, 함수 표현식)

- __proto__ 접근자 프로퍼티 vs prototype 프로퍼티

	- 둘은 동일한 프로토타입을 가리키지만, 주체가 다름
	
	- __proto__ 접근자 프로퍼티
	
		- 소유 : 모든 객체
		
		- 값 : 프로토타입의 참조
		
		- 사용 주체 : 모든 객체
		
		- 사용 목적 : 객체가 자신의 프로토타입에 접근 또는 교체하기 위해 사용
		
	- prototype 프로퍼티
	
		- 소유 : constructor
		
		- 값 : 프로토타입의 참조
		
		- 사용 주체 : 생성자 함수
		
		- 사용 목적 : 생성자 함수가 자신이 생성할 객체(인스턴스)의 프로토타입을 할당하기 위해 사용

#### 프로토타입의 constructor 프로퍼티와 생성자 함수

- 모든 프로토타입은 constructor 프로퍼티를 가짐

	- constructor 프로퍼티는 prototype 프로퍼티로 자신을 참조하는 생성자 함수 생성 시 가리킴

- new 생성자로 생성된 객체는 프로토타입의 constructor 프로퍼티를 상속 받아 사용 가능함

	- function Person(...) {} const me = new Person(...); (me.constructor === Person); -> true

---

### 4. 리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입

- 객체 생성 방식

	- new 연산자와 함께 생성자 함수에 의해 생성된 인스턴스는 프로토타입의 constructor 프로퍼티에 의해 생성자 함수와 연결됨
	
		- const add = new Function(...); add.constructor === Function -> true
	
	- 리터럴 표기법에 의해 생성된 인스턴스는 프로토타입의 constructor 프로퍼티가 가리키는 생성자 함수가 반드시 객체를 생성했다고 단정 지을 수 없음
	
		- const obj = {}; obj.constructor === Object -> true
		
- 추상 연산

	- ECMAScript 사양에서 내부 동작의 구현 알고리즘을 표현한 것, 의사 코드
	
- 리터럴 표기법에 의한 생성된 객체 예제

	- 1. new.target이 undefind나 Object가 아닌 경우
	
		- 인스턴스 -> Foo.prototype -> Object.prototype 순으로 프로토타입 체인이 생성됨
		
		- class Foo extends Object {} new Foo(); -> Foo {}
		
	- 2. Object 생성자 함수에 의한 객체 생성
	
		- 인수가 전달되지 않거나 undefind/null을 전달할 때 추상 연산 OrdinaryObjectCreate를 호출해 빈 객체를 생성함
		
		- let obj = new Object(); obj -> {}
		
	- 3. 인수가 전달된 경우에는 인수를 객체로 변환함
	
		- obj = new Object(123); obj -> Number {123}
		
		- obj = new Object('123'); obj -> String {"123"}

- Object 생성자 함수 호출과 객체 리터럴의 평가

	- 둘은 추상 연산 OrdinaryObjectCreate를 호출해 빈 객체를 생성하지만, 세부 내용이 다름
	
	- 객체 리터럴에 의해 생성된 객체는 Object 생성자 함수가 생성한 객체가 아님
	
- 리터럴 표기법에 의한 생성된 객체의 생성자 함수와 프로토타입

	- 프로토타입과 생성자 함수는 단독으로 존재 불가능하고 언제나 쌍으로 존재함

		- 상속을 위해 프로토타입이 필요하므로, 가상적인 생성자 함수를 가지며 프로토타입이 함께 생성되고 prototype constructor 프로퍼티에 의해 연결됨
		
	- 리터럴 표기법 : 생성자 함수 : 프로토타입
	
		- 객체 리터럴 : Object : Object.prototype
		
		- 함수 리터럴 : Function : Function.prototype
	
		- 배열 리터럴 : Array : Array.prototype
		
		- 정규 표현식 리터럴 : RegExp : RegExp.prototype
	
---

### 5. 프로토타입의 생성 시점

- 모든 객체는 생성자 함수와 연결돼 있음

- Object.create 메서드와 클래스에 의한 객체 생성

	- 이 객체도 생성자 함수와 연결되어 있음

- 프로토타입의 생성 시점

	- 프로토타입은 생성자 함수 생성 시점에 더불어 생성됨 (반드시 쌍)
	
- 프로토타입의 구분

	- 사용자 정의 생성자 함수
	
	- 빌트인 생성자 함수

#### 사용자 정의 생성자 함수와 프로토타입 생성 시점

- 생성자 함수로서 호출 가능한 함수(constructor)는 함수 정의 평가 후 함수 객체 생성 시점에 프로토타입도 더불어 생성됨

	- new 연산자 + 내부 메서드 [[Construct]]를 갖는 함수 객체, 즉 일반 함수(함수 선언문, 함수 표현식)로 정의한 함수 객체 -> 생성자 함수로 호출 O
	
- 사용자 정의 생성자 함수의 프로토타입 생성 시점

	- 자신이 평가되어 함수 객체로 생성되는 시점(런타임 이전)에 프로토타입도 더불어 생성됨
	
		- 이후 자신의 생성자 함수의 prototype 프로퍼티에 바인딩됨 
	
	- 생성된 프로토타입의 프로토타입은 언제나 Object.prototype임

#### 빌트인 생성자 함수와 프로토타입 생성 시점

- 빌트인 생성자 함수의 프로토타입 생성 시점

	- 빌트인 생성자 함수가 생성되는 시점(전역 객체 생성 시점)에 프로토타입이 생성됨
	
		- 이후 빌트인 생성자 함수의 prototype 프로퍼티에 바인딩됨

- 전역 객체

	- 코드 실행 이전 단계에 자바스크립트 엔진에 의해 생성되는 특수한 객체
	
	- CSR(브라우저)에서는 window 객체, SSR(Node.JS)에서는 global 객체
	
		- window.Object === Object -> true
		
	- 표준 빌트인 객체(Object, String, Number, Function, Array...)들과 환경에 따른 호스트 객체(Client Web API 또는 Node.JS의 호스트 API), var 키워드로 선언한 전역 변수, 전역 함수를 프로퍼티로 가짐
	
		- Math, Reflect, JSON을 제외한 표준 빌트인 객체는 모두 생성자 함수임

- 객체 생성 이전에 생성자 함수, 프로토타입은 이미 객체화되어 존재함

	- 이후 생성자 함수/리터럴 표기법으로 객체 생성 시 프로토타입은 생성된 객체의 [[Prototype]] 내부 슬롯에 할당됨(객체가 프로토타입을 상속 받음)

---

### 6. 객체 생성 방식과 프로토타입의 결정

- 객체 생성 방법

	- 객체 리터럴, Object 생성자 함수, 생성자 함수, Object.create 메서드, 클래스(ES6)
	
		- 세부 차이는 있으나, 모두 프로토타입이 추상 연산 OrdinaryObjectCreate에 전달되는 인수에 의해 결정됨
		
			- 인수는 객체가 생성되는 시점에 객체 생성 방식에 의해 결정됨
		
- 추상 연산 OrdinaryObjectCreate

	- 추상 연산 과정
	
		- 필수로 자신이 생성할 객체의 프로토타입을 인수로 전달 받음, 추가할 프로퍼티 목록을 옵션으로 전달함
	
		- 빈 객체 생성 후, 객체에 추가할 프로퍼티 목록이 인수로 전달된 경우 프로퍼티를 객체에 추가함
	
		- 인수로 전달 받은 프로토타입을 자신이 생성한 객체의 [[Prototype]] 내부 슬롯에 할당, 생성한 객체를 반환함

- 객체 리터럴과 Object 생성자 함수에 의한 객체 생성 방식의 차이

	- 프로퍼티를 추가하는 방식의 차이
	
		- 객체 리터럴 방식은 객체 리터럴 내부에 프로퍼티를 추가함
		
		- Object 생성자 함수 방식은 일단 빈 객체를 생성한 이후 프로퍼티를 추가해야 함
	
#### 객체 리터럴에 의해 생성된 객체의 프로토타입

- 객체 리터럴에 의해 생성된 객체의 프로토타입은 Object.prototype임

	- 자바스크립트 엔진은 객체 리터럴 평가해 객체 생성 시 추상 연산 OrdinaryObjectCreate를 호출, 추상 연산 OrdinaryObjectCreate에 Object.prototype 프로토타입이 전달됨
	
	- Object 생성자 함수, Object.prototype, 생성된 객체 사이가 연결됨 
	
		- const obj = { x: 1 }; obj.constructor === Object, obj.hasOwnProperty('x') -> true
	
#### Object 생성자 함수에 의해 생성된 객체의 프로토타입

- Object 생성자 함수에 의해 생성된 객체의 프로토타입은 Object.prototype임
	
	- 객체 리터럴과 같이 추상 연산 OrdinaryObjectCreate를 호출, 추상 연산 OrdinaryObjectCreate에 Object.prototype 프로토타입이 전달됨
	
	- Object 생성자 함수를 인수 없이 호출하면 빈 객체가 생성됨
	
	- Object 생성자 함수, Object.prototype, 생성된 객체 사이가 연결됨 
	
		- const obj = new Object(); obj.x = 1; obj.constructor === Object, obj.hasOwnProperty('x') -> true

#### 생성자 함수에 의해 생성된 객체의 프로토타입

- 생성자 함수에 의해 생성된 객체의 프로토타입은 생성자 함수의 prototype에 바인딩되어 있는 객체임

	- 객체 리터럴과 같이 추상 연산 OrdinaryObjectCreate를 호출, 추상 연산 OrdinaryObjectCreate에 생성자 함수의 prototype에 바인딩되어 있는 객체가 전달됨

	- 생성자 함수, 생성자 함수의 prototype에 바인딩되어 있는 객체, 생성된 객체 사이가 연결됨 

		- function Person(...) {} const me = new Person(...);
	
	- 프로토타입은 일반 객체처럼 프로퍼티 추가/삭제가 가능하며 프로토타입 체인에 즉각 반영됨
	
		- 해당 생성자 함수를 통해 생성된 모든 객체는 프로토타입에 추가된 해당 메서드를 상속 받아 자신의 메서드처럼 사용 가능함
		
		- Person.prototype.say = function () { ... };
	
---

