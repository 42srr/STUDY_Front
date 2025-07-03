[모던 자바스크립트 Deep Dive]
[26장] ES6 함수의 추가 기능

---

### 1. 함수의 구분

- ES6 이전의 함수는 사용 목적에 따라 명확히 구분되지 않음
	
	- ES6 이전의 모든 함수는 일반 함수로서 호출 가능하며 (callable), 생성자 함수로서 호출 가능함 (constructor)
	
	- 불필요한 프로토타입 객체를 생성함
	
	- 이를 해결하기 위해 ES6에서는 일반 함수, 메서드, 화살표 함수로 구분함
	
	- constructor/prototype/super/arguments
	
		- 일반 함수 : O O X O
		
		- 메서드 : X X O O
		
		- 화살표 함수 : X X X X
		
---

### 2. 메서드

- 메서드

	- ES6 이전 일반적으로 메서드는 객체에 바인딩된 함수였음
	
	- ES6 메서드는 메서드 축약 표현으로 정의된 함수만을 의미함
	
		- foo() { return this.x; } -> 메서드
		
		- bar: function() { return this.x; } -> 일반 함수
		
	- ES6 메서드는 인스턴스를 생성 불가능한 non-constructor이므로, 생성자 함수로 호출 불가능함
	
		- prototype 프로퍼티 없고, 프로토타입도 생성하지 않음
		
		- 표준 빌트인 객체가 제공하는 프로토타입 메서드, 정적 메서드는 모두 non-constructor임

	- ES6 메서드는 자신을 바인딩한 객체를 가리키는 내부 슬롯 [[HomeObject]]를 가져서, super 키워드 사용 가능함 

---

### 3. 화살표 함수

- 화살표 함수

	- function 키워드 대신 화살표(=>)를 사용해 간략하게 함수를 정의하는 방법
	
	- 표현뿐만 아니라 내부 동작도 간략함
	
	- 콜백 함수 내부에서 this가 전역 객체를 가리키는 문제를 해결함

#### 화살표 함수 정의

- 화살표 함수 정의 문법

	- 함수 정의

		- 함수 표현식으로만 정의 가능함
	
		- const multiply = (x, y) => x * y; multiply(2, 3);
		
	- 매개변수 선언

		- const arrow = (x, y) => {...};
		
		- const arrow = x => {...};
		
		- const arrow = () => {...};
		
	- 함수 몸체 정의
	
		- const power = x => x ** 2;
		
		- const power = () => { const x = 1 };
		
		- const create = (id, content) => ({id, content});
		
		- const person = (name => ({ sayHi() { return `${name}`; }}))('Lee'); // 즉시 실행 함수
		
		- [1, 2, 3].map(v => v * 2);

#### 화살표 함수와 일반 함수의 차이

- 화살표 함수와 일반 함수의 차이

	- 화살표 함수는 인스턴스 생성 불가능한 non-constructor임 (prototype 프로퍼티 X, 프로토타입 생성 X)
	
	- 화살표 함수는 중복된 매개변수 이름 선언이 불가능함
	
	- 화살표 함수는 함수 자체의 this, arguments, super, new.target 바인딩을 갖지 않음
		
#### this

- this

	- 화살표 함수의 this는 콜백 함수 내부의 this와 외부 함수의 this가 서로 다른 값을 가리키게 되는 문제를 해결함
	
	- this 바인딩은 함수 호출 시 함수 호출 방식에 따라 this 바인딩할 객체가 동적으로 결정됨
	
	- 이때, 일반 함수로서 호출되는 콜백 함수는 내부의 this가 strict mode와 함께 적용되어 전역 객체가 아닌 undefined가 바인딩됨

- Array.prototype.map 메서드

	- 배열을 순회하며 배열의 각 요소에 대해 인수로 전달된 콜백 함수를 호출, 콜백 함수의 반환값들로 구성된 새로운 배열을 반환함
	
- 콜백 함수 내부의 this 문제를 해결하는 방법

	- add 메서드를 호출한 prefixer 객체를 가리키는 this를 일단 회피시킨 후 콜백 함수 내부에서 사용함
	
	- Array.prototype.map의 두 번째 인수로 add 메서드를 호출한 prefixer 객체를 가리키는 this를 전달함
	
	- Function.prototype.bind 메서드를 사용해 add 메서드를 호출한 prefixer 객체를 가리키는 this를 바인딩함
	
- 렉시컬 this

	- 화살표 함수는 함수 자체의 this 바인딩을 갖지 않음
	- 화살표 함수 내부에서 this를 참조하면 상위 스코프의 this를 그대로 참조하는 것

- 화살표 함수

	- () => this.x; === (function () { return this.x; }).bind(this);

	- 화살표 함수는 상위 스코프의 this를 참조함
	
		- 화살표 함수가 중첩되었다면, 상위 화살표 함수에도 this 바인딩이 없으므로 스코프 체인 상 가장 가까운 상위 함수 중에서 화살표 함수가 아닌 함수의 this를 참조함
	
		- 만약 함수가 전역 함수라면, 화살표 함수의 this는 전역 객체를 가리킴

		- 그렇기에 this를 교체 불가능함 (메서드를 화살표 함수로 정의 X)
	
	- 함수 자체의 super 바인딩을 가지지 않아서, 상위의 super(constructor 등)를 참조함
	
	- 함수 자체의 arguments 바인딩을 가지지 않아서, 상위의 arguments(즉시 실행 함수 등)를 참조함
	
#### super

- super 

	- 내부 슬롯 [[HomeObject]]를 갖는 ES6 메서드 내에서만 사용 가능한 키워드

#### arguments

- arguments

	- 호출 시 전달된 인수들의 정보를 담고 있는 순회 가능한 유사 배열 객체
	
	- 함수 내부에서 지역 변수처럼 사용 가능함
	
	- 함수 정의 시 가변 인자 함수 구현 시 유용함
	
	- 화살표 함수에서는 arguments 객체 사용 불가능, 상위 스코프의 arguments 객체 참조는 가능함
	
		- Rest 파라미터를 사용하면 화살표 함수로 가변 인자 함수 구현 가능함

---

### 4. Rest 파라미터

#### 기본 문법

- Rest 파라미터의 문법

	- 함수에 전달된 인수들의 목록을 배열로 전달 받음
	
	- 매개변수 이름 앞에 세 개의 점(...)을 붙여 정의
	
		- function foo(...rest) { ... } // [1,2,3,4,5]
	
	- 일반 매개변수와 함께 사용 시 함수 전달 인수들은 매개변수/Rest 파라미터에 순차적으로 할당됨
	
		- Rest 파라미터는 반드시 마지막 파라미터여야 하며, 1 개만 선언 가능함
	
		- function foo(param1, param2, ...rest) { ... } // 1, 2, [3,4,5]

	- 매개변수 개수 나타내는 length 프로퍼티에 영향을 주지 않음

#### Rest 파라미터와 arguments 객체

- Rest 파라미터와 arguments 객체

	- 문제 : arguments 객체는 배열이 아닌 유사 배열 객체로, 배열 메서드를 사용하려면 Function.prototype.call/apply 메서드를 사용해 배열로 변환해야 함
	
		- var array = Array.prototype.slice.call(arguments);
		
	- 해결 : ES6에서는 rest 파라미터를 사용해 가변 인자 함수의 인수 목록을 배열로 직접 전달 받을 수 있음
	
		- function sum(...args) { ... }
		
	- 함수와 ES6 메서드는 rest 파라미터, arguments 객체를 모두 사용 가능함
	
	- 화살표 함수는 함수 자체의 arguments 객체를 가지지 않아 rest 파라미터를 사용해야 함

---

### 5. 매개변수 기본값

- 매개변수 기본값

	- 자바스크립트 엔진이 매개변수의 개수와 인수의 개수를 체크하지 않음
	
		- 인수가 전달되지 않은 매개변수의 값은 undefined
		
		- 필요없는 인수 값은 무시됨
		
	- 인수가 전달되지 않았거나 undefined를 전달한 경우를 확인하기 위해 매개변수 기본값이 필요함 (rest 파라미터는 불가능)
	
		- function sum(x = 0, y = 0) { ... }
		
	- 매개변수 개수 나타내는 length 프로퍼티에 영향을 주지 않음

---
