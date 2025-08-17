# 43장 Ajax

## 43.1 Ajax란?

- 브라우저가 서버에 비동기 방식으로 데이터를 요청하고, 수신하는 방식을 의미함
- XMLHttpRequest 객체를 기반으로 동작함

## 43.2 JSON

- 클라이언트와 서버 간의 HTTP 통신을 위한 텍스트 데이터 포맷

### 43.2.1 JSON 표기 방식

- 키와 값으로 구성된 순수한 텍스트

### 43.2.2 JSON.stringify

- 객체나 배열을 JSON 포맷의 문자열로 변환하는 메서드
- 클라에서 서버로 객체를 전송하려면 객체를 문자열화 하는 직렬화를 거쳐야 함

### 43.2.3 JSON.parse

- JSON 포맷의 문자열을 객체로 변환함
- 역직렬화

## 43.3 XMLHttpRequest

### 43.3.1 XMLHttpRequest 객체 생성

### 43.3.2 XMLHttpRequest 객체의 프로퍼티와 메서드

- 다양함

### 43.3.3 HTTP 요청 전송

- 순서를 따라야 함
  1. XMLHttpRequest.prototype.open 메서드로 HTTP 요청 초기화
  2. 필요에 따라 XMLHttpRequest.prototype.setRequestHeader 메서드로 특정 HTTP 요청의 헤더 값을 설정
  3. XMLHttpRequest.prototype.send 메서드로 HTTP 요청을 전송

### 43.3.4 HTTP 응답 처리

- XMLHttpRequest 객체가 발생시키는 이벤트를 캐치해야 하는데 Web API라서 브라우저 환경에서 실행해야 함
