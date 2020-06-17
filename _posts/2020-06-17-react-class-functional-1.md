---
title: "[React] React Class Component(클래스형 컴포넌트), Functional Component(함수형 컴포넌트) 1편"
date: 2020-06-17 09:50:04 +09:00
tags: study react javascript
comments: true
---

React Class Component, Functional Component

## 리액트.. 클래스형 컴포넌트와 함수형 컴포넌트 알아보기
- 인프런 생활코딩 강의를 참고했습니다! ([인프런 강의 링크](https://www.inflearn.com/course/react-class-function-생활코딩))

### 클래스형 컴포넌트
- 리액트의 기능을 최대로 끌어올릴 수 있음
- 클래스 문법을 알아야하고, 조금 복잡함
- 대부분의 리액트 자료들이 클래스 방법으로 되어있음
``` javascript
class ClassComp extends React.Component {
  render() {
    return (
      <div className="container">
        <h2>class style component</h2>
        <p>Number: {this.state.number}</p>
        <p>Date: {this.state.Date}</p>
        <input type="button" value="random" onClick={ ... } />
      </div>
    );
  }
}
```

### 함수형 컴포넌트
- 함수의 문법만 알면 사용할 수 있음
- 컴포넌트 내부의 `state` 를 만들거나, `life cycle API` 를 사용할 수 없었음 -> `hook` 이라는 방법으로 상태를 다룰 수 있게 됨
``` javascript
function FuncComp(props) {
  return (
    <div className="container">
      <h2>function style component</h2>
      <p>Number: {number}</p>
      <p>Date: {_date}</p>
      <input type="button" value="random" onClick={ ... } />
    </div>
  );
}
```

## 예제 코드로 비교해 보자!
- `create-react-app` 으로 리액트 프로젝트 생성
``` shell
# create-react-app 이 없다면
npm install -g create-react-app
```
``` shell
# create-react-app 이 설치되어 있다면
npx create-react-app react-example
```

### 사용하지 않는 기본 소스 정리
- `App.css` 파일과 `index.css` 파일 내용 삭제
- `App.js` 파일 정리

``` javascript
// App.js
import React from 'react';
import './App.css';

function App() {
  return (
    <div className="App">
      <h1>Hello World</h1>
    </div>
  );
}

export default App;
```

### 컴포넌트 추가
- `App.js` 에 있는 `Hello World` 부분 밑에 (만들어 줄) 클래스형 컴포넌트와 함수형 컴포넌트 추가

``` javascript
...
<ClassComp />
<FuncComp />
...
```

### 함수형 컴포넌트 생성
- `App.js` 에 함수형 컴포넌트를 하나 생성해 보기
``` javascript
function FuncComp() {
  return (
    <div className="container">
      <h2>function style component</h2>
    </div>
  );
}
```

### 클래스형 컴포넌트 생성
- `App.js` 에 클래스형 컴포넌트도 하나 생성
``` javascript
class ClassComp extends React.Component {
  render() {
    return (
      <div className="container">
        <h2>class style component</h2>
      </div>
    );
  }
}
```

### App.css 수정
- 명확한 구분을 위해 `App.css` 수정
``` css
.container {
  border: 5px solid red;
  margin: 5px;
  padding: 5px;
}
```

## 지금까지의 내용 정리!
- 현재 완성된 화면
![image_01](https://user-images.githubusercontent.com/48206157/84844709-ed80c680-b085-11ea-9c27-fbe0db523d04.png)

- `App.js` 파일 소스

``` javascript
// App.js
import React from 'react';
import './App.css';

function App() {
  return (
    <div className="App">
      <h1>Hello World</h1>
      <ClassComp />
      <FuncComp />
    </div>
  );
}

class ClassComp extends React.Component {
  render() {
    return (
      <div className="container">
        <h2>class style component</h2>
      </div>
    );
  }
}

function FuncComp() {
  return (
    <div className="container">
      <h2>function style component</h2>
    </div>
  );
}

export default App;
```

- `App.css` 파일 소스
``` css
.container {
  border: 5px solid red;
  margin: 5px;
  padding: 5px;
}
```

## [2편에 계속...](./2020-06-17-react-class-functional-2.md)