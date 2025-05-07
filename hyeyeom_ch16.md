# ▣ 16장: 프로퍼티 어트리뷰트
## 16.1 내부 슬롯과 내부 메서드
- 자바스크립트 엔젠의 구현 알고리즘 설명을 위한 ECMAscript 사양에서 사용
- 이중 대괄호로 감싼 이름들
  - 원칙적으로 직접 접근 / 호출 방법 X
  - 엔진 내부의 로직
  - __proto__ 통해 간접 접근 가능
```
const o = {}

o.[[Prototype]]
o.__proto__
```

## 16.2 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체
자바스크립트 엔진
- 프로퍼티 생성, 프로퍼티 어트리뷰트 = 기본값 (자동정의)
- 프로퍼티 상태
  - Value : 값 
  - Writable : 갱신가능 여부
  - Enumerable : 열거가능 여부
  - configurable : 재정의 가능 여부
- 프로퍼티 어트리뷰트
  - 위 상태값들을 [[여기]] 갖는 내부 상태 값 (meta-property)
- Object.getOwnPropertyDescriptor메서드 사용 -> 간접적 확인 가능

Object.getOwnPropertyDescriptor(first, second)
- first : 객체 참조 전달
- second : 프로퍼티 키 -> 문자열로 전달
=> return : 프로퍼티 디스크립터 객체 반환 (없을 경우, undefined)
Object.getOwnPropertyDescriptors(first)
=> return : 프로퍼티 디스크립터 객체*들* 반환 (없을 경우, undefined)

## 16.3 데이터 프로퍼티와 접근자 프로퍼티
- 프로퍼티
  - 데이터 프로퍼티 : 일반적인 프로퍼티
  - 접근자 프로퍼티 : 자체값 X, 다른 프로퍼티의 값 읽고 저장시 호출되는 접근자 함수로 구성

### ____16.3.1 데이터 프로퍼티
- 프로퍼티 상태
  - Value : 값 
  - Writable : 갱신가능 여부
  - Enumerable : 열거가능 여부
  - configurable : 재정의 가능 여부
- 프로퍼티 어트리뷰트
  - 위 상태값들을 [[여기]] 갖는 내부 상태 값 (meta-property)

### ____16.3.2 접근자 프로퍼티
- 자체값 X
- get
- set
- Enumerable
- Configurable

- 접근자 함수 : getter/setter 함수라고도 부름
- 둘다 정의 / 둘 중 하나만 정의 가능
  - 값을 읽거나 저장할 때만 관여

## 16.4 프로퍼티 정의
새로운 프로퍼티를 추가하면서 프로퍼티 어트리뷰트 명시적 정의
기존 프로퍼티 어트리뷰트 재정의
- Object.defineProperty
  - 객체 참조
  - 데이터 프로퍼티의 키인 문자열
  - 프로퍼티 디스크립터 객체 전달
- Object.defineProperties
  - 한번에 여러개 프로퍼티 정의 가능

## 16.5 객체 변경 방지
- 객체 = 변경 가능한 값
  - 재할당 없이 직접 변경 가능
  - 위에서 한 것처럼 프로퍼티 재정의도 가능
- 그래서, 변경 못하도록 객체 변경 방지도 할 수 있음 
### ____16.5.1 객체 확장 금지
- Object.preventExtensions
  - 프로퍼티 추가 금지 의미
  - 확장이 금지된 객체는 프로퍼티 추가 금지
    - 프로퍼티 동적 추가 & Object.defineProperty 메서드로 추가 가능
- Object.isExtensible
  - 확장 가능 여부 확인

### ____16.5.2 객체 밀봉
- Object.seal
  - 프로퍼티 추가 / 삭제 / 프로퍼티 어트리뷰트 재정의 금지
  - *읽기*와 *쓰기*만 가능

### ____16.5.3 객체 동결
- Object.freeze
  - 객체 동결
  - 동결된 객체는 *읽기만 가능*

### ____16.5.4 불변 객체
- 앞서 변경 방지 메서드는 얕은 변경 방지
  - 직속 프로퍼티만 변경 방지
  - 중첩 객체까지는 영향 X
    - Object.freeze의 경우, 중첩 객체까지 동결 X
- 따라서 따로 함수를 만들어서 deepFreeze할 수 있게 각 객체마다 동결해줘야함