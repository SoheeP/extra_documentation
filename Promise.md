# Promise

Promise는 비동기 처리를 실행하고, 그 처리가 끝난 후에 다음 처리를 실행하기 위해 사용하는 **객체**

```js
// Promise 객체 생성
var promise = new Promise(function(resolve, reject) { ... });
```

* `resolve` : **함수 안의 처리가 끝났을 때** 호출해야 하는 콜백 함수. `resolve` 함수에는 어떠한 값도 인수로 넘길 수 있음. 이 값은 다음 처리를 실행하는 함수에 전달된다.
  &rarr; 이 함수가 실행되면 `then` 메서드에 등록한 함수가 실행되면서 `Promise` 안의 처리를 종료시킨다.
* `reject` : **함수 안의 처리가 실패했을 때** 호출해야 하는 콜백 함수. `reject` 함수에는 어떠한 값도 인수로 넘길 수 있음. 대부분의 경우 오류메시지의 문자열을 인수로 사용한다.
  &rarr; 이 함수가 실행되면 `Promise` 안의 처리를 종료시키며 `catch` 메서드로 인수를 넘긴다. 에러 핸들러로 사용

```js 
var promise = new Promise(function(resolve, reject){
    setTimeout(function(){
        console.log('A');
        resolve(); // 이때 인수를 넣으면 다음 then 실행 함수의 인수로 넘겨진다.
    }, 1000);
});
promise.then(function(){
    //resolve()가 실행 됐을 때 아래 코드가 실행이 된다
    console.log("B")
});
```

```js
//ajax 통신일 때
function getData(callback){
    $.get('url', function(response){
        callback(response); //서버의 response를 callback함수의 인수로 넘긴다
    });
};

getData(function(tableData){
    console.log(tableData); //이때 tableData는 이전에 전달 받은 response값
});

// 위 코드를 Promise로 바꾸면 아래 코드처럼 된다.
function getData(callback){
    return new Promise(function(resolve, reject){
        $.get('url', function(response){
            resolve(response);
        });
    });
};

getData().then(function(tableData){
    console.log(tableData); //response 값이 tableData로 전달
});
```



### then 메서드

```js
promise.then(onFullfilled);
```

* `onFullfilled` 함수는 **성공 콜백 함수**라고 하며 인수로 `response`를 받는다.
* `then` 메서드는 두번째 인수로 실패 콜백 함수를 지정할 수 있다. 성공하면 `onFullfilled`함수가 실행되고, 실패하면 `onRejected` 함수가 실행된다.
  &rarr; 아래에 나오는 `catch` 메서드에서 처리할 내용을 `then` 메서드 하나로 작성할 수 있다!

```js
promise.then(onFullfilled, onRejected);
```



### reject 함수와 catch 메서드

```js
promise.catch(onRejected);
```

* `onRejected` 함수는 **실패 콜백 함수**라고 하며  인수로 `error`를 받는다.

```js
var promise = new Promise(function(resolve, reject){
    setTimeout(function(){
        var n = parseInt(prompt("10 미만의 숫자를 입력하십시오"));
        if ( n <= 10 ){
            resolve(n);
        } else {
            reject(`오류: ${n}은 10 이상입니다.`)
        };
    }, 1000);
});

promise
.then(function(num){
    // 위에서 입력을 받은 n이 num으로 전달된다.
    console.log(`2^${num} = ${Math.pow(2, num)}`); 
})
.catch(function(error){
    // 위에서 입력한 reject의 인수를 받아오며 에러메세지를 띄운다
    console.log(error);
})
```



참고자료: 모던자바스크립트 입문(책), [자바스크립트 Promise 쉽게 이해하기](https://joshua1988.github.io/web-development/javascript/promise-for-beginners/)

