# 17장 생성자 함수에 의한 객체 생성

## 17.1 Object 생성자 함수
- 생성자 함수 : new 연산자와 함께 호출하여 객체를 생성하는 함수
	--> 생성자 함수에 의해 생성된 객체를 인스턴스(instance)라 함
- Object 생성자 함수 --> 빈 객체 생성하여 반환
- 빌트인 생성자 함수 : Object, String, Number, Boolean, Function, Array, Date, RegExp, Promise 등

## 17.2 생성자 함수

### 17.2.1 객체 리터럴에 의한 객체 생성 방식의 문제점
- 단 하나의 객체만 생성
--> 동일한 프로퍼티를 갖는 객체 여러개 생성하는 경우 매번 같은 프로퍼티 기술해야함
--> 비효율적

```
ex)
const circlel = {
	radius: 5,
 	getDiameter() {
		return 2 * this.radius;
	}
}；
```

### 17.2.2 생성자 함수에 의한 객체 생성 방식의 장점
- 프로퍼티 구조가 동일한 객체 여러 개 간편하게 생성 가능
- 함수를 new 연산자와 함께 호출하면 해당 함수는 생성자 함수로 동작
```
ex)
function Circle(radius) {
	// 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킴
	this.radius = radius;
	this.getDiameter = function () { 
		return 2 * this.radius;
	}；
}

const circlel = new Circle(5);
const circle2 = new Circle(10);
```

### 17.2.3 생성자 함수의 인스턴스 생성 과정
- 1) 인스턴스 생성과 this 바인딩
암묵적으로 빈 객체가 생성되며 이 객체는 this에 바인딩됨 --> 런타임 이전에 실행
- 2) 인스턴스 초기화
생성자 함수 내부 코드가 실행되며 this에 바인딩되어있는 인스턴스 초기화
(프로퍼티, 메서드 추가 및 초기화)
- 3) 인스턴스 반환
생성자 함수 내부 처리가 모두 끝나면 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환됨
(this가 아닌 객체를 명시적으로 반환하면 this 대신 그 객체가 반환)
(명시적으로 원시값 반환시 무시되고, this가 반환)

### 17.2.4 내부 메서드 [[Call]]과 [[Construct]]
- 함수는 일반 객체가 가지고 있는 내부 슬롯, 내부 메서드를 모두 가짐
	--> 함수는 객체(일반 객체와 동일하게 동작 가능)
- 일반 객체는 호출 불가 but 함수 객체는 호출 가능
	--> 함수 객체는 함수로써 동작하기 위한  [[Environment]], [[FormalParameters]] 등의 내부 슬롯과 [[Call]], [[Construct]] 등의 내부 메서드를 추가로 보유
- 일반 함수로 호출시 [[Call]], new 연산자와 함께 생성자 함수로 호출시 [[Construct]]가 호출됨
- [[Call]]을 갖는 함수 객체를 callable(호출 가능. 모든 함수 객체가 가짐.), [[Construct]]를 갖는 함수 객체를 constructor(생성자 함수로 호출 가능), [[Construct]]를 갖지 않는 함수 객체를 non-constructor(생성자 함수로 호출 불가능)라고 부름
--> 함수 객체는 constructor일수도, non-constructor일수도 있음

### 17.2.5 constructor와 non-constructor의 구분

### 17.2.6 new 연산자
- 함수를 new와 함께 생성자 함수로 호출시 내부의 this는 생성할 인스턴스를 가리킴. But 일반 함수로 호출시 내부의 this는 전역 객체 window를 가리킴.
- 일반적으로 생성자 함수는 첫 문자를 대문자로 기술하는 파스칼 케이스로 명명하여 일반 함수와 구분

### 17.2.7 new.target
