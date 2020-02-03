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

출처: 

[Express]: http://expressjs.com/en/4x/api.html#router.route



