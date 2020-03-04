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

##### app.js

```jsx
class App extends Component {
  constructor(props){
    //컴포넌트 초기화 시켜주고 싶은 코드를 넣는다
    super(props);
    this.state = {
      //초기화 대상
      subject: { title: 'Web', sub: 'World Wide Web'},
      contents: [
        {id: 1, title: 'HTML', desc: 'HTML is for informaition'},
        {id: 2, title: 'CSS', desc: 'CSS is for design'},
        {id: 3, title: 'JavaScript', desc: 'JavaScript is for interactive'},
      ]
    }
  }
  render(){
    return (
      <div className="App">
      <Subject title={this.state.subject.title} sub={this.state.subject.sub}></Subject>
      <Subject title="React" sub="For UI"></Subject>
      <TOC data={this.state.contents}></TOC>
      <Content title="HTML" desc="HTML is HyperText Markup Language."></Content>
    </div>
    );
  };
};
```

* `jsx`에서는 `render()` 할 html 코드 중 `js` 변수를 써서 보이고 싶은 부분은 `{}` 를 사용해서 쓰면 된다.

##### TOC.js

```jsx
class TOC extends Component {
  render(){
    let list = [];
    let data = this.props.data;
    let i = 0;
    while(i < data.length){
      list.push(<li key={data[i].id}><a href={"/content/"+data[i].id}>{data[i].title}</a></li>);
      i ++;
    }
    return(
      <nav>
        <ul>
          {list}
        </ul>
      </nav>
    )
  }
}

export default TOC;
```

* 태그를 반복문으로 생성하다보면, 실제 랜더링 했을때 아래와 같은 에러가 나타난다.

> index.js:1 Warning: Each child in a list should have a unique "key" prop.
>
> Check the render method of `TOC`. See https://fb.me/react-warning-keys for more information.
>     in li (at TOC.js:9)
>     in TOC (at App.js:26)
>     in div (at App.js:23)
>     in App (at src/index.js:7)

이 메시지는 react 내부에서 태그를 구별하기 위한 `key`값이 필요하다고 요구하는 상황이므로 필요한 `key`값을 함께 삽입해주면 아래 에러 메시지는 나타나지 않는다.

### event

react에서는 `props`나 `state` 값이 바뀌면 해당되는 컴포넌트의 `render()`가 항상 새로 실행되며, 화면이 새로 그려진다.

```jsx
class Subject extends Component {
  render(){
    return (
      <header>
        <h1><a href="/" onClick = {function(){
          alert('hi');
        }.bind(this)}>{this.props.title}</a></h1>
        {this.props.sub}
      </header>
    );
  };
};
```

* 이 경우 `a` 태그의 기본 이벤트 동작(click) 때문에 페이지가 새로고침되면서, 페이지가 새로 그려진다.
  &rarr; `e.preventDefault()` 로 변경

`header`의 링크를 클릭 했을 때, App.js 파일에 있는 `mode` 값을 바꾸고 싶다면 아래 처럼 `this`를 이용해서 쓸 수 있다.

##### App.js 

이해를 돕기 위해, Subject 부분에 `header`를 직접 삽입함)

```jsx
class App extends Component {
  constructor(props){
    //컴포넌트 초기화 시켜주고 싶은 코드를 넣는다
    super(props);
    this.state = {
      mode: 'read',
      //초기화 대상
      subject: { title: 'Web', sub: 'World Wide Web'},
      welcome: { title: 'Welcome', desc: 'Hello, React!!'},
      contents: [
        {id: 1, title: 'HTML', desc: 'HTML is for informaition'},
        {id: 2, title: 'CSS', desc: 'CSS is for design'},
        {id: 3, title: 'JavaScript', desc: 'JavaScript is for interactive'},
      ]
    }
  }
  render(){
    let _title, _desc = null;
    if(this.state.mode === 'welcome'){
      _title = this.state.welcome.title;
      _desc = this.state.welcome.desc;
    } else if(this.state.mode === 'read') {
      _title = this.state.contents[0].title;
      _desc = this.state.contents[0].desc;
    }
    return (
      <div className="App">
      <Subject title={this.state.subject.title} sub={this.state.subject.sub}></Subject>
      <header>
        <h1><a href="/" onClick = {function(e){
          this.setState({
            mode: 'welcome'
          })
        }.bind(this)}>{this.props.title}</a></h1>
        {this.props.sub}
      </header>
      <TOC data={this.state.contents}></TOC>
      <Content title={_title} desc={_desc}></Content>
    </div>
    );
  };
};

```

* 바로 직접 `this`를 쓰면 가리키는 객체가 없어서, `this`값은 `undefined`로 나온다. 그러므로, 함수가 끝날 때 `bind()` 함수를 써서 `Component`를 가리킬 수 있도록 한다.
* `constructor` 바깥 부분에서 `state`를 동적으로 바꾸고 싶다면 `this.setState`를 이용해서 바꿔야 한다.
  &rarr; 직접 바꿔버릴 경우(`this.state.mode = 'blah'`) react가 인지할 수 없다.

### 분할된 파일에서 event 를 쓸 때

##### App.js

```jsx
class App extends Component {
  constructor(props){
    //컴포넌트 초기화 시켜주고 싶은 코드를 넣는다
    super(props);
    this.state = {
      mode: 'read',
      selected_content_id: 2,
      //초기화 대상
      subject: { title: 'Web', sub: 'World Wide Web'},
      welcome: { title: 'Welcome', desc: 'Hello, React!!'},
      contents: [
        {id: 1, title: 'HTML', desc: 'HTML is for informaition'},
        {id: 2, title: 'CSS', desc: 'CSS is for design'},
        {id: 3, title: 'JavaScript', desc: 'JavaScript is for interactive'},
      ]
    }
  }
  render(){
    let _title, _desc = null;
    if(this.state.mode === 'welcome'){
      _title = this.state.welcome.title;
      _desc = this.state.welcome.desc;
    } else if(this.state.mode === 'read') {
      var i = 0;
      while(i < this.state.contents.length){
        var data = this.state.contents[i]
        if(data.id === this.state.selected_content_id){
          _title = data.title;
          _desc = data.desc;
          break;
        }
        i++;
      };
    }
    return (
      <div className="App">
      <Subject title={this.state.subject.title} sub={this.state.subject.sub} onChangePage={function(){
        this.setState({
          mode: 'welcome'
        })
      }.bind(this)}></Subject>
      <Subject title="React" sub="For UI"></Subject>
      <TOC data={this.state.contents} onChangePage={function(id){
        this.setState({
          mode: 'read',
          selected_content_id: +id
          // Number(id) 로 사용가능
        })
      }.bind(this)} ></TOC>
      <Content title={_title} desc={_desc}></Content>
    </div>
    );
  };
};
```

* `props` 값에 함수를 넣어준다.



##### TOC.js

```jsx
class TOC extends Component {
  render(){
    let list = [];
    let data = this.props.data;
    let i = 0;
    while(i < data.length){
      list.push(
      <li key={data[i].id}>
        <a href={"/content/"+data[i].id} data-id={data[i].id} onClick={function(e){
          e.preventDefault();
          this.props.onChangePage(e.target.dataset.id);
        }.bind(this)}>{data[i].title}</a>
      </li>
      /*또는
      <li key={data[i].id}>
        <a href={"/content/"+data[i].id} 
           onClick={function(id, e){
             e.preventDefault();
             this.props.onChangePage(id);
             }.bind(this, data[i].id)}>{data[i].title}
        </a>
      </li>
      */
    );
      i ++;
    }
    return(
      <nav>
        <ul>
          {list}
        </ul>
      </nav>
    )
  }
}
```

* `props` 값을 이용해 등록된 함수를 불러온다.
* `bind()` 두번째 인자부터는 연결한 함수의 매개변수로 들어간다.

### create 구현

##### App.js

```jsx
class App extends Component {
  ...
    return (
      <div className="App">
      <Subject title={this.state.subject.title} sub={this.state.subject.sub} onChangePage={function(){
        this.setState({
          mode: 'welcome'
        })
      }.bind(this)}></Subject>
      <Subject title="React" sub="For UI"></Subject>
      <TOC data={this.state.contents} onChangePage={function(id){
        this.setState({
          mode: 'read',
          selected_content_id: +id
        })
      }.bind(this)} ></TOC>
      <ul>
        <li><a href="/create">create</a></li>
        <li><a href="/update">update</a></li>
        <li><input type="button" value="button"></input></li>
      </ul>
      <Content title={_title} desc={_desc}></Content>
    </div>
    );
  };
};
```

* `create`, `update` 는 특정 페이지로 이동해서 내용을 추가/수정할 것이지만, `delete`는 페이지로 가서 변경할 것이 아니기 때문에 버튼으로 사용한다.
  &rarr; 미리 `delete` 페이지로 가게 되는 프로그램같은게 있다면, 누르지 않았어도 페이지 링크를 타고 진입해서 



참고자료: 인프런 - 생활코딩, react 공식문서

