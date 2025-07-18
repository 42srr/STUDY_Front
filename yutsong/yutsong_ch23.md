# 23장 실행 컨텍스트

## 23.1 소스코드의 타입

- 전역 코드 : 전역에 존재하는 소스 코드. 함수, 클래스 등 내부 코드는 포함되지 않음
- 함수 코드 : 함수 내부의 소스 코드. 함수 내부에 중첩된 함수, 클래스 등 내부 코드는 포함되지 않음
- eval 코드 : 빌트인 전역함수인 eval 함수에 인수로 전달되어 실행되는 소스코드
- 모듈 코드 : 모듈 내부에 존재하는 코드. 모듈 내부의 함수, 클래스 등 내부 함수는 포함되지 않음

- 각 타입의 소스코드를 평가하여 실행 컨텍스트를 생성함

## 23.2 소스코드의 평가와 실행

- 모든 소스코드는 실행 전 평가 과정을 거침
- 평가 과정에서는 실행 컨텍스트 생성, 선언문 실행, 생성된 식별자를 스코프에 등록
- 실행 과정(= 런타임)에서는 선언문을 제외한 소스코드가 순차적으로 실행됨
- 실행에 필요한 정보는 실행 컨텍스트가 관리하는 스코프에서 검색해서 취득
- 소스코드의 실행 결과는 다시 실행 컨텍스트가 관리하는 스코프에 등록

## 23.3 실행 컨텍스트의 역할

1. 전역 코드 평가

- 평가 과정에서는 선언문만 먼저 실행
- 선언으로 생성된 전역 변수나 함수가 실행 컨텍스트가 관리하는 전역 스코프에 등록됨

2. 전역 코드 실행

- 평가가 끝나면 런타임 시작 및 코드 순차 실행
- 전역 변수에 값이 할당되고 함수가 호출됨
- 함수 호출 시 전역 코드 실행을 일시 중단하고 실행순서를 변경하여 함수 내부로 진입

3. 함수 코드 평가

- 함수 코드도 평가 과정을 거쳐야 함
- 매개변수와 지역변수가 실행 컨텍스트가 관리하는 지역 스코프에 등록됨
- 이때 arguments 객체가 지역 스코프에 등록되고, this 바인딩도 결정됨

4. 함수 코드 실행

- 함수 코드 평가 후 런타임 시작
- 매개변수와 지역 변수에 값 할당 및 console.log 메서드 호출

### 함수 호출 종료 시 호출 이전으로 돌아가기 위해 현재 실행중인 코드와 이전에 실행한 코드를 구분해야 함

- 스코프, 식별자, 코드 실행 순서 등의 관리가 필요하다는 뜻

1. 선언된 식별자를 스코프를 구분해서 등록, 상태변화를 지속 관리
2. 스코프는 중첩 관계에 의해 스코프 체인 형성
3. 실행순서를 변경하거나 되돌아갈 수 있어야 함

- 실행컨텍스트가 이런 역할을 함.
- 소스코드를 실행하는데 필요한 환경을 제공하고 실형 결과를 관리하는게 실행 컨텍스트
- 식별자와 스코프는 렉시컬 환경으로 관리, 코드 실행 순서는 스택으로 관리

## 23.4 실행 컨텍스트 스택

- 전역 실행 컨텍스트와 함수 실행 컨텍스트 등 실행 컨텍스트는 스택 자료구조로 관리됨

1. 전역 코드의 평가와 실행

- 먼저 전역 실행 컨텍스트를 생성, 스택에 푸시

2. 함수 코드의 평가와 실행

- 함수 호출 시 전역 코드 실행 일시 중단
- 코드 제어권이 함수 내부로 이동
- 함수 내부 코드 평가 및 실행 컨텍스트 생성, 스택에 푸시

3. 중첩 함수 코드의 평가와 실행

- 중첩 함수 호출시 기존 함수의 코드 실행이 일시 중단
- 코드 제어권이 중첩 함수 내부로 이동
- 중첩 함수 내부 코드 평가 및 실행 컨텍스트 생성, 스택에 푸시

4. 함수 코드로 복귀

- 중첩 함수가 종료되면 기존 함수로 코드 제어권 이동
- 중첩 함수 실행 컨텍스트를 스택에서 제거

5. 전역 코드로 복귀

- 함수 종료 시 제어권이 전역 코드로 이동
- 함수 실행 컨텍스트를 스택에서 제거

### 실행 컨텍스트 스택은 코드의 실행 순서를 관리

- 스택 최상위의 실행 컨텍스트는 언제나 현재 실행중인 코드의 실행 컨텍스트

## 23.5 렉시컬 환경

- 식별자와 식별자에 바인딩된 값, 상위 스코프에 대한 참조를 기록하는 자료구조
- 실행 컨텍스트를 구성하는 컴포넌트임
- 스코프와 식별자를 관리함
- 객체 형태의 스코프를 생성하여 식별자를 키로 등록, 관리함

1. 환경 레코드

- 스코프에 포함된 식별자를 등록하고 등록된 식별자에 바인딩된 값을 관리하는 저장소

2. 외부 렉시컬 환경에 대한 참조

- 외부 렉시컬 환경에 대한 참조 = 상위 스코프를 가리킴
- 스코프 체인(단방향 링크드 리스트)을 구현함

## 23.6 실행 컨텍스트의 생성과 식별자 검색 과정

### 23.6.1 전역 객체 생성

- 전역 코드가 평가되기 이전에 전역 객체 생성
- 빌트인 전역 프로퍼티와 빌트인 전역 함수, 표준 빌트인 객체 추가
- 특정 동작 환경을 위한 호스트 객체를 포함
- 전역 객체도 프로토타입 체인의 일원

### 23.6.2 전역 코드 평가

1. 전역 실행 컨텍스트 생성

- 비어있는 전역 실행 컨텍스트 생성 및 스택에 푸시

2. 전역 렉시컬 환경 생성

- 전역 렉시컬 환경 생성, 전역 실행 컨텍스트에 바인딩
- 환경 레코드와 외부 렉시컬 환경에 대한 참조 컴포넌트로 구성됨
  2.1 전역 환경 레코드 생성 : 전역 환경 레코드는 전역 스코프, 빌트인 전역 프로퍼티, 빌트인 전역 함수, 표준 빌트인 객체 제공

  2.1.1 객체 환경 레코드 생성 : 함수 선언문으로 정의된 전역 함수는 BindingObject를 통해 전역 객첵의 프로퍼티와 메서드가 됨

  2.1.2 선언적 환경 레코드 생성 : let, const 키워드로 선언한 전역 변수는 선언적 환경 레코드에 등록되고 관리됨

  2.2 this 바인딩 : 전역 환경 레코드의 [[GlobalThisValue]]내부 슬롯에 this가 바인딩됨
  2.3 외부 렉시컬 환경에 대한 참조 결정 : 외부 렉시컬 환경에 대한 참조는 상위 스코프를 가리킴.

### 23.6.3 전역 코드 실행

- 전역 코드 순차적으로 실행
- 변수 할당문이 실행되어 전역 변수에 값이 할당됨
- 함수도 호출됨
- 선언된 식별자인지 확인하는 과정을 거침
- 식별자 결정 : 실행중인 실행 컨텍스트에서 식별자를 검색하여 어느 스코프의 식별자를 참조할지 결정하는 과정

### 23.6.4 전역 함수 코드 평가

1. 함수 실행 컨텍스트 생성

- 전역 함수 실행 컨텍스트 생성
- 함수 렉시컬 환경 완성
- 전역 함수 실행 컨텍스트를 실행 컨텍스트 스택에 푸시

2. 함수 렉시컬 환경 생성

- 전역 함수 렉시컬 환경을 생성하고 전역 함수 실행 컨텍스트에 바인딩
  2.1. 함수 환경 레코드 생성

  - 함수 환경 레코드는 매개변수, arguments 객체, 함수 내부의 지역 변수와 중첩함수 등록, 관리

    2.2. this 바인딩

    - 함수 환경 레코드의 [[ThisValue]] 내부 슬롯에 this 바인딩
    - this는 전역 객체를 가리킴

      2.3. 외부 렉시컬 환경에 대한 참조 결정

      - 전역 함수 정의가 평가된 시점에 실행중인 실행 컨텍스트의 렉시컬 환경의 참조가 할당됨

### 23.6.5 전역 함수 코드 실행

- 코드 실행 시 식별자 결정을 위해 실행중인 실행 컨텍스트의 렉시컬 환경에서 식별자 검색
- 실행중인 실행 컨텍스트의 렉시컬 환경에서 식별자 검색이 불가능하면 외부 렉시컬 환경에 대한 참조가 가리키는 렉시컬 환경으로 이동하여 식별자 검색

### 23.6.6 중첩함수 코드 평가

- 중첩함수 호출 시 중첩함수 내부로 코드 제어권이 이동
- 중첩함수 코드를 평가
- 실행 컨텍스트와 렉시컬 환경 생성 과정은 전역 함수 평가와 동일

### 23.6.7 중첩함수 코드 실행

- 런타임 시작시 중첩 함수의 소스코드가 순차적으로 실행되기 시작

### 23.6.8 중첩함수 코드 실행 종료

- 실행 컨텍스트 스택에서 중첩함수 실행 컨텍스트 제거
- 전역함수 실행 컨텍스트가 실행중인 실행 컨텍스트가 됨

### 23.6.9 전역 함수 코드 실행 종료

### 23.6.10 전역 코드 실행 종료

## 23.7 실행 컨텍스트와 블록 레벨 스코프
