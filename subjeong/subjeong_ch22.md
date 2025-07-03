[모던 자바스크립트 Deep Dive]
[22장] this

---

### 1. this 키워드

- 객체 리터럴 방식의 객체

	- 메서드 내부에서 자신이 속한 객체를 가리키는 식별자를 재귀적으로 참조 가능함
	
		- const circle = { radius: 5, getR() { return 2*circle.radius; } };
		
- 생성자 함수 방식의 객체

	- 생성자 함수 정의 후 new 연산자와 함께 생성자 함수 호출해야 함
	
		- function Circle(radius) { ???.radius = radius; } 
		
- this

	- 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수
	
		- 어디에서든 참조 가능, 단, strict mode가 적용된 일반 함수 내부에서는 undefined가 바인딩됨 (객체 생성 X이므로)
	
	- this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조 가능함
	
	- this가 가리키는 값, 즉 this 바인딩은 함수 호출 방식에 의해 동적으로 결정됨
	
- this 바인딩

	- this(키워드로 분류되지만 식별자 역할)와 this가 가리킬 객체를 바인딩하는 것

		- 바인딩 : 식별자와 값을 연결하는 과정

	- 객체 리터럴 방식의 객체 : 메서드를 호출한 객체를 가리키는 this
	
		- const circle = { radius: 5, getR() { return 2*this.radius; } };
		
	- 생성자 함수 방식의 객체 : 생성자 함수가 생성할 인스턴스를 가리키는 this
	
		- function Circle(radius) { this.radius = radius; } 

---

### 2. 함수 호출 방식과 this 바인딩

- 렉시컬 스코프와 this 바인딩의 결정 시기

	- 렉시컬 스코프 : 함수 정의가 평가되어 함수 객체가 생성되는 시점에 상위 스코프를 결정함

	- this 바인딩 : 함수 호출 시점에 결정됨
	
- 함수의 다양한 호출 방식

	- 일반 함수 호출
	
		- foo();
	
	- 메서드 호출
	
		- const obj = { foo }; obj.foo();
	
	- 생성자 함수 호출
	
		- new foo();
	
	- Funtion.prototype.apply/call/bind 메서드에 의한 간접 호출
	
		- const bar = { name: 'bar' }; foo.call(bar); foo.apply(bar); foo.bind(bar)();

#### 일반 함수 호출

- 일반 함수 호출

	- 기본적으로 this에 전역 객체가 바인딩됨
	
		- 일반 함수로 호출된 모든 함수(중첩 함수, 콜백 함수 등) 내부의 this에는 전역 객체가 바인딩됨
	
	- 단, 객체를 생성하지 않는 일반 함수에서는 의미 없음
	
		- strict mode가 적용된 일반 함수 내부의 this에는 undefined가 바인딩됨

- setTimeout 함수 
	
	- 두 번째 인수로 전달한 시간(ms)만큼 대기한 다음, 첫 번째 인수로 전달한 콜백 함수를 호출

- 메서드 내부의 중첩 함수, 콜백 함수의 this 바인딩 == 메서드의 this 바인딩 만드는 방법

	- const obj = { value: 100, foo() { const that = this; setTimeout(function () { console.log(that.value); }, 100); } }; obj.foo(); -> 100

- 화살표 함수

	- const obj = { value: 100, foo() { setTimeout(() => console.log(this.value), 100); } }; obj.foo();

#### 메서드 호출

- 메서드 호출

	- 메서드를 호출할 때 메서드 이름 앞의 마침표(.) 연산자 앞에 기술한 객체가 바인딩됨
	
		- 메서드 내부의 this는 메서드를 호출한 객체에 바인딩됨, 프로토타입 메서드도 마찬가지임
		
		- const a = { name: 'a', getName() { return this.name; } } }; const b = { name: 'b' }; b.getName = a.getName; b.getName() -> b
		
		- const getName = a.getName; getName() -> '' // 일반 함수 this.name == window.name
		
#### 생성자 함수 호출

- 생성자 함수 호출

	- 생성자 함수 내부의 this에는 생성자 함수가 생성할 인스턴스가 바인딩됨
	
		- function Circle(radius) { this.radius = radius; this.getR = function () { return this.radius; }; }

#### Function.prototype.apply/call/bind 메서드에 의한 간접 호출

- Function.prototype.apply/call

	- 주어진 this 바인딩과 인수 리스트 배열 또는 유사 배열 객체(인수 전달 방식 차이 O)을 사용해 함수를 호출함
	
	- argumants 객체는 배열이 아니므로 배열 메서드 대신 apply/call 메서드로 slice 가능함
	
- Function.prototype.bind

	- 함수를 호출하지 않음, 다만 첫 번째 인수로 전달한 값으로 this 바인딩이 교체된 함수를 새롭게 생성해 반환함
	
		- 메서드의 this와 메서드 내부 중첩 함수/콜백 함수의 this가 불일치하는 문제를 해결 가능함

---
