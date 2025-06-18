# 20장 strict mode

## 20.1 strict mode란?
- 암묵적 전역 : 선언하지 않은 변수에 값 할당시 JS 엔진이 전역 객체에 그 프로퍼티를 동적 생성(변수처럼 사용 가능) --> 오류 발생 원인이 될 가능성 큼
- strict mode : JS 문법을 더 엄격히 적용하여 오류 발생 가능성 높거나 JS 에닞ㄴ 최적화 작업에 문제 일으킬 수 있는 코드에 대해 명시적 오류 발생시킴
- ES6에서 도입된 클래스와 모듈은 기본적으로 strict mode가 적용됨

## 20.2 strict mode의 적용
- 전역의 선두 또는 함수 몸체의 선두에 'use strict'; 를 추가
- 전역 선두에 추가시 스크립트 전체에 적용
- 함수 몸체 선두에 추가시 해당 함수 및 중첩 함수에 적용

## 20.3 전역에 strict mode를 적용하는 것은 피하자
- 전역에 적용한 strict mode는 스크립트 단위로 적용됨
- strict mode 스크립트와 non-strict mode 스크립트 혼용은 오류 발생 가능성

## 20.4 함수 단위로 strict mode를 적용하는 것도 피하자
- strict mode 함수와 non-strict mode 함수 혼용은 바람직하지 않음
- 모든 함수에 일일이 strict 적용은 번거로움
- --> strict mode는 즉시 실행 함수로 감싼 스크립트 단위로 적용하는 것이 바람직

## 20.5 strict mode가 발생시키는 에러
- strict mode 적용시 에러가 발생하는 대표적인 사례 4가지

### 20.5.1 암묵적 전역
- 선언하지 않은 변수 참조 --> ReferenceError

### 20.5.2 변수, 함수, 매개변수의 삭제
- delete 연산자로 변수, 함수, 매개변수 삭제 --> SyntaxError

### 20.5.3 매개변수 이름의 중복
- 중복된 매개변수 이름 사용 --> SyntaxError

### 20.5.4 with 문의 사용
- with 문 사용 --> SyntaxError

## 20.6 strict mode 적용에 의한 변화

### 20.6.1 일반 함수의 this
- strict mode에서 함수를 일반 함수로서 호출하면 this에 undefined가 바인딩됨

### 20.6.2 arguments 객체
- strict mode에서 매개변수에 전달된 인수를 재할당하여 변경해도 arguments 객체에 반영 X
