# ▣ 25장: 클래스
## 25.1 클래스는 프로토타입의 문법적 설탕인가?
- 프로토타입 기반 객체지향 언어 = 클래스가 필요없는 ~
- ES5, 생성자 함수 + 프로토타입 = 상속 구현 가능
- ES6, 자바/C#과 같은 객체 생성 메커니즘 제시
-- 기존 폐지, 새로운 메커니즘 제시? NOPE.
-- 문법적 설탕 : 사실 클래스 = 함수, 기존 프로토타입 기반 패턴을 클래스 기반 패턴처럼 사용 가능
- 클래스 vs 생성자 함수
항목 | 클래스 | 생성자 함수
new 연산자 | 없이 호출, 에러 발생 | 없으면 그냥 일반함수 취급
상속 | extends & super 키워드 | 해당 키워드 지원 X
호이스팅 | 발생하지 않는 것처럼 작동 | 표현 방식에 따라 다름
strict mode | 해제 불가 | 암묵 지정 X
열거 | false | true

- 클래스 = 새로운 객체 생성 메커니즘의 하나로 보기 

## 25.2 클래스 정의
- 파스칼 케이스 (선택)
- 표현식으로 정의 = 일급 객체
-- 무명의 리터럴로 생성 가능
-- 변수/ 자료구조 저장 가능
-- 함수의 매개변수 전달 가능
-- 함수의 반환값으로 사용

- 클래스 = 함수
- 0개 이상 메서드만 정의 가능
-- 생성자, 프로토타입 메서드, 정적 메서드

- 클래스 & 생성자 함수 정의방식 -> 형태적인 면 유사

## 25.3 클래스 호이스팅
- 소스코드 평가 과정, 런타임 이전 먼저 평가
- 
## 25.4 인스턴스 생성
## 25.5 메서드
### ____25.5.1 constructor
### ____25.5.2 프로토타입 메서드
### ____25.5.3 정적 메서드
### ____25.5.4 정적 메서드와 프로토타입 메서드의 차이
### ____25.5.5 클래스에서 정의한 메서드의 특징
## 25.6 클래스의 인스턴스 생성 과정
## 25.7 프로퍼티
### ____25.7.1 인스턴스 프로퍼티
### ____25.7.2 접근자 프로퍼티
### ____25.7.3 클래스 필드 정의 제안
### ____25.7.4 private 필드 정의 제안
### ____25.7.5 static 필드 정의 제안
## 25.8 상속에 의한 클래스 확장
### ____25.8.1 클래스 상속과 생성자 함수 상속
### ____25.8.2 extends 키워드
### ____25.8.3 동적 상속
### ____25.8.4 서브클래스의 constructor
### ____25.8.5 super 키워드
### ____25.8.6 상속 클래스의 인스턴스 생성 과정
### ____25.8.7 표준 빌트인 생성자 함수 확장
