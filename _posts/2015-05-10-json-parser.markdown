---
layout: post
title:  Java - JsonParser
categories: Spring
---

최근 내가 담당하는 시스템내에 주소 검색 API를 기존 것에서 새로운것으로 변경해야 될 니즈가 생겼는데 기존 API는 XML로 결과값을 반환하는 반면 새로운 API는 JSON 문자열로 반환하는 이슈가 있었다. 기존에 있던 코드 역시 [org.w3c.dom](http://docs.oracle.com/javase/7/docs/api/org/w3c/dom/package-summary.html) 패키지내에 클래스를 이용하여 XML을 Parsing 하는 예제 였기에 변경하려면 받아온 JSON 문자열을 알맞게 다시 포장해줘야 했기 때문에 조금 귀찮았다. 


<h2>Reference</h2>
- [JsonParser Documentation](http://docs.oracle.com/javaee/7/api/javax/json/stream/JsonParser.html)
