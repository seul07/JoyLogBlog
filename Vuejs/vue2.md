# Vue.js(2) vue 인스턴스 및 템플릿 문법

# Vue Instance

-   Vue.js 화면 개발을 위해 꼭 생성해야 하는 필수 단위이다.Instance 생성
-   `// 새롭게 Vue를 선언 new Vue({ el: '#app', // 어떤 요소에 적용을 할 지 정함 여기서는 HTML 코드에 선언된 id="app"인 div 태그를 지정 data: { // data 는 해당 VueJS에서 사용할 정보들을 선언해주는 역할 title: '안녕 VueJS!' } })`

## 인스턴스 사용할 수 있는 속성과 API

```
new Vue({
  el: ,   // 인스턴스가 그려지는 화면의 시작점 (특정 HTML태그)
  template: ,   // 화면에 표시할 요소 (HTML, CSS 등)
  data: ,  // 뷰의 반응성(Reactivity) 가 반영된 데이터 속성
  methods: ,  // 화면의 동작과 이벤트 로직을 제어하는 메서드
  created: ,  // 뷰의 라이프 사이클과 관련된 속성
  watch: ,  // data 에서 정의한 속성이 변화했을 때 추가 동작을 수행할 수 있게 정의
});
```

---

# Vue 라이프 사이클

Vue 인스턴스 생성에 있어, 가장 먼저 호출되는 함수들로써, 스크립트에서는 window.onload 와 비슷한 느낌이다.

Vue 인스턴스는 **생성**(Create) 되고  
Dom 에 **부착**(Mount) 되고  
**업데이트** (Update) 되며  
**없어지는** (Destroy) 4가지 과정을 거치게 된다.

![](https://images.velog.io/images/yeccye/post/c472dbc8-e12e-4d5c-bd9b-a8d868d47eed/image.png)

### created

`data` 를 반응형으로 추적할 수 있게되며  
`computed,method,watch`등이 활성화되어 접근이 가능하게 된다.  
아직 **Dom**에는 추가되지 않은 상태이다.

```
var app = new Vue({
    el: '#app',
    data() {
        return {
            msg: 'hello';
        }
    },
    created(function() {
        console.log(this.msg); // hello
    })
})
```
​
### mounted
​
가장 많이 사용하는 mounted 훅이다.  
가상 Dom 내용이 실제 Dom 에 부착되고 난 이후에 실행된다.  
`data,computed,method,watch` 등 모든 요소에 접근이 가능하다.

```
var app = new Vue({
    el: '#app',
    mounted(function() {
        console.log('mounted');
    })
})
```

##### created는 데이터 초기화에 대한 목적, mounted는 DOM 조작에 대한 목적으로 사용할 수 있다.

---

# 템플릿 문법

뷰를 화면에 조작하는 방법을 의미한다.

## 데이터 바인딩 : interporation {{ }}

-   `<span>메시지: {{ msg }}</span>`
    -   Mustache Tag(이중중괄호) 를 사용한 보간법(Interporation)
-   Mustaches 는 HTML이 아닌 일반텍스트로 해석 한다.

## 디렉티브 : Directive v-bind

`v-bind` 디렉티브를 사용하여 Vue 인스턴스 내에 선언된 값을 HTML 코드의 속성 값에 사용할 수 있다.  
`v-` 접두사가 붙은 특별한 속성으로 화면의 DOM 조작을 쉽게 할 수 있는 문법을 제공한다.

> v-html HTML의 코드형태로 출력 가능하다.
> 
> ![](https://images.velog.io/images/yeccye/post/b46a6019-71a1-45b9-95ff-ae871d385656/image.png)

-   `v-once` 는 HTML 코드로 출력된 이후 어떤 후처리가 있어도 처음에 출력한 값을 유지시키고 싶을때 사용한다.
-   `v-on` 은 이벤트 리스너 이다.
    -   **이벤트 수식어**
        -   수식어는 점으로 표시되는 특수 접미사로, 디렉티브를 특별한 방법으로 바인딩 해야 함을 나타낸다. 예를 들어, .prevent 수식어는 트리거된 이벤트에서 event.preventDefault()를 호출하도록 v-on 디렉티브에게 알려준다.
            -   `<form v-on:submit.prevent="onSubmit"> ... </form>`
-   `v-model` 은 `<form>` 태그에서 submit 할때 사용하는 속성

## 약어

디렉티브를 줄여서 사용하는 방법이 있다  
`v-bind` 와 `v-on` 에 제공된다.

-   v-bind
-   `<!-- 전체 문법 --> <a v-bind:href="url"> ... </a> <!-- 약어 --> <a :href="url"> ... </a>`
-   v-on
-   `<a v-on:click="doSomething"> ... </a> <!-- 약어 --> <a @click="doSomething"> ... </a>`

> ### 참고
> 
> -   [Vue 라이프사이클](https://wormwlrm.github.io/2018/12/29/Understanding-Vue-Lifecycle-hooks.html)
> -   [Vuejs 템플릿문법](https://beomy.tistory.com/48)
