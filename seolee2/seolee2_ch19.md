19장 프로토타입
<aside>
💡

**자바스크립트를 이루고 있는 거의 “모든 것”이 객체**

</aside>

# 19.1 객체지향 프로그래밍

---

- 실제 세계의 실체(사물, 개념)를 인식하는 철학적 사고를 프로그래밍에 접목하려는 시도

```jsx
속성(attribute/property) : 특징이나 성질
추상화(abstraction) : 프로그램에 필요한 속성만 간추려 내어 표현하는 것
객체(object) : 속성을 통해 여러 값을 하나의 단위로 구성한 복합적인 자료구조
객체지향 프로그래밍(OOP, Object-Oriented Programming) : 
														독립적인 객체의 집합으로 프로그램을 표현하려는 프로그래밍 패러다임

상태(state) : 프로퍼티(property)
동작(behavior) : 메서드(method)

다른 객체와의 관계성(relationship) : 다른 객체와 메시지 주고받기, 데이터 처리, 상속
```

# 19.2 상속과 프로토타입

---

- 상속(inheritance) : 어떤 객체의 프로퍼티 또는 메서드를 다른 객체가 상속받아 그대로 사용

⇒ JS는 프로토타입을 기반으로 상속을 구현하여 불필요한 중복을 제거

```jsx
function Circle(radius) {
	this.radius = radius;
}

Cricle.prototype.getArea = function () {
	return Math.PI * this.radius ** 2;
};

Cricle 생성자 함수가 생성한 모든 인스턴스는 
Circle.prototype로부터 getArea 메서드를 상속
모두 하나의 메서드를 공유
```

# 19.3 프로토타입 객체

---

- 모든 객체는 하나의 프로토타입을 갖고 모든 프로토타입은 생성자 함수와 연결되어 있음
- [[Prototype]] 내부 슬롯 직접 접근 불가, __**proto**__ 접근자 프로퍼티를 통해 간접적으로 접근
- 프로토타입은 자신의 constructor 프로퍼티를 통해 생성자 합수에 접근
- 생성자 함수는 자신의 prototype 프로퍼티를 통해 프로토타입에 접근

## 19.3.1 __proto__ 접근자 프로퍼티

1. 접근자 프로퍼티다
    
    ```jsx
    자체적으로는 값을 갖지 않고 접근자 함수(get, set 프로퍼티 어트리뷰트)로 구성된 프로퍼티
    ```
    
2. 상속을 통해 사용됨
    
    ```jsx
    객체가 직접 소유하는 게 아닌 Object.prototype의 프로퍼티
    모든 객체는 상속을 통해 Object.prototype.__proto__ 접근자 프로퍼티 사용 가능
    ```
    
3. 상호 참조로 인한 프로토타입 체인 생성을 방지
    
    ```jsx
    프로토타입 체인은 단방향 링크드 리스트로 구현되어야 함
    ```
    
4. __**proto**__를 코드 내에서 직접 사용 비권장
    
    ```jsx
    직접 상속으로 생성된 객체는 Object.prototype을 상속받지 않아 __proto__ 사용 불가능
    
    getPrototypeOf : 참조 취득 시
    Object.setPrototypeOf : 프로토타입 교체
    ```
    

## 19.3.2 함수 객체의 prototype 프로퍼티

- 함수 객체만이 소유하는 prototype 프로퍼티는 생성자 함수가 생성할 인스턴스의 프로토타입

```jsx
__proto__ 접근자 프로퍼티 / 모든 객체 / 객체가 자신의 프로토타입에 접근 또는 교체

prototype 프로퍼티 / constructor / 생성자 함수 / 생성할 객체의 프로토타입 할당

function Person(name) {
	this.name = name;
}

const me = new Person('Lee');

console.log(Person.prototype === me.__proto__) // true;

생성자 함수의 prototype === 생성된 객체의 __proto__
```

## 19.3.3 프로토타입의 constructor 프로퍼티와 생성자 함수

- 모든 프로토타입은 constructor 프로퍼티를 가짐
    
    → prototype 프로퍼티로 자신을 참조하는 생성자 함수를 가리킴
    
    ```jsx
    me.constructor === Person
    
    me 객체에는 constructor 프로퍼티가 없지만
    me 객체의 프로토타입인 Person.prototype의 constructor 프로퍼티를 상속받아 사용
    ```
    

# 19.4 리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입

---

- 리터럴 표기법에 의해 생성된 객체도 프로토타입이 존재
- 프로토타입의 constructor 프로퍼티가 객체를 생성한 생성자 함수라고 단정할 수 없음
- 추상 연산 OrdinaryObjectCreate를 호출하여 빈 객체를 생성, Object 생성자 함수가 생성한 건 x
- 프로토타입과 생성자 함수는 단독 존재가 불가능하고 쌍으로 존재
    
    →리터럴 표기법에 의해 생성된 객체도 가상적인 생성자 함수를 가짐
    

<aside>
💡

리터럴 표기법에 의해 생성된 객체는 생성자 함수에 의해 생성되지는 않았지만

본질적으로 큰 차이가 없고 동일한 특성을 가지므로

constuctor로 연결된 생성자 함수가 객체를 생성했다고 여겨도 큰 무리는 없음

**but 수정되면 말이 달라짐**

</aside>

# 19.5 프로토타입의 생성 시점

---

- 프로토타입은 생성자 함수가 생성되는 시점에 함께 생성됨

## 19.5.1 사용자 정의 생성자 함수와 프로토타입 생성 시점

- constructor는 함수 정의가 평가되어 함수 객체를 생성하는 시점에 프로토타입 생성
- 생성된 프로토타입은 constructor만 가진 객체, 생성된 프로토타입의 프로토타입은 Object.prototype

## 19.5.2 빌트인 생성자 함수와 프로토타입 생성 시점

- 전역 객체가 생성되는 시점에 생성

# 19.6 객체 생성 방식과 프로토타입의 결정

---

- 프로토타입은 추상연산 OrdinaryObjectCreate에 전달되는 인수에 의해 결정
    
    → 객체 생성 시점에 객체 생성 방식에 의해 결정
    

## 19.6.1 객체 리터럴에 의해 생성된 객체의 프로토타입

- Object.prototype을 프로토타입으로 갖게 되고 그것을 상속

## 19.6.2 Object 생성자 함수에 의해 생성된 객체의 프로토타입

- Object.prototype을 프로토타입으로 갖게 되고 그것을 상속

```jsx
객체 리터럴 : 객체 리터럴 내부에 프로퍼티 추가
Object 생성자 함수 : 빈 객체를 생성한 이후 프로퍼티 추가
```

## 19.6.3 생성자 함수에 의해 생성된 객체의 프로토타입

- 생성자 함수의 prototype 프로퍼티에 바인딩된 객체
    
    ```jsx
    // 프로토타입의 확장과 상속
    consturctor 뿐이므로
    Person.prototype에 프로퍼티를 추가하여 하위(자식) 객체가 상속 가능
    ```
    

# 19.7 프로토타입 체인

---

```jsx
객체의 프로퍼티(메서드 포함)에 접근하려고 할 때 해당 객체에 존재하지 않으면 
[[Prototype]] 내부 슬롯의 참조를 따라 부모 프로토타입을 순차적으로 검색하는 것

자바스크립트의 상속과 프로퍼티 검색을 위한 메커니즘
스코프 체인은 식별자 검색을 위한 메커니즘
```

<aside>
💡

프로토타입의 최상위 객체는 언제나 Object.prototype

Object.prototype의 프로토타입은 null

**종점에서도 검색되지 않는다면 undefined 반환(에러 x)**

</aside>

# 19.8 오버라이딩과 프로퍼티 섀도잉

---

```jsx
오버라이딩 : 상위 클래스가 가진 메서드를 하위 클래스가 재정의하여 사용
오버로딩 : 함수의 이름이 동일하지만 매개변수의 차이로 구별하여 호출하는 방식 //JS는 미지원
프로퍼티 섀도잉 : 상속 관계에 의해 프로퍼티가 가려지는 현상
(부모와 자식이 같은 이름의 메서드를 가졌다면 자식부터 검색하여 존재하니 부모 확인 x)
```

- 하위 객체는 프로토타입에 get 접근만 가능, set은 불가능
    
    →삭제하려면 프로토타입에 직접 접근 필요
    

# 19.9 프로토타입의 교체

---

```jsx
프로토타입은 생성자 함수 또는 인스턴스를 통해 임의의 다른 객체로 변경 가능
-> 부모 객체인 프로토타입을 동적으로 변경하여 객체 간의 상속 관계 변경 가능

교체 시 constructor 프로퍼티와 생성자 함수 간의 연결이 파괴됨 
// constructor는 암묵적으로 Object가 됨
=> consturctor 프로퍼티를 추가해주기
```

## 19.9.1 생성자 함수에 의한 프로토타입의 교체

```jsx
객체 리터럴로 생성 시 
객체 리터럴에 constructor 프로퍼티가 없으면
constructor 프로퍼티와 생성자 함수 간의 연결이 파괴됨
```

## 19.9.2 인스턴스에 의한 프로토타입의 교체

```jsx
prototpye 프로퍼티에 다른 객체를 바인딩 : 미래에 생성할 인스턴스의 프로토타입 교체
__proto__ 접근자 프로퍼티를 통해 교체 : 이미 생성된 객체의 프로토타입 교체

생성자 함수의 prototype 프로퍼티가 교체된 프로토타입을 가리키지 않음
=> 생성자 함수의 prototype 프로퍼티도 재설정
```

<aside>
💡

프로토타입 교체는 번거로우므로 직접 교체 대신 직접 상속 혹은 클래스 사용

</aside>

# 19.10 instanceof연산자

---

```jsx
식별자           // 우변이 함수가 아닐 시 TypeError
객체 instanceof 생성자 함수 

우변 생성자 함수의 prototype에 바인딩된 객체가 좌변의 객체의 프로토타입 체인 상에 존재하면 true

**생성자 함수의 prototype에 바인딩된 객체가 프로토타입 체인 상에 존재하는지 확인**

-> prototype 교체로 constructor 프로퍼티와 생성자 함수의 연결이 파괴되더라도 상관없음
```

# 19.11 직접 상속

---

## 19.11.1 Object.create에 의한 직접 상속

- 명시적으로 프로토타입을 지정하여 새로운 객체 생성

```jsx
// 구조
Object.create(
[생성할 객체의 프로토타입으로 지정할 객체],
[생성할 객체의 프로퍼티 키와 프로퍼티 디스크립터 객체로 이뤄진 객체] // 옵션	
)

// 장점
new 연산자 없이도 객체 생성
프로토타입을 지정하면서 객체 생성
객체 리터럴에 의해 생성된 객체도 상속받을 수 있음
```

```jsx
// 프로토타입이 null인 객체, 즉 프로토타입 체인의 종점에 위치하는 객체 생성 가능
const obj = Object.create(null); 
obj.a = 1;

// 종점에 위치하는 객체는 Object.prototype의 빌트인 메서드 사용 불가능
console.log(obj.hasOwnProperty('a')); // TypeError
// Object.prototype.hasOwnProperty.call(obj, 'a')로 간접 호출은 가능
```

## 19.11.2 객체 내부에서 __**proto**__에 의한 직접 상속

```jsx
const myProto = { x : 10 };

const obj = {
	y : 20,
	// 객체 직접 상속 / obj -> myProto -> Object.prototype -> null
	__proto__: myProto
};
```

# 19.12 정적 프로퍼티 / 메서드

---

- 생성자 함수로 인스턴스를 생성하지 않아도 참조 / 호출 가능한 프로퍼티 / 메서드
- 생성한 인스턴스로는 참조 / 호출할 수 없음 (프로토타입 체인에 속하지 않음)
- Object.prototype.a 를 Object#b로 표기하는 경우도 있음 (.prototype. === #)

# 19.13 프로퍼티 존재 확인

---

## 19.13.1 in 연산자

```jsx
프로퍼티 키를 나타내는 문자열
key in object
       객체로 평가되는 표현식
       
확인 대상 객체가 상속받는 모든 프로토타입의 프로퍼티를 확인하므로 주의

Reflect.has([object],['key']) 도 동일하게 동작
```

## 19.13.2 Object.prototype.hasOwnProperty 메서드

```jsx
[object].hasOwnProperty(['key'])

객체에 특정 프로퍼티 존재 확인하는 건 같지만
객체 고유의 프로퍼티인 경우에만 true, 상속받은 프로토타입의 프로퍼티 키라면 false
```

# 19.14 프로퍼티 열거

---

## 19.14.1 for … in 문

```jsx
객체의 프로토타입 체인 상의 모든 프로퍼티를 순회하며 
프로퍼티 어트리뷰트 [[Enumerable]]의 값이 true인 경우에만 열거

for (변수선언문 in 객체) {...}

프로퍼티 키가 심벌이라면 열거 x

객체 자신의 프로퍼티만 열거하려면
for (const key in person) {
	if (!person.hasOwnProperty(key)) continue; // 객체 자신의 프로퍼티인지 확인
	console.log(key + ': ' + person[key]);
}

순서를 보장하지 않지만
모던 브라우저에서 순서를 보장하고 숫자 프로퍼티 키는 정렬까지 함

배열은 for ... in 보다 for , for ... of, Array.prototype.forEach 메서드 사용 권장
```

## 19.14.2 Object.keys/values/entries 메서드

```jsx
Object.keys : 객체 자신의 열거 가능한 프로퍼티 키를 배열로 반환
Object.values : 객체 자신의 열거 가능한 프로퍼티 값을 배열로 반환
Object.entries : 객체 자신의 열거 가능한 프로퍼티 키, 값의 쌍 배열을 배열에 담아 반환
```
