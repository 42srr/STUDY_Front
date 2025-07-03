[모던 자바스크립트 Deep Dive]
[18장] 함수와 일급 객체

---

### 1. 일급 객체

- 일급 객체의 조건

	- 무명의 리터럴로 생성 가능함 (런타임에 생성 가능)
	
	- 변수나 자료 구조(객체, 배열 등)에 저장 가능함
	
	- 함수의 매개변수에 전달 가능함
	
	- 함수의 반환값으로 사용 가능함
	
	- ex. 자바스크립트의 함수는 일급 객체임
	
		- const increase - function (num) { return ++num; }
		
		- const auxs = { increase, decrease };
		
		- function makeCounter(aux) { return function () { return "1"; }
		
		- const increaser = makeCounter(auxs.increase); console.log(increaser());

---

### 2. 함수 객체의 프로퍼티

- 함수는 객체이므로 프로퍼티를 가질 수 있음

	- function square(number) { return number * number; } console.dir(square);
	
- 함수 객체 고유의 데이터 프로퍼티

	- arguments, caller, length, name, prototype
	
- Object.prototype 객체의 프로퍼티를 상속 받은 접근자 프로퍼티

	- __proto__
	
- Object.prototype 객체의 프로퍼티는 모든 객체가 상속 받아 사용 가능함

	- 즉, __proto__ 접근자 프로퍼티는 모든 객체가 사용 가능함

#### arguments 프로퍼티

- arguments 객체

	- 함수 객체의 arguments 프로퍼티 값
	
		- 함수 호출 시 전달된 인수들의 정보를 담고 있는 순회 가능한 유사 배열 객체
	
		- 함수 내부에서 지역 변수처럼 사용됨 (함수 외부 참조 불가능)
	
	- 가변 인자 함수 구현 시 유용함
	
		- 함수 호출 시 모든 인수는 암묵적으로 arguments 객체의 프로퍼티로 보관됨 (매개변수 미만/초과 에러 X)

- arguments 프로퍼티

	- ES3부터 표준에서 폐지되어 함수 내부에서 지역 변수와 같은 arguments 객체를 참조해야 함
	
	- 함수 정의 시 선언 매개변수는 함수 몸체 내부 변수와 동일하게 취급됨
	
		- 함수 호출 시 함수 몸체 내에서 암묵적 매개변수 선언, undefined로 초기화 후 인수 할당됨
		
- arguments 객체의 구성
	
	- 인수를 프로퍼티 값으로 소유하며, 프로퍼티 키는 인수의 순서를 나타냄

	- callee 프로퍼티
	
		- 호출되어 arguments 객체 생성한 함수(함수 자신)을 가리킴
		
	- length 프로퍼티
	
		- 인수의 개수를 가리킴
		
- arguments 객체의 Symbol(Symbol.iterator) 프로퍼티

	- arguments 객체를 순회 가능한 자료구조인 이터러블로 만들기 위한 프로퍼티
	
	- function multi(x, y) { const iter = arguments[Symbol.iterator](); console.log(iter.next()); return x * y; }

- 유사 배열 객체

	- length 프로퍼티를 가진 객체로 for문으로 순회할 수 있는 객체

- 유사 배열 객체와 이터러블

	- arguments 객체는 배열 형태로 인자 정보를 담고 있지만 실제 배열이 아닌 유사 배열 객체임
	
		- ES6부터는 arguments 객체는 유사 배열 객체이면서 이터러블임
	
	- for (let i=0; i<arguments.length; i++) { res += arugments[i]; }

- Rest 파라미터

	- 유사 배열 객체는 배열이 아니므로 배열 메서드를 사용하려면 Function.prototype.call, Function.prototype.apply를 사용해 간접 호출해야 함
	
		- 이러한 번거로움을 해결하기 위해 ES6에 생김

#### caller 프로퍼티

- caller 프로퍼티

	- ECMAScript 사양에 포함되지 않은 비표준 프로퍼티
	
	- 함수 자신을 호출한 함수를 가리킴

#### length 프로퍼티

- length 프로퍼티

	- 함수를 정의할 때 선언한 매개변수의 개수를 가리킴
	
	- arguments 객체의 length 프로퍼티(인자의 개수) != 함수 객체의 length 프로퍼티(매개변수의 개수)

#### name 프로퍼티

- name 프로퍼티

	- 함수 이름을 나타냄
	
	- ES5 (빈 문자열을 값으로 가짐) -> 정식 표준 ES6 (함수 객체를 가리키는 식별자를 값으로 가짐)
	
		- var anonymousFunc - function() {}; console.log(anonymousFunc.name); -> anonymousFunc
	
#### __proto__ 접근자 프로퍼티

- 모든 객체는 [Prototype]]이라는 내부 슬롯을 가짐

- __proto__ 접근자 프로퍼티

	- [[Prototype]] 내부 슬롯이 가리키는 프로토타입 객체에 접근하기 위해 사용하는 접근자 프로퍼티
	
	- 내부 슬롯에는 직접 접근 불가능, 간접 접근 방법에 한해 프로토타입 객체에 접근 가능함
	
	- 객체 리터럴 방식 객체의 프로토타입 객체는 Object.prototype

		- console.log(obj.__proto__ === Object.prototype); -> true
	
	- 객체 리터럴 방식 객체의 프로토타입 객체인 Object.prototype의 프로퍼티를 상속 받음
	
		- obj.hasOwnProperty('a'); obj.hasOwnProperty('__proto__'); -> true false
	
- hasOwnProperty 메서드

	- 인수로 전달 받은 프로퍼티 키가 객체 고유의 프로퍼티 키인 경우에만 true 반환, 상속 받은 프로토타입의 프로퍼티 키인 경우 false를 반환함

#### prototype 프로퍼티

- prototype 프로퍼티

	- 생성자 함수로 호출 가능한 함수 객체, 즉 constructor만이 소유하는 프로퍼티
	
	- 일반 객체, 생성자 함수로 호출 불가능한 non-constructor에는 prototype 프로퍼티가 없음
	
		- 함수 객체는 prototype 프로퍼티를 소유함
		
			- (function () {}).hasOwnProperty('prototype'); -> true
			
		- 일반 객체는 prototype 프로퍼티를 소유하지 않음
		
			- ({}).hasOwnProperty('prototype'); -> false

	- 함수가 생성자 함수로 호출시 생성자 함수가 생성할 인스턴스의 프로토타입 객체를 가리킴
	
---
