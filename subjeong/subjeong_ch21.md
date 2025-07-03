[모던 자바스크립트 Deep Dive]
[21장] 빌트인 객체

---

### 1. 자바스크립트 객체의 분류

- 표준 빌트인 객체

	- ECMAScript 사양에 정의된 객체
	
		- 자바스크립트 실행 환경(브라우저/Node.JS 환경)과 관계 없이 언제나 사용 가능함
	
	- 애플리케이션 전역의 공통 기능을 제공함
	
		- 전역 객체의 프로퍼티로서 제공돼 별도의 선언 없이 전역 변수처럼 언제나 참조 가능함
	
- 호스트 객체

	- ECMAScript 사양에 정의되어 있지 않지만 자바스크립트 실행 환경(브라우저/Node.JS 환경)에서 추가로 제공하는 객체
	
	- 브라우저 환경에서는 DOM, BOM, Canvas, XMLHttpRequest, fetch, requestAnimationFrame, SVG, Web Storage, Web Somponent, Web Worker와 같은 클라이언트 사이드 Web API를 호스트 객체로 제공
	
	- Node.JS 환경에서는 Node.JS 고유의 API를 호스트 객체로 제공
	
- 사용자 정의 객체

	- 표준 빌트인 객체, 호스트 객체처럼 기본 제공되는 객체가 아닌 사용자가 직접 정의한 객체
	
---

### 2. 표준 빌트인 객체

- 자바스크립트는 40여개의 표준 빌트인 객체를 제공함

	- Math, Reflect, JSON을 제외한 모두 인스턴스를 생성 가능한 생성자 함수 객체임
	
		- 생성자 함수 객체인 표준 빌트인 객체는 프로토타입 메서드, 정적 메서드를 제공
		
		- 생성자 함수 객체가 아닌 표준 빌트인 객체는 정적 메서드만 제공
		
- 표준 빌트인 객체의 prototype 프로퍼티에 바인딩된 객체는 다양한 빌트인 프로토타입 메서드를 제공함

	- 표준 빌드인 객체는 인스턴스 없이도 호출 가능한 빌트인 정적 메서드를 제공
	
- 표준 빌트인 객체 예시

	- Number 생성자에 의한 Number 객체 생성
	
		- const numObj = new Number(1.5); -> Number {1.5}
	
	- toFixed는 Number.prototype의 프로토타입 메서드임
		- numObj.toFixed(); -> 2
		
	- isInteger는 Number의 정적 메서드임
	
		- Number.isInteger(0.5); -> false

---

### 3. 원시값과 래퍼 객체

- 래퍼 객체

	- 문자열, 숫자, 불리언 값에 대해 객체처럼 접근하면 생성되는 임시 객체

- 원시값과 래퍼 객체

	- 원시값은 객체가 아니라서 프로퍼티나 메서드를 가질 수 없지만, 원시값을 객체처럼 사용하면, 자바스크립트 엔진은 암묵적으로 연관된 객체를 생성해 생성된 객체로 프로퍼티 접근이나 메서드 호출 후 다시 원시값으로 되돌림

	- 원시값인 문자열, 숫자, 불리언 값들에 대해 객체처럼 마침표 표기법(또는 대괄호 표기법)으로 접근 시 자바스크립트 엔진이 일시적으로 원시값을 연관된 객체로 변환해 주기 때문임
	
	-  원시 타입인 문자열이 래퍼 객체인 String 인스턴스로 변환되고 이후 래퍼 객체의 [[StringData]] 내부 슬롯에 할당된 원시값으로 되돌려지고 래퍼 객체는 가비지 컬렉션 대상이 됨
	
		- 문자열 래퍼 객체인 String 생성자 함수의 인스턴스는 String.prototype의 메서드를 상속 받아 사용 가능함
		
		- const str = 'hi'; str.name = 'lee'; (str.name); (typeof str, str); -> undefined / string hi
		
		- const str = 'hi'; str.length; str.toUpperCase(); typeof str -> string

		- const num = 1.5; num.toFixed(); (typeof num, num); -> 2 / number 1.5

- 문자열, 숫자, 불리언, 심벌 이외의 원시값 (null, undefined)는 래퍼 객체를 생성하지 않음

---

### 4. 전역 객체
	
- globalThis

	- ECMAScript2020(ES11)에서 도입, 브라우저 환경과 Node.JS 환경에서 전역 객체를 가리키던 다양한 식별자를 통일한 식별자
	
	- 표준 사양이므로 ECMAScript 표준 사양을 준수하는 모든 환경에서 사용 가능함
	
		- globalThis === this | window | self | frames | this | global -> true


- 전역 객체

	- 코드 실행 이전 단계에 자바스크립트 엔진에 의해 어떤 객체보다도 먼저 생성되는 특수한 객체
	
	- 어떤 객체에도 속하지 않은 모든 빌트인 객체의 최상위 객체
		
	- 브라우저 환경에서는 window(또는 self, this, frames)가 전역 객체를 가리킴
	
	- Node.JS 환경에서는 global이 전역 객체를 가리킴
	
	- 표준 빌트인 객체, 환경에 따른 호스트 객체, var 키워드로 선언한 전역 변수와 전역 함수를 프로퍼티로 가짐
	
	- 전역 객체의 프로퍼티/메서드는 전역 객체 식별자를 생략하여 참조/호출 가능하므로 전역 변수/전역 함수처럼 사용 가능함
	
- 전역 객체의 특징

	- 전역 객체를 생성 가능한 생성자 함수가 제공되지 않음 (의도적 생성 X)
	
	- 전역 객체의 프로퍼티를 참조할 때 window(또는 global)를 생략 가능함
	
		- window.parseInt('F', 16); parseInt('F', 16); window.parseInt === parseInt; -> true
	
	- 모든 표준 빌트인 객체를 프로퍼티로 가짐
	
	- 자바스크립트 실행 환경에 따라 추가적으로 프로퍼티, 메서드를 가짐
	
	- var 키워드로 선언한 전역 변수와 선언하지 않은 변수에 값을 할당한 암묵적 전역, 전역 함수는 전역 객체의 프로퍼티가 됨
	
		- var foo = 1; window.foo; -> 1
		
		- bar = 2; window.bar -> 2
		
		- function baz() { return 3; } window.baz(); -> 3
		
	- let, const 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아님, window.foo와 같이 접근 불가능함 (전역 렉시컬 환경의 선언적 환경 레코드 내 존재함)
	
		- let foo = 123; window.foo; -> undefined
		
	- 브라우저 환경의 모든 자바스크립트 코드는 하나의 전역 객체 window를 공유함		

#### 빌트인 전역 프로퍼티

- 빌트인 전역 프로퍼티

	- 전역 객체의 프로퍼티
	
	- 주로 애플리케이션 전역에서 사용하는 값을 제공
	
- Infinity

	- 무한대를 나타내는 숫자값 Infinity를 가짐
	
		- window.Infinity == Infinity; -> true
		
		- (3/0) (-3/0) (typeof Infinity); -> Infinity / -Infinity / number
		
- NaN

	- 숫자가 아님을 나타내는 숫자값 NaN을 가짐, Number.NaN 프로퍼티와 같음
	
		- (window.NaN); (Number('xyz')); (1*'string'); (typeof NaN); -> NaN / NaN / NaN / number
		
- undefined

	- 원시 타입 undefined를 값으로 가짐
	
		- (window.undefined); var foo; (foo); (typeof undefined); -> undefined / undefined / undefined

#### 빌트인 전역 함수

- 빌트인 전역 함수
	
	- 애플리케이션 전역에서 호출 가능한 빌트인 함수

	- 전역 객체의 메서드

- eval (최적화 없으므로 지양)

	- 주어진 문자열 코드를 런타임에 평가 또는 실행함
		
		- 표현식이면 문자열 코드를 런타임에 평가해 값을 생성함
		
		- 표현식이 아닌 문이면 문자열 코드를 런타임에 실행함
		
		- eval('1 + 2; 3 + 4;'); -> 7
		
		- eval('var x = 5;'); -> undefined
		
		- eval('({a: 1})'); -> {a: 1}
		
		- eval('(function() { return 1; })'); -> 1
	
	- 기존의 스코프를 런타임에 동적으로 수정함

		- function foo() { eval('varx x = 2;'); }
		
	- strict mode에서 eval 함수 자신의 자체적인 스코프를 생성함
	
		- let, const 키워드를 사용한 변수 선언문이라면 암묵적으로 strict mode가 적용됨
	
		- const x = 1; function foo() { 'use strict'; eval('var x = 2; console.log(x);'); -> 2

- isfinite

	- 전달 받은 인수가 유한수이면 true, 무한수이면 false를 반환함
	
	- 숫자가 아닌 경우 숫자 타입 변환 후 검사를 수행함, 이때 NaN이면 false를 반환함
	
	- isFinite(0); isFinite(2e64); isFinite('10'); isfinite(null); -> true
	
	- isFinite(Infinity); isFinite(-Infinity); isFinite(NaN); isFinite('Hello'); -> false
	
- isNaN

	- 전달 받은 인수가 NaN인지 검사하여 결과를 불리언 타입으로 반환함
	
		- 숫자가 아닌 경우 숫자 타입 변환 후 검사를 수행함
		
		- isNaN(NaN); isNaN('blabla'); isNaN(undefined); isNaN({]); isNaN(new Date().toString()); -> true
		
		- isNaN(10); isNaN('10'); isNaN(''); isNaN(' '); isNaN(true); isNaN(null); isNaN(new Date()); -> false
		
- parseFloat

	- 전달 받은 문자열 인수를 부동 소수점 숫자, 즉 실수로 해석해 반환함
	
		- parseFloat('  3.14  '); -> 3.14
		
		- parseFloat('10.00'); -> 10
		
		- parseFloat('34 45 years'); -> 34
		
		- parseFloat('He 45 years'); -> NaN 
		
- parseInt

	- 전달 받은 문자열 인수를 정수로 해석해 반환함
	
		- 문자열이 아니면 문자열로 변환한 후 수행함
	
		- parseInt('10.123'); -> 10
		
		- parseInt('10', 2); -> 10
		
		- parseInt('0xf'); parseInt('f', 16); -> 15 (O)
		
		- parseInt('0b10'); parseInt('0o10'); -> 0 (X)
		
		- parseInt('A0'); parseInt('20', 2); -> NaN
		
		- parseInt('58', 8); -> 5
		
- encodeURI

	- 완전한 URI를 문자열로 전달 받아 이스케이프 처리를 위해 인코딩함
	
		- URI : 인터넷에 있는 자원을 나타내는 유일한 주소 (URL, URN 등)
		
		- URL은 아스키 문자 셋으로만 구성되어야 하므로 이스케이프 처리가 필요함
	
- decodeURI	
		
	- 인코딩된 URI를 인수로 전달 받아 이스케이프 처리 이전으로 디코딩함
		
- encodeURIComponent

	- URI 구성 요소를 인수로 전달 받아 인코딩함
	
		- 단, 알파벳, 0~9 숫자, -_.!~*'() 문자는 이스케이프 처리에서 제외됨
		
		- 인수를 쿼리 스트링의 일부로 간주하므로 쿼리 스트링 구분자(=, ?, &)까지 인코딩함
		
- decodeURIComponent

	- 매개변수로 전달된 URI 구성 요소를 디코딩함
	
		- 매개변수를 완전한 URI 전체로 간주하므로 쿼리 스트링 구분자(=, ?, &)는 인코딩하지 않음

	
### 암묵적 전역

- 암묵적 전역

	- 선언하지 않은 식별자 y에 값을 할당하면 자바스크립트 엔진이 windiow.y로 해석해 전역 객체의 프로퍼티가 되는 현상
		
		- function foo () { y = 20; } console.log(y);
		
	- y는 변수가 아니므로 변수 호이스팅이 발생하지 않음
	
	- y는 단지 프로퍼티이므로 delete 연산자로 삭제 가능함
