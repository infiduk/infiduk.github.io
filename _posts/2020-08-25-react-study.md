---
title: "[React] 나중에 보면 부끄러울 수 있는 리액트(React) 정리 2"
date: 2020-08-25 11:27:04 +09:00
tags: study react javascript
comments: true
---

나.부.리 2

## React 정리....
- 오늘은 `Redux` 중심

## Spread Operator

### 정보의 업데이트가 이루어질 때
- `React` 에서 `setState` 를 할 때, 기존 정보가 새 정보로 업데이트 됨
- `...` 연산자를 사용해 원래 배열을 유지하면서 다른 요소를 추가할 수 있음

``` javascript
var colors = ['red', 'yellow', 'blue']

// var newColors = ['red', 'yellow', 'blue', 'green'] 와 같음
var newColors = [...colors, 'green']
```

### 함수 인자로 사용할 때
- 필요한 parameter 의 개수가 정해지지 않았을 때 사용

``` javascript
function func(...param) {
  console.log(param);
}

// [ 1, 2, 3 ]
func(1, 2, 3);
```

## Immer
- `React` 에서 배열이나 객체를 업데이트 할 때, 직접 수정은 불가능 (기존의 배열, 객체도 함께 수정됨)
- 객체의 경우 전개 연산자(...)를 이용해 값을 수정했고, 배열은 전개 연산자와 concat, filter, map 등을 이용하여 수정
- 불변성을 지켜주면서 값을 수정할 수 있게 하는 라이브러리

``` javascript
// produce 로 불러옴
import produce from "immer"

const baseState = [
  {
      todo: "Learn typescript",
      done: true
  },
  {
      todo: "Try immer",
      done: false
  }
]

// baseState >> 현재 state
// draftState >> 현재 state 를 복사한 것
// nextState >> produce 가 반환하는 값
const nextState = produce(baseState, draftState => {
  draftState.push({todo: "Tweet about it"})
  draftState[1].done = true
})
```

## Redux
- `React` 생태계에서 가장 사용률이 높은 상태관리 라이브러리
- `Component` 들의 상태 관련 로직들을 다른 파일로 분리시켜서 관리할 수 있음
- `Content API` 와 `useReducer` Hook을 사용해서 개발하는 방식과 유사

### Redux 에서 사용되는 키워드
1. Action
  - 상태에 변화가 필요할 때 발생시키는 것
  - 저장소에 정보를 전달하기 위한 데이터 묶음
  - 하나의 객체로 표현
  - `type` 필드를 필수적으로 가지고 있어야 함

  ``` javascript
  {
    type: "STUDY_REDUX",
    data: {
      id: 0,
      text: "리덕스를 배워보자"
    }
  }
  ```

2. Action Creator (액션 생성함수)
  - 액션을 만드는 함수
  - parameter 를 받아 액션 객체 형태로 만들어 줌
  - `Component` 에서 액션을 쉽게 발생시키기 위해 만들어 졌기 때문에 `export` 키워드를 붙여 다른 파일에서 불러와 사용
  - 필수적이진 않고, 필요 시 액션을 발생시킬 때 마다 생성할 수 있음

  ``` javascript
  export function codingRedux(data) {
    return {
      type: "CODING_REDUX",
      data
    };
  }

  // arrow function 의 형태로도 생성 가능
  export const codingRedux = data => ({
    type: "CODING_REDUX",
    data
  });
  ```

3. Reducer
  - 변화를 일으키는 함수
  - 각각의 상태변화를 어떻게 할지 관리해주는 정보가 담겨 있음
  - 두 개의 parameter(`state`, `action`) 를 필요로 함
  - 현재의 상태와 전달받은 액션을 참고하여 새로운 상태를 만들어서 반환
  - 여러 `reducer` 들을 하나로 합쳐 주는 `CombineReducers` 도 있음

  ``` javascript
  function reducer(state, action) {
    // 상태 업데이트 로직
    return alteredState;
  }
  ```

4. Store
  - `Application` 당 하나의 `Store` 를 가짐
  - 현재의 앱 상태, `reducer`, 내장 함수 등이 있음

  ``` javascript
  // createStore
  // parameter 로 reducer 들을 넣어줌
  import { createStore } from "redux"
  const store = createStore(firstReducer)

  // getState
  store.getState()
  
  // dispatch
  // store 에 있는 reducer 에게 action 을 전달해 줌
  store.dispatch(firstReducer("GO_ACTION"))
  ```

5. Dispatch
  - `Store` 의 내장함수 중 하나
  - 액션을 발생시키는 것
  - 액션 형태의 값을 parameter 로 받음, dispatch(action) 의 형태

6. Subscribe
  - `Store` 의 내장함수 중 하나
  - 함수 형태의 값을 parameter 로 받고 액션이 dispatch 될 때 마다 전달된 함수가 호출
  - 직접 사용하진 않고, `connect` 함수나 `useSelector` Hook 을 사용하여 `Redux` 상태에 구독

### Redux-React
- `React` 에 `Redux` 를 연결해주는 역할

1. Provider
  - 단순한 하나의 Component
  - `react` 로 작성된 Component 들을 Provider 안에 넣으면 하위 Component 들이 Provider 를 통해 redux store 에 접근이 가능해짐

  ``` javascript
  import React from "react"
  import ReactDOM from "react-dom"
  import { Provider } from "react-redux"
  import App from "./App"
  import createStore from "redux"

  // store 생성
  const store = createStore( ... )

  ReactDOM.render(
    // Provider 안에 Component 넣기
    <Provider store={store}>
      <App />
    </Provider>,
    document.getElemenyById('root')
  )
  ```

2. connect
  - `Provider` 하위에 존재하는 컴포넌트가 `Store` 에 접근할 수 있도록 연결
  - 반드시 `mapStateToProps`, `mapDispatchToProps` 를 인자로 넘겨줘야 `Component` 가 `this.props` 로 접근할 수 있음

  ``` javascript
  import { connect } from "react-redux"
  ..

  const Todo = connect();
  export default Todo(TodoApp);

  // 위의 소스를 한 줄로 표현한 것
  export default connect()(TodoApp);
  ```

3. mapStateToProps
  - `connect` 함수의 `첫번째 인자`로 사용됨
  - `Store` 가 `update` 될 때마다 자동적으로 호출되기 때문에, 원하지 않는다면 `null` 이나 `undefined` 값을 제공해야 함
  - 첫번째 인자는 `state`, 두번째 인자는 `객체`

4. mapDispatchToProps
  - `connect` 함수의 `두번째 인자`로 사용됨
  - `Store` 에 접근한 `Component` 가 `Store` 의 상태를 바꾸기 위해 `dispatch` 를 사용할 수 있게 함

### Redux 의 3가지 규칙
1. 하나의 `Application` 안에는 하나의 `Store`
  - 여러개의 `Store` 가 가능하긴 하나, 권장하지는 않음

2. 읽기전용 state
  - `React` 에서 `state` 를 `update` 할 때, `setState` 를 사용하거나 `concat`, `...` 으로 기존의 `state` 는 수정하지 않고 새로운 것을 만들어서 수정
  - 기존 상태를 변화시키지 않기 때문에 개발자 도구를 통해 뒤로 돌리거나 앞으로 돌릴 수 있음
  - 불변성을 유지해야 하는 이유는 내부적으로 데이터가 변경 되는 것을 감지하는 `shallow equality` 검사를 하기 때문
  - `Immutable.js`, `Immer.js` 를 사용해 불변성을 유지하며 상태를 관리할 수 있음

3. `Reducer` 는 `순수한 함수(pure function)` 여야 함
  - `Reducer` 는 `state` 와 `action` 객체를 parameter 로 받음
  - 이전의 `state` 는 절대 건들지 않고, 변화를 일으킨 새로운 상태 객체를 만들어서 반환
  - 똑같은 parameter 로 호출된 `Reducer` 는 언제나 **똑같은 결과값**을 반환해야 함
  - 실행할 때 마다 다른 값을 나타내는 것들(new Date(), 랜덤 숫자 생성 ...)은 Reducer 밖에서 처리해야 함 -> `Redux Middleware` 를 사용

### Redux Hook

## Redux saga

## Context API

### Redux 와 Context API 의 차이
1. `Redux` 에는 미들웨어 개념이 존재
  - `Reducer` 함수 사용
  - `Action` 객체가 `Reducer` 에서 처리되기 전에 원하는 작업을 수행하도록 할 수 있음
  - `Middleware` 는 주로 비동기 작업을 처리할 때 사용
2. 함수 및 Hook
  - `Context API`의 경우 `useReducer` 를 사용할 때 `Context` 를 새로 생성하고, `Provider` 를 설정하고, `전용 Custom Hook` 을 따로 만들어서 사용
  - `Redux` 의 경우 상태, 액션 생성 함수를 `Component의 props` 로 받아올 수 있음
  - `useSelector`, `useDispatch`, `useStore` 등의 Hook 을 사용해 상태를 조회하거나 디스패치 함
  `Context API` 는 `Context` 가 지니고 있는 상태가 바뀌면 해당 `Context` 의 내부 `Component` 들이 모두 리렌더링 되지만, `Redux` 는 실제 상태가 바뀔 때만 리렌더링
3. 상태를 관리할 때
  - `Context API` 를 사용해 글로벌 상태를 관리할 때는 기능별로 `Context` 를 만들어서 관리 (필수적인 것은 아님)
  - `Redux` 에서는 모든 글로벌 상태를 커다란 상태 객체에 넣어서 사용해야 함
  - `Redux` 에서는 매번 `Context` 를 새로 만드는 수고를 덜 수 있음

## React memo
- `React` 는 먼저 `Component` 를 `렌더링(Rendering)` 한 뒤, 이전 렌더링 결과와 비교하여 결과가 다를 경우 `DOM` 을 업데이트 함
- `Component `가 `React.memo()` 로 래핑될 때 `React` 는 `Component` 를 렌더링하고 결과를 `메모이징(Memoizing)` 하며, 다음 렌더링 시 `props` 가 같다면 메모이징된 결과를 가져옴
- 컴포넌트의 `props` 가 바뀌지 않았다면, 리렌더링을 방지하여 `Component` 의 리렌더링 성능 최적화를 해줌
- 렌더링 최적화가 필요하지 않은 `Component` 에 `React.memo()` 를 사용하는 것은 불필요한 `props` 비교만 하는 것이기 때문에 꼭 필요한 경우에만 사용하는 게 좋음
- 두번째 `parameter` 에 `propsAreEqual` 함수를 사용하여 특정 값들만 바뀌었는지 비교할 수 있음

``` javascript
// 메모이징된 MemoizedComponent 를 반환
export const MemoizedComponent = React.memo(comp);
```

## Redux actions

## 참고
- [Using the spread operator in React setState](https://medium.com/@thejasonfile/using-the-spread-operator-in-react-setstate-c8a14fc51be1)
- [Spread 연산자, Rest 파라미터](https://velog.io/@chlwlsdn0828/Js-Spread-%EC%97%B0%EC%82%B0%EC%9E%90-Rest-%ED%8C%8C%EB%9D%BC%EB%AF%B8%ED%84%B0)
- [23. Immer 를 사용한 더 쉬운 불변성 관리](https://react.vlpt.us/basic/23-immer.html)
- [리덕스+리액트 Redux with React #6 immer 사용하기](https://velog.io/@hwang-eunji/리덕스리액트-Redux-with-React-immer-사용하기)
- [이머(Immer)를 소개해: 불변성 쉽게 하자](https://medium.com/@wongni/이머-immer-를-소개해-불변성-쉽게-하자-24b00b6ff13f)
- [리덕스](https://react.vlpt.us/redux/)
- [Redux-React의 기본](https://velog.io/@jeonghoheo/Redux-React-요약)
- [Context API 사용하기](https://velog.io/@kwonh/React-Context-API-사용하기)
- [React.memo() 현명하게 사용하기](https://ui.toast.com/weekly-pick/ko_20190731/)