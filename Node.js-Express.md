# Node.js - Express

##### router.route(path)

선택적 미들웨어로 HTTP 동사를 처리하는 데 사용할 수있는 **단일 경로의 인스턴스를 리턴**합니다. `router.route ()`를 사용하여 **중복 경로 이름 지정 및 입력 오류를 방지**하십시오.
위의` router.param ()` 예제를 기반으로 다음 코드는 `router.route ()`를 사용하여 다양한 HTTP 메소드 핸들러를 지정하는 방법을 보여줍니다.
이 방법은 단일 `/ users / : user_id `경로를 재사용하고 다양한 HTTP 메소드에 대한 핸들러를 추가합니다.



참고 : `router.route ()`를 사용하는 경우 미들웨어 순서는 메소드 핸들러가 라우트에 추가 될 때가 아니라 라우트가 작성된시기를 기반으로합니다. 이를 위해 메소드 핸들러가 추가 된 경로에 속하는 것으로 간주 할 수 있습니다.

```js
var router = express.Router()

router.param('user_id', function (req, res, next, id) {
  // sample user, would actually fetch from DB, etc...
  req.user = {
    id: id,
    name: 'TJ'
  }
  next()
})

router.route('/users/:user_id')
  .all(function (req, res, next) {
    // runs for all HTTP verbs first
    // think of it as route specific middleware!
    next()
  })
  .get(function (req, res, next) {
    res.json(req.user)
  })
  .put(function (req, res, next) {
    // just an example of maybe updating the user
    req.user.name = req.params.name
    // save user ... etc
    res.json(req.user)
  })
  .post(function (req, res, next) {
    next(new Error('not implemented'))
  })
  .delete(function (req, res, next) {
    next(new Error('not implemented'))
  })
```





원문: 

Returns an instance of a single route which you can then use to handle HTTP verbs with optional middleware. Use `router.route()` to avoid duplicate route naming and thus typing errors.

Building on the `router.param()` example above, the following code shows how to use `router.route()` to specify various HTTP method handlers.
This approach re-uses the single `/users/:user_id` path and adds handlers for various HTTP methods.

NOTE: When you use `router.route()`, middleware ordering is based on when the *route* is created, not when method handlers are added to the route. For this purpose, you can consider method handlers to belong to the route to which they were added.

출처: [Express][Express]

[Express]: http://expressjs.com/en/4x/api.html#router.route



##### [process.cwd()](https://nodejs.org/api/process.html#process_process_cwd)

Added in: v.0.1.8

* Returns: <string>

```js
<%- include(`${process.cwd()}/views/Common/Base/head.ejs`, {path: 'index',title:"HOME "}) %>
```



The `process.cwd()` method returns the current working directory of the Node.js process.

##### Express-session

```js
//app.js

var session = require('express-session');

app.use(session({
    //config
    secret: '@#$Signature@!@#',
    resave: false,
    saveUninitialized: true
}))

```

* secret: 쿠키가 임의로 변조하는 것을 방지하기 위한 값. 이 값을 통해 세션을 암호화하여 저장한다.
* resave : 세션을 언제 저장할 지 정하는 값. `false`를 권장하며 필요하면 `true`로 설정
* saveUninitialized: 세션이 저장되기 전에 uninitialized 상태로 미리 만들어서 저장

출처: [Velopert.log](https://velopert.com/406)



##### res.locals()

요청의 범위가 지정된 **응답 로컬 변수**를 포함하는 객체로, 해당 요청 / 응답주기 동안 **렌더링 된 뷰**에만 사용 가능합니다 (있는 경우). 그렇지 않으면 이 속성은 `app.locals`와 동일합니다. 이 특성은 요청 경로 이름, 인증된 사용자, 사용자 설정 등과 같은 요청 레벨 정보를 노출하는 데 유용합니다.



```js
app.use(function (req, res, next) {
  res.locals.user = req.user
  res.locals.authenticated = !req.user.anonymous
  next()
})
```

* `app.locals` : 서버가 실행되기 전부터 `app`객체가 존재한다.
* `res.locals` : 클라이언트의 연결할 때마다 `res` 객체가 생긴다.



원문: An object that contains response local variables scoped to the request, and therefore available only to the view(s) rendered during that request / response cycle (if any). Otherwise, this property is identical to [app.locals](https://expressjs.com/ko/api.html#app.locals).

This property is useful for exposing request-level information such as the request path name, authenticated user, user settings, and so on.



##### Express - async / await

`router` 는 `async` 메소드가 아닌 경우 error가 발생하면 express의 에러 핸들러에서 처리하지만, `async` 키워드를 붙인 `callback` 함수 내의 error 를 감지하지 못한다.

```js
// Express 에러 핸들러
app.use('/asycn-function', (req, res) => {
    throw new Error('사용자 정의 에러 발생')
})

```

그래서 `async` 키워드가 붙은 `callback` 함수의 error는 아래처럼 `try catch`문을 이용해서 처리해줘야 한다.

```js
app.use('/async-function', async (req, res, next) => {
    try{
        const result = await asyncFunction();
        throw new Error('Async 사용자 정의 에러 발생');
        res.json(result);
    } catch(error) {
        next(error);
    };
});
```

위처럼 처리할 경우 매번 `async` 키워드에서  작성해줘야 하므로 `wrapper`를 작성해서 처리하는 게 좋다.

```js
function wrap(asyncFn) {
    return (async (req, res, next) => {
      try {
        return await asyncFn(req, res, next);
      } catch (error) {
        return next(error);
      }
    }); 
};
```

출처: [Express 라우트에서 async await를 사용하려면](https://medium.com/@changjoopark/express-%EB%9D%BC%EC%9A%B0%ED%8A%B8%EC%97%90%EC%84%9C-async-await%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EB%A0%A4%EB%A9%B4-7e8ffe0fcc84), [router 에서 asycn await callback사용하기](https://kjwsx23.tistory.com/199)