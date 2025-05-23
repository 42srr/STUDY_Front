# 19장 프로토타입

- 자바스크립트는 멀티 패러다임 프로그래밍 언어
- ES6에서 클래스가 도입되었지만 프로토타입 기반의 객체지향 언어의 문법적 설탕
- 자바스크립트의 거의 모든 것은 객체

## 19.1 객체지향 프로그래밍

- 객체의 집합으로 프로그램을 표현하려는 프로그래밍 패러다임을 의미
- 추상화 : 다양한 속성 중 프로그램에 필요한 속성만 간추려 표현하는 것
- 속성을 통해 여러 개의 값을 하나의 단위로 구성한 복합적인 자료구조가 객체
- 객체의 상태를 나타내는 데이터와, 상태 데이터를 조작할 수 있는 동작을 하나의 논리적인 단위로 묶어 생각
- 객체는 상태 데이터와 동작을 하나의 논리적인 단위로 묶은 복합적인 자료 구조
- 상태 데이터가 프로퍼티, 동작이 메서드

## 19.2 상속과 프로토타입

- 상속은 어떤 객체의 프로퍼티 또는 메서드를 다른 객체가 상속받아 사용하도록 하는 것
- 자바스크립트는 프로토타입 기반 상속을 구현
- 생성자 함수는 동일한 프로퍼티 구조를 갖는 객체를 여러개 생성할 때 유용함
- 하지만 동일한 생성자 함수에 의해 생성된 모든 인스턴스가 동일한 메서드를 중복 소유하는 것은 낭비임
- 이를 상속으로 해결 가능
- 생성자 함수가 생성한 모든 인스턴스는 자신의 프로토타입인 상위 객체에 있는 상위객체명.prototype의 모든 메서드와 프로퍼티를 상속받음
- 따라서 내용이 동일한 메서드는 상속을 통해 공유할 수 있음

## 19.3 프로토타입 객체

- 프로토타입 객체는 객체간 상속을 구현하기 위해 사용
- 프로토타입은 어떤 객체의 상위 객체로써, 다른 객체에 공유 프로퍼티(메서드 포함)를 제공
- 하위 객체는 상속받은 상위 객체의 프로퍼티를 자신의 프로퍼티처럼 사용 가능
- 모든 객체는 [[Prototype]]이라는 내부 슬롯을 가지며 이 내부 슬롯의 값은 프로토타입의 참조임
- [[Prototype]]에 저장되는 프로토타입은 객체 생성 방식에 의해 결정됨
- 모든 객체는 하나의 프로토타입을 가짐
- 모든 프로토타입은 생성자 함수와 연결됨
- [[Prototpye]] 내부 슬롯에는 직접 접근 불가, `__proto__` 접근자 프로퍼티를 통해 간접 접근 가능
- 프로토타입은 자신의 constructor 프로퍼티를 통해 생성자 함수에 접근 가능
- 생성자 함수는 자신의 prototype 프로퍼티를 통해 프로토타입에 접근 가능

### 19.3.1 `__proto__`접근자 프로퍼티

- 모든 객체는 `__proto__`접근자 프로퍼티를 통해 자신의 프로토타입, 즉 [[Prototype]] 내부 슬롯에 간접 접근 가능

#### `__proto__`는 접근자 프로퍼티다.

- 내부 슬롯은 프로퍼티가 아님
- JS는 원칙적으로 내부 슬롯과 내부 메서드에 직접 접근하거나 호출하는 방법을 제공하지 않음
- 접근자 프로퍼티는 자체적으로는 값 프로퍼티를 갖지 않고, 접근자 함수인 [[Get]], [[Set]] 프로퍼티 어트리뷰트로 구성된 프로퍼티임

#### `__proto__`접근자 프로퍼티는 상속을 통해 사용된다.

- `__proto__`는 객체가 직접 소유하지 않고, Object.prototype의 프로퍼티임
- 모든 객체는 상속을 통해 Object.prototype.`__proto__` 접근자 프로퍼티 사용 가능
- Object.prototype : 모든 객체는 프로토타입의 계층 구조인 프로토타입 체인에 묶여 있음. 자바스크립트 엔진은 객체의 프로퍼티에 접근할때, 해당 객체에 접근하려는 프로퍼티가 없다면 `__proto__`접근자 프로퍼티가 가리키는 참조를 따라 자신의 부모 역할을 하는 프로토타입의 프로퍼티를 순차적으로 검색함

#### `__proto__`접근자 프로퍼티를 통해 프로토타입에 접근하는 이유

- [[Prototype]] 내부 슬롯의 값인 프로토타입에 접근할때 상호 참조에 의해 프로토타입 체인이 생성되는 것을 방지하기 위해 접근자 프로퍼티를 사용하는 것임
- 프로토타입 체인은 단방향 링크드 리스트로 구현되어야 함

#### `__proto__`접근자 프로퍼티를 코드 내에서 직접 사용하는 것은 권장하지 않는다.

- 모든 객체가 `__proto__`접근자 프로퍼티를 사용할 수 있는 것은 아니기 때문에
- 코드 내에서 `__proto__`접근자 프로퍼티를 직접 사용하는 것은 권장하지 않음
- 대신 Object.getPrototypeOf 메서드나 Object.setPrototypeOf 메서드를 사용

### 19.3.2 함수 객체의 prototype 프로퍼티

- 함수 객체만이 소유하는 prototype 프로퍼티는 생성자 함수가 생성할 인스턴스의 프로토타입을 가리킴
- non-constructor는 prototype 프로퍼티를 소유하지 않으며 프로토타입도 생성하지 않음
- 모든 객체가 가지고 있는 `__proto__`접근자 프로퍼티와 함수 객체만이 가지고 있는 prototype 프로퍼티는 결국 동일한 프로토타입을 가리킴

### 19.3.3 프로토타입의 constructor 프로퍼티와 생성자 함수

- 모든 프로토타입은 constructor 프로퍼티를 가짐
- constructor 프로퍼티는 prototype 프로퍼티로 자신을 참조하고 있는 생성자 함수를 가리킴

## 19.4 리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입

- 생성자 함수에 의해 생성된 인스턴스는 프로토타입의 constructor 프로퍼티에 의해 생성자 함수와 연결
- constructor 프로퍼티가 가리키는 생성자 함수는 인스턴스를 생성한 생성자 함수
- 리터럴 표기법에 의해 생성된 객체도 프로토타입이 존재하지만 constructor 프로퍼티가 가리키는 생성자 함수가 반드시 객체를 생성한 생성자 함수라고 단정할 수 없음
- 프로토타입과 생성자 함수는 단독으로 존재할 수 없고 언제나 쌍으로 존재함

## 19.5 프로토타입의 생성 시점

- 모든 객체는 생성자 함수와 연결되어 있음
- 프로토타입은 생성자 함수가 생성되는 시점에 더불어 생성됨

### 19.5.1 사용자 정의 생성자 함수와 프로토타입 생성 시점

- constructor는 함수 정의가 평가되어 함수 객체를 생성하는 시점에 프로토타입도 더불어 생성됨
- non-constructor는 프로토타입이 생성되지 않음
- 생성된 프로토타입은 constructor 프로퍼티만 갖는 객체임
- 프로토타입도 객체이므로 프로토타입도 자신의 프로토타입을 가짐

### 19.5.2 빌트인 생성자 함수와 프로토타입 생성 시점

- 빌트인 생성자 함수도 생성 시점에 프로토타입이 생성됨
- 생성된 프로토타입은 빌트인 생성자 함수의 prototype 프로퍼티에 바인딩 됨
- 전역 객체 : 코드가 실행되기 이전 단계에 자바스크립트 엔진에 의해 생성되는 특수한 객체

## 19.6 객체 생성 방식과 프로토타입의 결정

- 객체 생성 방식
  1. 객체 리터럴
  2. Object 생성자 함수
  3. 생성자 함수
  4. Object.create 메서드
  5. 클래스(ES6)
- 모든 객체는 추상연산 OrdinaryObjectCreate에 의해 생성됨

### 19.6.1 객체 리터럴에 의해 생성된 객체의 프로토타입

- 객체 리터럴로 생성된 객체의 프로토타입은 Object.prototype임

### 19.6.2 Object 생성자 함수에 의해 생성된 객체의 프로토타입

- Object 생성자 함수를 호출하면 객체 리터럴과 마찬가지로 추상연산 OrdinaryObjectCreate가 호출됨
- 객체 리터럴 방식은 객체 리터럴 내부에 프로퍼티를 추가함
- Object 생성자 함수 방식은 일단 빈 객체를 생성하고 프로퍼티를 추가함

### 19.6.3 생성자 함수에 의해 생성된 객체의 프로토타입

- new 연산자와 함께 생성자 함수를 호출하는 경우에도 추상연산 OrdinaryObjectCreate가 호출됨
- 프로토타입도 객체이므로 프로퍼티를 추가/삭제할 수 있음

## 19.7 프로토타입 체인

- JS는 객체의 프로퍼티에 접근하려고 할 때 해당 객체에 접근하려는 프로퍼티가 없으면 [[Prototype]] 내부 슬롯의 참조를 따라 자신의 부모 역할을 하는 프로토타입의 프로퍼티를 순차적으로 검색
- 프로토타입 체인은 상속을 구현하는 메커니즘
- call 메서드 : this로 사용할 객체를 전달하면서 함수를 호출
- 프로토타입 체인의 최상위에 위치한 객체는 언제나 Object.prototype임
- Object.prototpye의 프로토타입인 [[Prototype]] 내부 슬롯의 값은 null임
- 종점에서도 프로퍼티 검색이 안되면 undefined를 반환함
- 프로토타입 체인은 상속과 프로퍼티 검색을 위한 메커니즘임
- 프로퍼티가 아닌 식별자는 스코프 체인에서 검색
- 스코프 체인은 식별자 검색을 위한 메커니즘
- 스코프 체인과 프로토타입 체인은 서로 협력해서 식별자와 프로퍼티를 검색

## 19.8 오버라이딩과 프로퍼티 섀도잉

- 프로토타입이 소유한 프로퍼티를 프로토토타입 프로퍼티라고 함
- 인스턴스가 소유한 프로퍼티를 인스턴스 프로퍼티라고 함
- 프로토타입 프로퍼티와 같은 이름의 프로퍼티를 인스턴스에 추가하면 인스턴스 프로퍼티로 추가
- 상속 관계에 의해 프로퍼티가 가려지는 현상이 프로퍼티 섀도잉
- 오버라이딩 : 상위 클래스가 가지고 있는 메서드를 하위 클래스가 재정의하여 사용하는 방식
- 오버로딩 : 함수의 이름은 동일하지만 매개변수 정보가 다른 메서드를 구현하고, 매개변수에 의해 메서드를 구별하여 호출하는 방식

## 19.9 프로토타입의 교체

- 프로토타입은 임의의 다른 객체로 변경할 수 있음
- 부모 객체인 프로토타입을 동적으로 변경할 수 있다는 뜻
- 객체 간의 상속 관계도 동적으로 변경 가능
- 프로토타입은 생성자 함수 또는 인스턴스에 의해 교체 가능

### 19.9.1 생성자 함수에 의한 프로토타입의 교체

- 프로토타입 교체시 constructor 프로퍼티와 생성자 함수 간의 연결이 파괴됨

### 19.9.2 인스턴스에 의한 프로토타입의 교체

- 프로토타입은 생성자 함수의 prototype 프로퍼티 뿐만 아니라 인스턴스의 `__proto__`접근자 프로퍼티를 통해 접근 가능
- 인스턴스의 `__proto__`접근자 프로퍼티를 통해 프로토타입 교체 가능
- 생성자 함수의 prototype 프로퍼티에 다른 임의의 객체를 바인딩하는 것은 미래에 생성할 인스턴스의 프로토타입을 교체하는 것
- `__proto__`접근자 프로퍼티를 통해 프로토타입을 교체하는 것은 이미 생성된 객체의 프로토타입을 교체하는 것
- 프로토타입으로 교체한 객체에는 constructor 프로퍼티가 없으므로 constructor 프로퍼티와 생성자 함수 간의 연결이 파괴됨

## 19.10 instanceof 연산자

- 이항 연산자로써 좌변에 객체를 가리키는 식별자, 우변에 생성자 함수를 가리키는 식별자를 피연산자로 받음
  ` 객체 instanceof 생성자함수`
- 우변의 생성자 함수의 prototype에 바인딩된 객체가 좌변의 객체의 프로토타입 체인 상에 존재하면 true로 평가됨
- 생성자 함수의 prototype에 바인딩된 객체가 프로토타입 체인 상에 존재하는지 확인함

## 19.11 직접 상속

### 19.11.1 Object.create에 의한 직접 상속

- Object.create 메서드는 명시적으로 프로토타입을 지정하여 새로운 객체를 생성
- Object.create도 추상연산 OrdinaryObjectCreate를 호출함
- Object.create 메서드는 첫 번째 매개변수에 전달한 객체의 프로토타입 체인에 속하는 객체를 생성함

### 19.11.2 객체 리터럴 내부에서 `__proto__`에 의한 직접 상속

- ES6에서는 객체 리터럴 내부에서 `__proto__`접근자 프로퍼티를 사용해서 직접 상속을 구현할 수 있음

## 19.12 정적 프로퍼티 / 메서드

- 정적 프로퍼티 / 메서드는 생성자 함수로 인스턴스를 생성하지 않아도 참조 / 호출할 수 있는 프로퍼티 / 메서드를 말함
- 생성자 함수가 생성한 인스턴스는 자신의 프로토타입 체인에 속한 객체의 프로토타입 / 메서드에 접근할 수 있음
- 정적 프로퍼티 / 메서드는 인스턴스의 프로토타입 체인에 속한 객체의 프로퍼티 / 메서드가 아니므로 인스턴스로 접근할 수 없음
- 인스턴스 / 프로토타입 메서드 내에서 this를 사용하지 않으면 그 메서드는 정적 메서드로 변경 가능
- 인스턴스가 호출한 인스턴스 / 프로토타입 메서드 내에서 this는 인스턴스를 가리킴
- 프로토타입 메서드를 호출하려면 인스턴스 생성 필요
- 정적 메서드는 인스턴스 생성 없이도 호출 가능

## 19.13 프로퍼티 존재 확인

### 19.13.1 in 연산자

- in 연산자는 객체 내에 특정 프로퍼티가 존재하는지 여부를 확인함
- 확인 대상 객체의 프로퍼티와 확인 대상 객체가 상속받은 프로토타입의 프로퍼티도 확인함

### 19.13.2 Object.prototype.hasOwnProperty 메서드

- Object.prototype.hasOwnProperty 메서드를 사용해도 프로퍼티 존재 확인 가능

## 19.14 프로퍼티 열거

### 19.14.1 for...in 문

- 객체의 모든 프로퍼티를 순회하며 열거할 수 있음
- 순회 대상 객체의 프로퍼티 뿐만 아니라 상속받은 프로토타입의 프로퍼티까지 열거함
- [[Enumerable]]의 값이 false면 열거 불가능

### 19.14.2 Object.keys / values / entries 메서드

- 상속받은 프로퍼티를 제외하고 객체 자신의 프로퍼티만 열거하려면 Object.keys / values/ entries 메서드를 사용하는게 권장됨
