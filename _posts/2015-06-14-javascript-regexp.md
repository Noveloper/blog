---
layout: post
title:  JavasScript - RegExp
categories: javascript
---

프론트 단 작업을 하다보면 특정한 패턴의 입력만 허용하도록 하는 validation 로직을 작성해야 할 때가 있다. JavaScript 에서 정규식 표현을 이용하는 방법을 알아보고자 한다. <br><br>

<h2>RegExp</h2>
JavaScript 내장객체로 RegExp 객체가 있으며 JavaScript 에서 정규표현식을 사용하는 방법은 아래와 같이 두가지가 있다.

```javacript
var pattern1 = /qwer/i; // Object initializer
var pattern2 = new RegExp("qwer", "i"); // User RegExp Constructor 
```

자주 사용하는 Expression Flag 는 다음과 같이 3가지가 있다.

```java
g(global) - 문자열 내의 모든 문자열을 검색
i(ignore case) - 대소문자 구분을 하지 않음
m(multi line) - 문자열이 개행되어도 검색
```

정규식 표현방법은 엄청나게 다양하기 때문에 어느정도 외우는것은 학습이나 경험으로 커버한다 치고 필요할 때 표현식 테이블을 참고 하는것이 좋을 것 같다. <br>

- [정규표현식 사용법 표](http://www.nextree.co.kr/p4327/)



<h2>Reference</h2>

- [Javascript RegExp - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)
- [JavaScript RegExp Reference - w3schools.com](http://www.w3schools.com/jsref/jsref_obj_regexp.asp)
- [정규표현식 사용법 표](http://www.nextree.co.kr/p4327/)
