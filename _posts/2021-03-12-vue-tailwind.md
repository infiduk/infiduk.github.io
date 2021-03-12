---
title: "[Vue/Tailwind] 뷰(Vue)에 Tailwind 적용시키기"
date: 2021-03-12 09:03:04 +09:00
tags: study vue tailwind css javascript typescript
comments: true
---

뷰(Vue)에 Tailwind 적용시키기
Vue Component with Tailwind CSS

## Tailwind?

[Tailwind](https://tailwindcss.com)

기존의 CSS 프레임워크(Framework) - Vuetify, Buefy 등은 UI를 구성하는 데 필요한 컴포넌트들이 미리 정의되어 있어 개발 시 해당 컴포넌트들을 사용해 쉽게 디자인을 입힐 수 있습니다.

하지만, 컴포넌트가 이미 정의되어 있기 때문에 원하는 형태로 커스터마이징 할 때는 어느정도의 번거로움이 생길 수 밖에 없었습니다.

그래서 다른 CSS를 찾아보다가 발견한 녀석이 Tailwind라는 친구입니다.

Tailwind도 사전에 CSS들이 정의되어 있다는 점이 기존의 프레임워크들과 같다고 볼 수도 있는데요, 컴포넌트 형태가 아닌 클래스 형태로 정의되어 있다는 것이 다른 점입니다.

즉, HTML 문서에 클래스를 정의하고 원하는 대로 가져와서 UI를 구성할 수 있습니다.

물론 이미 컴포넌트가 정의되어 있는 기존의 CSS 프레임워크로 디자인을 구성하는 것 보다 상대적으로 시간이 더 필요하겠지만,

원하는 대로 UI를 커스터마이징을 할 수 있고 CSS를 직관적으로 알아볼 수 있기 때문에 한번 사용해 보는 것도 나쁘지 않을 것 같다고 생각합니다. :)

```html
<!-- 적용 예시, Tailwind 공식 문서 -->
<figure class="bg-gray-100 rounded-xl p-8">
  <img
    class="w-32 h-32 rounded-full mx-auto"
    src="/sarah-dayan.jpg"
    alt=""
    width="384"
    height="512"
  />
  <div class="pt-6 space-y-4">
    <blockquote>
      <p class="text-lg font-semibold">
        “Tailwind CSS is the only framework that I've seen scale on large teams.
        It’s easy to customize, adapts to any design, and the build size is
        tiny.”
      </p>
    </blockquote>
    <figcaption class="font-medium">
      <div class="text-cyan-600">Sarah Dayan</div>
      <div>Staff Engineer, Algolia</div>
    </figcaption>
  </div>
</figure>
```

Tailwind에 정의되어 있는 클래스를 직접 사용하여 UI를 입힐 수 있습니다.

## Vue에 적용시키는 방법

### Tailwind CSS 설치

먼저 Vue 프로젝트에 Tailwind CSS를 설치해줍니다.

`npm install -D tailwindcss@latest postcss@latest autoprefixer@latest`

Vue 프로젝트가 없다면 아래의 명령어를 통해 프로젝트를 생성하면 됩니다.

`vue create tailwindcss-vue`

Vue CLI가 없다면 아래의 명령어를 통해 설치해주시고, Vue 프로젝트를 생성하면 됩니다.

`npm install -g @vue/cli`

### configuration file 생성

Tailwind, postcss의 설정 파일을 생성해줍니다.

`npx tailwindcss init -p`

### 최적화 하기

Tailwind CSS의 용량은 상대적으로 큰 편에 속합니다. (약 800kb 조금 안됨)

프로젝트의 용량을 가볍게 하기 위해 최적화 과정을 진행해줍니다.

purge 부분을 아래와 같이 바꿔주시면 됩니다.

```javascript
module.exports = {
  // purge: [],
  purge: ["./index.html", "./src/**/*.{vue,js,ts,jsx,tsx}"],
  darkMode: false, // or 'media' or 'class'
  theme: {
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [],
};
```

### css 파일 생성

`./src` 경로 밑에 Tailwind css를 import 해주기 위한 css 파일을 만들어 줍니다.

```css
/* ./src/index.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### css 파일 적용

`./src/main.js`에 만들어 둔 css 파일을 적용시킵니다.

```javascript
import { createApp } from "vue";
import App from "./App.vue";
import "./index.css";

createApp(App).mount("#app");
```

### 실행

`npm run serve` 명령어를 통해 Vue 프로젝트를 실행시키면 Vue에 Tailwind CSS 적용이 완료됩니다!

## 에러

혹시 프로젝트를 실행시킬 때 아래와 같은 에러가 발생한다면 참고하시기 바랍니다.

`PostCSS plugin tailwindcss requires PostCSS 8`

### 해결 방법

postcss 8 -> 7 버전을 사용하는 방법으로 해결할 수 있습니다.

기존에 설치했던 모듈을 삭제해줍니다.

`npm uninstall tailwindcss postcss autoprefixer`

특정 버전의 모듈로 설치를 진행합니다.

`npm install tailwindcss@npm:@tailwindcss/postcss7-compat postcss@^7 autoprefixer@^9`

설치가 완료되었다면, 다시 `npm run serve` 로 프로젝트를 실행시키면 됩니다.

## 참고

- [Install Tailwind CSS with Vue 3 and Vite (공식 문서)](https://tailwindcss.com/docs/guides/vue-3-vite)
- [다 된 Vue에 Tailwindcss 뿌리기](https://imkh.dev/vue-tailwindcss/)
