---
title: "[Blockchain/Ethereum] EIP-747: wallet_watchAsset"
date: 2023-01-04 17:20:00 +09:00
tags: study blockchain metamask
comments: true
---

EIP-747: wallet_watchAsset

## TL;DR

`wallet_watchAsset` 은

사용자의 웹 월렛(지갑)에 토큰(자산)을 추가할 수 있도록 제안하는 RPC 메소드로,

아래의 방법처럼 사용하면 된다.

```jsx
...
ethereum.request({
  method: 'wallet_watchAsset',
  params: {
    type: 'ERC20',
    options: {
      address: '0xb60e8dd61c5d32be8058bb8eb970870f07233155',
      symbol: 'FOO',
      decimals: 18,
      image: 'https://foo.io/token-image.svg',
    },
  },
});
  .then((success) => {
    if (success) {
      console.log('FOO successfully added to wallet!')
    } else {
      throw new Error('Something went wrong.')
    }
  })
  .catch(console.error)
...
```

해당 코드를 적용해 보면,

메타마스크 익스텐션에는 아래의 캡쳐 화면과 같이 나타난다.

토큰 추가 버튼을 누르면 익스텐션에 해당 토큰이 추가된 것을 확인할 수 있다.

![1.png](https://user-images.githubusercontent.com/48206157/210513798-cdedba55-c502-49a4-a183-886dbced92a1.png)

## 주저리

오늘도 평화로운 인피덕의 회사 생활

사내에서 개발 중인 서비스는 필연적으로 여러 종류의 토큰(코인)을 사용해야 하는 서비스로,

사용자가 본인의 토큰(자산)을 확인하려면

하나하나 메타마스크 익스텐션에 추가해야하는 번거로움이 있었다 ㅎ

사실 이 내용을 인지하지 않고 있다가, 얼마 전에 이런 기능이 있었으면 좋겠다는 의견을 들었던 인피덕

팀장님과 눈빛 교환 후 RPC 콜 때릴 만한 친구를 찾아보게 되는데..

## wallet_watchAsset

### 이게 머임

사용자 웹 월렛(지갑)에 토큰(자산)을 추가할 수 있도록 제안하는 RPC 메소드

### 어디다 씀

웹 월렛이나 블록체인 댑 서비스, 토큰을 사용하는 모든 곳에 가능한 것으로 보인다.

### 왜 씀

~예시로 설명~

옛날 옛적에.. 호랑이 담배피던 시절…

웹 월렛을 사용하고 있는 인피덕은 `INFIDUK` 이라는 토큰만 가지고 있었다.

(웹 월렛이라는 단어가 어렵다면 메타마스크라고 생각해도 좋다.)

인피덕이 `MAPLE` 이라는 토큰을 100개 정도 에어드랍 받았다고 생각해 보자.

하지만 인피덕은 `INFIDUK` 토큰만 가지고 있었기 때문에 지갑 상으로는 `MAPLE` 토큰을 확인할 수 없었다. (토큰을 추가해야 월렛에 보임)

당황한 인피덕은 지갑에 `MAPLE` 토큰을 추가하기 위해 구글링하며 끙끙 앓았고,

마침내 `MAPLE` 토큰의 주소와 심볼, 소수점 등을 알아내어

지갑 내의 자산 추가 기능을 찾아 해당 내용으로 본인이 사용하는 지갑에 `MAPLE` 토큰을 추가했다.

…

이와 같은 사용자의 부정적인 경험을 방지하기 위해

개발자 측면에서 `wallet_watchAsset` 메소드를 사용한 기능을 서비스에 넣어두면

(버튼을 누르면 `wallet_watchAsset` 메소드를 호출하는 코드)

사용자는 버튼 한번에 쉽고 간단하게 토큰을 추가할 수 있게 된다.

**이럴 때 사용하면 좋은 RPC 메소드**

### 어케 씀 (파람스)

문서에는 아래와 같이 정리되어 있다.

```jsx
interface WatchAssetParameters {
  type: string; // 추가하려는 자산의 타입 (아마도 대부분이 'ERC20' 일 것)
  options: {
    address: string, // 토큰 컨트랙트 주소
    symbol?: string, // 심볼 이름
    decimals?: number, // 소수점 (아마도 대부분 18일텐데, 왜냐면 이더리움이 18 임)
    image?: string // 토큰 이미지 (png, jpg, svg 등의 이미지 링크 혹은 base64 형태)
  };
}
```

### ㄹㅇ로 어케 씀

다른 EIP 메소드들과 동일하게 `ethereum.request` 를 사용하며,

파람스로는 위에서 알아본 친구들을 넣으면 된다.

아래의 코드는 추가할 토큰의 타입이 **ERC20**일 경우에 정상적으로 동작하는 코드이고,

코드는 아래와 같이

```jsx
...
ethereum.request({
  method: 'wallet_watchAsset',
  params: {
    type: 'ERC20',
    options: {
      address: '0xb60e8dd61c5d32be8058bb8eb970870f07233155',
      symbol: 'FOO',
      decimals: 18,
      image: 'https://foo.io/token-image.svg',
    },
  },
});
  .then((success) => {
    if (success) {
      console.log('FOO successfully added to wallet!')
    } else {
      throw new Error('Something went wrong.')
    }
  })
  .catch(console.error)
...
```

이런 식으로 작성하면 된다.

파람스에 들어가는 값들은 문서에 정리된 그대로 사용했다.

리턴되는 값은 `boolean` 타입으로 내려오는데, 자산이 정상적으로 추가된 경우 `true` 가,

그 이외의 경우는 모두 에러로 처리하면 된다.

해당 코드를 적용해 보면,

메타마스크 익스텐션에는 아래의 캡쳐 화면과 같이 나타난다.

토큰 추가 버튼을 누르면 익스텐션에 해당 토큰이 추가된 것을 확인할 수 있다.

![2.png](https://user-images.githubusercontent.com/48206157/210513798-cdedba55-c502-49a4-a183-886dbced92a1.png)

완료~

## 주저리2

아직 한국에서는 이 메소드를 사용하는 곳이 많이 없나보다.

구글링해도 한글로 쓰인 문서가 없는 걸 보면..

그렇다면…….내가…………………. 맨 처음…..?! 🥴

## 참고

- [EIP-747: Add wallet_watchAsset to Provider](https://eips.ethereum.org/EIPS/eip-747)
