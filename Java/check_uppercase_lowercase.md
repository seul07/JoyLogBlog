# [Java] 대소문자 확인 및 대소문자 변환

# 대소문자 확인

Character 클래스에서 제공하는 메서드를 사용 하면 된다.

> isUpperCase()  
> 전달된 값이 대문자인 경우 true 그렇지 않으면 false 반환  
> isLowerCase()  
> 전달된 값이 소문자인 경우 true 그렇지 않으면 false 반환

#### 예시

```
 char value = 'C';

if(Character.isUpperCase(value)) {
    System.out.println("대문자입니다.");
}

if(Character.isLowerCase(value)) {
    System.out.println("소문자입니다.");
}
```

#### 실행

```
대문자입니다.
```

# 대소문자 변환

String 클래스에서 제공하는 메서드를 사용하면 된다.

> toUpperCase()  
> 문자열을 모두 대문자로 변환해준다.  
> toLowerCase()  
> 문자열을 모두 소문자로 변환해준다.

#### 예시

```
String value = "A";

String result = value.toLowerCase();

System.out.println(result);
```

#### 실행

```
a
```
