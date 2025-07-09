▣ 27장: 배열
27.1 배열이란?
- 배열 = 여러 개의 값을 순차적으로 나열한 구조
- 배열이 가진 값 = 요소(element)
- 자신의 위치 값 = 인덱스
- 접근시 대괄호 표기법
- 배열이라는 타입은 존재 X -> 객체 타입 (object)
27.2 자바스크립트 배열은 배열이 아니다
- 띠용...
- 여기서의 배열 , 희소 배열 ! 
    - 각각의 메모리 공간 동일한 크기 X여도 됌
    - 연속적으로 이어져 있지 않아도 됌
    - => 일반적인 배열 흉내냄

27.3 length 프로퍼티와 희소 배열
- 희소배열의 length > 희소배열 실제 요소 개수
    - 일치 하지 않다는 말
- 희소 배열을 허용하지만 최대한 만드는 것을 피하기
- 최대한 같은 타입의 요소를 연속적으로 위치 시키자!
27.4 배열 생성
____27.4.1 배열 리터럴
- 가장 일반적이고 간편한 방식

____27.4.2 Array 생성자 함수
- new Array() 이런식으로도 가능
- 근데 일반 함수로 호출해도 생성자 함수로 작동
    - Array 생성자 함수 내부에서 new.target 확인하기 때문
____27.4.3 Array.of
- 전달인자를 배열로 만듬
____27.4.4 Array.from
- 유사 배열 객체를 변환해 배열로 만듬
- 'Hello' 이런거 넣으면 하나씩 쪼개서 배열로 만들어 줌 **좋다**
27.5 배열 요소의 참조
27.6 배열 요소의 추가와 갱신
27.7 배열 요소의 삭제

/ 아래 부분은 후루룩 읽고 실습해보는게 더 좋을 듯! /
27.8 배열 메서드
____27.8.1 Array.isArray
____27.8.2 Array.prototype.indexOf
____27.8.3 Array.prototype.push
____27.8.4 Array.prototype.pop
____27.8.5 Array.prototype.unshift
____27.8.6 Array.prototype.shift
____27.8.7 Array.prototype.concat
____27.8.8 Array.prototype.splice
____27.8.9 Array.prototype.slice
____27.8.10 Array.prototype.join
____27.8.11 Array.prototype.reverse
____27.8.12 Array.prototype.fill
____27.8.13 Array.prototype.includes
____27.8.14 Array.prototype.flat
27.9 배열 고차 함수
____27.9.1 Array.prototype.sort
____27.9.2 Array.prototype.forEach
____27.9.3 Array.prototype.map
____27.9.4 Array.prototype.filter
____27.9.5 Array.prototype.reduce
(중요) 이거 진짜 많이 씀 / 코테에서도 많이 보고
____27.9.6 Array.prototype.some
____27.9.7 Array.prototype.every
____27.9.8 Array.prototype.find
____27.9.9 Array.prototype.findIndex
____27.9.10 Array.prototype.flatMap