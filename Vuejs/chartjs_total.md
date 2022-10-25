# Chart.js 누적 막대 그래프 총합 표시하기 (Stack Bar, Total) 

Chart.js 플러그인 기본 옵션으로는 
누적 막대그래프의 total 값을 나타내지 않는다.
이는 option 의 tooltips 로 간단하게 구현 가능하다.

```
tooltips: {
  mode: "label",
  callbacks: {
    footer: function (data) {
      var total = 0;
      for (var i = 0; i < data.length; i++) {
        total += data[i].yLabel;    // 세로막대는 yLabel , 가로막대는 xLabel 
      }
      return "Total: " + total;
    },
  },
},
```

option 들을 정의할때 이 코드만 추가하면 된다.

![image](https://user-images.githubusercontent.com/75015063/197731216-182c7bfe-56dd-4cd5-9be2-b01e5f8d52ff.png)

막대 개별 값과 총 합을 확인 할 수 있다.
