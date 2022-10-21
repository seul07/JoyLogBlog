# Vue.js(3) Vue 인스턴스 속성 및 컴포넌트

# Vue 인스턴스

```
new Vue({
  el:,
  template:,
  data: ,
  methods: ,
  created: ,
  watch: ,
});
```

-   el: 인스턴스가 그려지는 화면의 시작점
-   template: 화면에 표시할 요소
-   data: 데이터
-   methods: 이벤트 함수들
-   created: 라이프사이클 중 하나
-   watch: data에서 정의한 속성이 변경됐을 때 추가 동작을 정의
-   computed: 데이터를 계산한 결과를 속성으로 사용하기 위해 사용

## methods 함수저장소

## computed

-   데이터의 값에 따라서 바뀌는 값을 정의하는 속성이다.
-   템플릿 내에 표현식을 넣을 수 있다. 하지만 간단한 연산일 때만 이용하는 것이 좋다.
    
    ```
    <div id="example">
    {{ message.split('').reverse().join('') }}
    </div>
    ```
    
    이렇게 연산식이 복잡하다면? 이를 위해 **computed** 속성이 존재한다.

```
<div id="example">
  <p>원본 메시지: "{{ message }}"</p>
  <p>역순으로 표시한 메시지: "{{ reversedMessage }}"</p>
</div>

var vm = new Vue({
  el: '#example',
  data: {
    message: '안녕하세요'
  },
  computed: {
    // 계산된 getter
    reversedMessage: function () {
      // `this` 는 vm 인스턴스를 가리킵니다.
      return this.message.split('').reverse().join('')
    }
  }
})
```

### watch

대부분의 경우 computed 속성이 더 적합하지만 사용자가 만든 감시자가 필요한 경우가 있다. 그래서 Vue는 watch 옵션을 통해 데이터 변경에 반응하는 보다 일반적인 방법을 제공한다. 이는 데이터 변경에 대한 응답으로 비동기식 또는 시간이 많이 소요되는 조작을 수행하려는 경우에 가장 유용하다.

```
//template
<div id="watch-example">
  <p>
    yes/no 질문을 물어보세요:
    <input v-model="question">
  </p>
  <p>{{ answer }}</p>
</div>
//script
var watchExampleVM = new Vue({
  el: '#watch-example',
  data: {
    question: '',
    answer: '질문을 하기 전까지는 대답할 수 없습니다.'
  },
  watch: {
    // 질문이 변경될 때 마다 이 기능이 실행됩니다.
    question: function (newQuestion) {
      this.answer = '입력을 기다리는 중...'
      this.debouncedGetAnswer()
    }
  }
})  
```

### computed VS watch

-   computed : 선언형 프로그래밍 방식
    -   계산된 값을 출력하기위함이다.
-   watch : 명령형 프로그래밍 방식
    -   어떤 조건이 되었을때 함수를 실행시키기 위함이다.
    -   데이터를 감시해서 값이 변화할 때마다 정의한 함수가 실행된다.
    -   데이터 변경의 응답으로 비동기식 계산이 필요한 경우나 시간이 많이 소요되는 계산을 해야 할때 사용하는 것이 좋다.  
        보통은 명령형 프로그래밍인 watch 보다는 선언형 프로그래밍인 computed를 사용하는 것이 더 좋다.

> watch를 사용하면, API롤 호출하고 그 결과에 대한 응답을 받기 전까지 중간 상태를 설정할 수있습니다. computed를 사용하면 API 호출 결과를 기다리는 동안의 중간 상태을 설정할 수 없습니다.

### computed VS method

computed와 methods의 차이점은 **캐싱** 여부이다. computed속성은 내부적으로 데이터를 캐싱하고있다. methods는 매번 새로 호출해서 계산한다.

**computed**는 종속 대상이 변경 될 때만 함수를 호출한다.. message 값이 변하지 않는 한 reversedMessage를 여러번 호출하여도 다시 계산하지 않고 **캐싱한 결과를 즉시 반환**한다.  
시간이 많이 걸리는 계산을 할 때, **computed**을 사용하면 더 좋은 효율의 어플리케이션을 만들 수 있다.  
캐싱을 하지 않고, **호출 할 때마다 새롭게 계산을 해야 하는 경우**에는 **methods**를 사용해야 한다.

---

# 컴포넌트

화면의 영역을 일정한 단위로 쪼개어 재활용 가능한 형태로 관리하는 것이다.

#### 전역등록

`Vue.component('my-component-name', { /* ... */ })`

를 이용해서 컴포넌트를 **전역**으로 등록한다.

컴포넌트의 이름은 첫 번째 인자로 들어가는데, **케밥표기법** 으로 작성하는 것을 권장한다.  
`MyComponentName`처럼 파스칼표기법으로도 할 수 있지만, DOM에 바로 쓸 때는 케밥-표기법 이름만 가능하기 때문에 굳이 쓸 이유는 없다.

```
// 사용
<div id="app">
  <component-a></component-a>
  <component-b></component-b>
  <component-c></component-c>
</div>
​
// 등록
Vue.component('컴포넌트이름', 컴포넌트 내용);
Vue.component('component-a', { /* ... */ })
Vue.component('component-b', { /* ... */ })
Vue.component('component-c', { /* ... */ })

new Vue({ el: '#app' })
```

이렇게 **전역등록**한 컴포넌트는 어떤 루트 Vue인스턴스 에서도 사용할 수 있다.

#### 지역등록

전역등록은 단점이 있다. 사용하지 않는 컴포넌트도 최종 빌드에 포함되는 것이다. 불필요하게 코드 양이 커진다.

이 경우에 컴포넌트를 일반 자바스크립트 객체로 정의할 수 있다.  
`const ComponentA = { /* ... */ }`

사용할때는 components 옵션을 통해 쓸 수 있다.

```
new Vue({
  el: '#app',
  components: {
    'component-a': ComponentA,
    'component-b': ComponentB
  }
})
```

components객체의 각 속성에서 키가 엘리먼트의 이름이 되고 value에 컴포넌트 객체를 지정하면 된다.

지역 등록된 컴포넌트는 당연히 하위 컴포넌트에서는 사용이 불가능하다.

## 컴포넌트 통신

컴포넌트마다 관계가 생성되며 인스턴스의 `data`는 `root` 컴포넌트에서 관리하는  
data 를 **내리고, 올리고** 해야한다.

**props** :  
상위 컴포넌트의 정보를 하위 컴포넌트로 전달하기 위한 특성이다.  
하위 컴포넌트는props 옵션을 사용하여 수신 할 것으로 기대되는 props를 명시적으로 선언해야한다.

> HTML 태그안에는 케밥케이스  
> javascript props() 에서는 카멜케이스로 작성해야한다.

**문법**  
`v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"`

**$.emit()** : 하위 컴포턴트에서 상위 컴포넌트로 보내는 것이다.  
! 주의 : camel 표기법 사용하면 안된다. kebab 표기법 사용해야한다.

**문법**  
`v-on:하위컴포넌트에서 발생한 event 이름="상위 컴포넌트의 method 이름"`

**같은 레벨에서 컴포넌트 통신방법**  
Root 컴포넌트로 전달했다가 내려줘야한다.  
**emit** 과 **props()** 동시 사용

> ### 참조
> 
> -   [Vue 컴포넌트](https://velog.io/@kwonh/Vue-Vue%EC%8B%9C%EC%9E%912-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-webpack)
> -   [캡틴판교-Vue.js 입문서(인프런 강좌)](https://joshua1988.github.io/web-development/vuejs/vuejs-tutorial-for-beginner/)
> -   [computed VS watch](https://beomy.tistory.com/49)
