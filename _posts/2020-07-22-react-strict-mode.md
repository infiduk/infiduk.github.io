---
title: "[React] React에서 render가 두 번씩 돼요!"
date: 2020-07-22 11:20:04 +09:00
tags: study react javascript
comments: true
---

React Component Render Twice

## React component render twice
- `react` 에서 `render` 가 될 때 마다 `console` 로 찍는 코드를 작성 중...

``` javascript
render() {
    console.log("render!");
    ...
```

![image_01](https://user-images.githubusercontent.com/48206157/88127453-9931af00-cc0e-11ea-8292-10ceaab2e57c.png)

- 띠용? 렌더링이 두 번씩 되어 출력됨
- [찾아보니](https://stackoverflow.com/questions/61254372/my-react-component-is-rendering-twice-because-of-strict-mode) `App.js` 에 `React.StrictMode` 가 있어서 그렇다고 함

``` javascript
// <React.StrictMode></React.StrictMode> 요거..
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```

- `create-react-app` 으로 프로젝트를 생성하면 자동으로 추가되는 것 같음

``` javascript
ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

- `strict mode` 삭제 후 돌려보니 두 번씩 되던 렌더링이 한 번으로 됨

![image_02](https://user-images.githubusercontent.com/48206157/88128157-49ec7e00-cc10-11ea-8696-11a12dcab99d.png)

## React strict mode
- `strict mode` 란 `App` 내의 잠재적인 문제를 알아내기 위한 도구
- 자바스크립트에 있는 키워드.. 묵인하던 에러 메시지를 발생시킨다고 함 (문법 검사를 엄격하게 진행)

- [공식 문서 (en)](https://reactjs.org/docs/strict-mode.html)
- [공식 문서 (ko)](https://ko.reactjs.org/docs/strict-mode.html)
