---
layout: post
title:  Spring - View Controller
categories: Spring
---

Spring 을 이용해서 Web을 개발할 때 개발자가 가장 친숙하게 보는 문장은 아마 다음 한줄일 것이다.

```java
@RequestMapping(value = "url", method = "?")
```

<br>
이 문장에 익숙해진 개발자는 어느순간 자신도 모르게 다음 공식을 통해서 작업을 할 것이다.

```java
1 RequestMapping : 1 page
```
<br>
Spring에 좀 더 익숙한 개발자는 다음과 같은 문장을 통해서 공식을 변경할 것이다.

```java
@RequestMapping(value = {"url_1", "url_2", ... "url_n"}, method = ""}
@RequestMapping(value = url/{param}/, method = ""}
```

```java
1 RequestMapping : n page
```

<br>
그럼, 다음 공식은 가능할까?

```java
0 RequestMapping : 1 page
```

<br>
<h2>View Controller</h2>
사실 위와 같은 의문이 왜 필요한지 잘 공감이 안될수도 있지만 예를들어 어떠한 경우에도 변하지 않는 정적인 페이지가 있다고 치자. 이 페이지는 이 블로그 우측 상단에 위치한 [About this](http://noveloper.github.io/blog/about/)처럼 주인장이 저 내용을 변경하지 않는한 사용자의 어떤 액션으로도 저 내용은 변하지 않는다.

저 내용을 뿌려주기 위해서 개발자는 굳이 다음과 같은 작업을 해야한다.

```java
@RequestMapping(value = /blog/about, method = "GET"}
public String goAbout() {
  return "about";
}
```

<br>
큰 소요는 아니지만 귀찮은 작업인건 분명하다. 

지금부터 소개할 View Controller 는 Request Mapping 에서 Handler(Controller)를 찾지 못한 경우, Request Url과 같은 경로에 있는 View 를 찾아 맵핑시켜주는 방법이다.

```java
ex) /blog/about => /WEB-INF/blog/about.jsp
```

<br>
Spring bean 설정 파일에 다음을 추가한다.

```xml
<mvc:view-controller path="/*"/>
```

<br>
다음은 View Resolver 를 설정해준다. 만약 JSP Resolver를 설정해야 한다면

```xml
<!-- JSP View Resolver -->
<bean id="jspViewResolver" class="org.springframework.web.servlet.view.UrlBasedViewResolver">
	<property name="viewClass" value="org.springframework.web.servlet.view.JstlView" />
	<property name="prefix" value="/WEB-INF/blog/" />
	<property name="suffix" value=".jsp" />
</bean>
```

<br>
보다시피 prefix 는 view 페이지 앞에 있는 경로고 suffix는 뒤에 있는 경로인데 이 예제에선 .jsp 라는 확장자가 지정되어있다.
이 설정은 위에서 예로 들었던 /blog/about URL을 다음과 같은 View로 연결해준다.

```java
/blog/about => /WEB-INF/blog/about.jsp
```

<br>
<h2>Conclusion</h2>

- View Controller 를 활용하면 페이지를 추가하거나 변경할 때 해당 페이지와 Spring 설정 파일만 변경해주면 되므로 Java 코드는 건드릴 필요가 없다는 장점이 있다. 


<br>
<h2>Reference</h2>

- [Web MVC framework - Spring](http://docs.spring.io/spring/docs/current/spring-framework-reference/html/mvc.html)
- [Spring MVC 3 view controller example](http://www.techzoo.org/spring-framework/spring-mvc-3-view-controller-example.html)
