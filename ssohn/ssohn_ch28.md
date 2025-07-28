# 28장 Number

## 28.1 Number 생성자 함수

- 표준 빌트인 객체인 Number 객체는 생성자 함수 객체다. 따라서 new 연산자와 함께 호출하여 Number 인스턴스를 생성할 수 있다.
- Number 생성자 함수에 인수를 전달하지 않고 new 연산자와 함께 호출하면 [[NumberData]] 내부 슬롯에 0을 할당한 Number 래퍼 객체를 생성한다.
- Number 생성자 함수의 인수로 숫자를 전달하면서 new 연산자와 함께 호출하면 [[NumberData]] 내부 슬롯에 인수로 전달받은 숫자를 할당한 Number 래퍼 객체를 생성한다.
- Number 생성자 함수의 인수로 숫자가 아닌 값을 전달하면 인수를 숫자로 강제 변환한 후, [[NumberData]] 내부 슬롯에 변환된 숫자를 할당한 Number 래퍼 객체를 생성한다.
- 인수를 숫자로 변환할 수 없다면 NaN을 [[NumberData]] 내부 슬롯에 할당한 Number 래퍼 객체를 생성한다.
- 인수를 숫자로 변환할 수 없다면 NaN을 [[NumberData]] 내부 슬롯에 할당한 Number 래퍼 객체를 생성한다.

## 28.2 Number 프로퍼티

### 28.2.1 Number.EPSILON

- Number.EPSILON은 부동소수점으로 인해 발생하는 오차를 해결하기 위해 사용한다.

### 28.2.2 Number.MAX_VALUE

- Number.MAX_VALUE는 자바스크립트에서 표현할 수 있는 가장 큰 양수 값이다.
- Number.MAX_VAULE보다 큰 숫자는 Infinity다.

### 28.2.3 Number.MIN_VALUE

- Number.MIN_VAULE는 자바스크립트에서 표현할 수 있는 가장 작은 양수 값이다.
- Number.MIN_VALUE보다 작은 숫자는 0이다.

### 28.2.4 Number.MAX_SAFE_INTEGER

- Number.MAX_SAFE_INTEGER는 자바스크립트에서 안전하게 표현할 수 있는 가장 큰 정수값이다.

### 28.2.5 Number.MIN_SAFE_INTEGER

- Number.MIN_SAFE_INTEGER는 자바스크립트에서 안전하게 표현할 수 있는 가장 작은 정수값이다.

### 28.2.6 Number.POSITIVE_INFINITY

- Number.POSITIVE_INFINITY는 양의 무한대를 나타내는 숫자값 Infinity와 같다.

### 28.2.7 Number.NEGATIVE_INFINITY

- Number.NEGATIVE_INFINITY는 음의 무한대를 나타내는 숫자값 -Infinity와 같다.

### 28.2.8 Number.NaN

- Number.NaN은 숫자가 아닌(Not-a-Number)을 나타내는 숫자값이다.
- Number.NaN은 window.NaN과 같다.

## 28.3 Number 메서드

### 28.3.1 Number.isFinite

- ES6에서 도입된 Number.isFinite 정적 메서드는 인수로 전달된 숫자값이 정상적인 유한수, 즉 Infinity 또는 -Infinity가 아닌지 검사하여 그 결과를 불리언 값으로 반환한다.
- 빌트인 전역 함수 isFinite는 전달받은 인수를 숫자로 암묵적 타입 변환하여 검사를 수행하지만 Number.isfinite는 전달받은 인수를 숫자로 암묵적 타입 변환하지 않는다.
- 따라서 숫자가 아닌 인수가 주어졌을 때 반환값은 언제나 false다.

### 28.3.2 Number.isInteger

- ES6에서 도입된 Number.isInteger 정적 메서드는 인수로 전달된 숫자값이 정수인지 검사하여 그 결과를 불리언 값으로 반환한다.

### 28.3.3 Number.isNaN

- ES6에서 도입된 Number.isNaN 정적 메서드는 인수로 전달된 숫자값이 NaN인지 검사하여 그 결과를 불리언 값으로 반환한다.
- 빌트인 전역 함수 isNaN은 전달받은 인수를 숫자로 암묵적 타입 변환하여 검사를 수행하지만 Number.isNaN 메서드는 전달받은 인수를 숫자로 암묵적 타입 변환하지 않는다.
- 따라서 숫자가 아닌 인수가 주어졌을 때 반환값은 언제나 false다.

### 28.3.4 Number.isSafeInteger

- ES6에서 도입된 Number.isSafeInteger 정적 메서드는 인수로 전달된 숫자값이 안전한 정수인지 검사하여 그 결과를 불리언 값으로 반환한다.
- 안전한 정수 값은 -(2^53 - 1)과 2^53 - 1 사이의 정수값이다.

### 28.3.5 Number.prototype.toExponential

- toExponential 메서드는 숫자를 지수 표기법으로 변환하여 문자열로 반환한다.

### 28.3.6 Number.prototype.toFixed

- toFixed 메서드는 숫자를 반올림하여 문자열로 반환한다.
- 반올림하는 소수점 이하 자릿수를 나타내는 0~20 사이의 정수값을 인수로 전달할 수 있다.
- 인수를 생략하면 기본값 0이 지정된다.

### 28.3.7 Number.prtotype.toPrecision

- toPrecision 메서드는 인수로 전달받은 전체 자릿수까지 유효하도록 나머지 자릿수를 반올림하여 문자열로 반환하다.
- 인수로 전달받은 전체 자릿수로 표현할 수 없는 경우 지수 표기법으로 결과를 반환한다.
- 전체 자릿수를 나타내는 0~21 사이의 정수값을 인수로 전달할 수 있다. 인수를 생략하면 기본값이 0이 지정된다.

### 28.3.8 Number.prototype.toString

- toString 메서드는 숫자를 문자열로 변환하여 반환한다. 진법을 나타내는 2~36 사이의 정수값을 인수로 전달할 수 있다.
- 인수를 생략하면 기본값 10진법이 지정된다.