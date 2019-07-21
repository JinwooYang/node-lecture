템플릿 문자열
==

기존 자바스크립트에서 문자열을 조합할때는 다음과 같이 + 기호를 사용했다.

```js
var name = 'John';
var age = 20;
var job = 'programmer';

var str = '안녕 내 이름은 ' + name + '. 나는 ' + age + '살이고 직업은 ' + job + '야.';

console.log(str); // output: 안녕 내 이름은 John. 나는 20살이고 직업은 programmer야.
```

ES6 에서는 템플릿 문자열을 이용해 다음과 같이 조합할 수 있다.

```js
const name = 'John';
const age = 20;
const job = 'programmer';

const str = `안녕 내 이름은 ${name}. 나는 ${age}살이고 직업은 ${job}야.`;

console.log(str); // output: 안녕 내 이름은 John. 나는 20살이고 직업은 programmer야.
```

일반 문자열과 달리 `(back tick) 기호로 문자열을 감싸고, 조합할 변수 이름을 ${}로 감싸준다.