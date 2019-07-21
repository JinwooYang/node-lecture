화살표 함수
==

기존 함수는 다음과 같이 선언했다.

```js
function add(x, y) {
    return x + y;
}
```

또는 다음과 같이 함수를 변수에 할당해서 이용했다.
```js
var add = function(x, y) {
    return x + y;
};
```

ES6에서는 **화살표 함수(arrow function)** 가 추가되었다.

```js
const add = (x, y) => { 
    return x + y;
}
```

함수내에 return문 1줄만 존재할때는 줄여서 다음과 같이 쓸 수 있다.

```js
const add = (x, y) => x + y;
```

기존 함수와 화살표 함수는 this 객체의 바인딩 규칙이 다르다.

기존 함수의 this는 함수의 호출자로 바인딩되지만, 화살표 함수의 this는 함수 바깥 스코프의 this 객체를 그대로 캡처한다.

다음은 호출자가 변경될 때 this 객체가 어떻게 변경되는지 보여주는 예제이다.
```js
const objA = {
    name: 'objA',
    whoAmI() {
        console.log(this.name);
    }
};

objA.whoAmI(); // objA

const objB = {
    name: 'objB',

    whoAmI: objA.whoAmI
};

// objA의 whoAmI 함수를 가져왔지만
// 호출자가 objB이기 때문에 this는 objB가 된다.
objB.whoAmI(); // objB
```

다음의 코드를 보고 출력 결과를 예상해보자.

```js
const multiplier = {
    numbers: [1, 2, 3],
    factor: 2,

    multiplyAll() {
        this.numbers.forEach(function(num) {
            console.log(num * this.factor);
        });
    }
};

multiplier.multiplyAll();
```

얼핏보면 2, 4, 6이 출력되어야 할 것 같지만 그렇지 않다.

위 코드의 forEach 내부로 전달된 function은 this.factor에 접근하고 있다.
하지만 this 객체는 호출자이고 이 function의 호출은 forEach 내부에서 이루어지므로 이 때 호출자는 multiplier 객체가 아니다.

따라서 this.factor는 undefined 값이 되고 때문에 출력 결과는 다음과 같다.

```
NaN
NaN
NaN
```

위 코드를 우리가 의도한대로 동작하게 만드려면 this 객체를 바깥쪽 스코프에서 대입해놓고 사용하는 방법이 있다.

```js
const multiplier = {
    numbers: [1, 2, 3],
    factor: 2,

    multiplyAll() {
        const self = this;
        this.numbers.forEach(function(num) {
            console.log(num * self.factor);
        });
    }
};

multiplier.multiplyAll();
```

출력:
```
2
4
6
```

또는 화살표 함수를 사용하면 된다.

```js
const multiplier = {
    numbers: [1, 2, 3],
    factor: 2,

    multiplyAll() {
        this.numbers.forEach((num) => {
            console.log(num * this.factor);
        });
    }
};

multiplier.multiplyAll();
```

