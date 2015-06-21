---
layout: post
title:  Javascript - Closure
categories: javascript
---

이번에는 Javascript를 보다 깊게 이해하기 위해서 꼭 이해해야 한다는 클로져(Closure)에 대해서 정리해 보고자 한다. <br>

Javascript 에서의 '변수' 의 영역은 Global 과 local로 나뉜다. <br>

```javascript
var a; // Global variable

function func() {
  var b; // Local variable
}
```

일반적으로 함수 외부에 선언된 전역(Global) 변수를 함수 내부에서는 사용할 수 있고, 함수 내부에 선언된 지역(Local) 변수를 함수 외부에서는 사용할 수 없지만 이를 위반하고 사용 가능하게 하는 것이 클로저(Closure) 이다. <br>



<h2>Reference</h2>

- [JavaScript Closures - w3schools.com](http://www.w3schools.com/js/js_function_closures.asp)
- [클로져(Closures) - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Closures)




