---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 문과 표현식

## 리터럴

- 숫자, 문자, 미리 약속된 기호('', \[], {} 등)로 표기한 코드
- JS 엔진은 런타임에 리터럴을 평가해 값을 생성한다.
- 값을 생성하기 위해 미리 약속한 표기법

## 표현식(expression)

위 용어 정리에서 보면 값으로 평가될 수 있는 문이라고 적혀있다.\
또한 바로 위에서 본 리터럴은 값으로 평가되기 때문에 **리터럴도 표현식**이라 할 수 있다.

```js
// 리터럴 표현식
8;
('soomgo');

// 식별자 표현식
profile;
soomgo.user;

// 연산자 표현식
10 + 20;
total == 100;

// 함수/메서드 호출 표현식
login();
profile.dispatchUnreadChatMessageCount();
```

## 문(Statement)

- 선언문, 할당문, 조건문, 반복문 등으로 구분할 수 있다.

```js
// 변수 선언문
var soomgo;

// 할당문
soomgo = 100;

// 함수 선언문
function foo() {}

// 조건문
if (soomgo > 10) {
  console.log(soomgo);
}
```

### 표현식인 문과 표현식이 아닌 문

표현식인 문

- 값으로 평가될 수 있는 문

표현식이 아닌 문

- 값으로 평가될 수 없는 문

```js
// 변수 선언문은 표현식이 아닌문이다.
var x;
// 할딩문은 그 자체가 표현식이지만 완전한 문이기도 하다. 즉, 할딩문은 표현식인 문이다.
x = 10;
// 반대로 표현식이 아닌 문은 값처럼 사용할 수 없다.
var foo = var x; // Uncaught SyntaxError: Unexpected token 'var'
```

> 완료 값
>
> > 크롬 개발자 도구에서 어떤 문을 실행하게 되면 undefined 또는 어떤 리터럴이 출력되는 것을 볼 수 있다.\
> > 여기서 표현식이 아닌 문이 실행되면 undefined를 출력하는데 이를 완료 값이라 한다.\
> > 표현식인 문을 실행하면 평가된 값을 반환한다.

### 블록문

0개 이상의 문을 중괄호({})로 묶은 것\
코드 블록 또는 블록이라고도 부른다.\
문의 끝에는 보통 세미콜론을 붙이는 것이 보통이지만 블록문은 세미콜론을 붙이지 않는다. 이는 블록문이 자체 종결성을 가지고있기 때문이다.

블록문은 중의적 표현이다. 즉, 블록문일 수도 있고 객체 리터럴일 수도 있다. 자바스크립트 엔진은 {}가 단독으로 존재하면 엔진은 블록문으로 해석하고, {}가 피연산자로 사용되면 객체 리터럴로 해석한다. 마찬가지로 함수 리터럴도 중의적인 코드이다. [함수](broken-reference) 이름이 있는 함수 리터럴이 단독으로 사용되면 함수 선언문으로 해석하고 함수 리터럴이 값으로 평가되어야하는 문맥(변수에 할당하거나 피연산자로 사용할때)에는 함수 리터럴 표현식으로 해석한다.

### 조건문

조건문은 조건식의 평가 결과에 따라 코드 블록을 실행한다. JS에서 조건문은 if...else문과 switch문을 제공한다.

#### if...else문

`if...else`문 조건식의 평가 결과에 따라 실행할 코드 블록을 결정한다.\
여기서 조건식은 불리언 값으로 평가되어야 한다. 만약 조건식이 불리언 값이 아닌 값으로 평가되면 조건식의 평가 결과는 불리언 값으로 암묵적 타입 변환된다.

추가로 `if...else`문은 표현식이 아닌 문이므로 값처럼 사용할 수 없다.\
하지만 `if...else`문과는 다르게 [삼항 조건 연산자](operator.md##삼항-조건-연산자)는 표현식이므로 값처럼 사용할 수 있다.\
이런 점을 잘 활용한다면 조금 더 간결하고 가독성이 좋은 코드를 작성할 수 있다.

```js
var condition;
if (true) {
  condition = true;
} else {
  condition = false;
}
// or
var condition = true ? true : false;
```

#### switch문

switch문은 조건식의 평가 결과와 일치하는 case문으로 실행 흐름을 이동시킨다.\
만약 조건식의 평가 결과와 일치하는 case문이 없다면 default문으로 실행 흐름을 이동시키거나 문의 끝까지 실행한다.\
또한 switch문에서 [break문](statement-and-expression.md#break문)을 사용하지 않으면 다음 case문으로 실행 흐름이 이어진다. 이를 [폴스루(fall through)](statement-and-expression.md#폴스루fall-through)라 한다.

```js
var x = 2;
switch (x) {
  case 1:
    console.log('1');
    break;
  case 2:
    console.log('2');
    break;
  case 3:
    console.log('3');
    break;
  default:
    console.log('default');
}
// 2
```

**폴스루(fall through)**

- switch문은 조건식의 평가 결과와 일치하는 case문을 찾으면 이후의 모든 case문을 건너뛴다.\
  이때 break문을 생략하면 다음 case문으로 실행 흐름이 이어진다. 이를 폴스루라 한다.

```js
// 폴스루 예제
var x = 1;
switch(x) {
  case 1:
  case 2: // case 1과 2는 같은 코드를 실행한다. 따라서 break문을 생략하면 1과 2는 폴스루된다.
    console.log('1 or 2');
    break;
  case 3:
    console.log('3');
    break;
  default:
    &nbsp;console.log('default');
}
// 1 or 2
```

### 반목문

반복문은 조건식의 평가 결과가 참인 경우 코드 블록을 반복 실행한다.\
JS에서 반복문은 for문, while문, do...while문을 제공한다.

#### for문

for문은 반복 횟수가 정해져 있는 경우 주로 사용한다.\
해당 문은 다음과같은 구조를 가진다.

```js
for (초기화식; 조건식; 증감식) {
  // 반복 실행할 문
}
```

- 초기화식: 변수 선언문 또는 할당문으로 이루어진 표현식이다.
- 조건식: 조건식은 불리언 값으로 평가되어야 한다. 조건식의 평가 결과가 참인 경우 코드 블록을 실행한다. (불리언 값이 아닌 값으로 평가되면 불리언 값으로 암묵적 타입 변환된다.)
- 증감식: 증감식은 [증가 또는 감소 연산자](operator.md#단항-산술-연산자)를 사용한 표현식이다. 증감식은 변수의 값을 증가 또는 감소시킨다.

```js
// for문 예제
for (var i = 0; i < 3; i++) {
  console.log(i);
}
// 0
// 1
// 2
```

위 각 식들은 생략할 수 있다.

```js
// 초기화식, 증감식 생략
var i = 0;
for (; i < 3; ) {
  console.log(i);
  i++;
}
// 0
// 1
// 2
```

만약 모든 식을 생략하면 무한루프가 된다.

```js
// 초기화식, 조건식, 증감식 모두 생략
var i = 0;
for (;;) {
  if (i > 2) break; // 무한루프를 방지하기 위해 break문을 사용한다. 하단의 break문에서 조금 더 자세히 설명한다.
  console.log(i);
  i++;
}
// 0
// 1
// 2
```

#### while문

while문은 조건식의 평가 결과가 참인 경우 코드 블록을 계속해서 반복 실행한다. 주로 반복횟수가 정해져 있지 않은 경우에 사용한다.\
while문은 다음과 같은 구조를 가진다.

```js
while (조건식) {
  // 반복 실행할 문
}
```

while문은 다음과같이 작성할 수 있다.

```js
// while문 예제
var i = 0;
while (i < 3) {
  console.log(i);
  i++;
}
// 0
// 1
// 2
```

while문은 조건식의 평가 결과가 항상 참이면 무한루프가 된다.

```js
// 무한루프
while (true) {
  console.log('무한루프');
}
```

무한루프를 방지하기 위해 while문은 break문과 함께 사용한다.

```js
// 무한루프를 방지하기 위해 break문과 함께 사용
var i = 0;
while (true) {
  if (i > 2) break;
  console.log(i);
  i++;
}
// 0
// 1
// 2
```

#### do...while문

do...while문은 while문과 구조가 거의 동일하다. 다만 do...while문은 코드 블록을 먼저 실행한 후 조건식을 평가한다.

```js
// do...while문 예제
var i = 0;
do {
  console.log(i);
  i++;
} while (i < 3);
// 0
// 1
// 2
```

### break문

break문은 반복문, switch문에서 실행 흐름을 벗어나게 한다.\
만약 그 와애서 break문을 사용하면 SyntaxError가 발생한다.

```js
var x = 1;
if (x === 1) {
  break;
}
// SyntaxError: Illegal break statement
```

아래는 일반적으로 break문을 사용하는 예제이다.

```js
// break문 예제
// 반복문
var i = 0;
while (true) {
  if (i > 2) break;
  console.log(i);
  i++;
}

// switch문
var x = 1;
switch (x) {
  case 1:
    break;
  case 2:
    break;
  default:
    break;
}
```

#### break문과 레이블 문

break문은 반복문, switch문에서만 사용할 수 있다. 하지만 break문은 레이블 문과 함께 사용하면 반복문, switch문 외에도 사용할 수 있다.

> **레이블 문**: **식별자가 붙은 문**으로 식별자는 반드시 유효한 식별자이어야 한다.
>
> ```js
> // 레이블 문 예제
> labelName: statement;
> ```

```js
// 레이블 문과 break문 예제
var x = 0;
var z = 0;

labelCancelLoops: while (true) {
  console.log('Outer loops: ' + x);
  x += 1;
  z = 1;
  while (true) {
    console.log('Inner loops: ' + z);
    z += 1;
    if (z === 10 && x === 10) {
      break labelCancelLoops;
    } else if (z === 10) {
      break;
    }
  }
}
// Outer loops: 0
// Inner loops: 1 ~ 9
// Outer loops: 1
// Inner loops: 1 ~ 9
// ...
```

> 바로 아래에 언급될 continue문도 레이블 문과 함께 사용할 수 있습니다.

### continue문

continue문은 반복문에서만 사용할 수 있다. continue문은 반복문의 현재 진행중인 반복을 멈추고 다음 반복을 실행한다.

```js
// continue문 예제
for (var i = 0; i < 5; i++) {
  if (i % 2) continue;
  console.log(i);
}
// 0
// 2
// 4
```
