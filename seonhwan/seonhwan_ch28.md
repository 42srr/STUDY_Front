# 28장 Number

## 28.1 Number 생성자 함수
- new 연산자와 함께 호출 : [[NumberData]] 내부 슬롯에 인수로 전달받은 숫자 할당한 Number 래퍼 객체 생성.
						단, 숫자가 아닌 값 전달시 인수로 숫자 강제 변환 후 할당.
						숫자로 변환 불가시 NaN 할당.
- new 연산자 없이 호출 : Number 인스턴스 X. 숫자 반환(숫자로 변환 불가한 인수 전달시 NaN).
						--> 숫자로 명시적 타입 변환시 사용

## 28.2 Number 프로퍼티

### 28.2.1 Number.EPSILON (ES6)
- 1과 1보다 큰 숫자 중에서 가장 작은 숫자와의 차이
- 약 2.2204460492503130808472633361816e-16
- 부동소수점으로 인해 발생하는 오차 해결 위해 사용(가장 널리 쓰이는 부동 소수점 표준 IEEE 754는 2진법 변환시 무한소수가 되어 미세한 오차 발생 경우가 생기는 구조적 한계 있음)
	```
	0.1 + 0.2 === 0.3	// false

	// 두 수 차의 절대값이 Number.EPSILON 미만이면 같은 수로 인정
	function isEqual(a, b) { return (Math.abs(a - b) < Number.EPSILON); }
	```

### 28.2.2 Number.MAX_VALUE
- JS에서 표현 가능한 가장 큰 양수값(1.7976931348623157e+308)
- Number.MAX_VALUE 보다 큰 숫자는 Infinity

### 28.2.3 Number.MIN_VALUE
- JS에서 표현 가능한 가장 작은 양수 값(5e-324)
- Number.MIN_VALUE 보다 작은 숫자는 0

### 28.2.4 Number.MAX_SAFE_INTEGER
- JS에서 '안전하게' 표현 가능한 가장 큰 정수값(9007199254740991)

### 28.2.5 Number.MIN_SAFE_INTEGER
- JS에서 '안전하게' 표현 가능한 가장 작은 정수값(-9007199254740991)

### 28.2.6 Number.POSITIVE_INFINITY
- Number.POSITIVE_INFINITY === Infinity	// true

### 28.2.7 Number.NEGATIVE_INFINITY
- Number.NEGATIVE_INFINITY === -Infinity	// true

### 28.2.8 Number.NaN
- 숫자가 아님(Not-a-Number)을 나타내는 숫자값
- window.NaN, NaN과 같음
- Number.NaN === window.NaN	// false
	--> JS에서 NaN은 자기 자신과도 같지 않은 유일한 값

## 28.3 Number 메서드

### 28.3.1 Number.isFinite (ES6)
- 정상적인 유한수 : true
- 숫자 X or Infinity or -Infinity : false
- 빌트인 전역 함수 isFinite는 인수를 숫자로 암묵적 타입 변환.
	But Number.isFinite는 변환 X.

### 28.3.2 Number.isInteger (ES6)
- 인수가 정수이면 true
- 숫자로 인수 타입 변환 X

### 28.3.3 Number.isNaN (ES6)
- 인수가 NaN이면 true
- 인수 숫자로 암묵적 타입 변환 X (빌트인 전역 함수 isNaN은 변환 O)
ex)
console.log(Number.isNaN(NaN))			// true
console.log(Number.isNaN(Number.NaN))	// true
console.log(Number.isNaN(global.NaN))	// true

### 28.3.4 Number.isSafeInteger (ES6)
- 인수로 전달된 숫자값이 안전한 정수이면 true
- 인수 숫자로 암묵적 타입 변환 X
- 안전한 정수값 : -(2^53 - 1) ~ +(2^53 - 1)

- 안전한 정수
	- 정수를 정확하게 표현하고 올바르게 비교할 수 있는 능력을 의미
	- IEEE-754 배정밀도 숫자로 정확히 표현될 수 있는 정수
	- JS는 IEEE 754 표준을 따르는 64bit 부동소수점 형식으로 모든 숫자를 표현.
		이 형식에서 52bit만이 mantissa(가수)를 나타내는데 사용
		--> 2^53 - 1 보다 큰 정수는 정확하게 표현될 수 없음
	```
	const x = Number.MAX_SAFE_INTEGER + 1;
	const y = Number.MAX_SAFE_INTEGER + 2;

	console.log(x === y); // true (수학적으로 틀림)
	--> 부동소수점 표현의 한계로 인해 두 값이 같은 방식으로 표현됨
	```

- 안전한 정수 벗어나는 경우 해결책
	```
	const toSafeInteger = (num) =>
		Math.round(
			Math.max(Math.min(num, Number.MAX_SAFE_INTEGER), Number.MIN_SAFE_INTEGER)
		);
	```

### 28.3.5 Number.prototype.toExponential
- 숫자를 지수 표기법으로 변환하여 문자열로 반환
- 인수로 소수점 이하로 표현할 자릿수 전달
- 지수 표기법 : e 앞에 있는 숫자에 10의 n승을 곱하는 형식으로 수를 표현 (소수점 앞은 1자리)
	```
	console.log((77.1289).toExponential());		// "7.71289e+1"
	console.log((77.1289).toExponential(3));	// "7.713e+1"

	1. 77.1289는 원시 타입(number)
	2. 임시 래퍼 객체 생성 : 원시 값을 해당하는 래퍼 객체(Number)로 감쌈
	3. 메서드 호출 후 임시 객체 삭제

	즉, 내부적으로
	let	temp = new Number(77.1289);
	let	result = temp.toExponential();
	temp = null;	// 임시 객체 삭제
	와 같은 작업이 일어남.

	console.log(77.toExponential(3));		// SyntaxError: Invalid or unexpected token
	- 숫자 뒤의 '.'은 부동 소수점 소수 구분 기호인지, 객체 프로퍼티 접근 연산자인지 의미가 모호함
	- JS엔진은 숫자 뒤의 '.'을 부동 소수점 숫자의 소수 구분 기호로 해석
		--> 에러 발생
		--> 그룹 연산자'()' 사용하면 됨

	console.log(77..toExponential(2));		// "7.70e+1"
	console.log(77.1289.toExponential(2));	// "7.713e+1"
	- 첫번째 '.'은 소수 구분 기호, 두번째 '.'은 객체 프로퍼티 접근 연산자로 해석 (숫자에 소수점은 하나만 존재함)

	console.log(77 .toExponential());		// "7.7e+1"
	- JS 숫자는 정수부와 소수부 사이에 공백 포함 불가
		--> 숫자 뒤의 '.' 뒤에 공백이 오면 '.'을 프로퍼티 접근 연산자로 해석
	```

### 28.3.6 Number.prototype.toFixed
- 숫자를 반올림하여 문자열로 반환
- 반올림하는 소수점 이하 자릿수(이 자릿수 까지 반올림)를 나타내는 0 ~ 20 사이 정수값을 인수로 전달(생략시 기본값 0)
	```
	console.log((12345.6789).toFixed());	// "12346"
	console.log((12345.6789).toFixed(1));	// "12345.7"
	console.log((12345.6789).toFixed(7));	// "12345.6789000"
	console.log((12345.6789).toFixed(-1));	// RangeError: toFixed() digits argument must be between 0 and 100
	```

### 28.3.7 Number.prototype.toPrecision
- 인수로 전달받은 전체 자릿수까지 유효하도록 나머지 자릿수를 반올림하여 문자열로 반환
- 인수로 전달받은 전체 자릿수로 표현 불가한 경우 지수 표기법으로 결과 반환
- 전체 자릿수를 나타내는 0 ~ 21 사이 정수값 전달 가능(생략시 기본값 0)

### 28.3.8 Number.prototype.toString
- 숫자를 문자열로 변환하여 반환
- 진법을 나타내는 2~36 사이 정수값을 인수로 전달 가능(생략시 기본값 10진법 적용)
	```
	console.log(10.8.toString());	// 10.8
	console.log((13).toString());	// 13
	console.log((4).toString(2));	// 100
	```
