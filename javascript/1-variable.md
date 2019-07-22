변수 선언
==

변수 선언 방식에는 세가지 키워드 (var, let, const)가 존재한다.

var
--

ES6 이전에 사용하던 방식.
변수의 재선언이 가능하며 *function-scoped* 이기 떄문에 다음 코드가 문제없이 동작한다.

```js
// 이미 선언한 변수의 재선언이 가능하다.
var a = 5;
var a = 'Hello world';
```
```js
// 변수를 if 블록 안에서 선언했다.
if (true) {
    var a = 3;
}

// 하지만 if 블록 바깥에서도 접근이 가능하다.
console.log(a); // output: 3
```

위 코드에서 변수 a가 if 블록 바깥에서도 접근이 가능한 이유는

자바스크립트에서는 변수의 선언부와 할당부가 다음과 같이 분리되기 떄문이다.

```js
// 변수 a의 선언이 전역 스코프로 이동했다.
var a;

if (true) {
    a = 3;
}

console.log(a); // output: 3
```

위와 같은 동작을 **호이스팅(hoisting)** 이라고 부르며 var는 function 단위로 호이스팅 되기 떄문에 의도치 않은 실수를 일으키기 쉬워진다.

let, const
--

ES6 이후로 추가된 키워드. var와는 다르게 변수의 재선언이 불가능하고 *block-scoped* 이므로 다음 코드에서 에러가 발생한다.

```js
// 변수의 재선언이 불가능하다.
let a = 5;
let a = 'Hello world'; // SyntaxError: Identifier 'a' has already been declared
```

```js
// 변수를 if 블록 안에서 선언했다.
if (true) {
    let a = 3;
}

// if 블록 밖에서 접근할 수 없다.
console.log(a); // ReferenceError: a is not defined
```

let과 const 키워드가 호이스팅 되지 않는 것은 아니다.
단지 let, const는 function 단위가 아닌 block 단위로 호이스팅이 일어난다.

예를 들어 아래의 코드는
```js
if (true) {
    console.log(a);
    let a = 10;
}
```

아래의 코드로 변환된다.
``` js
if (true) {
    let a;
    console.log(a);
    a = 10;
}
```

그렇다고해서 위 코드에서 에러가 발생하지 않는건 아니다.
let 키워드는 할당되지 않은 변수를 사용할때 에러를 일으키므로 `console.log(a);` 를 실행할 때 `ReferrenceError` 가 발생한다.

let과 const의 차이
--

let 키워드로 선언한 변수는 재할당이 가능하지만 const로 선언한 변수는 재할당이 불가능하다.

```js
let a = 10;
a = 'Hello world'; // 문제 없음
```

```js
const a = 10;
a = 'Hello world'; // TypeError: Assignment to constant variable
```

또한 const는 반드시 변수를 선언 할 때 초기값 할당이 이루어져야 한다.

```js
let a;
a = 'Hello world'; // 문제 없음
```

```js
const a; // SyntaxError: Missing initializer in const declaration
a = 'Hello world';
```