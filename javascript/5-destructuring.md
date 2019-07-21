비구조화 할당
==

다음과 같은 객체가 있다고 해보자.
```js
const john = {
    name: 'John',
    status: {
        isTired: false,
        isHappy: true
    },
    friends: [
        'Peter',
        'Alice',
        'Logan',
        'Amy'
    ],
};
```

ES5에서는 다음처럼 객체의 속성값을 하나씩 가져와야 했다.

```js
var name = john.name;
var status = john.status;
```

ES6에서는 다음과 같이 가져올 수 있다.

```js
const {name, status, friends} = john;

console.log(name);    // John
console.log(status);  // {isTired: false, isHappy: true}
console.log(friends); // ["Peter", "Alice", "Logan", "Amy"]
```

비구조화 할당은 배열에도 적용되며 다음과 같은 코드를 사용할 수 있다.

```js
const [peter, alice, , amy, matilda = 'Unknown'] = friends;

console.log(peter);   // Peter
console.log(alice);   // Alice
console.log(amy);     // Amy

// 4번 인덱스의 요소는 없으므로 기본값인 Unknown이 출력된다.
console.log(matilda); // Unknown
```

나머지 패턴을 이용하면 배열의 나머지 요소들을 한번에 가져올 수 있다.
```js
const [peter, ...restFriends] = friends;

console.log(restFriends); // ["Alice", "Logan", "Amy"]
```