# [Vue.js] Hot Reload 동작 안할때

예전에 만들어 놨던 Vue.js + SpringBoot 프로젝트를 새로 띄웠는데  
Vue 의 장점인 hot reload 가 갑자기 동작을 하지 않았다.  
Vue 의 코드를 바꾸면 항상 rebuild 후 스프링을 재시작하는 것이 너무 불편해서  
급하게 구글에 검색해서 간단한 해결책을 찾았다.

# package.json 에 --watch 추가

build --watch 를 통해 실시간으로 재빌드 하여 변화를 감지하도록 추가 하였다.

![image](https://user-images.githubusercontent.com/75015063/197155466-15780637-578b-4df3-b164-16e0f0954743.png)

이제 예전처럼 Vue의 내용을 변경하면 바로 반영이 되었다.
