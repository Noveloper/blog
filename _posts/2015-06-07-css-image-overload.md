---
layout: post
title:  css - Image 겹치기
categories: css
---

이번에 프론트단을 개발하던 것이 월(Month) 정보가 가로로 배치되어있고 월별로 막대 그래프같은 아웃풋을 보여줘야 하던 것이라 table과 img태그를 이용해서 작업을 했었다. 서버단에서 넘어온 월별로의 데이터를 JSTL forEach 구문을 이용해서 그려주게 작업을 했는데 서버단에서 해당 월당 2개 이상의 데이터가 존재하는 케이스가 있어서 프론트 단에서는 특정 월에 막대가 한개만 있어야 하는데 여러개가 그려지고 있었다. 이것은 본디 해당 데이터를 Database에 입력하기전에 전달받은 Row 데이터의 문제가 있었고 이를 해결하기 위해 서버단에서도 검증해야하지만 프론트단에서도 중복된 데이터에 한해서 이미지를 겹치게 그리는 방법으로 해결하기로 생각했다. <br>

<h2>Solution</h2>
이미지를 겹치기 위해서 Style 프로퍼티의 Position을 이해해야 한다. <br>
position의 default 값은 static이며 이는 해당 document에 그려지는 element 순서대로 위치하게 한다. <br>
relative는 기본 위치에서 해당 element를 이동시켜준고 td 정렬 기준으로 div 전반부를 사용한다. <br>
absolute는 가장 가까운 곳에 위치한 조상 엘리먼트에 상대적으로 위치가 조정된다. <br>

내 코드의 구조가 td > div > img 로 되있었으므로 다음과 같이 작성하면 해당 td에 들어가는 이미지에 한해서 겹쳐지게 된다. 

```html
<td>
  <div style="position: relative;">
    <img style="position: absolute;"/>
  </div>
</td>
```

<br>
absolute 로 지정하면 td 정렬 기준으로 div 왼쪽 영역부터 채워지니 이점 고려해서 left, top, padding 프로퍼티 값을 부여해서 컨트롤 하면 원하는 위치로 img 태그를 놓을 수 있다.

<h2>Reference</h2>

- [CSS - Position ](http://www.w3schools.com/cssref/pr_class_position.asp)
- [Div - 영역겹치기](http://howways.blogspot.kr/2014/01/HTML-DIV-Layer-Position-Absolute-Relative-Z-index-Visibility.html)
