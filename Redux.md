# Redux - 작성중



redux는 flux아키텍쳐를 구현하기 쉽게 해주는 라이브러리

mvc 디자인 패턴

액션 > 컨트롤러 > 모델 < > 뷰

앱의 규모가 커지면 모델, 뷰의 갯수가 굉장히 많이 늘어나면서 복잡해짐.



flux 는 일종의 아이디어(추상적인 개념)

액션 > 디스패쳐 > 스토어 > 뷰

뷰에서 디스패쳐로 액션을 보내고, 디스패쳐는 액션이 중첩되지 않도록 대기시킨다.

http://bestalign.github.io/2015/10/06/cartoon-guide-to-flux/



1. 단 하나의 진실 근원(Single source of Truth)
   flux에서는 여러개의 store의 사용하지만, <u>리액트는 어플리케이션의 state를 위해 단 한개의 store를 사용한다.</u>
   구조는 컴포넌트별, 이벤트별, 앱의 데이터 / ui 상태에 따라 구조하는 등 네스팅해서 사용해도 된다. 아무렇게나 구조하면 된다.
2. 읽기전용 State(State is Read-only)
   무조건 action이 dispatch되어야 state가 변경
3. Changes are made with pure Functions
   순수함수: 비동기적처리 X(네트워크 및 데이터베이스 접근 X 인수변경 X)
   Date.now(), Math.random()같은거 쓰면 안된다.

http://bestalign.github.io/2015/10/26/cartoon-intro-to-redux/

리듀서는 변화를 일으켜주는 함수라고 알면 되고, 한개일수도 있고 여러개일수도 있다.
최상위 관리자는 루트 리듀서.

상태 객체는 직접 변경되는게 아니라, 새로운 조각을 복사하고 합친다.

smart는 액션을 직접 처리 책임, 자신의 style, dom을 갖고 있지 않다. dumb들이 dom을 제어.

dumb들은 props를 통해서 함수를 받고, 사용. 단순히 호출.

**자주 사용해야만 이해할수 있을거야 ㅠㅠ** 개념을 이해하기.!!





action은 작업의 정보를 가지고 있는 객체

대문자, 언더스코어로 액션이름을 정한다.

필수로 가져야 하는 속성: type(종류)

액션파일이 많으면 파일 분리해도 된다.



리듀서는 변화를 일으키는 함수. 순수해야된다!!- 동일한 인수 = 동일한 결과

이전 상태와 액션을 받아서 다음 상태(새 상태)를 반환한다!!



스토어 만들거면 `createStore`함수로 생성

하는 일:

1. dispatch(action) : 액션 전달
2. getState() 현재 상태 반환
3. subscriibe(listener) 상태 바뀔 때 전달
4. replaceReducer(nextReducer) 보통 사용할일 없음.. 핫로더@_@??

### react-redux

provider 컴포넌트로 전달, connect로 연결해줘야 한다

connect는 또다른 함수를 반환.........................................새로운 컴포넌트 클래스 반환

```js
//connect 함수를 실행하면 새로운 컴포넌트를 반환하는데, 그 인수로 Counter 컴포넌트를 넣는것.
export default connect()(Counter);
```



option들이 4개 있다.

`mapDispatchToProps`를 더 쉽게 쓰는 법, `bindActionCreators` 사용하기.(잘 안쓰기도 한다)

단, 단점은 action 이름 그대로 써야 한다.(임의의 이름을 쓸수없다)

```js
import React, { Component } from 'react';
import Value from './Value';
import Controls from './Controls';
import { connect, bindActionCreators } from 'react-redux';

import * as actions from './../actions'

class Counter extends Component {
  render() {
    return (
      <div>
        <Value />
        <Controls />
      </div>
    );
  }
}

// redux의 state를 인수
const mapStateToProps = (state) => {
  return {
    number: state.counter.number,
    color: state.ui.color
  };
}

const mapDispatchToProps = (dispatch) => {
  //처리를 자동으로 해준다
  return bindActionCreators(actions, dispatch);
}

export default Counter;
```





##### redux-toolkit

`redux`에서 출시(?)한 버전. 이걸 쓰면 `redux-saga`, `redux-thunk`, `immer` 등을 쓰지 않아도 된다.

`redux-toolkit`에서 제공하는 `configureStore`를 쓰면 `initailState`를 굳이 정의해주지 않아도 된다.

```js
const { configureStore, getDefaultMiddleware } = require('@reduxjs/toolkit');

const reducer = require('./reducers') // reducer파일
const firstMiddleware = (store) => (next) => (action) => {
    console.log(action)
    next(action)
}
const store = configureStore({
    reducer,
//    preloadedState 서버측에서 initialState를 줄 때는 필요하지만 그 외에는 안 써도 된다.
    middleware : [firstMiddleware, ...getDefaultMiddleware] //getDefaultMiddleware로 기본 thunk middleware까지 포함시켜줌
    devTools: true || process.env.Node_ENv !== 'production'
})

module.exports = store;
```

코드는 [Zerocho - 리덕스vs몹엑스 리뉴얼 3-1. 툴킷을 선택한 이유](https://www.youtube.com/watch?v=nVBeWqP_xqM) 코드 참고

