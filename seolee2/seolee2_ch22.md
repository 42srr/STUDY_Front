22장 this
# 22.1 this 키워드

---

<aside>
💡

자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수

</aside>

- this 바인딩은 함수 호출 방식에 의해 동적으로 결정

```jsx
바인딩 : 식별자와 값을 연결하는 과정
```

# 22.2 함수 호출 방식과 this 바인딩

---

```jsx
렉시컬 스코프와 this 바인딩의 결정 시기가 다름
```

## 22.2.1 일반 함수 호출

- 전역 객체
- strict mode인 경우 undefined

## 22.2.2 메서드 호출

- 메서드를 호출한 객체 (마침표 연산자 앞에 기술한 객체)
