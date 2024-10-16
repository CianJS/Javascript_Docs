# 일급 객체

자바스크립트의 객체는 아래 조건을 모두 만족하는 일급객체이다. 아래의 조건을 모두 충족하는 객체를 일급 객체라고 한다.

1. 무명의 리터럴로 생성할 수 있다. 즉, 런타임에 생성이 가능하다.
2. 변수나 자료구조(객체, 배열 등)에 저장할 수 있다.
3. 함수의 매개변수에 전달할 수 있다.
4. 함수의 반환값으로 사용할 수 있다.

Example

```js
// 1. 함수는 무명의 리터럴로 생성할 수 있다.
// 2. 함수는 변수에 저장할 수 있다.
// 런타임(할당 단계)에 함수 리터럴이 평가되어 함수 객체가 생성되고 변수에 할당된다.
const increase = function (num) {
  return ++num;
};

const decrease = function (num) {
  return --num;
};

// 2. 함수는 객체에 저장할 수 있다.
const predicates = { increase, decrease };

// 3. 함수의 매개변수에 전달할 수 있다.
// 4. 함수의 반환값으로 사용할 수 있다.
function makeCounter(predicate) {
  let num = 0;

  return function () {
    num = predicate(num);
    return num;
  };
}

// 3. 함수는 매개변수에게 함수를 전달할 수 있다.
const increaser = makeCounter(predicates.increase);
console.log(increaser()); // 1
console.log(increaser()); // 2

// 3. 함수는 매개변수에게 함수를 전달할 수 있다.
const decreaser = makeCounter(predicates.decrease);
console.log(decreaser()); // -1
```

위 예제에서 함수가 일급 객체라는 것은 함수를 객체와 동일하게 사용할 수 있다는 것을 의미한다. 객체는 값이기에 함수 또한 값으로 취급할 수 있다. ([함수 자세히보기](undefined.md))

일급 객체로서 함수가가 가지는 가장 큰 특징은 일반 객체처럼 함수의 매개변수에 전달할 수 있으며 함수의 반환값으로도 사용할 수 있다는 점이다.\
여기서 한 가지 다른 점은 일반 객체는 호출할 수 없지만 함수 객체는 호출할 수 있다는 것이다. ([내부 메서드 \[\[Call\]\]과 \[\[Construct\]\] 살펴보기](new-function.md))

## 함수 객체의 프로퍼티

console.dir 메서드를 사용하면 함수 객체의 프로퍼티를 확인할 수 있다.

```js
function square(number) {
  return number * number;
}

console.dir(square);
```

![](function\_property\_check.png)

아래는 square 함수의 모든 프로퍼티의 프로퍼티 어트리뷰트를 getOwnPropertyDescriptors 메서드로 확인한 것이다.

![](function\_descriptor\_check.png)

위 이미지에서처럼 arguments, caller, length, name, prototype 프로퍼티는 모두 함수 객체의 데이터 프로퍼티이다. 또한 일반 객체에는 없는 함수 객체 고유의 프로퍼티이다.

### arguments 프로퍼티

arguments 프로퍼티는 함수 호출 시 전달된 인수(argument)들의 정보를 담고 있는 순회 가능한(iterable) **유사 배열 객체**이며, 함수 내부에서 지역 변수처럼 사용된다.

자바스크립트는 함수의 매개변수와 인수의 개수가 일치하는지 체크하지 않는다. 따라서 함수를 호출할 때 매개변수에 인수를 할당하지 않으면 암묵적으로 undefined가 할당된다.

```js
function multiply(x, y) {
  console.log(arguments);
  return x * y;
}

console.log(multiply()); // NaN
console.log(multiply(1)); // NaN
console.log(multiply(1, 2)); // 2
console.log(multiply(1, 2, 3)); // 2
```

위 예제에서 multiply 함수는 매개변수 x, y를 선언하였다. 하지만 함수를 호출할 때 인수를 전달하지 않았다. 매개변수는 함수 몸체 내부에서 변수와 동일하게 취급된다. 함수가 호출되면 함수 몸체 내부에서 암묵적으로 매개변수가 선언되고 undefined로 초기화된다.

만약 선언된 매개변수의 개수보다 인수의 개수가 더 적으면 인수에 암묵적으로 할당된 undefined를 유지되어 사용된다. 반대로 선언된 매개변수의 개수보다 인수의 개수가 더 많으면 초과된 인수는 무시된다. 초과된 인수는 arguments 객체의 프로퍼티에 보관된다.

```js
function sum() {
  let res = 0;

  // arguments 객체는 length 프로퍼티를 갖는 유사 배열 객체이므로 for 문으로 순회할 수 있다.
  for (let i = 0; i < arguments.length; i++) {
    res += arguments[i];
  }

  return res;
}

console.log(sum()); // 0
console.log(sum(1, 2)); // 3
console.log(sum(1, 2, 3)); // 6
```

위 예제에서 sum 함수는 매개변수를 선언하지 않았다. 하지만 함수 몸체 내부에서 arguments 객체를 참조하여 인수의 개수에 상관없이 인수의 합을 구한다.\
즉, arguments 객체의 내부에 보관된 초과된 인수들이 보관되어 있다는 것을 의미한다.

위의 예제에서처럼 arguments 객체는 매개변수 개수를 확정할 수 없는 **가변 인자 함수**를 구현할 때 유용하다.

위쪽에 간단히 언급된 것처럼 arguments 객체는 유사 배열 객체인데, 유사 배열 객체란 length 프로퍼티를 가짐으로 for 문으로 순회할 수 있는 객체를 말한다.

> 유사 배열 객체와 이터러블
>
> > ES6에서 도입된 이터레이블 프로토콜을 준수하면 순회 가능한 자료구조인 이터러블이 된다. ES5에서는 이터러블의 개념이 없었기 때문에 arguments 객체는 유사 배열 객체로 구분되었다. 하지만 ES6부터 arguments 객체는 arguments 객체는 유사 배열 객체이면서 이터러블인 객체이다.

### caller 프로퍼티

caller 프로퍼티는 ECMAScript 사양에 포함되지 않은 비표준 프로퍼티이다.\
caller 프로퍼티는 함수 자신을 호출한 함수를 가리킨다.

```js
function foo(func) {
  return func();
}

function bar() {
  return "caller : " + bar.caller;
}

console.log(foo(bar)); // caller : function foo(func) { return func(); }
console.log(bar()); // caller : null
```

위 예제에서 bar 함수는 foo 함수에 의해 호출되었다. 이때 bar 함수의 caller 프로퍼티는 foo 함수를 가리킨다. 하지만 bar 함수는 일반 함수로서 호출되었기 때문에 caller 프로퍼티는 null을 가리킨다. 이는 모듈과 관련이 있다.

### length 프로퍼티

length 프로퍼티는 함수를 정의할 때 선언한 매개변수의 개수를 가리킨다.

```js
function foo() {}
console.log(foo.length); // 0

function bar(x) {
  return x;
}
console.log(bar.length); // 1

function baz(x, y) {
  return x * y;
}
console.log(baz.length); // 2
```

### name 프로퍼티

name 프로퍼티는 함수 이름을 나타낸다. 함수 객체의 name 프로퍼티는 ES6에서 도입되었다.

```js
// 기명 함수 표현식
var namedFunc = function foo() {};
console.log(namedFunc.name); // foo

// 익명 함수 표현식
var anonymousFunc = function () {};
// ES5: name 프로퍼티는 빈 문자열을 값으로 갖는다.
// ES6: name 프로퍼티는 함수 객체를 가리키는 변수 이름을 값으로 갖는다.
console.log(anonymousFunc.name); // anonymousFunc

// 함수 선언문
function bar() {}
console.log(bar.name); // bar

// ES6: 화살표 함수
const arrowFunc = () => {};
console.log(arrowFunc.name); // arrowFunc
```

### \_\_proto\_\_ 접근자 프로퍼티

모든 객체는 \_\_proto\_\_ 접근자 프로퍼티를 통해 자신의 프로토타입, 즉 \[\[Prototype]] 내부 슬롯에 간접적으로 접근할 수 있다.

```js
const obj = { a: 1 };

// obj 객체는 __proto__ 접근자 프로퍼티를 소유하지 않는다.
// obj 객체는 [[Prototype]] 내부 슬롯에 의해 Object.prototype 객체를 자신의 프로토타입으로 가지고 있다.
console.log(obj.__proto__ === Object.prototype); // true
```

### prototype 프로퍼티

prototype 프로퍼티는 생성자 함수로 호출할 수 있는 함수 객체, 즉 constructor만이 소유하는 프로퍼티이다.\
일반 객체와 생성자 함수로 호출할 수 없는 non-constructor는 prototype 프로퍼티를 소유하지 않는다.

```js
// 함수 객체는 prototype 프로퍼티를 소유한다.
(function () {}).hasOwnProperty("prototype"); // true

// 일반 객체는 prototype 프로퍼티를 소유하지 않는다.
({}).hasOwnProperty("prototype"); // false
```
