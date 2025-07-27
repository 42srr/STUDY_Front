# 32장 String

## 32.1 String 생성자 함수

- String 객체는 표준 빌트인 객체이며 생성자 함수 객체
- new 연산자와 함께 호출하여 String 인스턴스 생성 가능
- String 래퍼 객체는 유사배열객체이면서 이터러블
- 배열과 유사하게 인덱스를 이용해 각 문자에 접근 가능
- 각 문자열은 원시 값이므로 변경 불가능
- String 생성자 함수의 인수로 문자열이 아닌 값을 넣으면 인수를 문자열로 강제 변환

## 32.2 length 프로퍼티

- 문자열의 문자 개수를 반환

## 32.3 String 메서드

- 배열에는 원본 배열을 직접 변경하는 메서드와 새로운 배열을 생성해서 반환하는 메서드가 있음
- String 객체는 언제나 새로운 문자열을 반환
- 문자열은 변경 불가능한 원시값이기 때문에 String 래퍼 객체도 읽기전용 객체로 제공

### 32.3.1 String.prototype.indexOf

- 대상 문자열에서 인수로 전달받은 문자열을 검색, 첫번째 인덱스를 반환

### 32.3.2 String.prototype.search

### 32.3.3 String.prototype.includes

### 32.3.4 String.prototype.startsWith

### 32.3.5 String.prototype.endswith

### 32.3.6 String.prototype.charAt

### 32.3.7 String.prototype.substring

### 32.3.8 String.prototype.slice

### 32.3.9 String.prototype.toUpperCase

### 32.3.10 String.prototype.toLowerCase

### 32.3.11 String.prototype.trim

### 32.3.12 String.prototype.repeat

### 32.3.13 String.prototype.replace

### 32.3.14 String.prototype.split
