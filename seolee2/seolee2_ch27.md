27장 배열
# 27.1 배열이란?

---

- 여러 개의 값을 순차적으로 나열한 자료구조

```jsx
요소 : 배열이 가지고 있는 값
인덱스 : 자신의 위치를 나타내는 0 이상의 정수
=> 일반 객체와 달리 값의 순서가 있음
요소 접근 시 대괄호[인덱스]

length 프로퍼티 : 요소의 개수 = 배열의 길이
for문을 통해 순차적으로 요소에 접근 가능

배열은 객체 타입
```

# 27.2 자바스크립트 배열은 배열이 아니다

---

```jsx
밀집 배열 : 동일한 크기의 메모리 공간이 빈틈없이 연속적으로 나열된 자료구조의 배열

효율적인 임의 접근 O(1) 가능
정렬되지 않았다면 선형 검색 O(n)

희소 배열 : 배열의 요소가 연속적으로 이어지지 않은 배열

자바스크립트의 배열은 일반적인 배열의 동작을 흉내 낸 특수한 객체
```

```jsx
일반적인 배열은 인덱스로 요소에 빠르게 접근할 수 있지만 삽입, 삭제는 비효율적

자바스크립트 배열은 해시 테이블로 구현된 객체이므로 인덱스 접근이 일반적인 배열보다 느리지만
삽입, 삭제는 일반적인 배열보다 빠른 성능
```

# 27.3 length 프로퍼티와 희소 배열

---

```jsx
배열의 길이를 바탕으로 자동 결정되지만 명시적으로 할당 가능
현재보다 작은 값 : 배열의 길이가 줄어듬
큰 값 : 값은 변경되지만 길이는 그대로

희소배열은 [,1,,2] 허용되지만 사용하지 않는 것이 좋음
```

# 27.4 배열 생성

---

## 27.4.1 배열 리터럴

```jsx
쉼표로 구분하여 대괄호로 묶음
```

## 27.4.2 Array 생성자 함수

```jsx
인수의 개수에 따라 다르게 동작

1개이고 숫자 : length 프로퍼티 값이 인수인 배열 생성
인수가 없는 경우 빈 배열
2개 이상이거나 숫자가 아닌 경우 인수를 요소로 갖는 배열 생성
```

## 27.4.3 Array.of

```jsx
인수가 1개이고 숫자이더라도 인수를 요소로 갖는 배열 생성
```

## 27.4.4 Array.from

```jsx
유사 배열 객체 또는 이터러블 객체를 인수로 받아 배열로 변환해 반환
```

# 27.5 배열 요소의 참조

---

```jsx
존재하지 않는 요소에 접근하면 undefined 반환
희소 배열의 존재하지 않는 요소도 undefined
```

# 27.6 배열 요소의 추가와 갱신

---

```jsx
존재하지 않는 인덱스를 사용해 값을 할당하면 새로운 요소 추가

현재 배열의 length 프로퍼티보다 큰 인덱스로 추가하면 희소 배열이 되며
명시적으로 값을 할당하지 않은 요소는 생성되지 않음

이미 요소가 존재하는 요소에 값을 재할당하면 갱신
정수 이외의 값을 인덱스처럼 사용하면 프로퍼티가 생성되며
이는 length 프로퍼티 값에 영향을 주지 않음
```

# 27.7 배열 요소의 삭제

---

```jsx
delete 연산자 사용 가능
=> 희소배열이 되고 length는 변하지 않으므로 사용하지 않는 것이 좋음

Array.prototype.splice 메서드 사용
```

# 27.8 배열 메서드

---

```jsx
배열에는 원본 배열을 직접 변경하는 메서드와 새로운 배열을 생성하여 반환하는 메서드가 있다
```

## 27.8.1 Array.isArray

```jsx
전달된 인수가 배열이면 true, 배열이 아니면 false 반환
```

## 27.8.2 Array.prototype.indexOf

```jsx
원본 배열에서 인수로 전달된 요소를 검색하여 인덱스 반환

여러 개라면 첫 번째로 검색된 요소의 인덱스 반환
존재하지 않으면 -1 반환
```

## 27.8.3 Array.prototype.push

```jsx
인수로 전달받은 모든 값을 원본 배열의 마지막 요소로 추가하고 변경된 length 반환
원본 배열을 직접 변경

성능이 좋지 않으므로 요소 하나 추가 시 length 프로퍼티를 사용해 직접 추가하는 것이 빠름
```

## 27.8.4 Array.prototype.pop

```jsx
마지막 요소를 제거하고 제거한 요소를 반환
빈 배열이면 undefined 반환
원본 배열을 직접 변경
```

## 27.8.5 Array.prototype.unshift

```jsx
인수로 전달받은 모든 값을 원본 배열의 선두에 요소로 추가하고 변경된 length 반환
원본 배열을 직접 변경
```

## 27.8.6 Array.prototype.shift

```jsx
첫 번째 요소를 제거하고 제거한 요소 반환
빈 배열이면 undefined
원본 배열 직접 변경
```

## 27.8.7 Array.prototype.concat

```jsx
인수로 전달된 값을 마지막 요소로 추가한 새로운 배열 반환
전달 값이 배열인 경우 해체하여 새로운 배열의 요소로 추가
원본 변경 x
```

## 27.8.8 Array.prototype.splice

```jsx
배열 중간 요소를 추가하거나 제거하는 경우에 사용
원본 배열을 변경

start : 제거를 시작할 인덱스, 음수인 경우 배열 끝에서의 인덱스
deleteCount(옵션) : start부터 제거할 요소의 개수
items(옵션) : 제거한 위치에 삽입할 요소의 목록
```

## 27.8.9 Array.prototype.slice

```jsx
인수 범위의 요소를 복사하여 배열로 반환
원본 변경 x

얕은 복사
```

## 27.8.10 Array.prototype.join

```jsx
원본 배열의 모든 요소를 문자열로 변환한 후 인수로 받은 문자열(구분자)로 연결한 분자열 반환
구분자 생략 시 기본은 ','
```

## 27.8.11 Array.prototype.reverse

```jsx
원본 배열의 순서를 반대로 뒤집음
원본 배열 변경
변경된 배열을 반환
```

## 27.8.12 Array.prototype.fill

```jsx
인수로 전달받은 값을 배열의 처음부터 끝까지 요소로 채움
원본 배열 변경
두번째 인수로 시작 인덱스, 세번째로 정지 인덱스(미포함) 전달
```

## 27.8.12 Array.prototype.includes

```jsx
배열 내 특정 요소 포함 여부를 true, false로 반환
두 번째 인수로 검색 시작 인덱스 전달 가능
```

## 27.8.14 Array.prototype.flat

```jsx
인수로 전달한 깊이만큼 재귀적으로 배열을 평탄화시킴
```

# 27.9 배열 고차 함수

---

```jsx
고차 함수 : 함수를 인수로 전달받거나 함수를 반환하는 함수
외부 상태의 변경이나 가변 데이터를 피하고 불변성을 지향

조건문과 반복문을 제거하고 변수의 사용을 억제하여 부수효과를 최대한 억제해 오류를 피하고 안정성 높임
```

## 27.9.1 Array.prototype.sort

```jsx
배열의 요소를 정렬하여 정렬된 배열 반환
직접 변경
기본적으로 오름차순으로 정렬

기본 정렬 순서는 숫자가 아닌 유니코드 문자열이므로
숫자 정렬 시 정렬 순서를 정의하는 비교 함수를 인수로 전달해야 함
array.sort((a, b) => a - b);
```

## 27.9.2 Array.prototype.forEach

```jsx
for문을 대체하여 자신의 내부에서 반복문 실행
성능은 좋지 않지만 가독성이 좋음
원본 배열을 변경하지 않지만 콜백 함수를 통해 변경할 수는 있음 
반환값은 항상 undefined

화살표 함수 내부에서 this를 참조하여 상위 스코프의 this를 그대로 참조 추천

break나 continue 사용 불가
```

## 27.9.3 Array.prototype.map

```jsx
전달받은 콜백 함수를 반복 호출하고
원본 변경 없이 콜백 함수 반환값들로 구성된 새로운 배열 반환

원본과 반환 배열의 length 반드시 일치 (1:1 매핑)
```

## 27.9.4 Array.prototype.filter

```jsx
콜백 함수를 반복 호출하여 반환값이 true인 요소로만 구성된 새로운 배열 반환
원본 변경 x
```

## 27.9.5 Array.prototype.reduce

```jsx
반환값을 계속 누산하여 결과값 반환
원본 배열 변경 x

(콜백 함수, 초기값)
초기값은 생략 가능하지만 전달하는 것이 안전
```

## 27.9.6 Array.prototype.some

```jsx
순회하면서 콜백 함수의 값이 한번이라도 참이면 true, 모두 거짓이면 false

빈 배열인 경우 false 이므로 주의
```

## 27.9.7 Array.prototype.every

```jsx
모두 참이면 true, 하나라도 거짓이면 false

빈 배열이면 true 이므로 주의
```

## 27.9.8 Array.prototype.find

```jsx
순회하며 반환값이 true인 첫 번째 요소 반환
없다면 undefined
```

## 27.9.9 Array.prototype.findIndex

```jsx
처음으로 참인 요소의 인덱스 반환
없다면 -1
```

## 27.9.10 Array.prototype.flatMap

```jsx
map 메서드와 flat 메서드를 순사적으로 실행
깊이 지정은 불가능하므로 필요 시 각각 호출
```
