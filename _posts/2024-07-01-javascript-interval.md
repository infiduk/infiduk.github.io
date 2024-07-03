---
title: "[JS] 브라우저 탭 전환 시 setTimeout이 정상 동작하지 않는 이유"
date: 2024-07-01 15:55:00 +09:00
tags: study javascript
comments: true
---

<a href="https://hits.seeyoufarm.com"><img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https://infiduk.github.io/2024/07/01/javascript-interval.html&count_bg=%23EDD513&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=%E2%9C%A8+page+view+%E2%9C%A8&edge_flat=false" /></a>

Why does setTimeout not work properly when switching browser tabs

## TL;DR

[Heavy throttling of chained JS timers beginning in Chrome 88](https://developer.chrome.com/blog/timer-throttling-in-chrome-88)

## 속보) 브라우저에서 양자역학의 증명이 가능하다?

사내 베타 서비스 개발에 여념이 없던 인피덕

오늘도 평화로운 데일리 스크럼을 하며 _누가누가 기획서 제대로 안 읽고 개발했나_ (a.k.a 자체 QA)를 진행하던 중이었다.

그러다 회원가입 시 이메일 인증을 받는 부분에서 이슈를 발견한 팀장님 says:

이메일을 입력하고 인증 번호 전송 버튼을 누른 다음, 메일 확인차 탭을 전환하고 인증 번호를 복사한 후

다시 회원가입 화면으로 돌아왔는데 시간이 천천히 흘렀다는 신비한 이야기

이거 완전 양자역학?

~~내가 회원가입 탭을 안 봤으니까 브라우저 시간이 느리게 흘렀을 수도 안 흘렀을 수도 빠르게 흘렀다가 다시 돌아왔을 수도 (아무 말)~~

어찌 됐든 **파워 블로거 인피덕**으로써 이 주제를 포스팅하지 않고 그냥 넘어갈 수 없었고 그러지 아니하여 아니할 수 없었다는 이야기

## 양자역학의 이유는 무엇일까?

위의 [크롬 개발자 문서 - Heavy throttling of chained JS timers beginning in Chrome 88](https://developer.chrome.com/blog/timer-throttling-in-chrome-88)를 참고했을 때,

비활성 탭에서 돌아가는 자바스크립트 타이머는 **CPU 및 배터리 사용의 최적화**를 위해 성능상 **제한**될 수 있다고 한다!

단순히 생각해 봐도, 많은 탭이 열려있을 때 각 탭에 있는 모든 타이머가 지연되지 않고 계속 실행된다면.. _~~메모리 폭발~~_

즉, 브라우저는 비활성 탭의 타이머를 그대로 두지 않고 최적화를 위해 타이머의 실행 간격을 느리게 조정하므로

탭을 옮긴 후 다른 작업을 하다가 시간이 지나고 나서 다시 원래의 탭으로 돌아왔을 때 타이머가 정상 작동하지 않았던 현상은 올바른 현상인 것!

그리고 자바스크립트는 싱글 스레드 기반의 언어이기 때문에 동기적으로 시간이 오래 걸리는 일을 처리하고 있는 상황에서도 **블로킹 현상**이 발생해 타이머가 정상 작동하지 않을 수 있다.

_여기서 잠깐, 블로킹이 뭔데? 라고 생각한 당신이라면 인피덕의 [블로킹 뽀시기](https://infiduk.github.io/2024/05/20/javascript.html) 글을 보고 오는 것을 추천한다._

## 양자역학을 방지하려면?

무지성 setTimeout이나 setInterval 등을 사용하지 말고, requestAnimationFrame라는 녀석을 사용해 보자.

### requestAnimationFrame?

애니메이션을 구현할 때 사용하는 함수로, 브라우저의 프레임 주기에 따라 동작하기 때문에 다음 프레임이 그려지기 전에 해당 함수가 먼저 실행된다는 특징을 가진다.

또한, setTimeout 등과 달리 지연 및 블로킹 현상이 생기지 않는다는 특징을 가지고 있다.

폴링의 경우를 예시로 들어보자.

setTimeout 등으로 타이머를 구현

- 탭이 비활성화되더라도 타이머가 백그라운드에서 계속 실행된다.

- 브라우저는 자원의 최적화를 위해 타이머의 시간 간격을 조정하게 되어 원래 탭으로 돌아오더라도 시간이 맞지 않는 현상이 발생한다.

하지만 requestAnimationFrame을 사용한다면?

- 구현한 탭이 활성화된 상태일 때만 현재 시간 - 기준 시간을 계산해서 화면에 뿌린다.

- 다른 탭에서 작업을 진행하다가 돌아와도 돌아온 시점의 시간 - 기준 시간을 비교하여 타이머를 그린다.

따라서 requestAnimationFrame을 활용해 시간을 계산하는 것이 훨씬 효율적이기 때문에 이 친구를 사용해 보도록 하자!

## 맺음말

그동안 수많은 사이트를 이용하면서 수많은 이메일 인증을 해왔었지만 **탭 전환 시 시간이 달라진다** 는 생각을 한 적이 없었다.

앞으로는 이런 인증을 받을 때 요 현상을 각각의 사이트가 어떻게 처리하고 있는지 확인해 보는 것도 매우 interesting 하겠다.

그리고 반복적인 시간 작업을 할 때 무지성 setTimeout이나 setInterval 사용을 좀 지양해야 할 필요가 있어 보인다.

후후.. to be continued...

## 참고

- Chat GPT
- [웹 애니메이션 최적화 requestAnimationFrame 가이드](https://inpa.tistory.com/entry/%F0%9F%8C%90-requestAnimationFrame-%EA%B0%80%EC%9D%B4%EB%93%9C)
