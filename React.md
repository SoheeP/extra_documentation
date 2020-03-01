# React

[TOC]





## 1. 개요

* Component 장점
  1. 가독성
  2. 재사용성
  3. 유지보수가 용이

### 개발환경 셋팅

* 툴체인: 필요한 도구(Tool)들이 모여 원하는 기능을 한번에 제공하도록 연결된 도구

```js
/**
* 기본설치
* version 명령어 단축키 대문자임에 주의할 것 - 3.4.0
*/
$ npm i -g create-react-app
$ create-react-app -V
```

* `npx` : `npm`을 실행시키되 임시로 실행하는 것과 같은 역할을 한다. 
  - 항상 최신상태로, 1회만 실행하기 때문에 컴퓨터의 저장공간을 차지하지 않는다는 장점이 있다.

그러나 어차피 계속 react 를 사용할 것이므로 `npm`으로 설치.

### Code 작성

```js
//실행
$ npm run start
```

* Public : `index.html` 파일이 있는 곳. Component들은 `#root`부분에 삽입된다.
* Src : 작업을 진행하는 폴더.



##### index.js

```js
// APP(component)을 랜더링(삽입)하고, index.html에 있는 #root 에 삽입된다.
ReactDOM.render(<App />, document.getElementById('root'));
```



##### App.js

```js
//함수형
import React from 'react';
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}


//class 형
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
  render(){
    return (
      <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
    );
  };
};
```



### Deploy(배포)

```js
$ npm run build

//간단한 웹서버
$ npm i -g serve
$ serve -s build
// or 
$ npx -g serve -s build
```

* build 폴더가 생기면서 필요한 부분만 취급해서 용량을 더 줄여준다.
  &rarr; 최상위 폴더에 build폴더 안쪽에 생성된 폴더들을 서버에 올려야 적용된다!



## 2. React 코딩

```jsx
class App extends Component {
  render(){
    return (
      <div className="App">
      <Subject></Subject>
    </div>
    );
  };
};

class Subject extends Component {
  render(){
    //render()는 반드시 있어야 한다
    //return 할때, 하나의 최상위 코드(div역할)가 무조건 있어야 한다
    return (
      <header>
        <h1>Web</h1>
        World Wide Web!
      </header>
    );
  };
};
```

* 이 문법은 `js`와 유사한, `jsx`로 작성한 것이며 이를 `create-react-app`에서 해석하는 것
* 컴포넌트의 이름에만 집중하게 함으로써 기본적인 복잡도를 낮춰주고, 더 많은 복잡한 코드를 좀 더 구현할 수 있는 가능성이 생긴다. :)

### attribute 사용하기

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
    //attribute 를 props 라고 이해하면 될 것 같다.
  }
}
```



### State / Props

* Component의  속성을 사용, 조작할 수 있는 `props` &rarr; 사용자에게 더 중요한 정보(외부적 정보)
* 사용자들이 알 필요가 없는(!) 정보가 `state` - 내부적 정보

```jsx
class App extends Component {
  constructor(props){
    //컴포넌트 초기화 시켜주고 싶은 코드를 넣는다
    super(props);
    this.state = {
      //초기화 대상
      subject: { title: 'Web', sub: 'World Wide Web'}
    }
  }
  render(){
    return (
      <div className="App">
      <Subject title={this.state.subject.title} sub="World Wide Web!"></Subject>
      <Subject title="React" sub="For UI"></Subject>
      <TOC></TOC>
      <Content title="HTML" desc="HTML is HyperText Markup Language."></Content>
    </div>
    );
  };
};
```

* `jsx`에서는 `render()` 할 html 코드 중 `js` 변수를 써서 보이고 싶은 부분은 `{}` 를 사용해서 쓰면 된다.

참고자료: 인프런 - 생활코딩, react 공식문서