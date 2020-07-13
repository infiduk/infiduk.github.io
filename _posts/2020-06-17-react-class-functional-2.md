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

// class 에서는 함수를 사용할 때 .bind(this)를 써줘야 함
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

### Functional 컴포넌트에서 state 사용하기
- `functional` 에서는 `state` 를 초기화 하고, 사용 하고, 값을 변경하는 작업이 어려웠었음
- 그 전에는 `props` 로 전달 되는 값을 화면에 표시해주는 용도로만 사용

## 3편에 계속...