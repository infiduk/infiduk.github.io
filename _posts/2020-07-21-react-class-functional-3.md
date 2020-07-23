---
title: "[React] React Class Component(클래스형 컴포넌트), Functional Component(함수형 컴포넌트) 3편"
date: 2020-07-21 09:35:04 +09:00
tags: study react javascript
comments: true
---

React Class Component, Functional Component

## 리액트.. 클래스형 컴포넌트와 함수형 컴포넌트 알아보기
- 인프런 생활코딩 강의를 참고했습니다! ([인프런 강의 링크](https://www.inflearn.com/course/react-class-function-생활코딩))

## [1편 보기...](https://infiduk.github.io/2020/06/17/react-class-functional-1.html)
## [2편 보기...](https://infiduk.github.io/2020/06/18/react-class-functional-2.html)

## Functional 컴포넌트가 class 컴포넌트와 대등할 수 있게 된 계기
- `state` 를 사용할 수 있게 됨 (`useState` 이용)
- `life cycle` 을 사용할 수 있게 됨

## 리액트의 Life Cycle

### class 컴포넌트
- 컴포넌트가 생성이 되면 `getDefaultProps()`, `getInitialState()` 라는 메소드를 호출
- 그 후, `componentWillMount()` 메소드를 호출 (컴포넌트가 mount 되기 전에 처리해야 하는 내용을 실행, render 호출 전)
- `render()` 메소드를 호출
- 컴포넌트가 mount 되면 `componentDidMount()` 를 호출 (컴포넌트가 생성된 이후 처리해야 하는 내용을 실행)

## class 에서 life cycle 구현 하기
- `life cycle` 의 구분을 위해 각 로그에 `style` 을 넣어줌
- `componentWillMount` > `render` > `componentDidMount` 의 순서로 로그가 찍히게 됨

``` javascript
// App.js
...
const classStyle = "color: red";
class ClassComp extends React.Component {
  state = {
    number: this.props.initNumber,
    date: (new Date().toString())
  }
  componentWillMount() {
    console.log("%cclass => componentWillMount", classStyle);
  }
  componentDidMount() {
    console.log("%cclass => componentDidMount", classStyle);
  }
  render() {
    console.log("%cclass => render", classStyle);
    ...
```

- `render` 전에 실행되어야 할 내용 들은 `componentWillMount` 메소드 안에 넣어줌
- `render` 이후에 실행되어야 할 내용, 즉 화면에 그려진 이후 처리되어야 하는 내용은 `componentDidMount` 에 넣어줌 (ex. 파일 다운로드 이후 처리되는 것)

### 그 이외의 life cycle
- 컴포넌트가 한번 만들어진 이후 컴포넌트에 변화가 생길 때 사용하는 메소드가 있음
- 컴포넌트의 `state` 나 `props` 가 변경될 경우 ...
- `render` 메소드를 호출할 것이냐 말 것이냐 여부를 결정하는 `shouldComponentUpdate` 메소드
- 컴포넌트가 업데이트 되기 전에 실행 되는 `componentWillUpdate` 메소드
- 컴포넌트가 업데이트 된 후 실행 되는 `componentDidUpdate` 메소드

``` javascript
// return 값이 true일 경우 component update 수행, false일 경우 update를 수행하지 않음
shouldComponentUpdate(nextProps, nextState) {
  console.log("%cclass => shouldComponentUpdate", classStyle);
  return true;
}
// 업데이트 된 component가 render 되기 전에 실행
componentWillUpdate() {
  console.log("%cclass => componentWillUpdate", classStyle);
}
// 업데이트 된 component가 render 된 이후 실행
componentDidUpdate() {
  console.log("%cclass => componentDidUpdate", classStyle);
}
```

## 지금까지의 내용 정리!
- `App.js` 파일 소스

``` javascript
import React, { useState } from 'react';
import './App.css';

function App() {
  return (
    <div className="App">
      <h1>Hello World</h1>
      <ClassComp initNumber={10} />
      <FuncComp initNumber={20} />
    </div>
  );
}

const classStyle = "color: red";
class ClassComp extends React.Component {
  state = {
    number: this.props.initNumber,
    date: (new Date().toString())
  }
  componentWillMount() {
    console.log("%cclass => componentWillMount", classStyle);
  }
  componentDidMount() {
    console.log("%cclass => componentDidMount", classStyle);
  }
  shouldComponentUpdate(nextProps, nextState) {
    console.log("%cclass => shouldComponentUpdate", classStyle);
    return true;
  }
  componentWillUpdate() {
    console.log("%cclass => componentWillUpdate", classStyle);
  }
  componentDidUpdate() {
    console.log("%cclass => componentDidUpdate", classStyle);
  }
  render() {
    console.log("%cclass => render", classStyle);
    return (
      <div className="container">
        <h2>class style component</h2>
        <p>Class Component Number: {this.state.number}</p>
        <p>Class Component Date: {this.state.date}</p>
        <input type="button" value="random1" onClick={
          function() {
            this.setState({number: Math.random()})
          }.bind(this)
        } />
        <input type="button" value="random2" onClick={
          function() {
            this.setState({date: (new Date().toString())})
          }.bind(this)
        } />
      </div>
    );
  }
}

function FuncComp(props) {
  let [ _number, setNumber ] = useState(props.initNumber);
  let [ _date, setDate ] = useState(new Date().toString());
  return (
    <div className="container">
      <h2>function style component</h2>
      <p>Functional Component Number: {_number}</p>
      <p>Functional Component Date: {_date}</p>
      <input type="button" value="random1" onClick={
        function() {
          setNumber(Math.random());
        }
      } />
      <input type="button" value="random2" onClick={
        function() {
          setDate(new Date().toString());
        }
      } />
    </div>
  );
}

export default App;
```

## 4편에 계속...