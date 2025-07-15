28장 Number
```jsx
표준 빌트인 객체인 Number는 원시 타입인 숫자를 다룰 때 유용한 프로퍼티와 메서드 제공
```

# 28.1 Number 생성자 함수

---

```jsx
new 연산자와 함께 호출하여 Number 인스턴스 생성
인수가 없으면 [[NumberData]] 내부 슬롯에 0을 할당한 래퍼 객체 생성
인수가 숫자면 해당 값 할당
인수가 숫자가 아니면 숫자로 강제 변환
변환이 불가능하면 NaN

new 연산자를 사용하지 않으면 Number 인스턴스가 아닌 숫자를 반환
```

# 28.2 Number 프로퍼티

---

## 28.2.1 Number.EPSILON

```jsx
1과 1보다 가장 큰 숫자 중 가장 작은 숫자와의 차이
겁나 작으므로 부동소수점 오차 해결에 사용
```

## 28.2.2 Number.MAX_VALUE

```jsx
짱큰 숫자
하지만 Infinity가 더 큼
```

## 28.2.3 Number.MIN_VALUE

```jsx
가장 작은 양수 값
0보단 큼
```

## 28.2.4 Number.MAX_SAFE_INTEGER

```jsx
자바스크립트에서 안전하게 표현할 수 있는 가장 큰 정수값
9007199254740991
```

## 28.2.5 Number.MIN_SAFE_INTEGER

```jsx
가장 작은
-900719925470991
```

## 28.2.6 Number.POSITIVE_INFINITY

```jsx
양의 무한대 (=Infinity)
```

## 28.2.7 Number.NEGATIVE_INFINITY

```jsx
음의 무한대 (= -Infinity)
```

## 28.2.8 Number.NaN

```jsx
숫자가 아님을 나타내는 숫자값
Number.NaN = window.NaN
```

# 28.3 Number 메서드

---

## 28.3.1 Number.isFinite

```jsx
인수가 정상적인 유한수인지 검사하여 불리언 값으로 반환
NaN이면 false

빌트인 전역 함수 isFinite와 달리 암묵적 타입 변환 x
=> 숫자가 아니면 false
```

## 28.3.2 Number.isInteger

```jsx
인수가 정수인지 검사하여 불리언 값 반환
암묵적 타입 변환 x
```

## 28.3.3 Number.isNaN

```jsx
인수가 NaN인지 검사하여 불리언 값 반환
암묵적 타입 변환 x
```

## 28.3.4 Number.isSafeInteger

```jsx
암묵적 타입 변환 없이 안전한 정수값인지 검사하여 결과를 불리언 값으로 반환
```

## 28.3.5 Number.prototype.toExponential

```jsx
숫자를 지수 표기법으로 변환하여 문자열로 반환
숫자 리터럴과 함께 사용할 경우 에러
```

## 28.3.6 Number.prototype.toFixed

```jsx
숫자를 반올림하여 문자열로 반환
생략하면 기본값 0, 0~20 자리수 인수로 전달
```

## 28.3.7 Number.prototype.toPrecision

```jsx
인수로 받은 전체 자릿수까지 유효하도록 나머지 자릿수를 반올림하여 문자열로 반환
표현할 수 없는 경우 지수 표기법으로 반환
0~21의 정수값을 인수로 전달 가능
```

## 28.3.8 Number.prototype.toString

```jsx
숫자를 문자열로 변환하여 반환
진법을 나타내는 2~36을 인수로 전달 가능
기본 십진법
```
