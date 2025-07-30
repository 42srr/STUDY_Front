▣ 28장: Number
원시 타입 숫자를 다룰때 유용한 프로퍼티 & 메서드 제공

28.1 Number 생성자 함수
- 생성자 함수 객체
    - new 연산자 함께 호출 -> 인스턴스 생성 가능
- 인수 전달 없이 new 연산자로 생성시, [[NumberData]] 내부 슬롯 0 할당 Number 래퍼 객체 생성

28.2 Number 프로퍼티
____28.2.1 Number.EPSILON
____28.2.2 Number.MAX_VALUE
____28.2.3 Number.MIN_VALUE
____28.2.4 Number.MAX_SAFE_INTEGER
안전하게 표현할 수 있는 가장 큰 정수 값
____28.2.5 Number.MIN_SAFE_INTEGER
____28.2.6 Number.POSITIVE_INFINITY
____28.2.7 Number.NEGATIVE_INFINITY
____28.2.8 Number.NaN
28.3 Number 메서드
____28.3.1 Number.isFinite
정상적인 유한수 인지 아닌지 판단
____28.3.2 Number.isInteger
정수인지 검사 후 그 결과 불리언으로 반환
검사 전엔 인수를 숫자로 암묵적 타입 변환 하지 않음
____28.3.3 Number.isNaN
____28.3.4 Number.isSafeInteger
안전한 정수값 -(253 - 1) ~ 253 - 1
____28.3.5 Number.prototype.toExponential
____28.3.6 Number.prototype.toFixed
____28.3.7 Number.prototype.toPrecision
____28.3.8 Number.prototype.toString