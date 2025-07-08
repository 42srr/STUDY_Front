# 30장 Date
- 날짜와 시간(연, 월, 일, 시, 분, 초, 밀리초)을 위한 메서드 제공하는 표준 빌트인객체 & 생성자 함수
- KST(한국 표준시) = UTC(협정 세계시 ≈ GMT(그리니치 평균시)) + 9h
- 현재 날짜, 시간은 JS 코드가 실행된 시스템의 시계에 의해 결정

## 30.1 Date 생성자 함수
- Date 객체는 내부적으로 날짜와 시간을 나타내는 정수값 가짐
	(1970.01.01 00:00:00(UTC)부터 Date 객체가 나타내는 날짜, 시간까지의 밀리초)
- Date 객체 콘솔 출력시 기본적으로 날짜, 시간 정보 출력
- new 연산자 없이 호출시 날짜, 시간 정보 나타내는 문자열 반환

### 30.1.1 new Date()
- 현재 날짜, 시간 가짐
```
console.log(new Date());	// Tue Jul 08 2025 08:28:50 GMT+0900 (대한민국 표준시)
```

### 30.1.2 new Date(milliseconds)
- 인수로 숫자 타입의 밀리초 전달시 1970.01.01 00:00:00(UTC) 기점으로 그 밀리초만큼 경과한 날짜와 시간 가짐
```
// Thu Jan 01 1970 09:00:01 GMT+0900 (대한민국 표준시)
// KST 기준 출력이라 +9h 
console.log(new Date(1000));
```

### 30.1.3 new Date(dataString)
- 날짜와 시간을 나타내는 문자열을 인수로 전달시 그에 해당하는 Date 객체 반환
- 인수로 전달한 문자열은 Data.parse 메서드에 의해 해석 가능한 형식이어야 함
```
/* 해석 가능 형식 */

// Wed Feb 26 2020 10:00:00 GMT+0900 (대한민국 표준시)
console.log(new Date('Feb, 26, 2020, 10:0:0'));
console.log(new Date('Feb 26 2020 10:00:00'));
console.log(new Date('Feb 26, 2020 10:00:00'));

// Mon Mar 02 2020 10:00:00 GMT+0900 (대한민국 표준시)
// 일 지정시 1~31 범위. 만약 해당 월 마지막 일 넘어갈경우 넘어간 날만큼 반영되어 날짜 지정됨
console.log(new Date('Feb 31, 2020 10:00:00'));

// Thu Mar 26 2020 10:00:00 GMT+0900 (대한민국 표준시)
console.log(new Date('2020/3/26/10:00:00:00'));

/* 해석 불가능 형식 */

const date = new Date('dsf1000');

date.getMonth();								// NaN
Date('dsf1000');								// 현재 날짜, 시간 문자열 반환
console.log(new Date('dsf1000'));				// Invalid Date
console.log(new Date('May 32, 2020 10:00:00'));	// Invalid Date (범위 초과)
```

### 30.1.4 new Date(year, month[, day, hour, minute, second, millisecond])
- 지정한 파라미터에 해당하는 날짜, 시간에 대한 Date 객체 반환
- year, month는 반드시 지정해야함
- 지정하지 않은 옵션 정보는 0 또는 1(범위 내 최소값)으로 초기화됨
- 인수 숫자로 암묵적 타입 변환됨
```
# 파라미터
- year : 연을 나타내는 1900년 이후의 정수. 0부터 99는 1900부터 1999로 처리됨.
- month : 월을 나타내는 0 〜 11까지의 정수	// 주의: 0부터 시작, 0 = 1월
- day : 일을 나타내는 1 〜 31까지의 정수
- hour : 시를 나타내는 0 〜 23까지의 정수
- minute: 분을 나타내는 0 〜 59까지의 정수
- second : 초를 나타내는 0 〜 59까지의 정수
- millisecond : 밀리초를 나타내는 0 〜 999까지의 정수
```

## 30.2 Date 메서드

### 30.2.1 Date.now
- 1970.01.01 00:00:00(UTC) 기점 현재 시간까지 경과한 밀리초 반환
```
new Date(Data.now);	// 현재 날짜, 시각
```

### 30.2.2 Date.parse
- 1970.01.01 00:00:00(UTC) 기점 인수로 전달된 지정 시간까지의 밀리초 반환
- new Data(dateString)의 인수와 동일 형식
```
console.log(new Date(Date.parse('Jan 1, 1970 00:00:00 UTC')));
console.log(new Date(Date.parse('Jan 1, 1970 09:00:00 UTC')));	// KST
console.log(new Date(Date.parse('Jan 1, 1970 00:00:00 KST')));	// Invalid Date (KST 타임존 약어 지원 X)
console.log(new Date(Date.parse('1970/01/01/09:00:00')));		// KST
```

### 30.2.3 Date.UTC
- 1970.01.01 00:00:00(UTC) 기점 인수로 전달된 지정 시간까지의 밀리초 반환
- new Date(year, month[, day, hour, minute, second, millisecond])의 인수와 동일 형식
- 인수는 로컬타임(KST)가 아닌 UTC로 인식됨
- 인수 숫자로 변환됨(숫자 변환 불가능한 인수 전달시 NaN)

### 30.2.4 Date.prototype.getFullYear
- Date 객체 연도 반환

### 30.2.5 Date.prototype.setFullYear
- Date 객체 연도 설정
- 옵션으로 월, 일도 설정 가능
```
const today = new Date();

today.setFullYear(2000);
console.log(today.getFullYear());	// 2000
console.log(today);					// Sat Jul 08 2000 17:38:55 GMT+0900 (대한민국 표준시)
today.setFullYear(1900, 0, 1);
console.log(today.getFullYear());	// 1900
console.log(today);					// Mon Jan 01 1900 17:38:55 GMT+0827 (대한민국 표준시)
```

### 30.2.6 Date.prototype.getMonth
- Date 객체 월 반환 (0 ~ 11)

### 30.2.7 Date.prototype.setMonth
- Date 객체 월 설정
- 옵션으로 일도 설정 가능
```
const today = new Date();

today.setMonth(0);
console.log(today.getMonth());	// 0
today.setMonth(1, 12);
console.log(today.getMonth());	// 1
console.log(today);				// Wed Feb 12 2025 17:42:34 GMT+0900 (대한민국 표준시)
```

### 30.2.8 Date.prototype.getDate
- Date 객체 날짜 반환 (1 ~ 31)

### 30.2.9 Date.prototype.setDate
- Date 객체 날짜 설정

### 30.2.10 Date.prototype.getDay
- Date 객체 요일 반환 (0(일) ~ 6(토))
- Date.prototype.setDay는 미존재

### 30.2.11 Date.prototype.getHours
- Date 객체 시간 반환 (0 ~ 23)

### 30.2.12 Date.prototype.setHours
- Date 객체 시간 설정 (0 ~ 23)
- 시간 외에 옵션으로 분, 초, 밀리초도 설정 가능
```
const today = new Date();

today.setHours(7);
console.log(today.getHours());	// 7
today.setHours(0, 0, 0, 0);
console.log(today.getHours());	// 0
console.log(today);				// Tue Jul 08 2025 00:00:00 GMT+0900 (대한민국 표준시)
```

### 30.2.13 Date.prototype.getMinutes
- Date 객체 분 반환 (0 ~ 59)

### 30.2.14 Date.prototype.setMinutes
- Date 객체 분 설정
- 옵션으로 초, 밀리초도 설정 가능

### 30.2.15 Date.prototype.getSeconds
- Date 객체 초 반환 (0 ~ 59)

### 30.2.16 Date.prototype.setSeconds
- Date 객체 초 설정
- 옵션으로 밀리초도 설정 가능

### 30.2.17 Date.prototype.getMilliseconds
- Date 객체 밀리초 반환 (0 ~ 999)

### 30.2.18 Date.prototype.setMilliseconds
- Date 객체 밀리초 설정

### 30.2.19 Date.prototype.getTime
- 1970.01.01 00:00:00(UTC) 기점 Date 객체 시간까지 경과된 밀리초 반환

### 30.2.20 Date.prototype.setTime
- Date 객체에 1970.01.01 00:00:00(UTC) 기점 경과된 밀리초 설정

### 30.2.21 Date.prototype.getTimezoneOffset
- UTC와 Date 객체에 지정된 locale 시간과의 차이를 분 단위로 반환 (UTC = KST - 9h)
	(UTC - locale)
- Date.prototype.setTimezoneOffset는 미존재
```
console.log(new Date().getTimezoneOffset() / 60);	// -9
```

### 30.2.22 Date.prototype.toDateString
- 사람이 읽을 수 있는 형식의 문자열로 Date 객체 날짜 반환
```
const today = new Date('2020/7/24/12:30');

console.log(today.toString());		// Fri Jul 24 2020 12:30:00 GMT+0900 (대한민국 표준시)
console.log(today.toDateString());	// Fri Jul 24 2020
```

### 30.2.23 Date.prototype.toTimeString
- 사람이 읽을 수 있는 형식의 문자열로 Date 객체 시간 반환
```
const today = new Date('2020/7/24/12:30');

console.log(today.toString());		// Fri Jul 24 2020 12:30:00 GMT+0900 (대한민국 표준시)
console.log(today.toTimeString());	// 12:30:00 GMT+0900 (대한민국 표준시)
```

### 30.2.24 Date.prototype.toISOString
- ISO 8601 형식으로 Date 객체의 날짜와 시간 표현한 문자열 반환
- ISO 8601 : 날짜와 시간과 관련된 데이터 교환을 다루는 국제 표준

### 30.2.25 Date.prototype.toLocaleString

### 30.2.26 Date.prototype.toLocaleTimeString

## 30.3 Date를 활용한 시계 예제
