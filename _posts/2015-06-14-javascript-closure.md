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
클로저는 사용 후에 소멸되는 지역변수를 붙잡아 둔다. <br>

만약, 우리가 어떠한 액션에 반응하여 특정 카운팅을 증가시켜야 할 때 보통 생각하는 방법은 전역 변수를 이용하는 방법이다.

```javascript
var actionCnt = 0;

function increment() {
  ++actionCnt;
}

increment();
increment();
...
increment();
```

이 방법은 사실 별 문제가 없어 보이고 가독성도 크게 나쁘지 않다. 일반적인 케이스에서는 말이다. 하지만 Javascript 코드가 길어지고 다른 Action에 대한 카운팅 변수들이 필요할 때 전역변수들이 무분별하게 많아져 코드는 더러워지고 가독성도 나빠지게 된다. 그리고 전역 변수의 생명 주기(Life Cycle)는 우리의 어플리케이션 (Window or Web Page) 가 살아있는 동안 영원히 살아있기 때문에 지역 변수에 비해 메모리 활용면에서 확실히 떨어진다. 



<h2>Reference</h2>

- [JavaScript Closures - w3schools.com](http://www.w3schools.com/js/js_function_closures.asp)
- [클로져(Closures) - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Closures)




