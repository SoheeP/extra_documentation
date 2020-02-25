# Express - ejs 

### ejs 템플릿 로드

```js
// express-generator 를 꼭 깔아줘야 한다(4.0버전 이후부터는 따로 깔아줘야 한다고 한다)
$ npm i express-generator -g

$ express --view=ejs myapp(디렉토리명)
$ npm install
```



### [Tags](https://ejs.co/#docs)

* `<%` : 'Scriptlet' tag. for control-flow, no output
  &rarr; Node.js에서 실행된다. 일반적인 DOM 제어가 어렵다.
* `<%_` : 'Whitespace Slurping' Scriptlet tag, strips all whitespace before it
  &rarr; 공백을 숨기는 태그
* `<%=` : Outputs the value into the templete (HTML escaped)
  &rarr; string 형태로 값이 출력된다.
* `<%-` : Outputs the unescaped value into the templete
  &rarr; html도 그대로 출력된다.
* `<%#` : Comment tag, no execution, no output
* `<%%` : Outputs a literal '<%'
* `%>` : Plain ending tag
* `-%>` : Trim-mod('newline slurp') tag, trims following newline
* `_%>` : 'Whitespace Slurping' ending tag, removes all whitespace after it

##### 주의사항

1. `<% %>`로 변수 선언을 하면 스코프 적용이 된다. `ejs` 내 자바스크립트(js 파일)과 `<% %>` 안의 변수 명은 겹치더라도 따로 인식이 된다.
2. `var a = <%= 1 %>;` 은 가능, `<% var a %> = 1;` 은 안된다.
   내장된 코드의 값을 html파일로 불러와서 값을 넣을 순 있지만, 새로운 변수를 html파일에 내장시킬 수 없다.

참고자료: [[node.js] ejs 사용설명서](https://yahohococo.tistory.com/43), [[node.js]EJS 템플릿 엔진](https://araikuma.tistory.com/454)

