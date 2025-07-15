30장 Date
```jsx
날짜와 시간을 위한 메서드를 제공하는 빌트인 객체이면서 생성자 함수

UTC : 국제 표준시
GMT와 거의 같음

KST = UTC + 9
```

# 30.1 Date 생성자 함수

---

```jsx
1970년 1월 1일 00:00:00(UTC)를 0인 기점으로 삼음
하루에 86,400,000(24h * 60m * 60s * 1000ms)
```

## 30.1.1 new Date()

```jsx
인수 없이 호출하면 현재 날짜와 시간을 가지는 Date 객체 반환
new 없이 호출하면 날짜 시간 정보를 나타내는 문자열 반환
```

## 30.1.2 new Date(milliseconds)

```jsx
기점에서 인수 밀리초 만큼 경과한 날짜와 시간을 나타내는 Date 객체 반환
```

## 30.1.3 new Date(dateString)

```jsx
Date.parse 메서드에 의해 해석 가능한 형식의 문자열을 전달하면
해당 날짜와 시간을 나타내는 Date 객체 반환

new Date('May 26, 2020 10:00:00');
new Date('2020/03/26/10:00:00');
```

## 30.1.4 new Date(year,month[,day,hour,minute,second,millisecond])

```jsx
연 월은 필수 // 지정하지 않으면 1970/1/1 000000
나머지는 0또는 1로 초기화
```

# 30.2 Date 메서드

---

## 30.2.1 Date.now

```jsx
기점으로 현재 시간까지 경과한 밀리초를 숫자로 반환
```

## 30.2.2 Date.parse

```jsx
인수로 전달된 시간까지의 밀리초를 숫자로 반환
```

## 30.2.3 Date.UTC

```jsx
UTC를 기점으로 인수 전달 시간까지를 반환
new Date(year,month[,day,hour,minute,second,millisecond]) 형식으로 인수를 사용해야 함
월은 0~11 0부터 시작
```

## 30.2.4 Date.prototype.getFullYear

```jsx
Date 객체의 연도를 나타내는 정수를 반환
```

## 30.2.5 Date.prototype.setFullYear

```jsx
Date 객체에 연도를 나타내는 정수 설정
옵션으로 월, 일도 설정 가능
```

## 30.2.6 Date.prototype.getMonth

```jsx
Date 객체의 월을 나타내는 0 ~ 11의 정수 반환
```

## 30.2.7 Date.prototype.setMonth

```jsx
Date 객체에 월을 나타내는 정수 설정
옵션으로 일 설정 가능
```

## 30.2.8 Date.prototype.getDate

```jsx
Date 객체의 날짜를 정수로 반환
```

## 30.2.9 Date.prototype.setDate

```jsx
Date 객체의 날짜 설정
```

## 30.2.10 Date.prototype.getDay

```jsx
요일을 나타내는 정수 반환 0 ~ 6 / 0 : 일요일
```

## 30.2.11 Date.prototype.getHours

```jsx
Date 객체의 시간을 정수로 반환
```

## 30.2.12 Date.prototype.setHours

```jsx
Date 객체에 시간을 설정
옵션으로 분 초 밀리초 가능
```

## 30.2.13 Date.prototype.getMinutes

## 30.2.14 Date.prototype.setMinutes

## 30.2.15 Date.prototype.getSeconds

## 30.2.16 Date.prototype.setSeconds

## 30.2.17 Date.prototype.getMilliseconds

## 30.2.18 Date.prototype.setMilliseconds

## 30.2.19 Date.prototype.getTime

```jsx
기점으로부터 Date 객체의 시간까지 경과된 밀리초를 반환
```

## 30.2.20 Date.prototype.setTime

```jsx
Date 객체에 기점에서 경과된 밀리초를 설정
```

## 30.2.21 Date.prototype.getTimezoneOffset

```jsx
UTC와 Date 객체에 지정된 로캘 시간과의 차이를 분 단위로 반환
```

## 30.2.22 Date.prototype.toDateString

```jsx
사람이 읽을 수 있는 형식의 문자열로 Date 객체의 날짜 반환
```

## 30.2.23 Date.prototype.toTimeString

```jsx
Date 객체의 시간을 문자열로 반환
```

## 30.2.24 Date.prototype.toISOString

```jsx
ISO 8601 형식으로 날짜와 시간을 표현한 문자열 반환
2020-07-24T03:30:00.000Z
```

## 30.2.25 Date.prototype.toLacaleString

```jsx
인수로 전달한 로캘을 기준으로 Date 객체의 날짜와 시간을 표현한 문자열을 반환
인수 생략 시 브라우저가 동작 중인 시스템의 로캘 적용
```

## 30.2.26 Date.prototype.toLocaleTimeString

```jsx
로캘 기준으로 시간을 표현한 문자열 반환
인수 생략 시 브라우저가 동작 중인 시스템의 로캘 적용
```

# 30.3 Date를 활용한 시계 예제

---
