# Vue.js(1) 프로젝트 생성 및 프로젝트 구성


# MVVM 이란?
​
-   비즈니스 로직과 프레젠테이션 로직을 UI로부터 분리하는 것이다.
-   역사 : 데이터 바인딩을 활용한 환경에서 데이터와 프레젠테이션 로직을 분리하기 위해서 만들어진 디자인 패턴이다.
​
![](https://images.velog.io/images/yeccye/post/8b898e42-2837-44ca-978e-6225b348b392/image.png)
​
### 1\. 모델 Model
​
-   비즈니스 로직과 데이터를 다룬다.2. 뷰 View
-   UI와 UI 로직을 다룬다.3. 뷰 모델 View Model
    -   View 를 표현하기위해 만든, View를 위한 Model이다.  
        View를 나타내주기 위한 Model 이자 View 를 나타내기 위한 데이터 처리를 하는 부분이다.
​
> ### 동작
> 
> 1.  사용자의 Action들은 View를 통해 들어오게 됨
> 2.  View에 Action이 들어오면, Command 패턴으로 View Model에 Action을 전달
> 3.  View Model은 Model에게 데이터를 요청
> 4.  Model은 View Model에게 요청받은 데이터를 응답
> 5.  View Model은 응답 받은 데이터를 가공하여 저장
> 6.  View는 View Model과 Data Binding하여 화면을 나타냄
​
---
​
# Vue.js 란?
​
![](https://images.velog.io/images/yeccye/post/0faafdaf-e208-497c-9747-dac1d59b748d/image.png)
​
-   웹 페이지 화면을 개발하기 위한 frontend framework
-   MVVM 패턴의 ViewModel 레이어에 해당하는 화면단 라이브러리이다.
-   양방향 데이터 바인딩을 제공한다.
-   컴포넌트 기반 프레임워크이다.
-   리액트와 앵귤러의 장점을 가졌다.
    -   앵귤러의 양방향 데이터 바인딩과 리액트의 단방향 데이터 흐름의 장점을 결합했다.특징 : Reactivity데이터의 변화에 따라 화면이 자동으로 변경되는 것을 말한다.  
        (코드 수정 후 새로고침을 통해 다시 로딩을 할 필요가 없다.)
​
---
​
# Vue.js 프로젝트 생성
​
기본적으로 npm(Node.js 설치) 과 git이 설치 되어있어야 실행 가능하다.
​
### 1\. Vue CLI 설치
​
vue-cli 는 기본 Vue 개발환경을 설정해주는 도구이다.
​
> CLI ?  
> 명령 줄 인터페이스(CLI, Command line interface) 또는 명령어 인터페이스는 텍스트 터미널을 통해 사용자와 컴퓨터가 상호 작용하는 방식을 뜻한다.
​
> npm install -g @vue/cli
​
터미널에서 위와같이 입력하여 설치한다.
​
### 2\. vue 프로젝트 생성
​
원하는 경로에서
​
> vue create 프로젝트명
​
을 입력하여 프로젝트를 생성한다.
​
![](https://images.velog.io/images/yeccye/post/ee276705-a3d4-4d08-8756-0a6d9f2d04ae/image.png)
​
Default 옵션을 선택한다.
​
### 3\. vue 서버 시작
​
> npm run serve
​
를 통해 서버를 시작한다.
​
---
​
# Vue.js 프로젝트 구조
​
![](https://images.velog.io/images/yeccye/post/274f3c04-e3ac-42cc-be3b-7d6ee3e02f82/image.png)
​
#### 1\. node\_modules
​
-   npm 으로 설치되는 라이브러리들이 모여있는 디렉토리2. public > index.html
-   npm run serve 를 통해 실제 실행되는 파일
-   프로젝트 배포시 필요한 파일
-   실제 build 된 파일들은 src 아래에 main.js 등 여러 파일들을 종합해서  
    최소한의 파일로 묶어서 주입3. src
-   실제 대부분의 코딩이 이루어지는 디렉토리
-   애플리테이션이 동작하는데 필요하는 로직들이 위치
    -   api/ : api 함수
    -   assets/ : 이미지, 기타 멀티미디어 등 파일들을 저장하는 장소
    -   compoments/ : vue 소스들을 저장하는 장소
    -   routes/ : vue-router 설정을 저장하는 장소
    -   store/ : vuex 를 이용한 상태관리
    -   utils/ : 필터 등의 유틸리티 함수
    -   views/ : 라우터 페이지
    -   App.vue : 페이지가 시작되는 최초의 컴포넌트
    -   main.js : 진입점. 가장먼저 시작되는 javascript 파일로 vue instance 생성하는 역할
​
#### 4\. .gitignore
​
-   git에서 특정파일 혹은 디렉토리를 관리 대상에서 제외할 때 사용하는 파일5. package.json
-   dependency 설정하는 파일로, maven 에 비유하면 repository 역할6. babel.config.js
-   js의 버전을 변환해주는 babel 의 설정파일7. jsconfig.json
-   import 경로를 ../../ 와 같은 상대경로가 아닌 @ 로 절대경로로 표기하기 위한 설정8. vue.config.js
-   vue cli 환경설정과 webpack 설정등을 변경할 수 있다.
-   주로 외부 참조파일의 경로를 변경할때 쓰인다. publicPath 변경
-   프록시 설정 가
​
> #### **참조**   
> [MVVM 패턴이란?](https://velog.io/@k7120792/Model-View-ViewModel-Pattern)  
> [Vue.js 란 무엇인가?](https://velog.io/@leyuri/Vue.js-%EC%86%8C%EA%B0%9C)  
> [vue.js 설치 및 세팅](https://velog.io/@feversore/vue.js-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EC%84%B8%ED%8C%85)  
> [vue-cli로 개발환경](https://ayoteralab.tistory.com/83)  
> [Vue.js 프로젝트 구조](https://k39335.tistory.com/64)  
> [Vue.js-03 프로젝트구조](https://ayoteralab.tistory.com/entry/Vuejs-03-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EA%B5%AC%EC%A1%B0)  
> [vue-proxy 사용하기](https://velog.io/@skyepodium/vue-proxy-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)  
> [★이미 진행중인 프로젝트에 vue 설치하기](https://trend21c.tistory.com/2125)  
> [★Vue 개발환경 만들기](https://velog.io/@kyusung/Vue-app-sfc-without-vue-cli)
