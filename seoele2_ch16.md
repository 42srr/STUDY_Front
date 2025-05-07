16장 프로퍼티 어트리뷰트
# 16.1 내부 슬롯과 내부 메서드

---

- 의사 프로퍼티와 의사 메서드
- ECMAScript 사양에 정의된 대로 구현되어 실제로 동작하지만 비공개, 접근 불가

# 16.2 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체

---

- JS 엔진은 프로퍼티 생성 시 프로퍼티의 상태를 나타내는 프로퍼티 어트리뷰트를 기본값으로 정의

```jsx
프로퍼티 상태 : 값, 값의 갱신 가능 여부, 열거 가능 여부, 재정의 가능 여부
           value     writable     enumerable      configurable 
           
Object.getOwnPropertyDescriptor([참조], '[프로퍼티 키]') 
메서드를 사용하여 반환된 프로퍼티 디스크립터 객체를 통해 간접적으로 확인 가능

ES8에 도입된 Object.getOwnPropertyDescriptors([참조]) => 모든 정보 담은 객체 반환
```

# 16.3 데이터 프로퍼티와 접근자 프로퍼티

---

```jsx
데이터 프로퍼티 : 키와 값으로 구성된 일반적인 프로퍼티
접근자 프로퍼티 : 자체적으로는 값이 없고 다른 데이터 프로퍼트의 값을 읽거나 저장할 때 호출되는
               접근자 함수로 구성된 프로퍼티
```

## 16.3.1 데이터 프로퍼티

## 16.3.2 접근자 프로퍼티

1. get : 데이터 프로퍼티의 값에 접근, getter 호출 → 결과 값 반환
2. set : 데이터 프로퍼티의 값을 저장, setter 호출 → 결과 값 저장

```jsx
const person = {
	firstName: 'Ungmo',
	lastName: 'Lee',
	
	get fullName() {
		return `${this.firstName} ${this.lastName}`;
	}
	set fullName() {
		[this.firstName, this.lastName] = name.split(' ');
	}
};
```

# 16.4 프로퍼티 정의

---

```jsx
새로운 프로퍼티를 추가하면서 프로퍼티 어트리뷰트를 명시적으로 정의하거나
기존 프로퍼티의 프로퍼티 어트리뷰트를 재정의하는 것

Object.defineProperty 메서드 사용

const person = {};

Object.defineProperty(person, 'fristName', {
	value: 'Ungmo',
	writable: true,
	enumerable: true,
	configurable: true
});

let descriptor = Object.getOwnPropertyDescriptor(person, 'firstName');

누락 시 undefined, false가 기본 값
Enumerable false : for ... in 문이나 Object.keys 등으로 열거 불가
Writable false : Value 값 변경 불가, 변경 시도 시 무시(에러 x)
Configurable false : 해당 프로퍼티 삭제 및 재정의 불가, 삭제 시도 시 무시(에러 x)

Object.defineProperties 메서드로 여러 프로퍼티 한번에 정의 가능
```

# 16.5 객체 변경 방지

---

## 16.5.1 객체 확장 금지(Object.preventExtensions)

- 프로퍼티 추가 금지(동적 추가, Object.defineProperty)
- Object.isExtensible 메서드로 확인 가능

## 16.5.2 객체 밀봉(Object.seal)

- 읽기와 쓰기만 가능
- Object.isSealed 메서드로 확인 가능

## 16.5.3 객체 동결(Object.freeze)

- 읽기만 가능
- Object.isFrozen 메서드로 확인 가능

## 16.5.4 불변 객체

```jsx
상기 항목들은 직속 프로퍼티만 변경 방지, 중첩 객체에는 영향을 주지 못함
=> 객체를 값으로 갖는 모든 프로퍼티에 대해 재귀적으로 Object.freeze 메서드 호출 필요
```
