---
title: "[React] 나중에 보면 부끄러울 수 있는 리액트(React) 정리 1"
date: 2020-08-24 21:32:04 +09:00
tags: study react javascript
comments: true
---

나.부.리 1

## React 정리....

## React Design Pattern
- `React` 의 `Component` 는 상태, DOM, 이벤트 등 다양한 것들을 관리하는 역할을 함
- `React` 에는 여러 `Design Pattern`이 있음

### Design Pattern?
- 재사용성과 유지보수성을 높이기 위해 사용
- 하나의 `Component` 에서 `Data의 Fetch` 와 `Render` 를 같이 표현하면 코드의 중복이 생길 수 있음
- 따라서, `Data를 가져오는 부분` 과 `가져온 데이터를 뿌리는 부분` 을 나눠줄 필요가 있음
- `Container` vs. `Presentational`
- `Stateful` vs. `Stateless`
- `Smart` vs. `Dumb`
- `Pure` vs. `Unpure` 등등으로 `Component` 를 관리

### Container Component
- `How things work`
- 데이터를 가져오기 위한 컴포넌트 (fetch)
- `style(css)` 가 거의 없음
- `stateful`
- userPage, followedUserList ...

### Presentational Component
- `How things look`
- 데이터를 화면에 나타내기 위한 컴포넌트
- `props` 를 가지고 `data` 를 화면에 출력
- 대부분 `Functional component` 로 작성
- page, sidebar, story, userInfo, list ...

## Redux
- 하나의 `store` 에 데이터를 보관하는 방법
- `store` 의 `state` 는 오직 `action` 을 통해서만 변경이 가능
- `reducer` 는 `pure function` 임
- 상태 관리 라이브러리
- `Flux Pattern` 구현

### Redux 동작 순서
- 변화 발생
- `action` 에서 감지, `type` 에 대한 정보를 가진 객체 생성
- 각 `action` 에 따라 정의된 `reducer` 가 새로운 상태를 만들고 `state` 갱신
- `Component` 들은 `store` 를 구독하고 있다가 상태 변화를 반영

## Redux saga
- `data fetching` 등의 비동기 동작들을 쉽게 하기 위한 라이브러리
- `redux middleware`
- `action` 에 대한 리스너
- 객체를 반환

## 참고
- [Presentational and Container Components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)