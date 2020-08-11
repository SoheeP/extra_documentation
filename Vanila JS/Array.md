# Array

배열은 Javascript에 내장되어 있는 <u>자료구조</u>이다. 객체의 일종이지만, 내부적으로 특별하게 취급되어 일반적인 객체들과는 다른 특징을 갖고 있다.

```js
console.log(typeof []) //object
```

`typeof`는 `object`로 결과가 나오지만, 배열은 `Array` 생성자의 인스턴스이며, 프로토타입 객체는 `object`와 다르게 `Array.prototype`이다.

대부분의 프로그래밍 언어에서 배열의 요소들은 모두 같은 데이터 타입이어야 하지만, 자바스크립트 배열은 어떤 데이터 타입의 조합이라도 포함할 수 있다.

```js
const misc = [
  'string',
  10,
  true,
  null,
  undefined,
  NaN,
  Infinity,
  ['nested array'],
  { object: true },
  function () {}
];

console.log(misc.length); // 10
```



### 배열 생성

`Array`생성자로 생성할 수도 있고, 배열 리터럴(`[]`)을 사용해서 생성할 수 있다.

```js
const createArr = new Array();
const createArr2 = [];
```

##### Array 생성자

`Array`생성자는 주어지는 인수에 따라 두 가지 방식으로 동작한다.

1. 인수가 1개일 경우 : 인수만큼 빈 배열을 만들어낸다. 만약 인수가 양의 정수가 아니라면 에러가 발생한다.

   ```js
   const createArr = new Array(3);
   console.log(createArr) // [empty x 3]
   ```

2. 이 외에 다른 모양으로 인수가 주어지면 그 인수들을 <u>요소</u>로 갖는 배열을 생성한다.

   ```js
   const createArr = new Array(1, 2, 3, 4);
   console.log(createArr) // [1, 2, 3, 4]
   ```

##### `Array.of`

`Array` 생성자의 동작 방식이 일관적이지 않는 문제로, ES6에 추가된 정적 메소드이다. `Array` 생성자와 달리, 인수를 요소로 가지는 배열을 생성한다.

```js
const createArr = Array.of(1, 2, 3)
console.log(createArr) // [1, 2, 3]

const oneElementArr = Array.of(2);
console.log(oneElementArr) // [1]
```

##### `Array.from`

이 메서드는 유사 배열 객체(array-like object)나 iterable한 객체를 배열로 변환해준다.

```js
//string 타입은 래퍼 객체를 통해 iterable로 다루어질 수 있다.
console.log(Array.from('hello')); // ["h", "e", "l", "l", "o"]

const divElements = document.querySelectorAll('div');
Array.from(divElements) // Array.prototype 들의 메서드를 쓸 수 있다.
```

> ❗ 원시타입과 래퍼 객체
>
> 원시타입: `string`, `number`, `boolean`, `null`, `undefined`, `symbol`
> 래퍼객체: `String`, `Number`, `Boolean`, `Symbol`
>
> 래퍼객체는 원시 타입을 감싸는 형태로 사용된다.
>
> ```js
> "hello".toUpperCase(); // "HELLO"
> ```
>
> `"hello"`는 원시타입의 `string`이지만 메소드를 호출할 수 있는데, 이는 프로그램이 문자열 `"hello"`의 프로퍼티를 참조하기 위해 래퍼객체로 임시로 변환하기 때문이다.
>
> ```js
> new String("hello").toUpperCase(); 
> ```
>
> 다만, 이렇게 생성된 임시 객체는 프로퍼티의 참조가 끝나면 소멸한다.

### 배열 요소 읽기, 추가, 수정, 삭제

##### 배열 요소 읽기

배열의 각 요소는 인덱스를 이용해 읽을 수 있으며, 0 이상의 정수만이 인덱스가 될 수 있다. 배열에 삽입된 순서대로 0부터 시작하는 인덱스를 가진다.

```js
const season = ['spring', 'summer', 'fall', 'winter'];

console.log(season[0]); // 'spring'
console.log(season[2]); // 'fall'
console.log(season[season.length - 1]); //'winter'
console.log(season[5]); // undefined
```

##### 배열 요소 추가

빈 배열일 경우, 인덱스를 사용하여 필요한 위치에 값을 할당할 수 있다. 배열의 길이는 마지막 인덱스를 기준으로 산정된다.

```js
const arr = [];

arr[1] = 1;
arr[3] = 3;
console.log(arr); // [empty, 1, empty, 3]
console.log(arr.length) // 4
```

존재하지 않는 요소를 참조하면 `undefined`가 반환된다.

```js
const arr = [];

arr[1] = 1;
arr[3] = 3;

//값이 할당되지 않은 인덱스 위치의 요소는 생성되지 않는다.
console.log(Object.keys(arr)) // ['1', '3']
console.log(arr[2]); // undefined 
```

##### 배열 요소 수정

인덱스로 요소를 직접 수정할 수 있다.

```js
const fruit = ['apple', 'pear', 'banana', 'strawberry'];

fruit[2] = 'blueberry';
console.log(fruit); // ['apple', 'pear', 'blueberry', 'strawberry']
```

##### 배열 요소 삭제

`delete` 연산자를 사용할 수 있다. 이 때, `length`에는 변함이 없다.

```js
const numberArr = [1, 2, 3, 4, 5];
delete numberArr[1];
console.log(numberArr) // [1, empty, 3, 4, 5]
```



### 메서드



출처: [includestdio](https://includestdio.tistory.com/26)