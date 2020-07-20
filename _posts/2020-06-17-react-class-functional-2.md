---
title: "[React] React Class Component(클래스형 컴포넌트), Functional Component(함수형 컴포넌트) 2편"
date: 2020-06-18 13:20:04 +09:00
tags: study react javascript
comments: true
---

React Class Component, Functional Component

## 리액트.. 클래스형 컴포넌트와 함수형 컴포넌트 알아보기
- 인프런 생활코딩 강의를 참고했습니다! ([인프런 강의 링크](https://www.inflearn.com/course/react-class-function-생활코딩))

## [1편 보기...](https://infiduk.github.io/2020/06/17/react-class-functional-1.html)

## state, props
- 컴포넌트를 사용하는 쪽은 컴포넌트가 제공하는 `props` 를 통해서 컴포넌트를 이용
- 컴포넌트를 만드는 쪽은 내부적으로 `state` 라는, `props` 와 구분되는 데이터를 통해 내부적으로 작업
- `props` 는 `class` 와 `functional` 모두 사용 가능
- `state` 는 `class` 에서만 사용이 가능했지만, `hook` 을 통해 `functional` 에서도 사용이 가능해짐
- 컴포넌트가 내부적으로 자신의 상태를 바꾸고 관리하기 위해 사용 -> `state`

## 각 컴포넌트에 props로 값 할당
- `App.js` 에 `class` 형과 `functional` 형 모두에 `initNumber` 를 할당

``` javascript
...
<ClassComp initNumber={2} />
<FuncComp initNumber={2} />
...
```

### class 컴포넌트가 props를 가져오는 방법
- `this.props.xxx` 의 형태로 값을 가져옴

``` javascript
// App.js
class ClassComp extends React.Component {
  render() {
    return (
      <div className="container">
        <h2>class style component</h2>
        <p>Number: {this.props.initNumber}</p>
      </div>
    );
  }
}
```

### functional 컴포넌트가 props를 가져오는 방법
- 리액트가 호출할 때 전달된 `props` 라는 값을 호출하도록 약속이 되어있음

``` javascript
// App.js

// props가 기본 형태이고, props 이외의 aaa나 bbb로 써도 문제는 없음
// function FuncComp(aaa) { 로 쓰고, 값을 가져올 때 aaa.값 이렇게 가져와도 됨
function FuncComp(props) {
  return (
    <div className="container">
      <h2>function style component</h2>
      <p>Funcinal Component Number: {props.initNumber}</p>
    </div>
  );
}
```

## 각 컴포넌트 별 state 사용 방법

### Class 컴포넌트에서 state 사용하기
- 먼저 초기 값을 설정 (현재 예제에서는 `number` 로 설정)
- 현재 `props` 의 값을 `state` 로 줬기 때문에, `state` 의 값이 바뀔 때 마다 `render()` 가 호출됨
- 달라진 `state` 의 값이 화면에 뿌려짐

``` javascript
// App.js

// class에서는 함수를 사용할 때 .bind(this)를 써줘야 함
class ClassComp extends React.Component {
  state = {
    number: this.props.initNumber
  }
  render() {
    return (
      <div className="container">
        <h2>class style component</h2>
        <p>Class Component Number: {this.state.number}</p>
        <input type="button" value="random" onClick={
          function() {
            this.setState({number: Math.random()})
          }.bind(this)
        } />
      </div>
    );
  }
}
```

### Functional 컴포넌트에서 state 사용하기 1
- `functional` 에서는 `state` 를 초기화 하고, 사용 하고, 값을 변경하는 작업이 어려웠었음
- 그 전에는 `props` 로 전달 되는 값을 화면에 표시해주는 용도로만 사용

### hook
- `react v16.8` 부터 사용
- `hook` 은 `react` 가 제공하기도 하고, 사용자가 정의해서 사용할 수도 있음
- 내장된 `hook` 의 경우는 이름이 `use` 로 시작함

### Functional 컴포넌트에서 state 사용하기 2
- `useState` 를 사용하기 위해 `import` 를 해줌

``` javascript
// App.js

import React, { useState } from 'react';
...
function FuncComp(props) {
  // useState는 두 개의 값으로 이루어져 있는 배열
  // 배열의 원소 중, 첫 번째 값이 state 값
  // 현재는 초기 값으로 아무 것도 넣어주지 않았기 때문에, number의 값은 undefined
  let numberState = useState();
  let number = numberState[0];
  return (
    <div className="container">
      <h2>function style component</h2>
      <p>Funcinal Component Number: {number}</p>
    </div>
  );
}
```

- `state` 에 초기 값을 주기 위해서는, `useState` 의 첫 번째 인자로 값을 넣어줌

``` javascript
// props로 넘어온 값을 초기 값으로 설정
let numberState = useState(props.initNumber);
// number의 값은 initNumber의 값으로 들어감
let number = numberState[0];

// 꼭 props로 넘어온 값으로만 초기 값으로 넣을 수 있는 것은 아님
// 임의의 값으로도 초기 값으로 설정 가능
let numberState = useState(2000);
```

- `state` 의 값을 변경하려면?
- `class` 에서는 `this.setState` 라는 메소드를 통해 `state` 의 값을 변경시킴
- 값이 변경되면 리액트가 `render` 메소드를 호출해 화면을 새로고침
- `functional` 에서는 `useState` 의 두 번째 인자를 활용해서 값을 변경함

``` javascript
...
// setNumber에는 함수가 담기고, setNumber를 활용해 state의 값을 변경
let setNumber = numberState[1];
// this는 class 안에서 사용되는 것이고, functional에서는 bind가 필요 없으므로 삭제
// setNumber가 가리키는 함수의 인자로 state의 변경할 값을 넣어줌
return (
  <div className="container">
    <h2>function style component</h2>
    <p>Funcinal Component Number: {number}</p>
    <input type="button" value="random" onClick={
      function() {
        setNumber(Math.random());
      }
    } />
  </div>
);
```

- `functional` 에서 `state` 를 만들 때는, `react` 의 `useState` 를 사용
- `useState` 는 배열을 리턴하는데, 그 중 첫 번째 값은 상태 값이고 두 번째 값은 상태를 변경할 수 있는 함수
- 이 두 인자들을 이용해 `state` 의 값을 만들고, 변경할 수 있음

## 컴포넌트 별 Date 출력하기

### Class 컴포넌트

``` javascript
// App.js

class ClassComp extends React.Component {
  state = {
    number: this.props.initNumber,
    date: (new Date().toString())
  }
  render() {
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
```

### Functional 컴포넌트

``` javascript
// App.js

function FuncComp(props) {
  let numberState = useState(props.initNumber);
  let number = numberState[0];
  let setNumber = numberState[1];

  let [ _date, setDate ] = useState(new Date().toString());

  // 해당 코드는 위의 한 줄의 코드로 간편하게 사용할 수 있음
  let dateState = useState(new Date().toString());
  let _date = {
    date: dateState[0],
    setDate: dateState[1]
  }
  return (
    <div className="container">
      <h2>function style component</h2>
      <p>Functional Component Number: {number}</p>
      <p>Functional Component Date: {_date.date}</p>
      <input type="button" value="random1" onClick={
        function() {
          setNumber(Math.random());
        }
      } />
      <input type="button" value="random2" onClick={
        function() {
          _date.setDate(new Date().toString());
        }
      } />
    </div>
  );
}
```

## 지금까지의 내용 정리!
- 현재 완성된 화면
![image_01](https://user-images.githubusercontent.com/48206157/87904095-92812b80-ca98-11ea-99ce-9ee10a0139cc.png)

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

class ClassComp extends React.Component {
  state = {
    number: this.props.initNumber,
    date: (new Date().toString())
  }
  render() {
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

## 3편에 계속...