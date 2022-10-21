# [Java] 사용자 Web/App/Mobile 접속 구분하기

# User Agent
​
사용자가 어떤 디바이스로 접속했는지에 대한 정보가 필요할때 Request Header 의 User Agent 로 확인 할 수 있다.
​
> #### User Agent 가 가지고 있는 정보 예시
> 
> Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36
​
```
​
 public void getUserDevice(HttpServletRequest request) {
​
        String userAgent = request.getHeader("User-Agent");
        // 모바일 기종 체크
        boolean isMobile = userAgent.matches(".*(iPhone|iPod|iPad|BlackBerry|Android|Windows CE|LG|MOT|SAMSUNG|SonyEricsson).*");
        // APP_ios, APP_Andriod 등 구분하고자 하는 앱의 특정 변수
        if(userAgent.indexOf("APP_ios") > -1 || userAgent.indexOf("APP_Andriod") >-1){
            System.out.println("App 으로 접속");
        }else if(isMobile){
            System.out.println("Mobile 으로 접속");
        }else {
            System.out.println("Web 으로 접속");
        }
}
```
