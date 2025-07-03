[모던 자바스크립트 Deep Dive]
[16장] 프로퍼티 어트리뷰트

---

### 1. 내부 슬롯과 내부 메서드

- 내부 슬롯, 내부 메서드

	- 자바스크립트 엔진의 구현 알고리즘을 설명하기 위해 ECMAScript 사양에서 사용하는 의사 프로퍼티, 의사 메서드
	
	- ([[...]])로 감싸진 이름들
	
	- 자바스크립트 엔진의 내부 로직이며, 일부에 한해 간접 접근 수단을 제공함
	
		- ex. 모든 객체가 가지는 o.[[Prototype]]의 o.__proto__

---

### 2. 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체

- 프로퍼티 어트리뷰트

	- 자바스크립트 엔진이 관리하는 내부 상태 값인 내부 슬롯
	
		- [[Value]], [[Writable]], [[Enumerable]], [[Configurable]] 
		
		- Object.getOwnPropertyDescriptor 메서드로 간접 확인 가능함

- 자바스크립트 엔진은 프로퍼티 생성 시 프로퍼티 상태 값을 기본값으로 자동 정의함
	
	- 프로퍼티 값, 값 갱신 가능 여부, 열거 가능 여부, 재정의 가능 여부

- Object.getOwnPropertyDescriptor 메서드

	- 매개변수는 (객체의 참조, 프로퍼티 키를 문자열로) 전달함
	
	- 반환 값은 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크럽터 객체 1개를 반환함
	
	- 존재하지 않거나 상속 받은 프로퍼티에 대해 요구하면 undefined를 반환함
		
	- ex. const person = { name:'Lee' }; console.log(Object.getOwnPropertyDescriptor(person, 'name'));
	
	- ES8에서는 Object.getOwnPropertyDescriptors 메서드가 N개 정보를 반환함

---

### 3. 데이터 프로퍼티와 접근자 프로퍼티

- 프로퍼티

	- 데이터 프로퍼티
	
	- 접근자 프로퍼티

#### 데이터 프로퍼티

- 데이터 프로퍼티

	- 키와 값으로 구성된 일반적인 프로퍼티
	
	- Object.getOwnPropertyDescriptor(function() {}, '__prototype');
	
	- 데이터 프로퍼티가 가지는 프로퍼티 어트리뷰트는 자바스크립트 엔진이 프로퍼티 생성 시 기본값으로 자동 정의됨
	
- 프로퍼티 어트리뷰트-프로퍼티 디스크립터 객체의 프로퍼티

	- [[Value]] : value
	
		- 프로퍼티 키를 통해 값 접근 시 반환되는 값
		
		- 프로퍼티 키를 통해 값 변경 시 [[Value]]에 재할당, 이때 프로퍼티가 없으면 프로퍼티를 동적 생성 & 생성된 프로퍼티의 [[Value]]에 값을 저장함

	- [[Writable]] : writable
	
		- 프로퍼티 값의 변경 가능 여부, 불리언 값
		
		- 값이 false인 경우 해당 프로퍼티의 [[Value]] 값 변경할 수 없는 읽기 전용 프로퍼티가 됨

	- [[Enumerable]] : enumerable
	
		- 프로퍼티의 열거 가능 여부, 불리언 값
		
		- 값이 false인 경우 해당 프로퍼티는 for...in문, Object.keys 메서드 등으로 열거 불가능함

	- [[Configurable]] : configurable
	
		- 프로퍼티의 재정의 가능 여부, 불리언 값
		
		- 값이 false인 경우 해당 프로퍼티의 삭제 프로퍼티 어트리뷰트 값의 변경이 금지됨, 단, [[Writable]]이 true인 경우 [[Value]]의 변경, [[Writable]]을 false로 변경은 허용됨

#### 접근자 프로퍼티

- 접근자 프로퍼티

	- 자체적으로는 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 접근자 함수로 구성된 프로퍼티
	
	- Object.getOwnPropertyDescriptor(Object.prototype, '__proto__');
	
	- ex. const person = { name: 'Lee', get getName() {}, set setName() {} };

- 프로퍼티 어트리뷰트-프로퍼티 디스크립터 객체의 프로퍼티

	- [[Get]] - get
	
		- 접근자 프로퍼티 키를 통해 데이터 프로퍼티 값 읽을 시 호출되는 접근자 함수
		
		- 프로퍼티 어트리뷰트 [[Get]]의 값(getter 함수)의 결과가 프로퍼티 값으로 반환됨
	
	- [[Set]] - set
	
		- 접근자 프로퍼티 키를 통해 데이터 프로퍼티의 값 저장 시 호출되는 접근자 함수
		
		- 프로퍼티 어트리뷰트 [[Set]]의 값(setter 함수)의 결과가 프로퍼티 값으로 저장됨
	
	- [[Enumerable]] - enumerable
	
		- 프로퍼티의 열거 가능 여부, 불리언 값
		
		- 값이 false인 경우 해당 프로퍼티는 for...in문, Object.keys 메서드 등으로 열거 불가능함
		
	- [[Configurable]] - configurable

		- 프로퍼티의 재정의 가능 여부, 불리언 값
		
		- 값이 false인 경우 해당 프로퍼티의 삭제 프로퍼티 어트리뷰트 값의 변경이 금지됨, 단, [[Writable]]이 true인 경우 [[Value]]의 변경, [[Writable]]을 false로 변경은 허용됨

- 동작 과정

	- 1. 프로퍼티 키 유효성 확인
	
	- 2. 프로토타입 체인에서 프로퍼티 검색
	
	- 3. 검색된 프로퍼티가 데이터, 접근자 중 무엇인지 확인
	
	- 4. 접근자라면 접근자 프로퍼티의 프로퍼티 어트리뷰트 [[Get]]의 값(getter 함수)를 호출해 결과를 반환함 (== Object.getOwnPropertyDescriptor 메서드가 반환하는 프로퍼티 디스크립터 객체의 get 프로퍼티 값)
	
- 프로토타입

	- 어떤 객체의 상위(부모) 객체 역할을 하는 객체
	
	- 하위(자식) 객체에게 자신의 프로퍼티와 메서드를 상속함
	
- 프로토타입 체인

	- 프로토타입이 단방향 링크드 리스트 형태로 연결되어 있는 상속 구조 (차례대로 검색해야 하는 구조)

---

### 4. 프로퍼티 정의

- 프로퍼티 정의란

	- 새로운 프로퍼티를 추가하면서 프로퍼티 어트리뷰트를 정의하거나, 기존 프로퍼티의 프로퍼티 어트리뷰트를 재정의하는 것
	
- Object.defineProperty 메서드

	- 인수로 (객체의 참조, 데이터 프로퍼티의 키인 문자열, 프로퍼티 디스크립터 객체)를 전달함
	
		- Object.defineProperty(person, 'fstName', { value: 'Lee' });
	
		- Object.defineProperty(person, 'fullName', { get() {}, set() {} });

	- 해당 메서드로 프로퍼티 정의 시 프로퍼티 디스크립터 객체의 프로퍼티를 일부 생략 가능함, 기본값 적용됨
	
		- value, get, set -> undefined
	
		- writable, enumerable, configurable -> false
	
	- 한 번에 하나의 프로퍼티만 정의 가능, Object.defineProperties 메서드로 여러 개도 정의 가능함

---

### 5. 객체 변경 방지

#### 객체 확장 금지

- Object.preventExtensions 메서드

	- 객체의 확장을 금지(프로퍼티 추가 금지)함
	
		- 프로퍼티 동적 추가, Object.defineProperty 메서드 금지됨

	- console.log(Object.isExtensible(person)); -> true

#### 객체 밀봉

- Object.seal 메서드

	- 객체를 밀봉(프로퍼티 추가 및 삭제, 프로퍼티 어트리뷰트 재정의 금지)함
	
		- 읽기, 쓰기만 가능함
		
	- console.log(Object.isSealed(person)); -> false

#### 객체 동결

- Object.freeze 메서드

	- 객체를 동결(프로퍼티 추가 및 삭제, 프로퍼티 어트리뷰트 재정의 금지, 프로퍼티 값 갱신 금지)함
	
		- 읽기만 가능함
		
	- console.log(Object.isFrozen(person)); -> false;

#### 불변 객체

- Object.freeze 메서드로 동결해도 얕은 변경 방지로 인해 중접 객체까지 동결 불가능함

	- 객체를 값으로 갖는 모든 프로퍼티에 대해 재귀적으로 Object.freeze 메서드를 호출해야 함

---
