---
title: "[React/NomadCoders] ReactJS로 영화 웹 서비스 만들기 (CP 1차시)"
date: 2022-07-22 11:38:00 +09:00
tags: study react javascript nomadcoders
comments: true
---

<a href="https://hits.seeyoufarm.com"><img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https://infiduk.github.io/2022/07/22/react-for-beginners.html&count_bg=%23EDD513&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=%E2%9C%A8+page+view+%E2%9C%A8&edge_flat=false" /></a>

ReactJS로 영화 웹 서비스 만들기 (CP 1차시)

## CP 프론트 스터디 1차시 내용 정리

💪 React.js는 **킹갓엠페러제너럴충무공마제스티**이다!

## #1

### 들어가며

리액트도 초창기에는 굉장히 적은 사람들이 사용했다.

하지만 2022년 지금! 리액트는 **프론트를 대표하는 프레임워크**로 자리매김하고 있다.

왜 많은 사람들이 다른 프레임워크를 두고 **어썸한 리액트**를 사용했는지 알아보고 공부해 보자.

### 왜 리액트인가?

새로운 기술을 배우고자 할 때 **주의**해야 할 점

1. **누가** 해당 기술을 **사용**하고 있는지

2. 그들(새로운 기술을 사용하는 개발자)의 **규모**가 큰지

3. 그들에게 **중요한 기술**인지

리액트는 전세계 상위 1만 개의 사이트 중, 무려 약 **45%가 사용**하고 있는 기술이다.

넷플릭스, 페이스북, 에어비앤비 등등 **웹 사이트로 사용자를 유치하는 대형 회사**들도 리액트를 사용하고 있다.

→ 이런 기술을 배우는 게 좋은 선택 👍

페이스북의 경우, 리액트를 만들고 그냥 방치해 두는 게 아니라 **직접 활용**하고 있다.

페이스북 페이지도 다시 리액트로 만들고 개발자도 채용하며 **지속적인 투자 및 업데이트**를 진행하고 있다.

기술을 배울 때 **커뮤니티나 생태계**가 매우 중요한데, 리액트 커뮤니티가 엄청 크다.

→ 거의 대부분의 Javascript 커뮤니티를 가져왔다고 봐도 무방하다. (리액트가 **JS 기반**이기 때문)

리액트를 활용한 기술도 늘어나고 있다.

- 대표적으로 **RN(React Native)**이 있고, 최근에는 VR도 리액트로 제작하려는 사람도 있다.

npm 기준, 일주일 동안의 다운로드 수가 **천만 회**를 넘어가는 프레임워크

따라서, 프론트 프레임워크로 리액트를 공부하는 건 아주 좋은 선택이다!

### 준비물

JS 기본 지식, 브라우저, VS Code

## #2

### 왜 리액트를 사용하는가?

리액트는 UI와 **상호작용하는 기술**이다.

- HTML, JS를 `interactive` 하게 만들어 준다.

### 바닐라 JS vs. 리액트

바닐라 JS

```html
<!-- react-for-beginners/vanilla.html -->

<!DOCTYPE html>
<html>
  <body>
    <span>Total clicks: 0</span>
    <button id="btn">Click me</button>
  </body>
  <script>
    let counter = 0;
    const button = document.getElementById("btn");
    const span = document.querySelector("span");
    function handleClick() {
      counter = counter + 1;
      span.innerText = `Total clicks: ${counter}`;
    }
    button.addEventListener("click", handleClick);
  </script>
</html>
```

1. HTML 코드를 작성해 버튼 하나를 만든다.

2. 만든 버튼을 JS로 가져온다.

3. 해당 버튼의 `click event` 를 감지한다.

4. click 할 때 마다 숫자 1씩 증가되는 기능을 넣어준다.

5. HTML span 태그에 카운터가 업데이트 되도록 수정한다.

리액트

```html
<!-- react-for-beginners/index.html -->

<!DOCTYPE html>
<html>
  <body>
    <div id="root"></div>
  </body>
  <!-- 리액트는 앱의 interactive를 높여주는 라이브러리이고, -->
  <!-- react-dom은 모든 리액트 element를 HTML body에 놓을 수 있게 해주는 패키지 -->
  <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
  <script>
    const root = document.getElementById("root");
    const span = React.createElement(
      "span",
      { id: "sexy-span", style: { color: "red" } },
      "Hello I'm a span"
    );
    ReactDOM.render(span, root);
  </script>
</html>
```

1. 리액트를 **CDN**으로 가져온다.

2. JS와 리액트를 활용해 HTML 코드를 작성한다.

   1. `React.createElement` 로 span 태그를 생성한다.

   2. `ReactDOM` 으로 HTML 코드에 만든 리액트 element를 렌더링 한다.

      1. root라는 id를 가진 div 태그에 span 태그를 렌더링 한다.

   3. `React.createElement` 는 **첫 번째 인자로 HTML 태그**를, **두 번째 인자로 property**를, **세 번째 인자로 content**를 받는다.

   4. (여기부터는 아래의 **리액트로 버튼 만들기** 참고) span 태그와 동일한 방법으로 버튼을 생성한다.

   5. span 태그와 버튼을 한번에 렌더링 한다.

      1. `React.createElement` 의 **세 번째 인자에 array 형태**로 span 태그와 버튼을 넣어주고, 이렇게 만든 리액트 element를 렌더링 한다.

   6. h3 태그 컴포넌트에도 두 번째 인자로 `mouse enter event listener` 등록한다.

   7. span 태그를 h3 태그로 변경한다.

   8. 버튼 컴포넌트(`React.createElement`)의 **두 번째 인자로 `click event listener`** 를 등록한다.

      1. 바닐라 JS에서 click event는 `click` 이지만, 리액트에서 click event는 `onClick` 이다.

바닐라 JS는 **HTML을 먼저** 만들고, **JS로 가져와**서 **HTML을 수정**해서 사용한다.

리액트는 **JS로 시작**해 **HTML을 만든다.**

- 즉, 리액트는 **HTML을 JS로 업데이트** 하기 때문에 **사용자에게 보여지는 내용을 컨트롤**할 수 있다.

### 리액트로 버튼 만들기

```html
<!-- react-for-beginners/index.html -->

<!DOCTYPE html>
<html>
  <body>
    <div id="root"></div>
  </body>
  <!-- 리액트는 앱의 interactive를 높여주는 라이브러리이고, -->
  <!-- react-dom은 모든 리액트 element를 HTML body에 놓을 수 있게 해주는 패키지 -->
  <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
  <script>
    const root = document.getElementById("root");
    const h3 = React.createElement("h3", {
      id: "title",
      onMouseEnter: () => console.log("mouse enter");
      }, "Hello I'm a span"
    );
    const btn = React.createElement("button", {
      onClick: () => console.log("I'm clicked"),
      style: {
        backgroundColor: "tomato",
      }}, "Click me"
    );
    const container = React.createElement("div", null, [h3, btn]);
    ReactDOM.render(container, root);
  </script>
</html>
```

interactive한 앱에서 하는 작업 모두 **event를 감지**하는 작업이다. → 리액트가 동작하는 방법

`React.createElement` 의 두 번째 인자로 property를 줬을 때는 HTML 태그에 보이지만, event listener를 줬을 때는 보이지 않는 이유

- 두 번째 인자로 property(ex. id, class, style …)를 줬을 때, **리액트가** 해당 값들이 **HTML 태그 안**에 들어가야 하는 것을 **알기 때문**이다.

- 두 번째 인자로 event listener를 줬을 때, **리액트가** 해당 값 들이 **JS에서 돌아가는 이벤트**인 것을 **알기 때문**이다.

### 복습

1. 리액트와 react-dom을 CDN으로 가져온다.

   1. 리액트는 element를 생성하고 event listener 추가하는 것을 도와준다. → **interactive power**를 가지고 있다.

   2. react-dom은 리액트 element를 HTML 코드로 바꿔준다.

      1. 코드 상으로 `<div id="root"></div>` 부분에 `ReactDOM` 리액트 element를 넣는다.

      2. `ReactDOM.render` 은 리액트 element를 root div 안에서 보여주라는 것을 의미한다.

      3. `ReactDOM.render` 의 **첫 번째 인자**는 렌더링 할 **리액트 element**를, **두 번째 인자**는 타겟팅되는 **HTML 태그**를 받는다.

2. `React.createElement` 의 첫 번째 인자는 root에 들어갈 HTML 태그를, 두 번째 인자는 id나 class, event listener 등의 props object를, 세 번째 인자는 리액트 element 등을 받는다.

   1. 리액트 개발자들은 **interactive한 앱**을 만들기 위해서 **event listener가 필요**하다고 생각하고, element에 event listener를 달고자 했다. → 리액트가 훌륭한 이유

   2. **원하는 만큼** props에 event listener를 추가할 수 있다.

### JSX (createElement를 대체할 수 있는 방법)

왜 `React.createElement` 를 대체하는가?

조금 더 편리하게 사용하기 위해

JSX란?

- Javascript를 확장한 문법

HTML과 **비슷한 문법**으로 리액트 element를 만들 수 있게 해준다.

```jsx
...
// React.createElement
const h3 = React.createElement("h3", {
  id: "title",
  onMouseEnter: () => console.log("mouse enter");
  }, "Hello I'm a span"
);
const btn = React.createElement("button", {
  onClick: () => console.log("I'm clicked"),
  style: {
    backgroundColor: "tomato",
  }}, "Click me"
);

// JSX
const Title = (
  <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
    Hello I'm a title
  </h3>
);
const Button = (
  <button
    style={{ backgroundColor: "tomato", }}
    onClick={() => console.log("I'm clicked")}
  >Click me</button>
);
...
```

위의 코드처럼 변환한 코드를 바로 사용하려면 에러가 발생한다. → 브라우저가 이해하지 못하기 때문

[Babel](https://babeljs.io/repl#?browsers=defaults%2C%20not%20ie%2011%2C%20not%20ie_mob%2011&build=&builtIns=false&corejs=3.21&spec=false&loose=false&code_lz=Q&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=true&presets=env%2Creact%2Cstage-2&prettier=false&targets=&version=7.18.4&externalPlugins=&assumptions=%7B%7D) 을 사용해 브라우저가 이해할 수 있는 `React.createElement` 의 형태로 변환해야 한다.

```jsx
// JSX
const Title = (
  <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
    Hello I'm a title
  </h3>
);
const Button = (
  <button
    style={{ backgroundColor: "tomato" }}
    onClick={() => console.log("I'm clicked")}
  >
    Click me
  </button>
);

// Babel로 변환한 코드
("use strict");

const Title = /*#__PURE__*/ React.createElement(
  "h3",
  {
    id: "title",
    onMouseEnter: () => console.log("mouse enter"),
  },
  "Hello I'm a title"
);
const Button = /*#__PURE__*/ React.createElement(
  "button",
  {
    style: {
      backgroundColor: "tomato",
    },
    onClick: () => console.log("I'm clicked"),
  },
  "Click me"
);
```

- Babel을 CDN 형태로 가져와서 사용

```html
<!-- react-for-beginners/index.html -->

<!DOCTYPE html>
<html>
  <body>
    <div id="root"></div>
  </body>
  <!-- 리액트는 앱의 interactive를 높여주는 라이브러리이고, -->
  <!-- react-dom은 모든 리액트 element를 HTML body에 놓을 수 있게 해주는 패키지 -->
  <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
  <!-- jsx 문법을 변환하기 위해 Babel을 가져옴 (이 방식은 느려서 선호되는 방식은 아님) -->
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    const root = document.getElementById("root");
    const Title = (
      <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
        Hello I'm a title
      </h3>
    );
    const Button = (
      <button
        style={{ backgroundColor: "tomato" }}
        onClick={() => console.log("I'm clicked")}
      >
        Click me
      </button>
    );
    const container = React.createElement("div", null, [Title, Button]);
    ReactDOM.render(container, root);
  </script>
</html>
```

해당 HTML 파일을 로컬 환경에서 실행한 후,

**개발자 도구의 Elements 탭**에서 **JSX로 작성한 script와 Babel이 변환한 script**가 모두 존재하는 것을 확인할 수 있다.

### 컴포넌트 in 컴포넌트 (JSX)

컴포넌트를 JSX 문법으로 가져올 때, 단순히 div 태그 안에 컴포넌트명을 텍스트로 작성해서 가져올 수는 없다.

- `<div>Title Button</div>` 과 같은 형태는 불가능

1. 가져올 컴포넌트를 **함수 형태**로 바꿔준다.

   - 익명함수의 형태로 변경해도 좋고, 일반적인 함수 표현식으로 변경해도 좋다.

   - 일반적인 함수 표현식으로 변경하려면 **반드시 JSX 문법을 return** 해야 한다.

   ```jsx
   ...
   // arrow function (익명함수)
   const Title = () => (
     <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
       Hello I'm a title
     </h3>
   );
   const Button = () => (
     <button
       style={{ backgroundColor: "tomato", }}
       onClick={() => console.log("I'm clicked")}
     >Click me</button>
   );

   // same as
   function Title() {
     return (
   	  <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
   	    Hello I'm a title
   	  </h3>
   	);
   }
   function Button() {
     return (
   	  <button
   	    style={{ backgroundColor: "tomato", }}
   	    onClick={() => console.log("I'm clicked")}
   	  >Click me</button>
   	);
   }
   ...
   ```

2. **JSX 문법의 형태**로 리액트 컴포넌트를 가져온다.

   - 일반적인 **HTML 태그를 사용할 때**와 **동일한 방법**을 사용한다.

   ```jsx
   ...
   const Container = (
     <div>
       <Title />
       <Button />
     </div>
   );

   // same as
   const Container = (
     <div>
   	  <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
   	    Hello I'm a title
   	  </h3>
       <button
   	    style={{ backgroundColor: "tomato", }}
   	    onClick={() => console.log("I'm clicked")}
   	  >Click me</button>
     </div>
   );

   ...
   ```

   - 위의 코드는 div를 렌더링 하는 컴포넌트가 Title, Button에 관련된 코드를 포함시키고 있는 형태라고 생각하면 된다.

   - 컴포넌트의 첫글자는 **반드시 대문자**여야 한다.

     - 만약 소문자면, 리액트와 JSX 문법은 `<button />` 태그가 **일반적인 HTML의 버튼 태그**라고 생각할 것

   - JSX는 앱을 여러 작은 요소로 나눠 관리할 수 있도록 도와준다.

   - 마찬가지로 **개발자 도구의 Elements 탭**에서 확인해 보면, JSX로 작성한 부분이 `React.CreateElement` 로 변환된 것을 확인할 수 있다.

3. Container까지 함수로 변경한 후, `ReactDOM` 코드도 JSX 문법으로 변경해 준다.

   ```html
   <!-- react-for-beginners/index.html -->

   <!DOCTYPE html>
   <html>
     <body>
       <div id="root"></div>
     </body>
     <!-- 리액트는 앱의 interactive를 높여주는 라이브러리이고, -->
     <!-- react-dom은 모든 리액트 element를 HTML body에 놓을 수 있게 해주는 패키지 -->
     <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
     <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
     <!-- jsx 문법을 변환하기 위해 Babel을 가져옴 (이 방식은 느려서 선호되는 방식은 아님) -->
     <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
     <script type="text/babel">
       const root = document.getElementById("root");
       const Title = () => (
         <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
           Hello I'm a title
         </h3>
       );
       const Button = () => (
         <button
           style={{ backgroundColor: "tomato" }}
           onClick={() => console.log("I'm clicked")}
         >
           Click me
         </button>
       );
       const Container = () => (
         <div>
           <Title />
           <Button />
         </div>
       );
       ReactDOM.render(<Container />, root);
     </script>
   </html>
   ```

## 끝!
