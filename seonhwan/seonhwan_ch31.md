# 31장 RegExp

## 31.1 정규 표현식이란?
- 정규 표현식(regular expression)
	- 일정한 패턴을 가진 문자열의 집합을 표현하기 위해 사용하는 형식 언어
	- 문자열 대상으로 패턴 매칭 기능(특정 패턴과 일치하는 문자열 검색, 추출, 치환 등)
	- 반복문, 조건문 없이 패턴 정의하고 테스트 가능
- 형식 언어(formal language) : 특정한 법칙들에 따라 적절하게 구성된 문자열들의 집합
```
const tel = '010-1234-5678';

// 정규 표현식 리터럴은 RegExp 객체를 생성
// 아래 세가지는 동일 의미
const regExp1 = new RegExp('^\\d{3}-\\d{4}-\\d{4}$');
const regExp2 = new RegExp(/^\d{3}-\d{4}-\d{4}$/);
const regExp3 = /^\d{3}-\d{4}-\d{4}$/;

console.log(typeof regExp1, typeof regExp2, typeof regExp3);			// object object object
console.log(regExp1.test(tel), regExp2.test(tel), regExp3.test(tel));	// true true true
```

## 31.2 정규 표현식의 생성
- 정규 표현식 리터럴(일반적), RegExp 생성자 함수로 생성 가능
- 정규 표현식 리터럴 : /패턴/플래그 (앞뒤 '/'는 각각 시작, 종료 기호)
- RegExp 생성자 : new RegExp(pattern[, flags])
```
const 	target = 'Is this all there is?';
let		regExp = /is/;

// 아래 결과 모두 true
console.log(/is/i.test(target));
console.log(new RegExp(/is/i).test(target));	// ES6
console.log(new RegExp('is', 'i').test(target));
console.log(new RegExp(/is/, 'i').test(target));

regExp = new RegExp(/is/, 'ig');
console.log(target.match(regExp));

/*
Nullish Coalescing 연산자 '??' (ECMAScript 2020(ES11))
- 왼쪽 피연산자가 null 또는 undefined 일 때만 오른쪽 피연산자 반환(아니면 왼쪽 피연산자 반환)
- 즉, 왼쪽 피연산자가 값이 확정되어 있는 변수인 경우만 그대로 반환
*/
const count = (str, char) => (str.match(new RegExp(char, 'gi')) ?? []).length;

console.log(count('Is this all there is?', 'is'));	// 3
console.log(count('Is this all there is?', 'abc'));	// 0
console.log(1 ?? [1, 2, 3]);						// 1
console.log(null ?? [1, 2, 3]);						// [1, 2, 3]
console.log(undefined ?? "abc");					// "abc"
```

## 31.3 RegExp 메서드

### 31.3.1 RegExp.prototype.exec
- 인수로 전달받은 문자열에 대해 정규 표현식 패턴을 검색하여 매칭 결과를 배열로 반환(결과 없으면 null)
- g 플래그(문자열 내 모든 패턴 검색)를 지정해도 첫 번째 매칭 결과만 반환
```

```

### 31.3.2 RegExp.prototype.test

### 31.3.3 RegExp.prototype.match

## 31.4 플래그

## 31.5 패턴

### 31.5.1 문자열 검색

### 31.5.2 임의의 문자열 검색

### 31.5.3 반복 검색

### 31.5.4 OR 검색

### 31.5.5 NOT 검색

### 31.5.6 시작 위치로 검색

### 31.5.7 마지막 위치로 검색

## 31.6 자주 사용하는 정규표현식

### 31.6.1 특정 단어로 시작하는지 검사

### 31.6.2 특정 단어로 끝나는지 검사

### 31.6.3 숫자로만 이루어진 문자열인지 검사

### 31.6.4 하나 이상의 공백으로 시작하는지 검사

### 31.6.5 아이디로 사용 가능한지 검사

### 31.6.6 메일 주소 형식에 맞는지 검사

### 31.6.7 핸드폰 번호 형식에 맞는지 검사

### 31.6.8 특수 문자 포함 여부 검사
