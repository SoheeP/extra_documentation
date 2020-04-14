# Js - Distructuring Assignment

### 구조 분해 할당(distructuring assignment)

비구조화 할당이라고도 하며, 객체나 배열을 변수로 분해할 수 있게 해주는 문법이다.

### 배열 분해하기

```js
let arr = ["Ilya", "Kantor"]

let [ firstName, surname ] = arr;

console.log(firstName); // "Ilya"
console.log(surname); // "Kantor"
```

`firstName`이란 변수와 ` surname` 이란 변수에 배열 `arr`의 요소를 하나씩 할당한다.



할당연산자(`=`) 좌측에는 할당할 수 있는(assignalbes) 것이라면 어떤 것이든 올 수 있다.

```js
let user = {};
[user.name, user.surname] = "Ilya Kantor".split(' ');

console.log(user.name) // "Ilya"
```



할당연산자(`=`) 좌측 값 갯수와 우측 값 갯수가 반드시 일치할 필요가 없다. 만약 좌측의 변수 개수가 우측 값 개수보다 많으면 남는 변수에는 `undefined` 값이 할당 된다.

```js
let [a, b, c] = [1, 2] // a = 1, b = 2, c = undefined
```

```js
var arr, first, second;
arr = [ first, second ] = [1, 2, 3, 4]

console.log(arr) // [1, 2, 3, 4]
console.log(first) // 1
console.log(second) // 2
```



#### 활용

##### 메서드 사용하여 분해하기.

```js
let [ firstName, surname ] = "Ilya Kantor".split(' ');
```



##### 쉼표 구분자로 필요없는 요소 건너뛰기

```js
let [ firstName, , title] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];

console.log(firstName) // "Julias"
console.log(title) // "Consul"
```



##### 이미 선언된 변수를 이용하기

```js
let [a, b] = [1, 2] // a = 1, b = 2
[a, b] = [b, a] // a = 2, b = 1
[c, d] = [2*a, 2*b] // c = 4, d = 2
```



##### 기본값 할당하기

```js
let [a=0, b=1, c=2] = [1, 2] // a = 1, b = 2, c = 2
```



##### `.entries()`로 반복해서 할당하기

```js
let user = {
    name: "John",
    age: 30
};

for(let [key, value] of Object.entries(user)){
    console.log(`${key}:${value}`);
}

// console.log(name:John)
// console.log(age:30)
```

* `Object.entries()`

  - `for...in`과 같은 순서로 주어진 객체 자체의 enumerable(열거할 수 있는) 속성 `[key, value]`쌍의 **배열**을 반환한다.

    ```js
    const object1 = {
      a: 'somestring',
      b: 42
    };
    console.log(Object.entries(object1))
    // [ ["a", "somestring"], ["b", 42] ]
    ```



##### `map` 활용하기

```js
let user = new Map();
user.set("name", "John");
user.set("age", "30");

for (let [key, value] of user) {
  console.log(`${key}:${value}`); 
}

// console.log(name:John)
// console.log(age:30)
```



> **:exclamation: 분해(destructuring)은 파괴(destructive)를 의미하지 않는다.**
>
> 어떤 것을 복사 한 뒤 변수로 분해(destructurizes)해주는 것이며, 이 과정에서 분해 대상은 수정 또는 파괴되지 않는다.

##### 반환 값을 비구조화 할당 받기

```js
let [name = prompt('name?'), surname = prompt('surname?')] = ["Julius"];

console.log(name);    // Julius
console.log(surname); // prompt로부터 받아온 값
```

* 변수  `name`은 배열에서 값을 받기 때문에, 함수가 기본값으로 지정된 `surname`의 `prompt` 함수만 실행이 된다.



##### 전개 구문(Spread syntax, '`...`') 나머지 요소 가져오기

```js
let [ name1, name2, ...rest ] =  ["Julius", "Caesar", "Consul", "of the Roman Republic"];

console.log(name1); // "Julius"
console.log(name2); // "Caesar"
console.log(rest) // [ "Consul", "of the Roman Republic" ]
```



출처: [모던 javascript 튜토리얼](https://ko.javascript.info/destructuring-assignment), 모던 자바스크립트 입문(책), [Object.entries(MDN)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/entries)

