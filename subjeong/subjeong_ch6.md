[모던 자바스크립트 Deep Dive]
[6장] 데이터 타입

---

### 1. 숫자 타입

- 숫자, 정수와 실수 구분 없이 하나의 숫자 타입만 존재 (원시 타입)

- 배정밀도 64비트 부동소수점 형식(ECMAScript)을 따라 모든 수를 실수로 처리

  - 정수로 표시된다 해도 사실은 실수라는 것

- 2,8,16진수 데이터 타입을 제공하지 않음

  - 값 참조 시 모두 10진수로 해석됨

- 그 외의 특별한 값

  - Infinity : 양의 무한대

  - -Infinity : 음의 무한대

  - NaN : 산술 연산 불가(not-a-number)

---

### 2. 문자열 타입

- 문자열 (원시 타입)

- 0개 이상의 16비트 유니코드 문자(UTF-16)의 집합으로 문자 표현

- 작은 따옴표(''), 큰따옴표(""), 백틱(``)으로 텍스트를 감싸 문자열을 토큰과 구분분

---

### 3. 템플릿 리터럴

- 멀티라인 문자열, 표현식 삽입, 태그드 템플릿 등 편리한 문자열 처리 기능을 제공

- 런타임에 일반 문자열로 변환되어 처리

- 백틱(``) 사용

#### 멀티라인 문자열

- 멀티라인 문자열 내에서는 이스케이프 시퀀스 없이도 줄바꿈(공백)이 허용됨

- 일반 문자열 내에서는 이스케이프 시퀀스로 줄바꿈(공백)을 표현

  - \0, \b, \f, \n(라인 피드), \r(캐리지 리턴), \t, \v, \uXXXX, \', \", \\

#### 표현식 삽입

- 문자열 연산자 '+'를 사용해 연결

  - 피연산자 중 하나 이상이 문자열인 경우 문자열 연결 연산자로 동작

  - 그 외의 경우 덧셈 연산자로 동작

- ${ }으로 표현식을 감싸서 삽입

  - 표현식의 평가 결과가 문자열이 아니더라도 문자열로 타입이 강제 변환되어 삽입

---

### 4. 불리언 타입

- 논리적 참(true)과 거짓(false) (원시 타입)

---

### 5. undefined 타입

- var 키워드로 선언된 변수에 암묵적으로 할당되는 값 (원시 타입)

- 자바스크립트 엔진이 변수를 초기화하여 값이 없음을 나타내는 데에 사용

  - 개발자는 값이 없음을 나타내는 데에 null을 사용

---

### 6. null 타입

- 값이 없다는 것을 의도적으로 명시할 때 사용하는 값 (원시 타입)

- 이전에 할당되어 있던 값에 대한 참조를 명시적으로 제거, 가비지 콜렉션으로 처리

- 함수가 유효한 값을 반환할 수 없는 경우에도 null 반환

---

### 7. 심벌 타입

- ES6에서 추가된 7번째 타입 (원시 타입)

- 다른 값과 중복되지 않는 유일무이한 값

- 주로 객체의 유일한 프로퍼티 키를 만들기 위해 사용

- 심벌 이외의 원시 타입은 리터럴로 생성, 심벌을 Symbol() 함수로 생성

  - `obj[Symbol('key')] = 'value';`

---

### 8. 객체 타입

- 객체, 함수, 배열 등 (객체 타입)

- 원시 타입과 객체 타입은 근본적으로 다름

- 자바스크립트를 이루고 있는 거의 모든 것이 객체임

---

### 9. 데이터 타입의 필요성

- 값을 저장할 때 확보해야 하는 '메모리 공간의 크기를 결정'

- 값을 참조할 때 한 번에 읽어 들여야 할 '메모리 공간의 크기를 결정'

- 메모리에서 읽어 들인 '2진수를 어떻게 해석할지 결정'

#### 데이터 타입에 의한 메모리 공간의 확보와 참조

- 자바스크립트 엔진은 데이터 타입에 따라 정해진 크기의 메모리 공간을 확보

- 심벌 테이블

  - 컴파일러 또는 인터프리터는 심벌 테이블이라고 부르는 자료 구조를 통해 식별자를 키로 바인딩된 값의 메모리 주소, 데이터 타입, 스코프 등을 관리리

#### 데이터 타입에 의한 값의 해석

- 메모리에서 읽어들인 2진수는 데이터 타입에 따라 다르게 해석됨

  - 0100 0001은 숫자로 65, 문자열로 'A'

---

### 10. 동적 타이핑

#### 동적 타입 언어와 정적 타입 언어

- 동적 타입 언어

  - 자바스크립트, 파이썬, PHP, 루비, 리스프, 펄 등

- 동적 타이핑

  - 자바스크립트의 변수는 선언이 아닌 할당에 의해 타입이 결정(타입 추론)

  - 재할당에 의해 변수 타입이 언제든지 동적으로 변할 수 있음

#### 동적 타입 언어와 변수

- 동적 타입 언어는 유연성은 높지만 신뢰성은 떨어짐

  - 변화하는 변수 값을 추적하기 어려움

  - 값을 확인하기 전까지 타입을 확신할 수 없음

- 변수 사용 시 주의사항

  - 변수는 꼭 필요한 경우에 한해 제한적으로 사용할 것

  - 변수의 유효 범위(스코프)는 최대한 좁게 만들어 부작용을 억제할 것

  - 전역 변수는 최대한 사용하지 않을 것

  - 변수보다는 상수를 사용해 값의 변경을 억제할 것

  - 변수 이름은 목적, 의미를 파악할 수 있도록 네이밍할 것

---
