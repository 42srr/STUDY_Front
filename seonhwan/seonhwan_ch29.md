# 29장 Math
- 수학적 상수, 함수를 위한 프로퍼티, 메서드 제공하는 표준 빌트인 객체
- 생성자 함수가 아니므로 정적 프로퍼티 & 정적 메서드만 제공

## 29.1 Math 프로퍼티

### 29.1.1 Math.PI
- 원주율 PI 값 반환(3.141592...)

## 29.2 Math 메서드
- 숫자로 변환 불가한 인자 전달 혹은 인자 생략시 NaN

### 29.2.1 Math.abs
- 인수로 전달된 숫자의 절대값 반환
	```
	Math.abs('         -1    ');	// 1
	Math.abs('    ');				// 0
	Math.abs(null);					// 0
	Math.abs([]);					// 0
	Math.abs(["    -3"]);			// 3
	Math.abs(["    -3", "2"]);		// NaN
	Math.abs('1 a');				// NaN
	그 외 인자로 {}, undefined 등 숫자로 변환 불가 혹은 인자 생략시 NaN
	```

### 29.2.2 Math.round
- 인수로 전달된 숫자의 소수점 이하를 반올림한 정수 반환
	```
	Math.round(1.6);	// 2
	Math.round(-1.6);	// -2
	```

### 29.2.3 Math.ceil
- 인수로 전달된 숫자의 소수점 이하를 올림한 정수 반환
	```
	console.log(Math.ceil(1.4));	// 2
	console.log(Math.ceil(-1.4));	// -1
	console.log(Math.ceil(-1.9));	// -1
	```

### 29.2.4 Math.floor
- 인수로 전달된 숫자의 소수점 이하를 내림한 정수 반환
	```
	console.log(Math.floor(1.4));	// 1
	console.log(Math.floor(-1.4));	// -2
	console.log(Math.floor(-1.9));	// -2
	```

### 29.2.5 Math.sqrt
- 인수로 전달된 숫자의 제곱근 반환(음수 전달시 NaN)

### 29.2.6 Math.random
- [0, 1) 범위의 난수 반환

### 29.2.7 Math.pow
- Math.pow(밑, 지수) --> 밑^지수
- 인자 개수 2개 미만이면 NaN
	```
	console.log(Math.pow(Math.sqrt(2), "  -2"));	// 0.49999999999999994
	console.log(Math.pow(-2, "  -2"));				// 0.25
	```
- 지수 연산자 사용 권장 (ES7, 가독성 좋음)
	```
	2 ** 2;				// 4
	2 ** 2 ** 2 ** 2;	// 65536 --> 2^16
	--> 오른쪽부터 계산

	2 ** 2 ** 2 ** 2
	-> 2 ** 2 ** 4
	-> 2 ** 16
	-> 65536
	```

### 29.2.8 Math.max
- 전달받은 인수 중 가장 큰 수 반환(인수 미전달시 -Infinity 반환)
	```
	console.log(Math.max(1, 2, 3));			// 3
	console.log(Math.max([1], 7, ["-16"]));	// 7
	console.log(Math.max([], -7, ["-16"]));	// 0
	```

### 29.2.9 Math.min
- 전달받은 인수 중 가장 작은 수 반환(인수 미전달시 Infinity 반환)
	```
	console.log(Math.min(1, 2, 3));			// 1
	console.log(Math.min([1], 7, ["-16"]));	// -16
	console.log(Math.min([], -7, ["-16"]));	// -16
	```