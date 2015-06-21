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
