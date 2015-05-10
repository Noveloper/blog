---
layout: post
title:  Spring - Servlet Filter 와 @ModelAttribute
categories: Spring
---


이번에 내가 담당하는 사이트의 내부 보안검수를 받았는데 특정 URL에서 크로스 사이트 스크립팅(이하 XSS) 공격 위험성이 있다는 진단을 받았다. 이 프로젝트는 Spring 기반으로 작성된 프로젝트로서 XSS 방어용 Servlet Filter 를 등록해놨기 때문에 예상치 못한 진단에 문제가 되는 해당 URL에 Mapping 되는 Controller 메서드들을 살펴보았는데 하나같이 전부 @ModelAttribute를 사용하는 곳이었다.
<br>
<h2>Why?</h2>
말 그대로 왜? 라는 의문을 가진채 일단 내가 직접 테스트 해보았더니 역시나 스크립트가 변환이 되지 않았다. 
그래서 해당 메서드에 HttpServletRequest 파라미터를 받아서 값을 출력해보았다.

```java
@RequestMapping(value = "/test/xss", method = "GET")
public testXSS(@ModelAttribute Person person, HttpServletRequest request) {
  // person print
  // request print
}
```

결과가 <b>기이</b>하다. <br>
request를 그대로 출력하면 변환이 되었고, Model로 받은 객체를 출력하면 변환이 안되었다.

<br>
<h2>Thinking</h2>
여기서 생각해 볼 수 있는건,

- Filter가 Request 값을 변환하기전에 Model이 Request 먼저 참조해서 값을 설정한다. (타이밍의 문제)
- Filter가 변환한 Request와 Model이 참조하는 Request가 다른 객체이다. (자원 비공유의 문제)

<br>
<h2>Problem of Timing</h2>
다음은 Spring 에서 Request의 Lifecycle 이다.

<img src="/blog/image/0503/0503_1.jpg">
