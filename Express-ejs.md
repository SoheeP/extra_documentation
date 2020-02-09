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



