▣ 30장: Date

- UTC : 국제 표준시
- GMT : 그리니치 평균시
=> 초의 소수점 단위만 차이

KST = UTC + 9 (UTC보다 9시간 빠르다!)
09시 일때 UTC는 00시

30.1 Date 생성자 함수
Date 생성자 함수로 생성한 Date 객체 = 내부적으로 날짜와 시간을 나타내는 정수값을 가짐
Date 객체가 나타내는 날짜 & 시간까지의 **밀리초** 를 나타냄
1970년 1월 1일 00:00(UTC) 나타내는 Date 객체는 내부적으로 정수값 0을 가짐

Date객체는 기본적으로 현재 날짜 & 시간 나타내는 정수값 가짐
생성자 함수로 객체를 생성하는 방법은 다음과 같이 4가지가 있음
____30.1.1 new Date()
____30.1.2 new Date(milliseconds)
____30.1.3 new Date(dateString)
____30.1.4 new Date(year, month, day, hour, minute, second, millisecond])

30.2 Date 메서드
____30.2.1 Date.now
____30.2.2 Date.parse
____30.2.3 Date.UTC
____30.2.4 Date.prototype.getFullYear
____30.2.5 Date.prototype.setFullYear
____30.2.6 Date.prototype.getMonth
____30.2.7 Date.prototype.setMonth
____30.2.8 Date.prototype.getDate
____30.2.9 Date.prototype.setDate
____30.2.10 Date.prototype.getDay
____30.2.11 Date.prototype.getHours
____30.2.12 Date.prototype.setHours
____30.2.13 Date.prototype.getMinutes
____30.2.14 Date.prototype.setMinutes
____30.2.15 Date.prototype.getSeconds
____30.2.16 Date.prototype.setSeconds
____30.2.17 Date.prototype.getMilliseconds
____30.2.18 Date.prototype.setMilliseconds
____30.2.19 Date.prototype.getTime
____30.2.20 Date.prototype.setTime
____30.2.21 Date.prototype.getTimezoneOffset
____30.2.22 Date.prototype.toDateString
____30.2.23 Date.prototype.toTimeString
____30.2.24 Date.prototype.toISOString
____30.2.25 Date.prototype.toLocaleString
____30.2.26 Date.prototype.toLocaleTimeString
30.3 Date를 활용한 시계 예제
```
(function printNow()
{
    const today = new Date();

    const dayNames = [
        '(일요일)',
        '(월요일)',
        '(화요일)',
        '(수요일)',
        '(목요일)',
        '(금요일)',
        '(토요일)'
    ];
    const day = dayNames[today.getDay()];

    const year = today.getFullYear();
    const month = today.getMonth() + 1;
    const date = today.getDate();
    let hour = today.getHours();
    let minutes = today.getMinutes();
    let second = today.getSeconds();
    const ampm = hour >= 12 ? 'PM' : 'AM';

    hour %= 12;
    hour = hour || 12; //hour 0이면 12를 재할당

    minute = minute < 10 ? '0' + minute : minute;
    second = second < 10 ? '0' + second : second;

    const now = `${year}년 ${month}월 ${date}일 &{day} ${hour}:${minute}:${second}${ampm}`;
    console.log(now);

    setTimeout(printNow, 1000);
})

```
