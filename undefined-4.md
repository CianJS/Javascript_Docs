# 생성자 함수

생성자 함수란 new 연산자와 함께 호출하여 객체(인스턴스)를 생성하는 함수를 말한다.\
자바스크립트는 Object, String, Number, Boolean, Function, Array, Date, RegExp, Promise 등의 빌트인 생성자 함수를 제공한다.

```js
const strObj = new String("Lee");
console.log(typeof strObj); // object
console.log(strObj); // String {"Lee"}

const numObj = new Number(123);
console.log(typeof numObj); // object
console.log(numObj); // Number {123}

const boolObj = new Boolean(true);
console.log(typeof boolObj); // object
console.log(boolObj); // Boolean {true}

const func = new Function("x", "return x * x");
console.log(typeof func); // function
console.dir(func); // f anonymous(x)
```

만약 위의 예제들과는 다르게 new 연산자와 함께 호출하지 않으면 생성자 함수로 동작하지 않고 일반 함수로 동작한다.

```js
const strObj = String("Lee");
console.log(typeof strObj); // string
console.log(strObj); // Lee
```

이러한 생성자 함수들 중에서 Object 생성자 함수를 살펴볼 것이다.

## Object 생성자 함수

Object 생성자 함수는 new 연산자와 함께 호출하여 객체를 생성한다.

```js
const obj = new Object();
obj.name = "Lee";
console.log(obj); // {name: "Lee"}
```

객체를 생성하는 방식은 두 가지가 있다. 첫 번째는 객체 리터럴을 사용하는 방식이고, 두 번째는 생성자 함수를 사용하는 방식이다. 이 중에서 객체 리터럴을 사용하는 방식이 더 간편하고 직관적이므로 객체 리터럴을 사용하는 것이 일반적이다.\
하지만 객체 리터럴에 의한 객체 생성 방식은 단 하나의 객체만 생성한다. 따라서 동일한 프로퍼티를 갖는 객체를 여러 개 생성해야 하는 경우에는 생성자 함수를 사용하는 편이 같은 프로퍼티를 계속 작성하지 않아도 되므로 보다 더 효율적이다.

```js
// 객체 리터럴을 사용한 방식
const obj1 = { name: "Lee", age: 20 };
const obj2 = { name: "Kim", age: 30 };
const obj3 = { name: "Park", age: 40 };
const obj4 = { name: "Choi", age: 50 };
```

반면에 위의 예제처럼 생성자 함수에 의한 객체 생성 방식은 객체(인스턴스)를 생성하기 위한 템플릿처럼 사용하여 프로퍼티 구조가 동일한 객체 여러 개를 간편하게 생성할 수 있다.

```js
// 위 예제를 생성자 함수를 사용하여 구현하면 다음과 같다.
const Person = function (name, age) {
  this.name = name;
  this.age = age;
};

const obj1 = new Person("Lee", 20);
const obj2 = new Person("Kim", 30);
const obj3 = new Person("Park", 40);
const obj4 = new Person("Choi", 50);
```

> this
>
> > this는 객체 자신의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수다. this가 가리키는 값, 즉 this 바인딩은 함수 호출 방식에 의해 동적으로 결정된다.

|  함수 호출 방식 | this가 가리키는 값(this 바인딩) |
| :-------: | :--------------------: |
|  일반 함수 호출 |          전역 객체         |
|   메서드 호출  | 메서드를 호출한 객체(마침표 앞의 객체) |
| 생성자 함수 호출 | 생성자 함수가 (미래에) 생성할 인스턴스 |

## 생성자 함수의 인스턴스 생성 과정

생성자 함수는 인스턴스를 생성하기위한 템플릿으로서 동작하여 인스턴스를 생성하는 것과 생성된 인스턴스를 초기화한다.\
그러나 생성자 함수의 코드 내부들 들여다보면 인스턴스를 생성하고 초기화하는 코드는 보이지 않는다.

```js
const Person = function (name) {
  this.name = name;
};

const me = new Person("Lee");
console.log(me); // Person {name: "Lee"}
```

new 연산자와 함께 생성자 함수를 호출하면 자바스크립트 엔진은 다음과 같은 과정을 거쳐 인스턴스를 생성하고 반환한다.

1. 인스턴스 생성과 this 바인딩
   1. 빈 객체 생성 및 this 바인딩
      1. 빈 객체를 생성한다. 이때 빈 객체는 암묵적으로 생성되며, 암묵적으로 생성된 빈 객체는 this에 바인딩된다.
   2. 생성자 함수 코드 실행
      1. this에 바인딩되어 있는 인스턴스를 초기화한다.

```js
const Person = function (name) {
  // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
  console.log(this); // Person {}

  // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
  this.name = name;
};

// 인스턴스 생성과 this 바인딩
const me = new Person("Lee");
console.log(me); // Person {name: "Lee"}
```

2. 인스턴스 초기화
   1. this에 바인딩되어 있는 인스턴스를 초기화한다.
      1. this에 바인딩되어 있는 인스턴스를 초기화한다.

```js
const Person = function (name) {
  // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
  console.log(this); // Person {}

  // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
  this.name = name;
};

...
```

3. 인스턴스 반환
   1. 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.

```js
const Person = function (name) {
  // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
  console.log(this); // Person {}

  // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
  this.name = name;
};

...

// 3. 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.
console.log(me); // Person {name: "Lee"}
```

만약 여기서 생성자 함수 내부에서 명시적으로 this가 아닌 다른 객체를 반환하면 this에 바인딩되어 있는 인스턴스가 아닌 return 문에 의해 명시적으로 반환한 객체가 반환된다.

```js
const Person = function (name) {
  // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
  console.log(this); // Person {}

  // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
  this.name = name;

  // 3. 명시적으로 다른 객체를 반환하면 this에 바인딩되어 있는 인스턴스가 아닌
  // 명시적으로 반환한 객체가 반환된다.
  return {};
};

const me = new Person("Lee");
console.log(me); // {}
```

하지만 명시적으로 원시값을 반환하면 원시값 반환은 무시되고 암묵적으로 this가 반환된다.

```js
const Person = function (name) {
  // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
  console.log(this); // Person {}

  // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
  this.name = name;

  // 3. 명시적으로 원시값을 반환하면 원시값 반환은 무시되고 암묵적으로 this가 반환된다.
  return 100;
};

const me = new Person("Lee");
console.log(me); // Person {name: "Lee"}
```

이러한 특징을 가진 생성자 함수에 명시적으로 this가 아니라 다른 값을 반환하는 것은 생성자 함수의 기본 동작에 위배되기 때문에 생성자 함수 내부에 return 문을 반드시 생략해야 한다.

## 내부 메서드 \[\[Call]]과 \[\[Construct]]

함수는 객체이므로 일반 객체와 동일하게 동작한다. 함수 객체는 일반 객체가 가지고 있는 내부 슬롯과 내부 메서드 모두 가지고 있기 때문이다. 뿐만 아니라 함수 객체만을 위한 \[\[Environment]] 내부 슬롯과 \[\[Call]], \[\[Construct]] 내부 메서드를 추가로 가지고 있다.

함수가 일반 함수로서 호출되면 함수 객체의 내부 메서드 \[\[Call]]이 호출되고 new 연산자와 함께 생성자 함수로서 호출되면 내부 메서드 \[\[Construct]]가 호출된다.

내부 메서드 \[\[Call]]을 갖는 함수 객체를 callable이라 한다. callable 함수는 함수 객체를 일반 함수처럼 호출할 수 있다. 이때 함수 객체의 내부 메서드 \[\[Call]]이 호출된다.\
또한 내부 메서드 \[\[Construct]]를 갖는 함수 객체를 constructor라 한다. constructor 함수는 new 연산자와 함께 생성자 함수로서 호출할 수 있다. 이때 함수 객체의 내부 메서드 \[\[Construct]]가 호출된다. 반대로 \[\[Construct]]를 갖지 않는 non-constructor 함수는 new 연산자와 함께 생성자 함수로서 호출할 수 없다.

### constructor와 non-constructor의 구분

자바스크립트 엔진은 함수 정의를 평가하여 함수 객체를 생성할 때 함수 정의 방식에 따라 함수를 constructor와 non-constructor로 구분한다.

* constructor: 함수 선언문, 함수 표현식, 클래스
* non-constructor: 메서드(ES6 메서드 축약 표현), 화살표 함수

여기서 중요한 점은 ECMAScript 사양에서 메서드란 ES6의 메서드 축약 표현만을 의미한다. 즉, 함수가 어디에 할당되어 있는지에 따라 메서드인지를 구분하는 것이 아니라 함수 정의 방식에 따라 constructor와 non-constructor를 구분한다.

```js
// 함수 선언문
function foo() {}

// 함수 표현식
const bar = function () {};

// 일반 함수로서 호출
foo(); // foo 함수 객체의 내부 메서드 [[Call]]이 호출된다.
bar(); // bar 함수 객체의 내부 메서드 [[Call]]이 호출된다.

// 생성자 함수로서 호출
new foo(); // foo 함수 객체의 내부 메서드 [[Construct]]가 호출된다.
new bar(); // bar 함수 객체의 내부 메서드 [[Construct]]가 호출된다.

// 메서드 축약 표현과 화살표 함수
const obj = {
  x() {},
};
const arrow = () => {};
new obj.x(); // TypeError: obj.x is not a constructor
new arrow(); // TypeError: arrow is not a constructor
```

## new 연산자

non-constructor가 아니라 constructor인 함수를 new 연산자와 함께 호출하면 해당 함수는 생성자 함수로 동작한다. 이때 내부 메서드 \[\[Construct]]가 호출된다.

```js
function add(x, y) {
  return x + y;
}

const addInst = new add();
// 객체가 아니라 원시값이 반환되어 반환문이 무시된다. 따라서 빈 객체가 생성되어 반환된다.
console.log(addInst); // add {}

// 객체를 반환하는 일반 함수
function Person(name) {
  return { name };
}

const me = new Person("Lee");
// 함수가 생성한 객체를 반환한다.
console.log(me); // Person {name: "Lee"}
```

위의 예제는 new 연산자를 통해 함수를 호출해 인스턴스를 생성했다. 하지만 반대로 new 연산자가 없이 함수를 호출하면 일반 함수로서 호출된다. 이때 내부 메서드 \[\[Call]]이 호출된다.

```js
function add(x, y) {
  this.total = x + y;
  return x + y;
}

const result = add(1, 2); // 함수로서 호출
console.log(result); // 3
console.log(total); // 3 - 일반 함수로서 호출된 함수의 this는 전역 객체 window를 가리킨다.
```

## new.target

ES6에서 도입된 new.target은 함수 내부에서 new 연산자와 함께 생성자 함수로서 호출되었는지 확인할 수 있는 연산자이다. new 연산자와 함께 생성자 함수로서 호출되면 함수 내부의 new.target은 함수 자신을 가리킨다. 하지만 new 연산자 없이 일반 함수로서 호출된 함수 내부의 new.target은 undefined다.

```js
function Circle(radius) {
  // 이 함수가 new 연산자와 함께 호출되지 않았다면 new.target은 undefined다.
  if (!new.target) {
    // new 연산자와 함께 생성자 함수를 재귀 호출하여 생성된 인스턴스를 반환한다.
    return new Circle(radius);
  }

  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// new 연산자 없이 생성자 함수를 호출하여도 new.target을 통해 생성자 함수로서 호출된다.
const circle = Circle(5);
console.log(circle.getDiameter()); // 10
```

> 스코프 세이프 생성자 패턴(scope-safe constructor pattern)
>
> > new.target은 ES6에서 도입된 문법으로 IE에서는 지원되지않는다. 따라서 스코프 세이프 생성자 패턴을 사용하여 new 연산자와 함께 생성자 함수로서 호출되었는지 확인할 수 있다.
> >
> > ```js
> > function Circle(radius) {
> >   // 이 함수가 new 연산자와 함께 호출되지 않았다면 this는 window를 가리킨다.
> >   if (!(this instanceof Circle)) {
> >     // new 연산자와 함께 생성자 함수를 재귀 호출하여 생성된 인스턴스를 반환한다.
> >     return new Circle(radius);
> >   }
> >
> >   this.radius = radius;
> >   this.getDiameter = function () {
> >     return 2 * this.radius;
> >   };
> > }
> >
> > // new 연산자 없이 생성자 함수를 호출하여도 생성자 함수로서 호출된다.
> > const circle = Circle(5);
> > console.log(circle.getDiameter()); // 10
> > ```

여기서 참고로 대부분의 빌트인 생성자 함수(Array, Number, String, Boolean, Function, Object, Promise 등)는 new 연산자와 함께 호출되었는지를 확인하여 new 연산자와 함께 호출되지 않았다면 암묵적으로 new 연산자를 사용하여 호출한 것처럼 동작한다.

```js
let obj = new Object();
console.log(obj); // {}

obj = Object();
console.log(obj); // {}

let f = new Function("x", "return x ** x");
console.log(f); // ƒ anonymous(x) { return x ** x }

f = Function("x", "return x ** x");
console.log(f); // ƒ anonymous(x) { return x ** x }
```

빌트인 생성자 함수들 중에서 String, Number, Boolean은 new 연산자와 함께 호출되었을 때 객체를 생성하여 반환하지만 new 연산자 없이 호출하면 문자열, 숫자, 불리언 값을 반환한다.

```js
const str = String(123);
console.log(str, typeof str); // 123 string

const num = Number("123");
console.log(num, typeof num); // 123 number

const bool = Boolean("true");
console.log(bool, typeof bool); // true boolean
```
