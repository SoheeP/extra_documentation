# JS import, export / CommonJS

### import, export - ES6 기반 모듈 내보내기, 불러오기

```js
import moment from 'moment';
```

##### 이점

* 모듈 관리 전용 키워드를 사용하기 때문에 가독성이 좋다.
  * `import`, `from`, `export`, `default`
* 비동기 방식으로 작동하므로 성능, 메모리 부분에서 유리하다.
* Named Parameter과 같은 CommonJs에서는 지원하지 않는 기능이 있다.

### 복수 객체 내보내기 / 불러오기

##### 내보내기

```js
// 예제코드 - currencty-function.js

const exchangeRate = 0.91;

// 안 내보냄
function roundTwoDecimals(amount) {
  return Math.round(amount * 100) / 100;
}

// 바로 내보내기 1
export function canadianToUs(canadian) {
  return roundTwoDecimals(canadian * exchangeRate);
}

// 선언 후 내보내기 2
const usToCanadian = function(us) {
  return roundTwoDecimals(us / exchangeRate);
};
export { usToCanadian };
```

* 내보내는 변수나 함수의 이름이 그대로 불러 낼 때 사용하게 되는 이름이 된다.
  &#8594; Named Exports

##### 불러오기

```js
// Destructuring
import { canadianToUs } from './currency-functions';

console.log('50 Canadian dollars equals this amount of US dollars:');
console.log(canadianToUs(50));

// Alias
import * as currency from './currency-functions';

console.log('30 US dollars equals this amount of Canadian dollars:');
console.log(currency.usToCanadian(30));
```



### 단일 객체 내보내기 / 불러오기

##### 내보내기

```js
//예제코드 - currency-object.js
const exchangeRate = 0.91;

// 안 내보냄
function roundTwoDecimals(amount) {
  return Math.round(amount * 100) / 100;
}

// 내보내기
export default {
  canadianToUs(canadian) {
    return roundTwoDecimals(canadian * exchangeRate);
  },

  usToCanadian: function(us) {
    return roundTwoDecimals(us / exchangeRate);
  }
};
```

* `export default` 키워드를 사용해서 한 객체로 묶어서 내보낸다.

* 이름이 정해지지 않아서 불러올 때 아무 이름이나 사용해서 불러올 수 있다.

* 만약 변수에 할당해서 내보내야 한다면, 아래처럼 작성할 수 있다.

  * ```js
    const obj = {
      canadianToUs(canadian) {
        return roundTwoDecimals(canadian * exchangeRate);
      }
    };
    
    obj.usToCanadian = function(us) {
      return roundTwoDecimals(us / exchangeRate);
    };
    
    export default obj;
    ```



##### 불러오기

```js
import currency from './currency-object';

console.log('50 Canadian dollars equals this amount of US dollars:');
console.log(currency.canadianToUs(50));

console.log('30 US dollars equals this amount of Canadian dollars:');
console.log(currency.usToCanadian(30));
```

* export에 이름이 없기 때문에, 불러온 모듈은 어떤 이름으로 불러내도 상관없다.



### CommonJS

`require` 키워드를 통해 불러오는 방식을 말하며, NodeJS에서 사용하고 있는 CommonJS키워드이기도 하다.

```js
const moment = require('moment');
```

##### 주의사항

* 특정 변수나 그 변수의 속성으로 내보낼 객체를 세팅해줘야 한다.
* `exports`, `module.exports` 는 사용해야할 상황이 다르다.
  1. 여러 개의 객체를 내보낼 경우, `exports` 변수의 속성으로 할당한다.
  2. 단 하나의 객체를 내보낼 경우, `module.exports` 변수 자체에 할당한다.



[출처]: https://www.daleseo.com/js-module-import/	"자바스크립트 ES6 모듈 내보내기/불러오기(import)"

