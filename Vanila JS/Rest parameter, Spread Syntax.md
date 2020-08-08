# Rest parameter, Spread Syntax 

### Rest Parameter(나머지 매개변수)

Rest 파라미터는 매개변수 이름 앞에 세개의 점 `...`을 붙여서 정의한 매개변수를 의미한다.

```js
function foo(...rest){
    console.log(Array.isArray(rest)); // true
    console.log(rest); // [1, 2, 3, 4, 5]
}

foo(1, 2, 3, 4, 5)

function sumArr(...rest){
    let sum = 0;
    for (let arg of rest) sum += arg;
    return sum;
}

alert( sumAll(1) ); //1
alert( sumAll(1, 3, 4) ) //8
```

함수에 전달된 인수들은 순차적으로 파라미터와 Rest 파라미터에 할당된다.

```js
function foo(param1, param2, ...rest){
    console.log(param1); // 3
    console.log(param2); // 5
    console.log(rest); // [2, 1, 4]
}

foo(3, 5, 2, 1, 4)
```

> ❗ Rest 파라미터는 남은 인수를 모으는 역할을 하므로, **<u>항상 마지막에 있어야 한다.</u>**
>
> ```js
> function foo(...rest, arg1) {} //error
> function foo(arg, ...rest, arg2) {} //error
> ```

Rest 파라미터는 함수 정의 시 선언한 매개변수 개수를 나타내는 함수 객체의 `length` 프로버티에 영향을 주지 않는다.

```js
function foo(...rest){}
console.log(foo.length) // 0

function bar(x, ...rest) {}
console.log(bar.length) // 1
```

### arguments 와 rest 파라미터

ES5에서는 인자의 개수를 사전에 알 수 없는 가변 인자 함수의 경우, `arguments` 객체를 통해 인수를 확인할 수 있다.

`arguments`객체는 순화가능한(iterable) 유사배열객체이며 함수 내부에서 지역변수처럼 사용할 수 있다.

```js
function showName() {
  alert( arguments.length );
  alert( arguments[0] );
  alert( arguments[1] );

  // arguments는 이터러블 객체이기 때문에
  // for(let arg of arguments) alert(arg); 를 사용해 인수를 나열할 수도 있다.
}

// 2, Julius, Caesar가 출력됨
showName("Julius", "Caesar");

// 1, Ilya, undefined가 출력됨(두 번째 인수는 없음)
showName("Bora");
```

유사배열객체이므로 배열 메소드를 사용하려면 `Function.prototype.call`을 사용해야 한다.

```js
// ES5
function sum() {
  /*
  가변 인자 함수는 arguments 객체를 통해 인수를 전달받는다.
  유사 배열 객체인 arguments 객체를 배열로 변환한다.
  */
  var array = Array.prototype.slice.call(arguments);
    //혹은 Array.from(arguments).slice 를 이용해도 된다.
  return array.reduce(function (pre, cur) {
    return pre + cur;
  });
}

console.log(sum(1, 2, 3, 4, 5)); // 15
```

> ❗ 화살표 함수에는 함수 객체의 `arguments` 프로퍼티가 없다.
>
> 화살표 함수에서 `arguments`객체에 접근 하면, 외부에 있는 일반 함수의 `arguments`객체를 가져온다.
>
> ```js
> function f() {
>   let showArg = () => alert(arguments[0]);
>   showArg();
> }
> 
> f(1); // 1
> ```
>
> 따라서 **<u>화살표 함수로 가변 인자 함수를 구현해야 할 때는 반드시 rest 파라미터를 사용</u>**해야 한다.
>
> ```js
> var normalFunc = function () {};
> console.log(normalFunc.hasOwnProperty('arguments')); // true
> 
> const arrowFunc = () => {};
> console.log(arrowFunc.hasOwnProperty('arguments')); // false
> ```

### Spread Syntax

rest 파라미터처럼 `...`을 사용하지만, Spread 문법은 대상을 개별 요소로 분리한다. Spread 문법의 대상은 이터러블이어야 한다.

```js
// ...[1, 2, 3]는 [1, 2, 3]을 개별 요소로 분리한다(→ 1, 2, 3)
console.log(...[1, 2, 3]) // 1, 2, 3

// 문자열은 이터러블이다.
console.log(...'Hello');  // H e l l o

// Map과 Set은 이터러블이다.
console.log(...new Map([['a', '1'], ['b', '2']]));  // [ 'a', '1' ] [ 'b', '2' ]
console.log(...new Set([1, 2, 3]));  // 1 2 3

// 이터러블이 아닌 일반 객체는 Spread 문법의 대상이 될 수 없다.
console.log(...{ a: 1, b: 2 });
// TypeError: Found non-callable @@iterator
```





출처: [Poiemaweb](https://poiemaweb.com/es6-extended-parameter-handling), [모던 javascript 튜토리얼](https://ko.javascript.info/rest-parameters-spread)

