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
request를 그대로 출력하면 변환이 되어있었고, Model로 받은 객체를 출력하면 변환이 안되어있었다.

<br>
<h2>Thinking</h2>
여기서 생각해 볼 수 있는건,

- Filter가 Request 값을 변환하기전에 Model이 Request 먼저 참조해서 값을 설정한다. (타이밍의 문제)
- Filter가 변환한 Request와 Model이 참조하는 Request가 다른 객체이다. (자원 비공유의 문제)
- Filter가 잘못됐다.

일단, 변환이 되고 있긴 하므로 Filter 가 잘못된 케이스의 우선순위를 가장 아래로 내려서 생각했다. <br>
(그리고 가까운 미래 필자는 후회하며 이불킥을 하게된다.)

<br>
<h2>Problem of Timing</h2>
다음은 Spring 에서 Request의 Lifecycle 이다.

<img src="/blog/image/0503/0503_1.jpg" />

[ 그림1 - Spring MVC Request Lifecycle ]

보면 사용자에게서 온 Request가 제일 먼저 Filter 를 거치기 때문에 타이밍의 문제는 아닌거 같다.

<br>
<h2>Problem of Not sharing Request</h2>
사실 이미 컨트롤러단에서 HttpServletRequest 로 받았을때는 아무 문제가 없었으므로 이 가설도 무의미하다. <br>
그렇다면 @ModelAttribute가 Request에서 값을 어떻게 빼가는 걸까?

<br>
<h2>Resolve</h2>
구글 검색을 통해 구글 그룹스에 유사한 내용이 있어서 읽어보았는데 @ModelAttribute 는 request의 getParameterValues 를 통해 값을 언어온다고 한다. 관련한 Spring 문서는 찾지 못했지만 이 근거를 가지고 구현된 Filter 소스를 다시 보았다. <br>
<br>
애초에 Filter가 Request의 값을 변환한다는 표현부터가 잘못됐던건 아닐까? <br>
Filter는 읽은 값을 변경해서 전달하는(필터링) 역할이지 기존값을 변경하는 역할이 아니다. <br>
<br>
다음은 문제가 된 XSS Filter 소스의 일부이다. 

```java
@Override
public void doFilter(ServletRequest req, ServletResponse res, FilterChain chain) throws IOException, ServletException {
  HttpServletRequest request = (HttpServletRequest)req;
  chain.doFilter(doXssFiltering(req), res);
}

@SuppressWarnings("unchecked")
private HttpServletRequest doXssFiltering(HttpServletRequest req) {
  XssSaxFilter filter = XssSaxFilter.getInstance("xss.xml", true);
	Map<String, String[]> params = req.getParameterMap();
	
	for (String key : params.keySet()) {
		String[] values = params.get(key);
		for (int i = 0; i < values.length; i++) {
			values[i] = filter.doFilter(values[i]).replace("\"", "&#34;");
		}
	}
	
	return req;
}
```

Filter 에서 Request의 getParameterMap 값만을 얻어와서 String을 변경하고 있다. 일단 getParameterMap 만을 사용하였기 때문에 보장도 안되거니와 Filter에서 직접 String 을 replace 하는건 좋지못한 방법같다. <br>
<br>
다음과 같은 Wrapper 클래스를 만들어서 request에서 값을 읽어 들일때 변환하도록 하였다.

```java
// Wrapper Class
class MyHttpServletRequestWrapper {
@Override
public String getParameter() {/* 변환후 리턴 */}
@Override
public String[] getParameterValues() {/* 변환후 리턴 */}
@Override
public Map<String, String[]> getParameterMap() {/* 변환후 리턴 */}
}
```

```java
// Filter 
...
chain.doFilter(new MyHttpServletRequestWrapper((HttpServletRequesst)req), res);
...
```

<br>
<h2>Conclusion</h2>


<br>
<h2>Reference</h2>

- [servlet filter 사용시의 @ModelAttribute - Google Groups](https://groups.google.com/forum/#!topic/ksug/guylCNnlnqY)
- [그림1 - Spring MVC Request Lifecycle](http://changpd.blogspot.kr/2013/03/spring.html)
