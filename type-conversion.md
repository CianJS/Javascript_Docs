# 타입변환(Type Conversion)

- 타입변환은 데이터 타입을 다른 데이터 타입으로 변환하는 것을 말한다.
- 타입변환은 명시적 타입 변환(explicit coercion)과 암시적 타입 변환(implicit coercion)으로 나뉜다.

## 명시적 타입 변환

- 명시적 타입 변환은 개발자가 직접 데이터 타입을 변환하는 것을 말한다.
- 또는 타입 캐스팅(type casting)이라고도 한다.

### 문자열 타입으로 변환

- 문자열 타입으로 명시적 타입 변환하는 경우는 다음과 같다.
  - `String` 생성자 함수를 사용한다.
  - Object.prototype.toString 메서드를 사용한다.
  - `+` 연산자를 통해 문자열 타입으로 변환한다.
  - 템플릿 리터럴을 사용한다.

example

```js
var str = String(1);
console.log(typeof str, str); // string 1

(1).toString(); // '1'
1 + ''; // '1'
```

### 숫자 타입으로 변환

- 숫자 타입으로 명시적 타입 변환하는 경우는 다음과 같다.
  - `Number` 생성자 함수를 사용한다.
  - Object.prototype.toString 메서드를 사용한다.
  - `+` 단항 산술 연산자를 통해 숫자 타입으로 변환한다.
  - `*` 산술 연산자를 통해 숫자 타입으로 변환한다.
  - `parseInt`, `parseFloat` 함수를 사용한다.

example

```js
var num = Number('1');
console.log(typeof num, num); // number 1

+'1'; // 1
'1' * 1; // 1
parseInt('1', 10); // 1
parseFloat('1.1'); // 1.1
```

### 불리언 타입으로 변환

- 불리언 타입으로 명시적 타입 변환하는 경우는 다음과 같다.
  - `Boolean` 생성자 함수를 사용한다.
  - Object.prototype.toString 메서드를 사용한다.
  - `!` 논리 부정 연산자를 두 번 사용한다.

## 암시적 타입 변환

- 암시적 타입 변환은 개발자가 직접 데이터 타입을 변환하지 않고 자바스크립트 엔진이 암묵적으로 데이터 타입이 변환되는 것을 말한다.
- 또는 타입 강제 변환(type coercion)이라고도 한다.

### 문자열 타입으로 변환

- 문자열 타입으로 암묵적 타입 변환하는 경우는 다음과 같다.
  - 문자열 연결 연산자(+)를 통해 문자열 타입으로 변환한다.
  - 템플릿 리터럴을 사용한다.

example

```js
var str = 1 + '';
console.log(typeof str, str); // string 1

var exp = `1 + 1 = ${1 + 1}`; // 평가 결과를 문자열로 암묵적 타입 변환한다.
```

### 숫자 타입으로 변환

- 숫자 타입으로 암묵적 타입 변환하는 경우는 다음과 같다.
  - 산술 연산자(-, \*, /, %)를 통해 숫자 타입으로 변환한다.
    - 피연산자를 숫자 타입으로 변환할 수 없다면 NaN을 반환한다.
  - 빈 문자열(''), 빈 배열(\[]), null, false는 0으로 암묵적 타입 변환한다.
  - true는 1로 암묵적 타입 변환한다.

example

```js
'1' - 0; // 1

var num = '' * 0;
console.log(typeof num, num); // number 0

+[]; // 0
null - 0; // 0
false - 0; // 0
true - 0; // 1

+undefined; // NaN
+{}; // NaN
+[1, 2]; // NaN
```

### 불리언 타입으로 변환

- 불리언 타입으로 암묵적 타입 변환하는 경우는 다음과 같다.
  - 빈 문자열(''), null, undefined, NaN, 0, -0은 false로 암묵적 타입 변환한다.
  - 그 외의 값은 true로 암묵적 타입 변환한다.
  - `if`, `삼항 조건 연산자`의 조건식은 암묵적 타입 변환을 거쳐 불리언 타입으로 평가한다.

> **주의할 점** 위에서 나온 두 가지 타입 변환이 기존의 원시 값을 변경하는 것이 아니라 새로운 원시 값을 생성한다는 것이다.
