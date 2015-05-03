---
layout: post
title:  InteliJ - Server.xml 에 Context 태그 지정
categories: InteliJ
---

톰캣을 이용하여 서버를 구동할 때 우리가 원하는 디렉토리를 Document Root로 지정하기 위해서는 Server.xml 에 Host태그아래에 Context태그를 지정해야 한다.

```xml
<Host>
...
  <Context path="" docBase="C:\noveloper\test" reloadable="true />
...
</Host>
```
