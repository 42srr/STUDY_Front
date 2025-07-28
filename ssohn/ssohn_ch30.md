# 30장 Date

## 30.1 Date 생성자 함수

- Date는 생성자 함수다.
- Date 생성자 함수로 생성한 Date 객체는 내부적으로 날짜와 시간을 나타내는 정수값을 갖는다.
- Date 생성자 함수로 생성한 Date 객체는 기본적으로 현재 날짜와 시간을 나타내는 정수값을 가진다.
- Date 생성자 함수로 객체를 생성하는 방법은 4가지가 있다.

### 30.1.1 new Date()

- Date 생성자 함수를 인수 없이 new 연산자와 함께 호출하면 현재 날짜와 시간을 가지는 Date 객체를 반환한다.
- Date 객체는 내부적으로 날짜와 시간을 나타내는 정수값을 갖지만 Date 객체를 콘솔에 출력하면 기본적으로 날짜와 시간 정보를 출력한다.
- Date 생성자 함수를 new 연산자 없이 호출하면 Date 객체를 반환하지 않고 날짜와 시간 정보를 나타내는 문자열을 반환한다.

### 30.1.2 new Date(milliseconds)

- Date 생성자 함수에 숫자 타입의 밀리초를 인수로 전달하면 1970년 1월 1일 00:00:00(UTC)을 기점으로 인수로 전달된 밀리초만큼 경과한 날짜와 시간을 나타내는 Date 객체를 반환한다.

### 30.1.3 new Date(dateString)

- Date 생성자 함수에 날짜와 시간을 나타내는 문자열을 인수로 전달하면 지정된 날짜와 시간을 나타내는 Date 객체를 반환한다.
- 이때 인수로 전달한 문자열은 Date.parse 메서드에 의해 해석 가능한 형식이어야 한다.

### 30.1.4 new Date(year, month[, dayy, hour, minute, second, millisecond])

- Date 생성자 함수에 연, 월, 일, 시, 분, 초, 밀리초를 의미하는 숫자를 인수로 전달하면 지정된 날짜와 시간을 나타내는 Date 객체를 반환한다.
- 이때 연, 월은 반드시 지정해야 한다.
- 지정하지 않은 옵션 정보는 0또는 1로 초기화된다.

## 30.2 Date 메서드

### 30.2.1 Date.now

- 1970년 1월 1일 00:00:00(UTC)을 기점으로 현재 시간까지 경과한 밀리초를 숫자로 반환한다.

### 30.2.2 Date.parse

- 1970년 1월 1일 00:00:00(UTC)을 기점으로 인수로 전달된 지정 시간(newDate(dateString)의 인수와 동일한 형식)까지의 밀리초를 숫자로 반환한다.

### 30.2.3 Date.UTC

- 1970년 1월 1일 00:00:00(UTC)을 기점으로 인수로 전달된 지정 시간까지의 밀리초를 숫자로 반환한다.
- Date.UTC 메서드는 new Date(year, month[, dayy, hour, minute, second, millisecond])와 같은 형식의 인수를 사용해야 한다.
- Date.UTC 메서드의 인수는 로컬 타임(KST)이 아닌 UTC로 인식된다.
- month는 월을 의미하는 0~11까지의 정수다. 0부터 시작하므로 주의가 필요하다.

### 30.2.4 Date.prototype.getFullYear

- Date 객체의 연도를 나타내는 정수를 반환한다.

### 30.2.5 Date.prototype.setFullYear

- Date 객체에 연도를 나타내는 정수를 설정한다. 연도 이외에 옵션으로 월, 일도 설정할 수 있다.

### 30.2.6 Date.prototype.getMonth

- Date 객체의 월을 나타내는 0 ~ 11의 정수를 반환한다. 1월은 0, 12월은 11이다.

### 30.2.7 Date.prototype.setMonth

- Date 객체에 월을 나타내는 0 ~ 11의 정수를 설정한다. 1월은 0, 12월은 11이다.

### 30.2.8 Date.prototype.getDate

- Date 객체의 날짜 (1 ~ 31)를 나타내는 정수를 반환한다.


### 30.2.9 Date.prototype.setDate

- Date 객체에 날짜 (1 ~ 31)를 나타내는 정수를 설정한다.

### 30.2.10 Date.prototype.getDay

- Date 객체의 요일 (0 ~ 6)을 나타내는 정수를 반환한다. 일요일이 0 토요일이 6

### 30.2.11 Date.prototype.getHours

- Date 객체의 시간 (0 ~ 23)을 나타내는 정수를 반환한다.

### 30.2.12 Date.prototype.setHours

- Date 객체에 시간 (0 ~ 23)을 나타내는 정수를 설정한다. 시간 이외에 옵션으로 분, 초, 밀리초도 설정할 수 있다.

### 30.2.13 Date.prototype.getMinutes

- Date 객체의 분 (0 ~ 59)을 나타내는 정수를 반환한다.

### 30.2.14 Date.prototype.setMinutes

- Date 객체에 분 (0 ~ 59)을 나타내는 정수를 설정한다. 분 이외에 옵션으로 초, 밀리초도 설정할 수 있다.

### 30.2.15 Date.prototype.getSeconds

- Date 객체의 초 (0 ~ 59)를 나타내는 정수를 반환한다.

### 30.2.16 Date.prototype.setSeconds

- Date 객체에 초 (0 ~ 59)를 나타내는 정수를 설정한다. 초 이외에 옵션으로 밀리초도 설정할 수 있다.

### 30.2.17 Date.prototype.getMilliseconds

- Date 객체의 밀리초 (0 ~ 999)를 나타내는 정수를 반환한다.

### 30.2.18 Date.prototype.setMilliseconds

- Date 객체에 밀리초(0 ~ 999)를 나타내는 정수를 설정한다.

### 30.2.19 Date.prototype.getTime

- 1970년 1월 1일 00:00:00(UTC)을 기점으로 Date 객체의 시간까지 경과된 밀리초를 반환한다.

### 30.2.20 Date.prototype.setTime

- Date 객체에  1970년 1월 1일 00:00:00(UTC)을 기점으로 경과된 밀리초를 설정한다.

### 30.2.21 Date.prototype.getTimezoneOffset

- UTC와 Date 객체에 지정된 locale 시간과의 차이를 분 단위로 반환한다. KST는 UTC에 9시간을 더한 시간이다. 즉, UTC = KST - 9h다

### 30.2.22 Date.prototype.toDateString

- 사람이 읽을 수 있는 형식의 문자열로 Date 객체의 날짜를 반환한다.

### 30.2.23 Date.prototype.toTimeString

- 사람이 읽을 수 있는 형식으로 Date 객체의 시간을 표현한 문자열을 반환한다.

### 30.2.24 Date.prototype.toISOString

- ISO 8601 형식으로 Date 객체의 날짜와 시간을 표현한 문자열을 반환한다.

### 30.2.25 Date.prototype.toLocaleString

- 인수로 전달한 locale을 기준으로 Date 객체의 날짜와 시간을 표현한 문자열을 반환한다 인수를 생략한 경우 브라우저가 동작 중인 시스템의 locale을 적용한다.

### 30.2.26 Date.prototype.toLocaleTimeString

- 인수로 전달한 locale을 기준으로 Date 객체의 시간을 표현한 문자열을 반환한다. 인수를 생략한 경우 브라우저가 동작 중인 시스템의 locale을 적용한다.

## 30.3 Date를 활용한 시계 예제