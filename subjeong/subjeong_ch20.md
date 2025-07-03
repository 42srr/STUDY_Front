[모던 자바스크립트 Deep Dive]
[20장] strict mode

---

### 1. strict mode란?

- 암묵적 전역

	- foo 함수 내 선언하지 않은 x 변수에 할당을 하면, 자바스크립트 엔진이 스코프 체인을 통해 x 변수의 선언 위치를 찾는데, 자바스크립트 엔진은 암묵적으로 전역 객체에 x 프로퍼티를 동적 생성하며 이는 전역 변수처럼 사용 가능한 현상

- strict mode

	- 자바스크립트 언어의 문법을 좀 더 엄격히 적용해 오류 또는 자바스크립트 엔진 최적화 문제에 대해 명시적인 에러를 발생

	- 잠재적인 오류 발생이 어려운 개발 환경을 만들기 위해 추가됨
	
	- ES6에서 도입된 클래스, 모듈은 기본적으로 적용됨
	
- ESLint (린트 도구)

	- 정적 분석 기능을 통해 소스코드를 실행하기 전 소스코드를 스캔하여 문법적 오류, 잠재적 오류와 그 원인을 리포팅해 줌
	
	- strict mode가 제한하는 오류, 코딩 컨벤션 설정

---

### 2. strict mode의 적용

- strict mode의 적용

	- 전역의 선두에 'use strict';를 추가해 스크립트 전체에 적용
	
	- 함수 몸체의 선두에 'use strict';를 추가해 해당 함수와 중첩 함수에 적용
	
	- 코드의 선두에 'use strict';를 위치시켜야 함

---

### 3. 전역에 strict mode를 적용하는 것은 피하자

- 전역에 적용한 strict mode는 스크립트 단위로 적용됨

	- <!DOCTYPE html><html><body><script>'use strict';</script> <script>x = 1</script> ... -> No Error
		
	- 즉시 실행 함수로 스크립트 전체를 감싸 스코프를 구분하고 즉시 실행 함수의 선두에 strict mode를 적용함
		
		- strict mode 스크립트, non-strict mode 스크립트 혼용은 오류 발생 가능성을 야기함
		
		- (function () { 'use strict'; ... }());

---

### 4. 함수 단위로 strict mode를 적용하는 것도 피하자

- strict mode는 즉시 실행 함수로 감싼 스크립트 단위로 적용해야 함

	- (function () { var let = 10; function foo() { 'use strict'; let = 20; } foo(); }()); -> Syntax Error

---

### 5. strict mode가 발생시키는 에러

#### 암묵적 전역

- 암묵적 전역

	- 선언하지 않은 변수를 참조하면 ReferenceError가 발생함
	
		- (function () { 'use strict'; x = 1; (x); }());

#### 변수, 함수, 매개변수의 삭제

- 변수, 함수, 매개변수의 삭제

	- delete 연산자로 변수, 함수, 매개변수를 삭제하면 SyntaxError가 발생함
	
		- (function () { 'use strict'; var x = 1; delete x; function foo(a) { delete a; } delete foo; }());

#### 매개변수 이름의 중복

- 매개변수 이름의 중복

	- 중복된 매개변수 이름을 사용하면 SyntaxError가 발생함
	
		- (function () { 'use strict'; function foo(x, x) { return x+x; } foo(1,2); }());

#### with 문의 사용

- with 문의 사용

	- with 문을 사용하면 SyntaxError가 발생함
	
	- (function () { 'use strict'; with({x:1}) { (x); } }());
	
- with 문

	- 전달된 객체를 스코프 체인에 추가함
	
	- 동일한 객체의 프로퍼티를 반복해서 사용할 때 객체 이름을 생략할 수 있음 (간단하지만 성능, 가독성 저하)

---

### 6. strict mode 적용에 의한 변화

#### 일반 함수의 this

- 일반 함수의 this

	- strict mode에서 함수를 일반 함수로 호출 시 this에 undefined가 바인딩됨
	
		- 생성자 함수가 아닌 일반 함수 내부에서는 this를 사용할 필요가 없기 때문
		
		- (funtcion () { 'use strict'; function foo() { (this); } foo(); function Foo() { (this); } new Foo(); }());

#### arguments 객체

- arguments 객체

	- strict mode에서는 매개변수에 전달된 인수를 재할당해 변경해도 arguments 객체에 반영되지 않음
	
		- (function (a) { 'use strict'; a = 2; (arguments); }(1));

---
