콜백과 프로미스(Promise)
==

콜백(Callback)
--

데이터 베이스의 Users 테이블을 제어하는 객체 Users가 있고

이 객체안에는 지정된 이름의 유저 한명을 비동기로 얻어오는 findOne 함수가 있다고 가정해보자.

```js
const Users = {
    findOne(name, callback) {
        let user = null;
        let err = null;

        // 데이터베이스에 name과 일치하는 유저를 쿼리해서 user 객체에 저장하고
        // 데이터베이스 요청이 실패한 경우 err에 에러 내용을 저장하는 임의의 코드
        // ...

        callback(err, user)
    }
};
```

위 함수를 이용해서 John이라는 유저를 가져오는 코드는 다음과 같다.

```js
Users.findOne('John', function(err, john) {
    if (err) {
        console.log(err);
        return;
    }

    console.log(john.status);
});
```

위 처럼 비동기 함수의 실행 결과를 전달 받기 위해 비동기 함수의 파라미터로 전달되는 함수를 **콜백**이라 부른다. 

이번에는 John, Peter, Alice를 순차적으로 가져오는 예제를 보자.

```js
Users.findOne('John', function(err, john) {
    if (err) {
        console.log(err);
        return;
    }

    Users.findOne('Peter', function(err, peter) {
        if (err) {
            console.log(err);
            return;
        }

        Users.findOne('Alice', function(err. alice) {
            if (err) {
                console.log(err);
                return;
            }

            console.log(john.status);
            console.log(peter.status);
            console.log(alice.status);
        });
    });
});
```

비동기 함수의 호출이 반복될때 마다 코드의 깊이가 한 단계씩 깊어져서 가독성이 안좋아지고

동일한 에러 처리 코드의 반복으로 코드가 장황해졌다.

위와 같은 현상을 **콜백 지옥(Callback Hell)** 이라고 부른다.

콜백 지옥은 코드를 쉽게 망가뜨리기 때문에 이를 해결하기 위해 프로미스를 사용한다.

프로미스(Promise)
--

