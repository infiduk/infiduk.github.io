---
title: "[Study] 지킬(Jekyll)에 Google Analytics 추가하기"
date: 2019-11-05 15:30:00 +09:00
tags: study jekyll
comments: true
---

Adding Google Analytics To Jekyll

## 지킬(Jekyll)에 Google Analytics 추가하기

> Google Analytics로 지킬 블로그 방문 통계를 알아보자!

## 1. Google Analytics 계정 만들기

### 1.1 Google Analytics 접속
- [Google Analytics](https://analytics.google.com/analytics/web/)에 접속합니다.
<br />
- Google 계정이 없다면, 먼저 [Google 가입](https://accounts.google.com/ServiceLogin?hl=ko&passive=true&continue=https://www.google.com/webhp%3Fhl%3Dko%26sa%3DX%26ved%3D0ahUKEwiN553QvdLlAhWEwosBHVwXDw4QPAgH)부터 진행해주세요!
<br />
(Google 계정으로 로그인이 되어있지 않을 경우, Google 로그인 화면으로 넘어갈 수 있습니다.)

### 1.2 Google Analytics 가입
- Google 계정으로 로그인한 상태로 위 `Google Analytics` 링크에 접속하면 아래 화면이 나타납니다.
- 오른쪽에 있는 `가입`을 선택합니다.
<br />
![image_01](https://user-images.githubusercontent.com/48206157/68184898-a1e04780-ffe3-11e9-9a96-26410554d2cb.JPG)

### 1.3 세부 정보 입력
- 먼저 가입할 계정의 이름을 입력합니다.
<br />
![image_02](https://user-images.githubusercontent.com/48206157/68184924-b15f9080-ffe3-11e9-991c-8d74f9e84e50.JPG)
<br />
<br />
- 계정 데이터에 대한 권한을 설정합니다.
<br />
![image_03](https://user-images.githubusercontent.com/48206157/68184925-b1f82700-ffe3-11e9-9827-ccbc9612f81f.JPG)
<br />
<br />
- 권한 설정이 완료되면 `다음`으로 넘어갑니다.

### 1.4 통계 플랫폼 선택
- `Google Analytics`를 적용할 플랫폼을 선택합니다.
<br />
(우리는 `Jekyll`에 대한 통계를 볼 목적이기 때문에 `웹`을 선택하면 됩니다.)
<br />
![image_04](https://user-images.githubusercontent.com/48206157/68184927-b1f82700-ffe3-11e9-94c8-b00b7b60a852.JPG)
<br />
<br />
- 선택이 완료되었다면, `다음`으로 넘어갑니다.

### 1.5 속성 설정
- `Google Analytics`를 적용할 웹 사이트의 이름과 URL, 카테고리와 시간대를 입력합니다.
<br />
![image_05](https://user-images.githubusercontent.com/48206157/68184928-b290bd80-ffe3-11e9-8c97-abfa7c8ab144.JPG)
<br />
<br />
- 모두 입력한 후, `만들기`를 클릭합니다.

### 1.6 Google Analytics 약관 동의
- `Google Analytics`를 사용하기 위해 약관에 동의해줍니다.
<br />
![image_06](https://user-images.githubusercontent.com/48206157/68184929-b290bd80-ffe3-11e9-85ae-0eb2df97652b.JPG)
<br />
![image_07](https://user-images.githubusercontent.com/48206157/68184930-b290bd80-ffe3-11e9-908b-7ac738e55586.JPG)

### 1.7 Google Analytics 가입 완료
- 성공적으로 가입이 되었다면 `완료` 메시지가 나타납니다.
<br />
![image_08](https://user-images.githubusercontent.com/48206157/68184932-b3295400-ffe3-11e9-9996-6af21cb774b3.JPG)

## 2. Jekyll 설정 바꾸기
- 테마에 따라 약간씩 다른 부분이 있을 수 있습니다.

### 2.1 gtag.js 복사
- `Google Analytics` 왼쪽 하단의 `관리` 탭을 선택합니다.
<br />
![image_09](https://user-images.githubusercontent.com/48206157/68187568-58472b00-ffea-11e9-8a3e-cdd615295223.JPG)
<br />
<br />
- `속성`의 `추적 정보`에서 `추적 코드` 탭을 선택합니다.
<br />
![image_10](https://user-images.githubusercontent.com/48206157/68187569-58472b00-ffea-11e9-8340-5c29b3354aec.JPG)
<br />
<br />
- `추적 ID`와 `Global Site Tag(gtag.js)` 부분을 복사해주세요.

### 2.2 gtag.js 붙여넣기
- `Jekyll`의 `_include` 폴더에 `analytics.html`이 있는지 확인해주세요.
<br />
  - `analytics.html`은 `Global Site Tag(gtag.js)`를 넣기 위해 필요한 파일입니다. 꼭 `analytics.html`로 파일 이름을 지정하지 않으셔도 됩니다.
  - 제 블로그에 적용한 `TeXt` 테마의 경우, `_include/analytics-providers`의 `google.html`이 `analytics.html`과 같은 역할을 하고 있습니다.
  <br />
  ![image_12](https://user-images.githubusercontent.com/48206157/68187304-b1fb2580-ffe9-11e9-8829-fc983ef1a796.png)
  <br />
  - `header.html`이나 `footer.html`안에 해당 `gtag.js`를 붙일 수 있도록 설정해 둔 테마도 있습니다!
- 파일이 준비 되었다면, 복사해둔 `gtag.js`를 붙여넣기 해주세요.
<br />
  ``` javascript
  <!-- Global site tag (gtag.js) - Google Analytics -->
  <!-- id 부분에 본인의 추적 ID를 쓰시면 됩니다. -->
  <!-- ex. UA-123456789-1 -->
  <script async src="https://www.googletagmanager.com/gtag/js?id=본인의 추적 ID"></script>
  <script>
    window.dataLayer = window.dataLayer || [];
    function gtag() { dataLayer.push(arguments); }
    gtag('js', new Date());
    // 마찬가지로 본인의 추적 ID를 넣어주시면 됩니다.
    gtag('config', '본인의 추적 ID');
  </script>
  ```

### 2.3 analytics import 하기
- 본인의 블로그 기본 틀 `html`에 위에서 작성한 `analytics.html`를 `include` 해줍니다.
  - `TeXt` 테마의 경우 `base.html`에 이미 `include` 되어 있습니다!
  - 아래 코드가 추가된 곳이 없으면 추가해주세요.
  <br />
  ![image_13](https://user-images.githubusercontent.com/48206157/68191604-3dc57f80-fff3-11e9-916c-c5a79afb46b0.png)

### 2.4 config 설정 변경
- `_config.yml` 파일에서 `analytics`나 `google analytics`를 찾아주세요.
<br />
  ``` yaml
  ...
  analytics:
    provider: google
    ...
    google:
      tracking_id : 본인의 추적 ID
  ...
  ```
- `analytics`의 `provider`를 `google`로 바꿔줍니다.
- `google`의 `tracking_id` 부분에는 본인의 추적 ID를 입력합니다.

## 완료!
- 모든 설정이 완료되었다면 배포를 해주시고, 본인 블로그에 접속한 후 `Google Analytics`를 확인해보면 실시간으로 활성 사용자가 변하는 것을 보실 수 있습니다!
<br />
![image_14](https://user-images.githubusercontent.com/48206157/68187567-57ae9480-ffea-11e9-997f-2cdbe45e5838.JPG)
- `실시간 보고서`를 확인하면 더 자세한 정보를 볼 수 있습니다.