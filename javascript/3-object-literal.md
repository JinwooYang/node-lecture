객체 리터럴
==

ES6 이전에는 객체 리터럴이 다음과 같았다.
```js
var sayNode = function() {
    console.log('Node');
};

var es = "ES";

// ES5 객체 리터럴
var oldObject = {
    sayJS: function() {
        console.log('JS');
    },
    sayNode: sayNode
};

// 동적 속성 할당은 리터럴 내부에서 불가능 했었음.
oldObject[es + 6] = 'Fantastic';
```

ES6 부터는 동일한 이름의 속성은 축약해서 한번만 적어도 되고 동적 속성 할당도 리터럴 내부에서 가능해졌다.
```js
// ES6 객채 리터럴
const newObject = {
    sayJS() {
        console.log('JS');
    },

    // 동일한 이름의 속성은 축약해서 적어도 된다.
    sayNode,

    // 동적 속성 할당도 리터럴 내부에서 처리 가능
    [es + 6]: 'Fantastic'
};
```
