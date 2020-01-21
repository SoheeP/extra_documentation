# Axios

### 기본사용법

```js
 axios({config}).then(function(res){
     //handle success
 })
.catch(function(err){
     //handle error
 })
.finally(function(){
     //always executed even if success or fail
 })

// Multiple concurrent requests
function getUserAccount() {
  return axios.get('/user/12345');
}

function getUserPermissions() {
  return axios.get('/user/12345/permissions');
}

axios.all([getUserAccount(), getUserPermissions()])
  .then(axios.spread(function (acct, perms) {
    // Both requests are now complete
  }));
```

다만, 이렇게만 작성하면 데이터를 우후죽순으로 요청하고 response의 응답도 제각각으로 받게 될 것이다(비동기).

* 동기(Synchronous: 동시에 일어나는): 요청과 결과가 동시에 일어난다 => 결과가 발생하기 전까지 요청은 끝까지 완료되지 않는다
* 비동기(Asynchronous: 동시에 일어나지 않는): 요청과 결과가 동시에 일어나지 않는다 => 결과가 나중에 발생하더라도 요청은 계속 진행된다.

##### Async & Await

```js
async function getUser() {
  try {
    const response = await axios.get('/user?ID=12345');
    console.log(response);
  } catch (error) {
    console.error(error);
  }
}
```

