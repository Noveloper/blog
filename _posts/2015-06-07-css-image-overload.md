---
layout: post
title:  css - Image 겹치기
categories: css
---

이번에 프론트단을 개발하던 것이 월(Month) 정보가 가로로 배치되어있고 월별로 막대 그래프같은 아웃풋을 보여줘야 하던 것이라 table과 img태그를 이용해서 작업을 했었다. 서버단에서 넘어온 월별로의 데이터를 JSTL forEach 구문을 이용해서 그려주게 작업을 했는데 서버단에서 해당 월당 2개 이상의 데이터가 존재하는 케이스가 있어서 프론트 단에서는 특정 월에 막대가 한개만 있어야 하는데 여러개가 그려지고 있었다. 이것은 본디 해당 데이터를 Database에 입력하기전에 전달받은 Row 데이터의 문제가 있었고 이를 해결하기 위해 서버단에서도 검증해야하지만 프론트단에서도 중복된 데이터에 한해서 이미지를 겹치게 그리는 방법으로 해결하기로 생각했다. <br>

<h2>Solution</h2>
이미지를 겹치기 위해서 Style 프로퍼티의 Position을 이해해야 한다. <br>
position의 default 값은 static이며 이는 해당 document에 그려지는 element 순서대로 위치하게 한다. <br>
내가 사용할것은 relative로서 기본 위치에서 해당 element를 이동시켜준다. ([사용예](http://www.w3schools.com/cssref/tryit.asp?filename=trycss_position_relative)) <br>



<h2>Reference</h2>

- [CSS - Position ](http://www.w3schools.com/cssref/pr_class_position.asp)
- [Div - 영역겹치기](http://howways.blogspot.kr/2014/01/HTML-DIV-Layer-Position-Absolute-Relative-Z-index-Visibility.html)
