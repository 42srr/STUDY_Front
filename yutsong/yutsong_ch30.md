# 30장 Date

- Date는 표준 빌트인 객체
- 날짜와 시간을 위한 메서드를 제공함
- 표준 빌트인 객체이면서 생성자 함수
- UTC는 국제 표준시(= GMT)
- KST는 UTC + 9시간
- 현재 날짜와 시간은 JS 코드가 실행된 시스템의 시계에 의해 결정

## 30.1 Date 생성자 함수

- Date 생성자 함수로 생성한 Date 객체는 내부적으로 날짜와 시간을 나타내는 정수값을 가짐
- 정수값은 UTC 기준 1970년 1월1일 00:00:00을 기점으로 Date 객체가 나타내는 날짜와 시간까지의 밀리초를 나타냄
- 기본적으로 Date 객체는 현재 날짜와 시간을 나타내는 정수값을 가짐

### 30.1.1 new Date()

- 인수 없이 new 연산자와 함께 Date를 호출하면 현재 날짜와 시간을 갖는 Date 객체를 반환함
- new 없이 호출하면 날짜와 시간 정보를 나타내는 문자열을 반환함

### 30.1.2 new Date(milliseconds)

- 인수로 숫자타입의 밀리초를 전달하면 1970년 기점으로부터 인수로 전달된 밀리초만큼 경과한 날짜와 시간을 나타내는 Date 객체를 반환

### 30.1.3 new Date(dateString)

- 날짜와 시간을 나타내는 문자열을 인수로 전달하면 지정된 날짜와 시간을 나타내는 Date 객체를 반환

### 30.1.4 new Date(year, month[, day, hour, minute, second, millisecond])

- 연, 월, 일, 시, 분, ... 등등을 나타내는 숫자를 인수로 전달하면 지정된 날짜와 시간을 나타내는 Date 객체를 반환
- 년, 월은 꼭 지정해줘야 하고 나머지는 따로 지정안해도 됨
- 따로 지정안한 옵션은 0또는 1로 초기화

## 30.2 Date 메서드

### 30.2.1 Date.now

- 1970년 기점으로부터 현재 시간까지 경과한 밀리초를 숫자로 반환

### 30.2.2 Date.parse

- 1970년 기점으로부터 인수로 전달된 지정 시간까지의 밀리초를 숫자로 반환

### 30.2.3 Date.UTC

- 1970년 기점으로부터 지정시간까지의 밀리초를 숫자로 반환

### 30.2.4 Date.prototype.getFullYear

- Date 객체의 연도를 나타내는 정수를 반환

### 30.2.5 Date.prototype.setFullYear

- Date 객체에 연도를 나타내는 정수를 설정

### 30.2.6 Date.prototype.getMonth

### 30.2.7 Date.prototype.setMonth

### 30.2.8 Date.prototype.getDate

### 30.2.9 Date.prototpye.setDate

### 30.2.10 Date.prototype.getDay

### 30.2.11 Date.prototype.getHours

### 30.2.12 Date.prototype.setHours

### 30.2.13 Date.prototype.getMinutes

### 30.2.14 Date.prototype.setMinutes

### 30.2.15 Date.prototype.getSeconds

### 30.2.16 Date.prototype.setSeconds

### 30.2.17 Date.prototype.getMilliseconds

### 30.2.18 Date.prototype.setMilliseconds

### 30.2.19 Date.prototype.getTime

### 30.2.20 Date.prototype.setTime

### 30.2.21 Date.prototype.getTimezoneOffset

### 30.2.22 Date.prototype.toDateString

### 30.2.23 Date.prototype.toTimeString

### 30.2.24 Date.prototype.toISOString

### 30.2.25 Date.prototype.toLocaleString

### 30.2.26 Date.prototype.toLocaleTimeString

## 30.3 Date를 활용한 시계 예제
