[모던 자바스크립트 Deep Dive]
[17장] 생성자 함수에 의한 객체 생성

---

- 객체 생성 방식

	- 객체 리터럴 (가장 간단)
	
	- 생성자 함수 (Object, String, Number, Boolean, Function, Array, Date, RegExp, Promise 등의 빌트인 생성자 함수)
	
---

### 1. Object 생성자 함수

- Object 생성자 함수

	- new 연산자 + Object 생성자 함수를 호출 시 빈 객체를 생성하여 반환
	
	- 이후 프로퍼티 or 메서드를 추가해 객체 완성 가능함
	
	- const person = new Object(); person.name = 'Lee'; person.say = function () { this.name = "say"; };

- 생성자 함수

	- new 연산자와 함께 호출해 객체(인스턴스)를 생성하는 함수
	
- 인스턴스

	- 생성자 함수에 의해 생성된 객체

---

### 2. 생성자 함수

#### 객체 리터럴에 의한 객체 생성 방식의 문제점

- 객체 리터럴 객체 생성의 장점

	- 직관적, 간편함
	
- 객체 리터럴 객체 생성의 단점

	- 단 하나의 객체만 생성함 (비효율적)
	
		- 동일한 프로퍼티를 갖는 객체를 여러 개 생성해야 하는 경우 매번 같은 프로퍼티를 기술해야 함
		
	- const circle = { radius: 5, getDiameter() {} };

#### 생성자 함수에 의한 객체 생성 방식의 장점

- 생성자 함수 객체 생성의 장점
	
	- 프로퍼티 구조가 동일한 객체 여러 개를 간편하게 생성 가능함
	
		- 객체(인스턴스)를 생성하기 위한 템플릿(클래스)처럼 활용
		
		- function Circle(radius) { this.radius = radius; this.getDiameter = function () {}; };
		
		- const circle = Circle(5);

- this

	- 객체 자신의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수
	
	- this가 가리키는 값(this 바인딩)은 함수 호출 방식에 따라 동적으로 결정됨
	
- 함수 호출 방식 : this가 가리키는 값(this 바인딩)

	- 일반 함수로서 호출 : 전역 객체
	
		- function foo() { console.log(this); } foo();
	
	- 메서드로서 호출 : 메서드를 호출한 객체(마침표 앞의 객체)
	
		- const obj = { foo }; obj.foo();
	
	- 생성자 함수로서 호출 : 생성자 함수가 (미래어) 생성할 인스턴스
	
		- const inst = new foo();

- 일반 함수와 동일한 방법으로 생성자 함수를 정의

- new 연산자와 함께 호출해야 생성자 함수로 동작함

	- const circle = Circle(15); -> X
	
	- const circle = new Circle(15); -> O
	
#### 생성자 함수의 인스턴스 생성 과정

- 생성자 함수의 역할

	- 템플릿(클래스)로서 동작해 인스턴스를 생성
	
	- 생성된 인스턴스를 초기화(인스턴스 프로퍼티 추가 및 초기값 할당)

- 바인딩

	- 식별자(변수 이름)와 값(메모리 공간의 주소)을 연결(바인딩)하는 과정
	
	- this 바인딩은 this와 this가 가리킬 객체를 바인딩하는 것

- 생성자 함수의 인스턴스 생성 과정

	- 1. 인스턴스 생성과 this 바인딩

		- 인스턴스 생성 및 반환 코드는 없지만, new 연산자와 함께 생성자 함수를 호출하면 자바스크립트 엔진이 암묵적으로 객체를 생성해 this에 바인딩함
	
	- 2. 인스턴스 초기화
	
		- 개발자가 처리함
	
	- 3. 인스턴스 반환
	
		- 완성된 인스턴스가 바인딩된 this를 암묵적으로 반환함
		
		- 생성자 함수 내부에서 return 문을 생략할 것
		
			- 다른 객체를 명시적 반환 시, this가 아닌 명시한 객체가 반환됨
		
			- 다른 원시 값을 명시적 반환 시, 무시되고 암묵적으로 this가 반환됨

#### 내부 메서드 [[Call]]과 [[Construct]]

- 함수와 객체의 공통점

	- 함수는 객체이므로 일반 객체와 동일하게 동작

	- 일반 객체의 내부 슬롯(프로퍼티), 내부 메서드 소유 가능
	
- 함수와 객체의 차이점

	- 함수는 일반 객체와 다르게 호출할 수 있음
	
	- 일반 객체의 내부 슬롯, 내부 메서드 + 함수 객체의 내부 슬롯([[Environment]], [[FormalParameters]]), 내부 메서드([[Call]], [[Construct]])
	
- [[Call]], [[Construct]]

	- 함수가 일반 함수로서 호출 시 함수 객체의 내부 메서드 [[Call]]이 호출됨
	
	- new 연산자와 함께 생성자 함수로서 호출 시 내부 메서드 [[Construct]]가 호출됨
	
- callable

	- 내부 메서드 [[Call]]을 갖는 함수 객체
	
	- 호출 가능한 함수
	
- constructor

	- 내부 메서드 [[Construct]]를 갖는 함수 객체
	
	- 생성자 함수로서 호출 가능한 함수
	
- non-constructor

	- 내부 메서드 [[Construct]]를 갖지 않는 함수 객체
	
	- 객체를 생성자 함수로서 호출할 수 없는 함수

- 모든 함수는 호출할 수 있지만(callable) 모든 함수 객체를 생성자 함수로서 호출할 수 있는 것은 아님(constructor, non-constructor)

#### constructor와 non-contructor의 구분

- 함수 정의 방식으로 구분함

- construcrot

	- 함수 선언문, 함수 표현식, 클래스(클래스도 함수)
	
	- function foo() {}
	
	- const bar = function () {};
	
	- const baz = { x: function () {} };
	
	- new foo(); new bar(); new bar.x();
	
- non-constructor

	- 메서드(ES6 메서드 축약 표현), 화살표 함수

	- const arrow = () => {};

	- const obj = { x() {} };
	
	- new arrow(); new obj.x(); -> TypeError

- 모든 함수 객체는 [[Call]]이 구현돼 있음

	- function foo() {} foo(); -> Success
	
- non-constructor인 함수 객체는 내부 메서드 [[Construct]]를 갖지 않음 

	- function foo() {} new foo(); -> Error

#### new 연산자

- new 연산자

	- new 연산자와 함께 함수 호출 시 생성자 함수로 동작
	
		 - 함수 객체의 내부 메서드 [[Call]]이 아닌 [[Construct]]가 호출됨
		 
		 - new 연산자는 non-constructor 함수가 아닌 constructor 함수와 함께 호출돼야 함
		 
		 - new + 생성자 함수로 정의하지 않은 일반 함수 -> 객체 반환 { x } 이 아니면 반환문 무시, 빈 객체 생성돼 반환 {}

	- new 연산자 없이 생성자 함수 호출 시 일반 함수로 동작
	
		- 함수 객체의 내부 메서드 [[Construct]]가 아닌 [[Call]]이 호출됨
		
		- 일반 함수로 호출 시 함수 내부의 this는 전역 객체 window를 가리킴, 함수 내부 프로퍼티 및 메서드는 전역 객체의 것이 됨
		
		- new 없는 생성자 함수 -> undefined로 반환, circle.getDiameter() 접근 불가능

#### new.target

- new.target

	- new 연산자 없이 생성자 함수가 호출되는 걸 방지하기 위해 파스칼 컨벤션 외 ES6에서 new.target 지원
	
	- this와 유사하게 constructor인 모든 함수 내부에서 암묵적인 지역 변수와 같이 사용, 메타 프로퍼티
	
	- new 연산자 사용 여부 확인 가능
	
		- new 연산자와 함께 생성자 함수로서 호출 시 함수 내부의 new.target은 함수 자신을 가리킴
		
		- new 연산자 없이 일반 함수로서 호출 시 함수 내부의 new.target은 undefined임

	- new 연산자 없어도 new 연산자와 함께 재귀 호출을 통해 생성자 함수로서 호출 가능
	
		- function Circle(radius) { if (!new.target) { return new Circle(radius); } this.radius = ... }
		
- 스코프 세이프 생성자 패턴 (new.target 대타)

	- function Circle(radius) { if (!(this instanceof Circle)) { return new Circle(radius); } this.radius = ... }
	
- new 연산자와 함께 생성자 함수에 의해 생성된 객체(인스턴스)는 프로토타입에 의해 생성자 함수와 연결됨

- 대부분의 빌트인 생성자 함수는 new 연산자와 함께 호출됐는지 확인 후 적절한 값 반환함

	- new 연산자 O/X이 동일하게 동작
	
		- Object( {} ), Function ( f anonymous(x) { return x ** x } )
	
	- new 연산자 O 시 객체 생성해 반환, X 시 각각 문자열, 숫자, 불리언 반환
	
		- String, Number, Boolean
		
---
