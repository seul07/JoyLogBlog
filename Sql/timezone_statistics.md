# [MySQL] 시간대별 방문 통계 구하기

# 방법 1

```
SELECT Hour(access_date) AS hh , count(access_date) AS cnt
FROM access_log
WHERE access_date BETWEEN '2022-01-01 00:00:00' AND date_format(now(),'%Y-%m-%d 23:59:59')
GROUP BY hh
ORDER BY hh ASC;
```

-   access\_date 에서 Hour() 로 시간값(0,1,2,3...) 만 가져온 뒤
-   그 값을 GROUP BY 를 통해 중복 제거와 함께 count 값을 구한다
-   BETWEEN AND 절로 구하고자 하는 기간을 지정한다

### 출력

![image](https://user-images.githubusercontent.com/75015063/197156750-4e17ba6f-1de6-4346-87bc-0412d75bfecf.png)

위와 같은 방법은 값이 있는 시간만 출력을 한다.

값의 유무와 상관없이 1~24 시간대별 방문 통계가 필요하다.

# 방법 2

우선 행번호나 시간 등 순차적으로 숫자를 출력해주는 테이블이 필요하다.

```
SELECT @N := @N +1 AS n
FROM access_log , (select @N:=0 from DUAL ) NN
LIMIT 24;
```

-   **SELECT @변수이름 := 대입값;**
-   변수 N 선언 및 0 으로 초기화 한 후
-   0부터 1씩 증가하여 최대 24까지 출력한다

#### 출력

![image](https://user-images.githubusercontent.com/75015063/197156777-1899ee1f-cba1-4916-969f-ab08cfb0a6cd.png)

\-1 로 초기화를 하면 0부터 23까지 출력되도록 할 수 있다. Hour 로 시간을 구할경우 24시는 0 시로 표시되기 때문에 -1 로 초기화 해야한다.

이제 이 테이블을 방문 통계 테이블과 조인하면 된다.

```
SELECT A.n AS h , ifnull(B.cnt,0) AS cnt
 FROM
 (SELECT @N := @N +1 AS n
    FROM access_log, (select @N:=-1 from DUAL ) NN
    LIMIT 24) AS A
LEFT JOIN 
    (SELECT HOUR(access_date) AS hh, COUNT(access_date) AS cnt 
    FROM access_log 
    WHERE access_date BETWEEN '2022-01-01 00:00:00' AND date_format(now(),'%Y-%m-%d 23:59:59')
    GROUP BY hh) AS B
    ON A.n = B.hh ;
```

-   값이 없는 컬럼은 ifnull 을통해 0 으로 처리해주었다

![image](https://user-images.githubusercontent.com/75015063/197156796-889318db-a169-43a6-aca3-649d91e7754e.png)

이제 0~23 시간 별로 접속 통계 값을 구할 수 있게 되었다.

> #### 참조
> 
> [\[MYSQL\] 쿼리문을 이용한 매시간대별 방문 통계 구하기](https://happyguy81.tistory.com/m/118)
