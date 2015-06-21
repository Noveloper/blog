---
layout: post
title:  JavasScript - RegExp
categories: javascript
---

프론트 단 작업을 하다보면 특정한 패턴의 입력만 허용하도록 하는 validation 로직을 작성해야 할 때가 있다. JavaScript 에서 정규식 표현을 이용하는 방법을 알아보고자 한다. <br><br>

<h2>RegExp</h2>
JavaScript 내장객체로 RegExp 객체가 있으며 JavaScript 에서 정규표현식을 사용하는 방법은 아래와 같이 두가지가 있다. 

```javascript
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

그리고 아래의 자체 함수와 같이 쓰인다.

```java
exec() - 해당 문자열이 표현식에 부합한다면 첫번째로 매칭된 문자열을 반환한다.
test() - 해당 문자열이 표현식에 부합하는지 여부를 반환. True or False
```

그 외 속성변수로 lastIndex, global, multiline, source 등이 있지만 검증 로직을 만들때는 그다지 사용 필요성이 없고, 검증 로직을 검증하는 로직을 만들때 필요한 속성들인 것 같다. <br><br>

<h2>Conclusion</h2>
정규표현식은 일반적으로 작성하면 엄청 길어졌을 로직을 아주 짧고 간략하게 작성 가능하고 정규표현식을 서로 아는 사람들에게 있어 오히려 긴 로직보다 가독성이 좋은 코드 작성법이기 때문에 개발자에게 있어서 선택이 아닌 필수적인 항목인 것 같다. <br><br>


<h2>Reference</h2>

- [Javascript RegExp - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)
- [JavaScript RegExp Reference - w3schools.com](http://www.w3schools.com/jsref/jsref_obj_regexp.asp)
- [정규표현식 사용법 표](http://www.nextree.co.kr/p4327/)
