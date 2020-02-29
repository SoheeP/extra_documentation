# JS window.location

### `window.location`

예제 도메인: `http://www.example.com:8080/find?q=devmo#test`

##### Properties

| Property | Description                                    | Example                                         |
| -------- | ---------------------------------------------- | ----------------------------------------------- |
| hash     | 주소값에 붙어있는 `anchor` 값 반환             | `#test`                                         |
| host     | URL의 도메인과 포트 반환                       | `www.example.com:8080`                          |
| hostname | URL의 도메인 반환                              | `www,example.com`                               |
| href     | URL 반환                                       | `http://www.example.com:8080/find?q=devmo#test` |
| origin   | 프로토콜 + URL의 도메인 + 포트 반환            | `http://www.example.com:8080`                   |
| pathname | URL 경로 반환                                  | `/find`                                         |
| port     | 서버포트 반환                                  | `8080`                                          |
| protocol | 프로토콜 반환                                  | `http:`                                         |
| search   | URL에 붙은 매개변수 `queryString(?)` 값을 반환 | `?q=devmo`                                      |



##### Methods

| Method           | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| assign(url)      | 새로운 주소 이동                                             |
| reload(forceget) | 현재페이지 새로고침                                          |
| replace(url)     | 새로운 주소 이동(세션 히스토리가 남지 않으므로 back버튼으로 이동 불가) |

```js
//새페이지로 이동
window.location.assign("http://www.example.com");
window.location = "http://www.example.com";

//현재 페이지 새로고침
window.location.reload(true);

// replace()를 이용하여 새 페이지로 이동
function reloadPageWithHash (){
    let initialPage = window.location.pathname;
    window.location.replace('http://example.com/#' + initialPage);
}
```



출처: [[javascript] window.location 객체](https://august5pm.tistory.com/8)