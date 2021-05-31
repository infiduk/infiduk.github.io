---
title: "[Vue(Nuxt)/vue-infinite-loading] 넉스트(Nuxt)에서 무한 스크롤(infinite scroll) 구현하기"
date: "2021-05-31 08:59:00 +09:00"
tags: study vue nuxt javascript typescript
comments: true
---

<a href="https://hits.seeyoufarm.com"><img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https://infiduk.github.io/2021/05/30/nuxt-infinite-scroll.html&count_bg=%23EDD513&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=%E2%9C%A8+Hi%2C+there%21+%E2%9C%A8&edge_flat=false" /></a>

넉스트(Nuxt)에서 무한 스크롤(infinite scroll) 구현하기
Nuxt component with infinite scroll

## 무한 스크롤(infinite scroll)?

무한 스크롤이란 사용자가 아래로 스크롤했을 때 현재 보고있는 콘텐츠의 더 많은 내용이 페이지 하단에 나타나도록 하여

사용자가 페이지네이션을 위해 추가적인 동작을 하지 않아도 자연스럽게 다음 콘텐츠를 볼 수 있는 기능입니다.

<!-- 아래 예시를 보시면 아~ 이거구나 하고 유추하실 수 있으실거예요.

[video_01](https://user-images.githubusercontent.com/48206157/120126685-0a130180-c1f8-11eb-81a7-87864d34aabf.mov) -->

## Nuxt에서 무한 스크롤을 구현하는 방법

이번 프로젝트는 nuxt를 사용하는 프로젝트이기 때문에, nuxt 환경에서 무한 스크롤을 구현하는 방법으로 진행하겠습니다.

데이터는 배열로 관리하고, 추가되는 데이터는 순서대로 배열에 push 됩니다.

간단한 기능 구현이기 때문에 에러 케이스들의 처리는 구현하지 않았습니다.

### vue-infinite-loading package 설치

먼저 `vue-infinite-loading` 패키지를 설치합니다.

[vue-infinite-loading](https://www.npmjs.com/package/vue-infinite-loading)

개인적으로 패키지를 사용하지 않고 직접 구현하고 싶었는데,

시간 관계 상 이번에는 패키지를 다운받아 적용하고 추후 여유가 생긴다면 **꼭! 직접 구현해 볼 생각입니다.**

아래의 명령어를 통해 패키지를 다운받아줍니다.

```bash
npm install vue-infinite-loading
```

### plugin 파일 생성

plugins 폴더에는 자주 사용될만한 속성, 함수, 외부 라이브러리 등을 정리한 파일이 들어갑니다.

다운받은 vue-infinite-loading 패키지를 적용, 커스텀하기 위해 plugins 폴더에 아래 내용의 plugin 파일을 생성해줍니다.

```javascript
// plugins/infinite-loading.js

import Vue from "vue";
import InfiniteLoading from "vue-infinite-loading";

Vue.component("infinite-loading", InfiniteLoading);

// vue-infinite-loading custom
Vue.use(InfiniteLoading, {
  slots: { noMore: "불러올 데이터가 없어요!" },
  props: { spinner: "circles" },
});
```

코드 아래 부분의 `Vue.use` 는 vue-infinite-loading 패키지의 옵션을 커스텀할 수 있는 부분입니다.

아래 API 문서에서 어떤 옵션을 커스텀할 수 있는지 볼 수 있습니다.

[API 문서](https://peachscript.github.io/vue-infinite-loading/)

`slot` 은 추가적인 데이터를 가져올 때 나타내는 메시지를 커스텀할 수 있습니다.

현재 프로젝트에서는 가져올 데이터가 없을 때 (noMore)의 메시지만 커스텀했는데

추가적으로 데이터가 없을 때 (noResult),

데이터를 가져오는 도중 에러가 발생했을 때 (error) 등의 메시지도 커스텀할 수 있습니다.

```javascript
Vue.use(InfiniteLoading, {
	slots: { error: "에러가 발생했네요. :(" },
	...
});
```

`props` 는 기능 상의 옵션을 커스텀할 수 있습니다.

현재 프로젝트에서는 `spinner` 의 모양만 커스텀했는데

하단 어느 위치에 도달했을 때 추가로 데이터를 가져올지 (distance),

데이터가 추가되는 방향 (direction) 등을 커스텀할 수 있습니다.

```javascript
Vue.use(InfiniteLoading, {
	...,
	props: {
		spinner: "bubbles",
		directioin: "top"
	}
});
```

### config 파일 수정

패키지 설치가 완료되었다면, `nuxt.config.ts` 파일의 `plugin` 부분에 위의 파일을 적용해줍니다.

```typescript
// nuxt.config.ts

...
plugins: [{ src: "~/plugins/infinite-loading", ssr: false }],
...
```

`ssr` 옵션이 `false` 일 경우, 해당 plugin은 클라이언트에서만 동작하게 한다는 의미입니다.

### component 생성

무한 스크롤 기능을 적용할 component를 만들어줍니다.

```javascript
// components/InfiniteList.vue

<template>
  <div>
    <div v-for="(item, idx) in scrollData" :key="idx">
      <div style="padding: 5px;">{{ item.id }} - {{ item.body }}</div>
    </div>
    <br />
    <infinite-loading
      v-if="scrollData.length"
      @infinite="scrolling"
    ></infinite-loading>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "InfiniteList",
  data() {
    return {
      scrollData: [],
      page: 1
    };
  },
  computed: {
    url() {
      // free fake api 사용
      return "https://jsonplaceholder.typicode.com/posts?_page=" + this.page;
    }
  },
  created() {
    this.fetchData();
  },

  methods: {
    async fetchData() {
      const response = await axios.get(this.url);
      this.scrollData = response.data;
    },
    scrolling($state) {
      // 스크롤이 페이지 하단에 위치해도 약간의 딜레이를 주고 데이터를 가져옴
      setTimeout(async () => {
        this.page++;
        const response = await axios.get(this.url);
        if (response && response.data.length > 1) {
          response.data.forEach(item => this.scrollData.push(item));
          $state.loaded();
        } else {
          $state.complete();
        }
      }, 500);
    }
  }
};
</script>
```

### component 라우팅

위에서 만든 무한 스크롤 기능을 확인해 봅시다!

pages 폴더에 test 라는 하위 폴더를 생성하고, 그 밑에 index 파일을 만들어 `/test` 경로로 접근할 수 있게 해줍니다.

```javascript
// pages/test/index.vue

<template>
  <div>
    <infiniteList />
  </div>
</template>

<script>
import infiniteList from "~/components/InfiniteList.vue";

export default {
  components: { infiniteList }
};
</script>
```

### 실행

프로젝트를 실행하고, `/test` 로 접속해보면 무한 스크롤 기능을 확인하실 수 있습니다!

<!-- 위에서 본 예제와 같은 화면을 보실 수 있습니다! -->

## 참고

- [Infinite Scroll Corrected](https://codesandbox.io/s/hoyxb?file=/nuxt.config.js)
- [API 문서](https://peachscript.github.io/vue-infinite-loading/)
