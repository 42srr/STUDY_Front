# 21장 빌트인 객체

## 21.1 자바스크립트 객체의 분류
- JS 객체는 크게 표준 빌트인 객체, 호스트 객체, 사용자 정의 객체로 분류됨
- 표준 빌트인 객체 : ECMAScript 사양에 정의된 객체. 애플리케이션 전역의 공통 기능 제공.
- 호스트 객체 : ECMAScript 사양에 정의 X. But JS 실행 환경(브라우저 or Node.js)에서 추가로 제공하는 객체.
- 사용자 정의 객체 : 표준 빌트인 객체와 호스트 객체처럼 기본 제공되는 객체가 아닌 사용자가 직접 정의한 객체.

## 21.2 표준 빌트인 객체
- JS는 40여개의 표준 빌트인 객체 제공
- Math, Reflect, JSON을 제외한 표준 빌트인 객체는 모두 생성자 함수 객체
- 생성자 함수인 표준 빌트인 객체가 생성한 인스턴스의 프로토타입은 표준 빌트인 객체의 prototype 프로퍼티에 바인딩된 객체임
- 표준 빌트인 객체는 인스턴스 없이도 호출 가능한 빌트인 정적 메서드 제공

## 21.3 원시값과 래퍼 객체
- 원시값 문자열, 숫자, 불리언 값의 경우 이들에 대해 객체처럼 마침표(또는 대괄호) 표기법으로 접근시 JS 엔진이 일시적으로 원시값을 연관된 객체(String, Number, Boolean)로 변환
--> JS 엔진이 암묵적으로 연관된 객체 생성하여 프로퍼티에 접근하거나 메서드, 호출 후 다시 원시값으로 되돌림

- 래퍼 객체 : 문자열, 숫자, 불리언 값에 대해 객체처럼 접근시 생성되는 임시 객체

## 21.4 전역 객체
- 코드 실행 이전, JS 엔진에 의해 어떤 객체보다도 먼저 생성되는 특수한 객체. 어떤 객체에도 속하지 않은 최상위 객체.
- JS 환경에 따라 지칭하는 이름이 다름.
	- 브라우저 : window(또는 self, this, frames)
	- Node.js : global
- 표준 빌트인 객체, 호스트 객체, var 키워드로 선언한 전역 변수(let, const는 아님), 전역 함수를 프로퍼티로 가짐

### 21.4.1 빌트인 전역 프로퍼티
- 전역 객체의 프로퍼티. 주로 애플리케이션 전역에서 사용하는 값 제공.
- Infinity : 무한대를 나타내는 숫자값 Infinity를 가짐
- NaN : 숫자가 아님을 나타내는 숫자값 NaN을 가짐 (== Number.NaN)
- undefined : 원시 타입 undefined를 값으로 가짐

### 21.4.2 빌트인 전역 함수
- 전역 객체의 메서드.
- eval : JS 코드를 나타내는 문자열을 인수로 전달받아 표현식이라면 런타임에 평가하여 값 생성, 문이라면 그 코드를 런타임에 실행
- isFinite : 전달받은 인수가 유한수이면 true, 무한수이면 false 반환. 전달받은 인수가 숫자가 아니면 숫자 타입으로 변환 후 검사하며, 인수가 NaN으로 평가되는 값이면 false 반환.
- isNaN : 전달받은 인수가 NaN인지 여부를 불리언 타입으로 반환. 전달받은 인수가 숫자가 아니면 숫자 타입으로 변환 후 검사.
- parseFloat : 전달받은 문자열 인수를 부동 소수점 숫자(실수)로 해석하여 반환
- parseInt : 전달받은 문자열 인수를 정수로 해석하여 반환
- encodeURI : 완전한 URI를 문자열로 전달받아 이스케이프 처리를 위해 인코딩함
- decodeURI : 인코딩된 URI를 인수로 전달받아 이스케이프 처리 이전으로 디코딩함
- encodeURIComponent : URI 구성 요소(component)를 인수로 전달받아 인코딩함
- decodeURIComponent : 인수로 전달된 URI 구성 요소를 디코딩함

### 21.4.3 암묵적 전역
- 암묵적 전역 : 선언하지 않은 식별자에 값 할당시 전역 객체의 프로퍼티가 됨 (전역 변수처럼 동작)
	- 변수가 아니므로 변수 호이스팅 발생 X
	- delete 연산자로 삭제 가능. 전역 변수는 delete 연산자로 삭제 불가.
