---
layout: post
title:  Spring - View Controller
categories: Spring
---

Spring 을 이용해서 Web을 개발할 때 개발자가 가장 친숙하게 보는 문장은 아마 다음 한줄일 것이다.

```java
@RequestMapping(value = "url", method = "?")
```

이 문장에 익숙해진 개발자는 어느순간 다음 공식을 통해서 작업을 할 것이다.

```java
1 RequestMapping : 1 page
```

Spring에 좀 더 익숙한 개발자는 다음과 같은 문장을 통해서 공식을 변경할 것이다.

```java
@RequestMapping(value = {"url_1", "url_2", ... "url_n"}, method = ""}
@RequestMapping(value = url/{param}/, method = ""}
```

```java
1 RequestMapping : n page
```

