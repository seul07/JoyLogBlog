# Vue.js(4) Router 및 Axios, async await 개념

# Vue Router

싱글페이지 애플리케이션 구현할 때 사용하는 라이브러리 이다.  
페이지간에 이동하는 기능 구현할때 사용한다.

> 라우터 인스턴스 생성  
> var router = new VueRouter({ ... })

-   라우터 옵션 추가 가능
    
    -   routes : 라우팅 할 URL 과 컴포넌트 값 지정
        -   path : 페이지 url
        -   component : 해당 페이지가 뿌려질 컴포넌트
    -   mode URL 의 해쉬 값 제거 속성
        -   mode=''history' ===> # 가 기본값으로 붙는 것을 제거
    
    2.  인스턴스에 라우터 인스턴스 등록  
        `new Vue({ router: router ...})`

## 설치

[https://router.vuejs.org/installation.html](https://router.vuejs.org/installation.html)  
공식사이트 설치 링크

`npm install vue-router`

npm : node pakcage manager

```
const router = new VueRouter({   // 라우터 객체 생성
    mode: 'history',
    routes: [    // 페이지의 라우팅 정보
        {
            path: '/login',   // 페이지 url
            component: () =>   // 해당 url 에서 표시될 컴포넌트
                import ('@/views/LoginPage.vue'),
        },   ... 
```

#### 코드 스플리팅 `import ('@/views/LoginPage.vue')`

기존처럼 import 를 통해 모든 컴포넌트를 처음에 로딩하는 것이 아니라  
해당 url 로 이동했을때만 들고 오도록 하는 것이다.

### `<router-view>`

페이지 url이 변경됬을때 그에따라 뿌려지는 영역

### router-link

`<router-link>` 는 실제 화면에서는 `<a href=''>` 태그로 변형되서 나온다.

```
<div id="app">
  <h1>Hello App!</h1>
  <p>
    <!-- 네비게이션을 위해 router-link 컴포넌트를 사용합니다. -->
    <!-- 구체적인 속성은 `to` prop을 이용합니다. -->
    <!-- 기본적으로 `<router-link>`는 `<a>` 태그로 렌더링됩니다.-->
    <router-link to="/login">Go to Login</router-link>
    <router-link to="/main">Go to Main</router-link>
  </p>
  <!-- 라우트 아울렛 -->
  <!-- 현재 라우트에 맞는 컴포넌트가 렌더링됩니다. -->
  <router-view></router-view>
</div>
```

#### 없는 페이지 접근 라우터 처리

path : '\*',  
compoment: () => import ( ... NotFoundPage.vue)

---

# Axios

-   ajax 통신과 같이 비동기 통신 기법이다.
-   vue resource 라이브러리 => 2년전에 없어짐
-   Vue 에서 가장 많이 사용하는 HTTP통신 라이브러리 이다.
-   `npm install axios` 를 통해 설치하거나  
    `<script src="https://unpkg.com/axios/dist/axios.min.js"></script>` CDN 입력을 통해 설치 한다.

axios 모듈에서 request/response 는 비동기로 처리되기 때문에 처리 순서를 지정하지 않으면 request로 요청을 보내고 나서 response 도 응답을 받기 전에 다음 구문을 수행해버려서 결과를 받아오지 못한다.

```
testFunction() {
    const response = axios.get('api/test')
    console.log(response)
}
```

결과  
`Promise {<pending>} __proto__: Promise [[PromiseStatus]]: "resolved" [[PromiseValue]]: Object`

javascript 는 axios() 를 사용해서 request를 보내는 연산을 수행하고 response를 언제 받는지는 잘 모르겠고, 다음 문장을 수행하기 때문이다.  
이를 순차적으로 처리하기위해 **Promise** 를 사용한다.

> Promisse  
> 데이터를 받아오기도 전에 데이터를 표시하려고 하면 오류가 발생 => 이 문제를 해결하기 위한 방법이다.

```
testFunction() {
    axios.get('api/test')
    .then(function(response) {
        console.log(response)
    })
}
```

`.then()` 만 붙이면 결과값을 불러온다.  
**단 !** `.then()` 구문 내에서만 순차적으로 처리한다.

예를 들어

```
testFunction() {
    axios.get('api/test')
    .then(function(response) {
        console.log(response)
    })

    console.log('Test')
}
```

`console.log('Test')`

---

# async await

비동기 처리방식인 콜백함수와 프로미스의 단점을 보완한다.  
`async function 함수명 () { await 비동기_처리_메서드_명() ; }`  
비동기 처리메서드는 `프로미스객체`를 반환하는 함수이다.

#### acync 는 어떤 값을 return 하던간에 Promise 가 리턴된다.

# Vue CLI

`npm install -g @vue/cli` 로 설치할 수 있다.  
권한이 없다면 sudo 앞에 붙이면 된다.

# main.js

`import App from './App.vue'`  
`new Vue({ el : '#app', render : h => h(App), // ==> 템플릿속성 정의됬을때 render 함수가 실행된다. })`

App 컴포넌트를 불러와서 Vue 에 집어넣고 랜더링 했다.

# 싱글파일 컴포넌트

`<template></template>`  
`<script></script>`  
`<style></style>`  
세 속성을 한파일에 관리하겠다는 것이 싱글파일 컴포넌트이다.

#### 싱글파일 컴포넌트에서 props 속성 사용

#### 싱글파일 컴포넌트에서 event emit 사용

# Store

#### state 여러 컴포넌트 간에 공유되는 데이터

#### mutations state값(데이터) 를 변경할 수 있는 유일한 메서드

```
 * commit() 으로 동작시킨다.
```

> #### 참조
> 
> 1.  [async..await와 axios 및 Promise](https://amanokaze.github.io/blog/Vuejs-async-await/)
