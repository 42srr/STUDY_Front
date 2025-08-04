# 37장 Set과 Map

## 37.1 Set

- Set 객체는 중복되지 않는 유일한 값들의 집합
- 중복 없고, 순서 없고, 인덱스로 접근 불가능

### 37.1.1 Set 객체의 생성

- Set 생성자 함수로 생성함
- Set 생성자 함수는 이터러블을 인수로 전달받아 Set 객체를 생성
- 이때 중복된 값은 요소로 저장되지 않음

### 37.1.2 요소 개수 확인

const {size} = new Set([1, 2, 2, 3]);
console.log(size); // 3

- size 프로퍼티는 getter 함수만 존재하는 접근자 프로퍼티이므로 size 프로퍼티에 숫자를 할당해도 Set 객체의 요소 개수를 변경할 수 없음

### 37.1.3 요소 추가

const set = new Set();
set.add(1).add(2);
console.log(set); // Set(2) {1, 2}

### 37.1.4 요소 존재 여부 확인

const set = new Set([1, 2, 3]);
console.log(set.has(2)); // true
console.log(set.has(4)); // false

### 37.1.5 요소 삭제

- delete 메서드 사용

### 37.1.6 요소 일괄 삭제

- clear 메서드 사용

### 37.1.7 요소 순회

- forEach 메서드 사용

### 37.1.8 집합 연산

- 교집합, 합집합, 차집합 등 구현 가능

## 37.2 Map

- 키와 값의 쌍으로 이루어진 컬렉션
- 객체와 유사하지만 차이점이 있음
- 객체는 문자열 또는 심벌 값을 키로 사용하지만 Map 객체는 객체를 포함한 모든 값을 키로 사용
- 객체는 이터러블이 아니지만 Map 객체는 이터러블

### 37.2.1 Map 객체의 생성

const map = new Map();
console.log(map); // Map(0) {}

- Map 생성자 함수는 이터러블을 인수로 전달받아 Map 객체를 생성
- 인수로 전달되는 이터러블은 키와 값의 쌍으로 이루어진 요소로 구성

### 37.2.2 요소 개수 확인

const {size} = new Map([['key1', 'value1], ['key2', 'value2']]);
console.log(size); // 2

### 37.2.3 요소 추가

const map = new Map();
map.set('key1', 'value1');
console.log(map);

- set 메서드는 새로운 요소가 추가된 Map 객체를 반환

### 37.2.4 요소 취득

const map = new Map();
const lee = {name : 'Lee'};
const kim = {name : 'Kim'};

map.set(lee, 'developer').set(kim, 'designer');
console.log(map.get(lee)); // developer
console.log(map.get('key')); // undefined

### 37.2.5 요소 존재 여부 확인

- has 메서드 사용

### 37.2.6 요소 삭제

- delete 메서드 사용

### 37.2.7 요소 일괄 삭제

- clear 메서드 사용

### 37.2.8 요소 순회

- forEach 메서드 사용
