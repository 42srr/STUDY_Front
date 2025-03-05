[모던 자바스크립트 Deep Dive]
[9장] 타입 변환과 단축 평가

---

### 1. 타입 변환이란?

- 명시적 타입 변환, 타입 캐스팅

  - 개발자가 의도적으로 값의 타입을 변환하는 것

  - ex. (10).toString()

- 암묵적 타입 변환, 타입 강제 변환

  - 개발자의 의도와는 상관없이 표현식을 평가하는 도중에 자바스크립트 엔진에 의해 암묵적으로 타입이 자동 변환되는 것

  - ex. 10 + ''

- 기존 원시 값(변경 불가능한 값)을 직접 변경하는 것이 아니라, 기존 원시 값을 사용해 다른 타입의 새로운 원시 값을 생성하여 단 한 번 사용하고 버림

---

### 2. 암묵적 타입 변환

#### 문자열 타입으로 변환

- - 가 문자열 연결 연산자로 동작

- 피연산자가 모두 문자열 타입이어야 함

  - 0 + '' -> "0"

  - -0 + '' -> "0"

  - 1 + '' -> "1"

  - -1 + '' -> "-1"

  - NaN + '' -> "NaN"

  - Infinity + '' -> "Infinity"

  - -Infinity + '' -> "-Infinity"

  - true + '' -> "true"

  - false + '' -> "false"

  - null + '' null -> 'null'

  - undefined + '' -> "undefined"

  - (Symbol()) + '' -> TypeError

  - ({}) + '' -> "[object Object]"

  - Math + '' -> "[object Math]"

  - [] + '' -> "10, 20"

  - (function(){}) + '' -> "function(){}"

  - Array + '' -> "function Array(){[native code]}"

#### 숫자 타입으로 변환

- -, \*, /가 산술 연산자로 작동

- 피연산자가 모두 숫자여야 함

- 객체, 빈 배열이 아닌 배열, undefined는 변환되지 않음

  - - ''-> 0

  - - '0' -> 0

  - - '1' -> 1

  - - 'string' -> NaN

  - - true -> 1

  - - false -> 0

  - - null -> 0

  - - undefined -> NaN

  - - Symbol() -> TypeError

  - - {} -> NaN

  - - [] -> 0

  - - [10, 20] -> NaN

  - - (function(){}) -> NaN

#### 불리언 타입으로 변환

- 자바스크립트 엔진이 불리언 타입이 아닌 값을 Truthy 값 또는 Falsy 값으로 구분

- 불리언 값으로 평가되어야 할 문맥에서 각각 true, false로 암묵적 타입 변환

- Falsy 값

  - false, undefined, null, 0, -0, NaN, ''(빈 문자열)

- Truthy 값

  - function isFalsy(v) {return !v;}

  - function isTruthy(v) {return !!v;}

  - true, '0'(빈 문자열이 아닌 문자열), {}, []

---

### 3. 명시적 타입 변환

- 명시적 타입 변환 방법

  - 표준 빌트인 생성자 함수를 new 연산자 없이 호출

  - 빌트인 메서드를 사용

  - 암묵적 타입 변환을 이용

#### 문자열 타입으로 변환

- 문자열이 아닌 값을 문자열 타입으로 변환하는 방법

  - String 생성자 함수를 new 연산자 없이 호출

    - 숫자 -> 문자열

      - String(1) -> "1"

      - String(NaN) -> "NaN"

      - String(Infinity) -> "Infinity"

    - 불리언 -> 문자열

      - String(true) -> "true"

      - String(false) -> "false"

  - Object.prototype.toString 메서드를 사용

    - 숫자 -> 문자열

      - (1).toString() -> "1"

      - (NaN).toString() -> "NaN"

      - (Infinity).toString() -> "Infinity"

    - 불리언 -> 문자열

      - (true).toString() -> "true"

      - (false).toString() -> "false"

  - 문자열 연결 연산자를 이용

    - 숫자 -> 문자열

      - 1 + '' -> '1'

      - NaN + '' -> "NaN"

      - Infinity + '' -> "Infinity"

    - 불리언 -> 문자열

      - true + '' -> "true"

      - false + '' -> "false"

#### 숫자 타입으로 변환

- 숫자 타입이 아닌 값을 숫자 타입으로 변환하는 방법

  - Number 생성자 함수를 new 연산자 없이 호출

    - 문자열 -> 숫자

      - Number('0') -> 0

      - Number('-1') -> -1

      - Number('10.53') -> 10.53

    - 불리언 -> 숫자

      - Number(true) -> 1

      - Number(false) -> 0

  - parseInt, parseFloat 함수를 사용(문자열 숫자로만 변환 가능)

    - 문자열 -> 숫자

      - parseInt('0') -> 0

      - parseInt('-1') -> -1

      - parseFloat('10.53') -> 10.53

  - - 단항 산술 연산자를 이용

    * 문자열 -> 숫자

      - - '0' -> 0

      - - '-1' -> -1

      - - '10.53' -> 10.53

    * 불리언 -> 숫자

      - - true -> 1

      - - false -> 0

  - - 산술 연산자를 이용

    * 문자열 -> 숫자

      - '0' \* 1 -> 0

      - '-1' \* 1 -> -1

      - '10.53' \* 1 -> 10.53

    * 불리언 -> 숫자

      - true \* 1 -> 1

      - false \* 1 -> 0

#### 불리언 타입으로 변환

- 불리언 타입이 아닌 값을 불리언 타입으로 변환하는 방법

  - Boolean 생성자 함수를 new 연산자 없이 호출

    - 문자열 -> 불리언

      - Boolean('x') -> true

      - Boolean('') -> false

      - Boolean('false') -> true

    - 숫자 -> 불리언

      - Boolean(0) -> false

      - Boolean(1) -> true

      - Boolean(NaN) -> false

      - Boolean(Infinity) -> true

    - null -> 불리언

      - Boolean(null) -> false

    - undefined -> 불리언

      - Boolean(undefined) -> false

    - 객체 -> 불리언

      - Boolean({}) -> true

      - Boolean([]) -> true

  - !부정 논리 연산자를 두 번 사용

    - 문자열 -> 불리언

      - !!'x' -> true

      - !!'' -> false

      - !!'false' -> true

    - 숫자 -> 불리언

      - !!0 -> false

      - !!1 -> true

      - !!NaN -> false

      - !!Infinity -> true

    - null -> 불리언

      - !!null -> false

    - undefined -> 불리언

      - !!undefined -> false

    - 객체 -> 불리언

      - !!{} -> true

      - !![] -> true

---

### 4. 단축 평가

#### 논리 연산자를 사용한 단축 평가

- 단축 평가

  - 논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환

  - 표현식 평가 도중에 평가 결과가 확정되면 나머지 평가 과정을 생략하는 것

  - 논리곱(&&), 논리합(||)은 평가 결과가 불리언이 아닐 수도 있음

    - true || anything -> true

    - false || anything -> anything

    - true && anything -> anything

    - false && anything -> false

- 논리곱(&&) 연산자

  - 두 개의 피연산자가 모두 true로 평가될 때 true를 반환 (좌항->우항)

  - 두 번째 피연산자가 논리곱 연산자 표현식의 평가 결과를 결정

    - 'Cat' || 'Dog' -> "Cat"

    - false || 'Dog' -> "Dog"

    - 'Cat' || false -> "Cat"

- 논리합(||) 연산자

  - 두 개의 피연산자 중 하나만 true로 평가되어도 true를 반환 (좌항->우항)

  - 논리 연산의 결과를 결정한 첫 번째 피연산자를 반환

    - 'Cat' && 'Dog' -> "Dog"

    - false && 'Dog' -> false

    - 'Cat' && false -> false

- 단축 평가 사용 예시

  - 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때

    - Falsy 값이면 elem으로 평가되고, Truthy 값이면 elem.value로 평가됨

      - var value = elem && elem.value -> null

  - 함수 매개변수에 기본값을 설정할 때

    - function get(str = '') {return str.length;}

    - get() -> 0, get('hi') -> 2

#### 옵셔널 체이닝 연산자

- ES11 도입, 옵셔널 체이닝(?.) 연산자 (> && 단축 평가)

  - 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환, 그렇지 않으면 우항의 프로퍼티를 참조

  - var value = elem?.value -> undefined

  - Falsy 값이라도 null 또는 undefined가 아니면 우항의 프로퍼티 참조를 이어감

    - str = ''; console.log(str?.length); -> 0 (O)

    - str = ''; console.log(str && str.length); -> '' (X)

#### null 병합 연산자

- ES11 도입, null 병합(??) 연산자 (> ||)

  - 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환, 그렇지 않으면 좌항의 피연산자를 반환

  - 기본 값 설정 시 유용

    - var foo = null ?? 'default string'

  - Falsy 값이라도 null 또는 undefined가 아니면 좌항의 피연산자를 반환

    - var foo = '' ?? 'default string' -> "" (O)

    - var foo = '' || 'default stirng' -> 'default string' (X)

---
