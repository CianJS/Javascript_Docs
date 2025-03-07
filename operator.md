# 연산자(Operator)

여기서는 자바스크립트에서 제공하는 연산자들을 다룹니다.

1. [산술 연산자](operator.md#산술-연산자)
2. [할당 연산자](operator.md#할당-연산자)
3. [비교 연산자](operator.md#비교-연산자)
4. [삼항 조건 연산자](operator.md#삼항-조건-연산자)
5. [논리 연산자](operator.md#논리-연산자)
6. [쉼표(,) 연산자](operator.md#쉼표-연산자)
7. [그룹 연산자](operator.md#그룹-연산자)
8. [typeof 연산자](operator.md#typeof-연산자)
9. [지수 연산자](operator.md#지수-연산자)

ps. [연산자 우선순위와 결합성](operator.md#연산자-우선순위와-결합성)

## 산술 연산자

1. [이항 산술 연산자](operator.md#이항-산술-연산자)
2. [단항 산술 연산자](operator.md#단항-산술-연산자)
3. [문자열 연결 연산자](operator.md#문자열-연결-연산자)

### 이항 산술 연산자

- 두 개의 피연산자를 산술 연산한다.
- 이항 산술 연산자는 피연산자에 어떠한 영향을 주지 않는다.
  - 즉, 피연산자의 값이 바뀌지 않는다.

```js
8 + 2; // 10
3 + 4; // 7

var a = 3;
var b = 6;
a + b; // 9

console.log(a, b); // 3 6
```

### 단항 산술 연산자

- 한 개의 피연산자를 산술 연산한다.

**+ 단항 연산자**는 피연산자를 숫자 타입으로 변화하여 반환한다.

```js
// 다만, 숫자 타입에게는 아무런 변화를 주지 않는다.
+5; // 5
var a = 3;
+a; // 3

var x = '5';
+x; // 5

var y = 'Test';
+y; // NaN (숫자 타입으로 변환할 수 없기에 NaN이 반환된다.)
+true; // 1
+false; // 0
+null; // 0
```

**- 단항 연산자**는 부호를 반전시키는 효과가 있다.

```js
var b = 10;
-b; // -10

-true; // 0
-false; // 1
-null; // -0

var x = 'hello world';
-x; // NaN
```

> `+null === -null` 는 `true`다.\
> 개발자 도구에서 각각을 따로 입력해보면 아래와같이 출력이 된다.\
> `+null` // 0\
> `-null` // -0\
> 0과 -0에 대한 비교가 되는 셈인데, ES6에서 새로 도입된 Object.is 메서드를 사용하면 더욱 정확한 비교가 가능하다. [일치 비교 연산자 자세히 살펴보기](operator.md#일치-비교)\
> Object.is(+null, -null); // false

[이항 산술 연산자](operator.md#이항-산술-연산자)와는 달리 피연산자에 영향을 주는 연산자가 있다.

- 증가/감소(++/--) 연산을 하면 피연산자의 값을 변경하는 암묵적 할당이 발생한다.

```js
var a = 1;

a++;
console.log(a); // 2

a--;
console.log(a); // 1
```

> [증가 연산자](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Increment)와 [감소 연산자](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Decrement)는 피연산자의 앞에 위치해있거나 뒤에 위치함에 따라 동작하는 방식이 다르다.

### 문자열 연결 연산자

\+ 기호는 만약 피연산자가 하나라도 문자열이 있다면 **문자열 연결 연산자**로 동작한다.

```js
'1' + 0; // 10
1 + '0'; // 10
```

## 할당 연산자

- 우항의 피연산자의 평가 결과를 좌항의 변수에 할당한다.
- 할당문은 표현식인 문이다.
  - 우항에 있는 값으로 평가된다.

```js
var a;
console.log((a = 10)); // 10

// 할당문은 표현식인 문이므로 다른 변수에 할당할 수도 있다.
var x = (z = 10);
console.log(x, z); // 10 10
```

## 비교 연산자

1. [동등 비교(==)](operator.md#동등-비교)
2. [일치 비교(===)](operator.md#일치-비교)
3. [대소 관계 비교 연산자](operator.md#문자열-연결-연산자)

### 동등 비교(==)

- 좌항과 우항의 피연산자를 비교할때 **암묵적 타입 변환**을 하여 타입을 일치시킨 뒤에 두 값을 비교한다.

> 암묵적 타입 변환(implicit coercion)에 대해 자세히 알아보려면 해당 [링크](https://dev.to/promisetochi/what-you-need-to-know-about-javascripts-implicit-coercion-e23)의 게시글을 읽어보자

```js
0 == '0'; // true
```

### 일치 비교(==)

- 암묵적 타입 변환을 하지 않고 비교한다.
  - 즉, 타입도 같고 값도 같은 경우에 true로 판단한다.

```js
0 === '0'; // false
10 === 10; // true
```

- 주의사항
  - NaN은 NaN과 일치 비교를 하면 false가 나온다.
  - 이 문제는 빌트인 함수인 Number.isNaN을 사용해 해결하자

```js
NaN === NaN; // false
Object.is(NaN, NaN); // false
Number.isNaN(NaN); // true
```

### 대소 관계 비교 연산자

```js
5 < 10; // true
5 > 10; // false
5 <= 5; // true
5 >= 10; // false
```

## 삼항 조건 연산자

- 삼항 조건 연산자는 조건식의 평가 결과에 따라 반환할 값을 결정한다.
- 만약 첫 번째 피연산자가 true이면 두 번째 피연산자를 반환하고, false이면 세 번째 피연산자를 반환한다.
  - 그러나 첫 번째 피연산자가 불리언 값이 아니라면 불리언 값으로 암묵적 타입 변환을 한다.

```js
var score = 85;
var result = score >= 60 ? '합격' : '불합격';
console.log(result); // 합격
```

추가로 살펴보자면 삼항 조건 연산자는 값으로 평가할 수 있는 표현식인 문이다. 위 예제처럼 변수에 할당하거나 다른 표현식의 피연산자로 사용할 수도 있다.

```js
var result = 'JS대 ' + (score >= 60 ? '합격' : '불합격');
console.log(result); // JS대 합격
```

## 논리 연산자

```js
// 논리곱(&&) 연산자
true && true; // true
true && false; // false
false && true; // false
false && false; // false

// 논리합(||) 연산자
true || true; // true
true || false; // true
false || true; // true
false || false; // false

// 논리 부정(!) 연산자
!true; // false
!false; // true
```

- 논리 부정(!) 연산자는 언제나 불리언 값이 반환된다. 하지만 피연산자가 불리언 값이 아닌 경우 불리언 값으로 **암묵적 타입 변환**된다.
- 논리곱(&&) 또는 논리합(||) 연산자는 평가 결과가 불리언이 아닐 수도 있다.
  - 논리곱과 논리합 연산자는 좌항에서 우항으로 평가가 진행된다.
  - 논리곱 연산자는 피연산자 중 하나라도 Falsy라면 false로 평가되어 false로 평가된 항의 값을 그대로 반환한다. 반대로 전부 Truthy라면 마지막 피연산자의 값을 반환한다.
  - 논리합 연산자는 피연산자 중 하나라도 Truthy이면 true를 반환한다. 만약 첫번째 항에서 true로 평가되었다면 첫번째 항의 값을 반환하고 두번째 피연산자는 평가하지 않는다.
    - 위와 같은 평가 방식을 **단축 평가**라고 한다. 즉, 평가 결과가 확정된 경우 나머지 평가 과정을 생략하는 것을 말한다.

> 드 모르간의 법칙
>
> > 논리 연산자를 조금 더 가독성 좋은 표현식으로 변환할 수 있다. `!(a && b) === !a || !b` >> `!(a || b) === !a && !b`

## 쉼표(,) 연산자

- 쉼표 연산자는 각각의 피연산자를 왼쪽에서 오른쪽 순서로 평가하고, 마지막 연산자의 값을 반환합니다.

```js
var x = 1;

x = (x++, x);
console.log(x); // 2

x = (2, 3);
console.log(x); // 3
--------------------
var a, b, c;

a = b = 3, c = 4; // 콘솔에는 4를 반환
console.log(a); // 3
```

## 그룹 연산자

- 수학 기호에서 사용하는 괄호와 같은 역할을 한다. (우선순위가 가장 높다)

```js
var x = 2 * (3 + 4);
console.log(x); // 14
```

## typeof 연산자

typeof 연산자는 아래와같이 사용할 수 있다.

> typeof <피연산자(변수, 또는 리터럴)>

- typeof 연산자로 변수를 연산하면 변수의 데이터 타입을 반환한다.
  - 더 정확히 이야기하면 변수에 할당된 값의 데이터 타입을 반환한다.\
    변수는 메모리 주소를 알고있을뿐인 [식별자](variable.md#식별자)이기때문이다.

```js
typeof 123; // number
typeof NaN; // number
typeof '123'; // string
typeof true; // boolean
typeof undefined; // undefined
typeof undeclaredVariable; // undefined
typeof Symbol(); // symbol
typeof {}; // object
typeof []; // object
typeof function () {}; // function
typeof null; // object
```

## 지수 연산자

- ES2016(ES7)에서 도입된 지수 연산자는 **거듭제곱**을 나타낸다.

```js
2 ** 3; // 8

// 만약 음수를 거듭제곱하려면 괄호로 묶어야 한다.
(-2) ** 2; // -4
```

ES2016(ES7) 이전에는 Math.pow 메서드를 사용해야 했다.

```js
Math.pow(2, 3); // 8
```

## 옵셔널 체이닝 연산자(?.)

- ES2020(ES11)에서 도입된 옵셔널 체이닝 연산자는 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고, 그렇지 않은 경우 우항의 프로퍼티 참조를 이어간다.

```js
var foo = null;
var baz = foo?.bar; // undefined

var foo = { name: 'Lee', age: 20 };
var baz = foo?.bar; // undefined

// falsy임에도 불구하고 옵셔널 체이닝 연산자는 프로퍼티 참조를 이어가는 경우
var foo = { name: 'Lee', age: 20, job: '' };
var baz = foo?.job; // ''

// 옵셔널 체이닝 연산자는 함수 호출에도 사용할 수 있다.
var foo = null;
var baz = foo?.(); // undefined
```

## null 병합 연산자(??)

- ES2020(ES11)에서 도입된 null 병합 연산자는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고, 그렇지 않은 경우 좌항의 피연산자를 반환한다.

```js
var foo = null;
var bar = 'default string';

var baz = foo ?? bar; // 'default string'
```

## 연산자 우선순위와 결합성

우선순위가 높은 연산자가 먼저 실행되고, 우선순위가 낮은 연산자가 나중에 실행된다.\
정확한 우선순위는 [MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)을 참고하자.

좌결합성과 우결합성\
좌결합성은 왼쪽에서 오른쪽으로 평가되고, 우결합성은 오른쪽에서 왼쪽으로 평가된다.

```js
// 좌결합성
2 + 3 + 4; // 9
2 + 3 + 4; // 이것과 같다.
// 우결합성
// 할당 연산자도 우결합성이다. 아래처럼 평가가 진행된다.
var x = (y = 2);
```
