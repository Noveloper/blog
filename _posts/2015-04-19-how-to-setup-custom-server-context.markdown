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

프로젝트를 진행하다보면 운영환경과 개발환경, 로컬환경이 다를 수 있기 때문에 이 Context 태그로 컨트롤하여 각각에 환경에 맞게 작업을 진행하였다.


<h2>What is problem?</h2>
이번에 Eclipse에서 InteliJ로 개발툴을 변경하였는데 단축키 같은 자잘한 이슈야 차차 익혀나가면 되는 문제고 처음 맞닥뜨린 문제가 이 Context 태그를 컨트롤 하는 일이었다. Eclipse는 tomcat서버를 생성하면 base가 되는 Tomcat Base 디렉토리를 복사해서 만들어 내부적으로 관리하기 때문에 Eclipse상에 Server 디렉토리에 있는 server.xml 을 사용자 마음대로 커스터마이징할 수 있었다. 근데 InteliJ는 Base 디렉토리 복사하지 않고 그 자체를 바라보기 때문에 Context 태그를 추가하기 위해서는 Base 파일을 수정해야 했다.

내가 작업하고 있는 프로젝트는 같은 프로젝트라도 로컬에서 A작업을 할 때와 B작업을 할 때 이용하는 Context의 내용이 달랐다. 만약 A작업에 해당되는 내용이 B작업에 영향을 미치지 않는다면 문제가 없겠지만 추후 문제가 생길 가능성이 있기 때문에 이 작업을 분기하기 위해서는 Tomcat Base 디렉토리를 복사해서 A작업 디렉토리, B작업 디렉토리를 만들어야 햇다.

하지만 이 방법은 Eclipse가 가진 장점에 비해 너무 불편한 방법이라고 생각하여 다른 방법을 찾아보았다.


<h2>Solution</h2>
지금부터 설명하는 방법은 굳이 Tomcat Base 디렉토리를 복사하여 다른 Tomcat 디렉터리를 만들지 않아도 되는 방법이다. 

InteliJ 메뉴에서 File > Project Structure 를 들어간다.

<img src="/blog/image/0419/0419_1.png" alt="Context Tag Setup - 1">
<img src="/blog/image/0419/0419_2.png" alt="Context Tag Setup - 2">
<img src="/blog/image/0419/0419_3.png" alt="Context Tag Setup - 3">
