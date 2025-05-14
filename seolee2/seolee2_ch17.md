17장 생성자 함수에 의한 객체 생성
- 생성자 함수(constructor) : new 연산자와 함께 호출하여 객체(인스턴스)를 생성하는 함수
- JS의 빌트인 생성자 함수 : String, Number, Boolean, Function, Array, Date, RegExp, Promise

# 17.1 Object 생성자 함수

---

`new Object();`

- 빈 객체를 생성하여 반환, 프로퍼티 또는 메서드를 추가하여 객체 완성

# 17.2 생성자 함수

---

## 17.2.1 객체 리터럴에 의한 객체 생성 방식의 문제점

- 단 하나의 객체만 생성

⇒ 동일한 프로퍼티를 갖는 여러 개의 객체 생성 시 비효율적

## 17.2.2 생성자 함수에 의한 객체 생성 방식의 장점

- 템플릿(클래스)처럼 동일한 프로퍼티 구조의 객체를 간편하게 생성

```jsx
this
객체 자신의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수
this 바인딩은 함수 호출 방식에 따라 동적으로 결정됨

일반 함수로서 호출 : 전역 객체
메서드로서 호출 : 메서드를 호출한 객체(마침표 앞의 객체)
생성자 함수로서 호출 : 생성자 함수가 생성할 인스턴스

function foo() {
	console.log(this)
}

foo(); //window

const obj = { foo };
obj.foo; // obj

const inst new foo(); // inst
```

```jsx
new 연산자와 함께 호출하면 생성자 함수, 아니면 일반 함수로 동작

일반 함수로 호출되면 반환문이 없으므로 암묵적으로 undefined를 반환
일반 함수로 호출된 this는 전역 객체를 가리킴
```

## 17.2.3 생성자 함수의 인스턴스 생성 과정

1. 인스턴스 생성과 this 바인딩
    
    ```jsx
    암묵적으로 빈 객체 생성 this에 바인딩(식별자와 값을 연결하는 과정)
    // 런타임 이전에 실행
    ```
    
2. 인스턴스 초기화
    
    ```jsx
    생성자 함수의 코드가 한 줄씩 실행되어 this에 바인딩된 인스터스를 초기화
    ```
    
3. 인스턴스 반환
    
    ```jsx
    모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this를 암묵적으로 반환
    
    this가 아닌 객체를 명시적으로 반환하면 해당 객체를 반환
    // 원시 값 반환 시도 시 무시되고 this 반환
    ```
    

## 17.2.4 내부 메서드 [[Call]]과 [[Construct]]

- callable : 내부 메서드 [[Call]]을 갖는 함수 객체 = 호출할 수 있는 객체 = 함수
- constructor ↔ non-constructor : 생성자 함수로서 호출 가능 여부

## 17.2.5 constructor와 non-constructor의 구분

- constructor : 함수 선언문, 함수 표현식, 클래스
- non-constructor : 메서드(ES6 메서드 축약 표현으로 한정), 화살표 함수

## 17.2.6 new 연산자

- new 연산자와 함께 호출 시 생성자 함수로 동작 : [[Construct]] 호출 → constructor이어야 함
- 생성자 함수는 파스칼 케이스로 명명하여 구별

## 17.2.7 new.target

- new 연산자와 함께 생성자 함수로서 호출되었는지 확인 가능

```jsx
if (!new.target) {
	return new Circle(radius); // new와 함께 재귀호출하여 일반 함수로 호출되는 실수를 방지
}
```

```jsx
Objcet와 Function 생성자 함수는 new 연산자 여부과 관계없이 동일하게 동작
String, Number, Boolean은 new 연산자가 없으면 객체 대신 각 타입을 반환
```
