---
title: "[React] onClick 사용 시 함수 넘길 때 주의 사항"
date: 2022-09-08 09:20:00 +09:00
tags: study react javascript typescript
comments: true
---

<a href="https://hits.seeyoufarm.com"><img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https://infiduk.github.io/2022/09/08/react-onclick.html&count_bg=%23EDD513&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=%E2%9C%A8+page+view+%E2%9C%A8&edge_flat=false" /></a>

리액트 onClick 사용 시 주의 사항

```jsx
... onClick={setCount(count + 1)} ...
```

은 안되고

```jsx
... onClick={() => setCount(count + 1)} ...
```

이 되는 이유

## 왜요?

첫 번째 방법의 경우, 함수를 실행하는 코드이기 때문에 컴포넌트가 렌더링 되는 동시에 실행이 된다.

그러면? 렌더링 될 때 `count` 가 `1` 증가 하는데, `state` 가 변경 되었으니 컴포넌트가 다시 렌더링 됨

다시 렌더링 됐으니 또 `count` 가 `1` 올라가고… `state` 변경으로 인해 또 다시 렌더링…

즉, 계속 이런 현상이 반복 되면 무한 루프에 빠져버려 돌아올 수 없는 길을 걷게 된다.

## 어떻게 해결 해요?

### onClick 전용 함수를 만들어 따로 빼서 사용

```jsx
...
const sc = () => setCount(count + 1)
or
function sc() { setCount(count + 1) }
...

... onClick={sc} ...
```

보통 위의 형태로 사용해 함수가 즉시 실행되는 것을 방지하고, 사용자가 클릭했을 때만 호출 되도록 한다.

### onClick 에 직접 Callback Function 을 넣어 사용

또는, onClick 에 콜백 함수의 형태로 함수를 넣어주는 방법도 있다.

```jsx
... onClick={() => setCount(count + 1)} ...
```

콜백 함수의 형태를 사용한 경우에도 마찬가지로,

컴포넌트가 렌더링 되었을 때 바로 실행되지 않고 클릭 시에만 호출된다.

## 여담

위의 예제는 예시를 위해 임의로 설정한 함수이다.

만약 이전 값이 현재 값에 영향을 미치는 경우에는 (클릭 시 값이 1 씩 증가하는 함수를 만드는 경우)

```jsx
setCount(prev ⇒ prev + 1)
```

의 형태로 사용하는 게 좋다.

### 이유

```jsx
setCount(count + 1);
setCount(count + 1);
setCount(count + 1);
setCount(count + 1);
```

를 실행 했을 때와

```jsx
setCount((prev) => prev + 1);
setCount((prev) => prev + 1);
setCount((prev) => prev + 1);
setCount((prev) => prev + 1);
```

를 실행 했을 때의 결과 값이 다르다.

### setState 주의사항

`setState` 는 비동기 함수이기 때문에 위의 방법으로 실행하면

하나의 `setState` 를 실행한 것과 같은 결과가 나오지만, (값이 1 만 증가됨)

아래의 방법 처럼 이전 값을 가져와서 업데이트를 진행 하면

계속 이전 값을 참조하게 되어 올바른 결과를 도출한다. (값이 4 증가됨)

## 참고

- [14. 배열에 항목 제거하기](https://react.vlpt.us/basic/14-array-remove.html)

- [what's the difference between setCount(prev => prev + 1) and setCount(count + 1)?](https://stackoverflow.com/questions/64311416/whats-the-difference-between-setcountprev-prev-1-and-setcountcount-1)
