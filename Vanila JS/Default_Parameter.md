# 매개변수 기본값

### 매개변수 기본값(Default Parameter value)

함수를 호출할 때 사용하는 매개변수(parameter)의 개수보다 인수(argument)가 적더라도 에러가 발생하진 않지만, `undefined`값이 나와서 의도치 않은 값이 도출될 수 있다.

```js
function sum(x, y){
    return x + y
}
console.log(sum(1)) // error가 아니라 NaN이 나온다.
```

매개변수에 적절한 인수가 전달되었는지 확인할 수 있다.

```js
function sum(x, y){
    //매개변수 값이 falsy value일 때, 기본값 0 할당.
    x = x || 0;
    y = y || 0;
    return x + y;
}

//아래처럼 써도 된다.
function sum(x = 0, y = 0){
    return x + y;
}
```

매개변수 기본값은 함수 정의 시 선언한 매개변수의 개수를 나타내는 함수 객체의 `length` 프로퍼티와 `arguments` 객체에 영향을 주지 않는다.

```js
function foo(x, y = 0){
    console.log(arguments)
}

console.log(foo.length) // arguments가 y만 기본값이 할당되어 있어서 1

foo(3) // Arguments [3]
foo(3, 2) // Arguments [3, 2] 인수가 두개여도 arguments의 length는 1
```

