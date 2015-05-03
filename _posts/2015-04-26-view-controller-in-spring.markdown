---
layout: post
title:  Spring - View Controller
categories: Spring
---

Spring 을 이용해서 Web을 개발할 때 개발자가 가장 친숙하게 보는 문장은 아마 다음 한줄일 것이다.

```java
@RequestMapping(value = "url", method = "?")
```

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
