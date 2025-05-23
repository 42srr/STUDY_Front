# 13장 스코프

## 13.1 스코프란?

- 스코프는 자바스크립트를 포함한 모든 프로그래밍 언어의 기본적이며 중요한 개념이다.
- var 키워드로 선언한 변수와 let 또는 const 키워드로 선언한 변수의 스코프도 다르게 동작한다.
- 변수는 코드의 가장 바깥 영역뿐 아니라 코드 블록이나 함수 몸체 내에서도 선언할 수 있다. 이때 코드블록이나 함수는 중첩될 수 있다.
- 모든 식별자 (변수 이름, 함수 이름, 클래스 이름 등)는 자신이 선언된 위치에 의해 다른 코드가 식별자 자신을 참조할 수 있는 유효 범위가 결정된다. 이를 스코프라 한다.
- 즉 스코프는 식별자가 유효한 범위를 말한다.
- 식별자 결정 : 자바스크립트 엔진은 이름이 같은 두 개의 변수 중에서 어떤 변수를 참조해야 할 것인지를 결정해야 함.
- 스코프란 자바스크립트 엔진이 식별자를 검색할 때 사용하는 규칙
- 식별자는 어떤 값을 구별할 수 있어야 하므로 유일 해야한다.
- 하나의 값은 유일한 식별자에 연결되어야 한다.
- 스코프를 통해 식별자인 변수 이름의 충돌을 방지하여 같은 이름의 변수를 사용할 수 있게 한다.
- 즉 스코프는 네임스페이스다.
- var 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언이 허용된다.
- let이나 const 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용하지 않는다.

## 13.2 스코프의 종류

### 13.2.1 전역과 전역 스코프

- 코드는 전역(global)과 지역(local)로 구분할 수 있다.
- 변수는 자신이 선언된 위치에 의해 자신이 유효한 범위인 스코프가 결정된다.
- 전역 변수는 어디서든지 참조할 수 있다.

### 13.2.2 지역과 지역 스코프

- 지역이란 함수 몸체 내부를 말한다
- 지역 변수는 자신의 지역 스코프와 하위 지역 스코프에서 유효하다.

## 13.3 스코프 체인

- 함수는 중첩될 수 있으므로 함수의 지역 스코프도 중첩될 수 있다.
- 이는 스코프가 함수의 중첩에 의해 계층적 구조를 갖는다는 것을 의미한다.
- 스코프가 계층적으로 연결된 것을 스코프 체인이라 한다.
- 변수를 참조할 때 자바스크립트 엔진은 스코프 체인을 통해 변수를 참조하는 코드의 스코프에서 시작하여 상위 스코프 방향으로 이동하며 선언된 변수를 검색한다

### 13.3.1 스코프 체인에 의한 변수 검색

- 자바스크립트 엔진은 스코프 체인을 따라 변수를 참조하는 코드의 스코프에서 시작해서 상위 스코프 방향으로 이동하며 선언된 변수를 검색한다.
- 상위 스코프에서 유효한 변수는 하위 스코프에서 자유롭게 참조할 수 있지만 하위 스코프에서 유효한 변수를 상위 스코프에서 참조할 수 없다는 것을 의미한다.

### 13.3.2 스코프 체인에 의한 함수 검색

- 스코프를 식별자를 검색하는 규칙이라고 표현하는 편이 좀 더 적합하다.

## 13.4 함수 레벨 스코프

- 지역은 함수 몸체 내부를 말하고 지역은 지역 스코프를 만든다
- 이는 코드 블록이 아닌 함수에 의해서만 지역 스코프가 생성된다는 의미이다.
- var 키워드로 선언된 변수는 오로지 함수의 코드 블록(함수 몸체)만을 지역 스코프로 인정한다. 이러한 특성을 함수 레벨 스코프라 한다.
- ```js
  var x = 1;
  if (true) {
  	// var 키워드로 선언된 변수는 함수의 코드블록 (함수몸체)만을 지역 스코프로 인정한다.
  	// 함수 밖에서 var 키워드로 선언된 변수는 코드 블록 내에서 선언 되었다 할지라도 모두 전역변수다.
  	// 따라서 x는 전역변수다. 이미 선언된 전역변수 x가 있으므로 x변수는 중복 선언된다.
  	// 이는 의도치 않게 변수 값이 변경되는 부작용을 발생시킨다.
  	var x = 10;
  }
  console.log(x); // 10
  ```

## 13.5 렉시컬 스코프

- ```js
  var x = 1;
  function foo() {
  	var x = 10;
  	bar();
  }

  function bar() {
  	console.log(x);
  }

  foo()；// ? -> 1
  bar(); // ? -> 1
  ```
- 자바스크립트는 렉시컬 스코프를 따른다.
- 렉시컬 스코프는 함수를 어디서 호출했는지가 아니라 함수를 어디서 정의했는지에 따라 상위 스코프를 결정한다.
- 함수가 호출된 위치는 상위 스코프 결정에 어떠한 영향도 주지 않는다.
- 즉 함수의 상위 스코프는 언제나 자신이 정의된 스코프다.
- 이처럼 함수의 상위 스코프는 함수 정의가 실행될 때 정적으로 결정된다.
- 함수 정의 (함수 선언문 또는 함수 표현식)가 실행되어 생성된 함수 객체는 이렇게 결정된 상위 스코프를 기억한다. 함수가 호출될 때마다 함수의 상위 스코프를 참조할 필요가 있기 때문이다.
