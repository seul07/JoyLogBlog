# 자바스크립트 스크롤 맨위/맨아래 로 올리기/내리기


## 전역객체 메서드 활용

```
window.scrollTo(x 좌표 , y 좌표)
```

-   x 좌표 : 문서 왼쪽 상단부터 가로축
-   y 좌표 : 문서 왼쪽 상단부터 세로축

## 문서 맨 위로 이동

```
window.scrollTo(0 , 0)
```

## 문서 맨 아래로 이동

```
window.scrollTo(0, document.body.scrollHeight)
```
