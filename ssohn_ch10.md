# 10장 객체 리터럴

## 10.1 객체란?

- 원시 값을 제외한 나머지 값(함수, 배열, 정규 표현식 등)은 모두 객체
- 객체 타입은 다양한 타입의 값 (원시 값 또는 다른 객체)을 하나의 단위로 구성한 복합적인 자료구조
- 원시 타입의 값, 즉 원시 값은 변경 불가능한 값이지만 객체 타입의 값, 즉 객체는 변경 가능한 값이다.
- 객체는 0개 이상의 프로퍼티로 구성된 집합이며, 프로퍼티는 키와 값으로 구성된다.
- 자바스크립트에 사용할 수 있는 모든 값은 프로퍼티 값이 될 수 있다. 따라서 함수도 프로퍼티 값으로 사용할 수 있다.
- 프로퍼티 값이 함수일 경우, 일반 함수와 구분하기 위해 메서드라 부른다.
- 객체는 프로퍼티와 메서드로 구성된 집합체
  - 프로퍼티 : 객체의 상태를 나타내는 값
  - 메서드 : 프로퍼티(상태 데이터)를 참조하고 조작할 수 있는 동작

## 10.2 객체 리터럴에 의한 객체 생성

- 클래스 기반 객체지향 언어는 클래스를 사전에 정의하고 필요한 시점에 new 연산자와 함께 생성자를 호출하여 인스턴스를 생성하는 방식으로 객체를 생성한다.
  - 인스턴스
    - 클래스에 의해 생성되어 메모리에 저장된 실체를 말한다.
    - 객체지향 프로그래밍에서 객체는 클래스와 인스턴스를 포함한 개념이다.
- 자바스크립트는 다양한 객체 생성 방법을 지원한다.
  - 객체 리터럴
  - Object 생성자 함수
  - 생성자 함수
  - Object,create 메서드
  - 클래스 (ES6)
- 리터럴은 사람이 이해할 수 있는 문자 또는 약속된 기호를 사용하여 값을 생성하는 표기법을 말한다.
- 객체 리터럴은 중괄호 ({...}) 내에 0개 이상의 프로퍼티를 정의한다.
- 객체 리터럴의 중괄호는 코드 블록을 의미하지 않는다는 데 주의하자.
- 객체 리터럴의 닫는 중괄호 뒤에는 세미콜론을 붙인다.

## 10.3 프로퍼티

- **객체는 프로퍼티의 집합이며, 프로퍼티는 키와 값으로 구성된다.**
- 프로퍼티를 나열할 때는 쉼표(,)로 구분한다.
- 프로퍼티 키와 프로퍼티 값으로 사용할 수 있는 값은 다음과 같다.
  - 프로퍼티 키 : 빈 문자열을 포함하는 모든 문자열 또는 심벌 값
  - 프로퍼티 값 : 자바스크립트에서 사용할 수 있는 모든 값
- 프로퍼티 키는 프로퍼티 값에 접근할 수 있는 이름으로서 식별자 역할을 한다.
- 심벌 값도 프로퍼티 키로 사용할 수 있지만 일반적으로 문자열을 사용한다. 이때 프로퍼티 키는 문자열이므로 따옴표로 묶어야 한다.
- **식별자 네이밍 규칙을 따르지 않는 이름에는 반드시 따옴표를 사용해야 한다.**
- 가급적 식별자 네이밍 규칙을 준수하는 프로퍼티 키를 사용할 것을 권장한다.
- 프로퍼티 키에 문자열이나 심벌 값 외의 값을 사용하면 암묵적 타입 변환을 통해 문자열이 된다.
- 이미 존재하는 프로퍼 키를 중복 선언하면 나중에 선언한 프로퍼티가 먼저 선언한 프로퍼티를 덮어쓴다. 이때 에러가 발생하지 않는다.

## 10.4 메서드

- 프로퍼티 값이 함수일 경우 일반 함수와 구분하기 위해 메서드라 부른다.
- 메서드는 객체에 묶여 있는 함수를 의미한다.

## 10.5 프로퍼티 접근

- 프로퍼티 접근 방법

  - 마침표 프로퍼티 접근 연산자(.)를 사용하는 **마침표 표기법**
  - 대괄호 프로퍼티 접근 연산자([...])를 사용하는 **대괄호 표기법**
- 대괄호 표기법을 사용하는 경우 **대괄호 프로퍼티 접근 연산자 내부에 지정하는 프로퍼티 키는 반드시 따옴표로 감싼 문자열**이어야 한다. 그렇지 않으면 자바스크립트 엔진은 식별자로 해석한다.
- 객체에 존재하지 않는 프로퍼티에 접근하면 undefined를 반환한다.
- ```js
  var person = {
    'last-name': 'Lee',
    1: 10
  };
  ```
- 여러 프로퍼티 접근 방식과 그 결과

  - person.'last `-name'` → SyntaxError: Unexpected string
  - `person.last-name` → 브라우저 환경: NaN
  - `person.last-name` → Node.js 환경: ReferenceError: name is not defined
  - `person[last-name]` → ReferenceError: last is not defined
  - `person['last-name']` → 'Lee' (정상적으로 값 반환)
- 숫자 프로퍼티로 접근

  - `person.1` → SyntaxError: Unexpected number
  - `person.'1'` → SyntaxError: Unexpected string
  - `person[1]` → 10 (정상적으로 값 반환)
  - `person['1']` → 10 (정상적으로 값 반환)
- 환경별 차이점

  - 브라우저와 Node.js 환경에서 `person.last-name`의 결과가 다르게 나타나는 이유 설명
  - 브라우저에서는 `name`이 전역 변수로 존재하여 빈 문자열로 평가됨
  - Node.js에서는 `name`이 정의되지 않아 ReferenceError 발생
  - 결국 `person.last`가 undefined이고 `-name`이 연산되면서 결과가 달라짐

## 10.6 프로퍼티 값 갱신

- 이미 존재하는 프로퍼티에 값을 할당하면 프로퍼티 값이 갱신된다.

## 10.7 프로퍼티 동적 생성

- 존재하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 생성되어 추가되고 프로퍼티 값이 할당된다.

## 10.8 프로퍼티 삭제

- delete 연산자는 객체의 프로퍼티를 삭제한다.
- 이때 delete 연산자의 피연산자는 프로퍼티 값에 접근할 수 있는 표현식이어야 한다.
- 만약 존재하지 않는 프로퍼티를 삭제하면 아무런 에러 없이 무시된다.

## 10.9 ES6에서 추가된 객체 리터럴의 확장 기능

### 10.9.1 프로퍼티 축약 표현

- 객체 리터럴의 프로퍼티는 프로퍼티 키와 프로퍼티 값으로 구성된다.
- 프로퍼티 값은 변수에 할당된 값, 즉 식별자 표현식일 수도 있다.
- ES6에서는 프로퍼티 값으로 변수를 사용하는 경우 변수 이름과 프로퍼티 키가 동일한 이ㅁ일 때 프로퍼티 키를 생략할 수 있다.
- 이때 프로퍼티 키는 변수 이름으로 자동 생성된다.

### 10.9.2 계산된 프로퍼티 이름

- 문자열 또는 문자열로 타입 변환할 수 있는 값으로 평가되는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수도 있다.
- 단 프로퍼티 키로 사용할 표현식을 대괄호로 묶어야 한다.
- 이를 계산된 프로퍼티 이름이라 한다.
- ES6에서는 객체 리터럴 내부에서도 계산된 프로퍼티 이름으로 프로퍼티 키를 동적 생성할 수 있다.

### 10.9.3 메서드 축약 표현

- ES6에서는 메서드를 정의할 때 function 키워드를 생략한 축약 표현을 사용할 수 있다.
- ES6의 메서드 축약 표현으로 정의한 메서드는 프로퍼티에 할당한 함수와 다르게 동작한다.
