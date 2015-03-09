---
layout: post
title:  "VisualVM 설치"
categories: Java
---


VisualVM을 사용하기 위해 설치하는 방법을 알아보겠다. 설치하는 방법은 VisualVM을 직접 설치하여 사용하는 것과 Eclipse 와 같은 IDE에 VisualVM 플러그인을 설치하는 방법으로 나뉜다. 


<h3>직접 설치</h3>
먼저 아래의 링크를 클릭하여 다운받는 곳으로 이동 후 최상단에 있는 최신버전을 다운받는다. <br/>
(현재 글을 작성하고 있는 PC의 OS가 Windows 이므로 그에 맞춰서 설명하도록 하겠다) <br/>
[VisualVM 다운로드 받는 곳](http://visualvm.java.net/download.html) 

<img src="/blog/image/visualvm_1.png" alt="visualvm 설치 - 1">

다운받고 압축을 해제한 다음 bin 폴더에 있는 VisualVM 을 실행하면 현재 자신의 PC에서 실행중인 어플리케이션 중에 JDK 기반으로 작성된 어플리케이션의 목록을 확인할 수 있다. 

<img src="/blog/image/visualvm_2.png" alt="visualvm 설치 - 2">

Local 환경 뿐 아니라 Remote를 클릭하여 원격에서 실행중인 Java 어플리케이션의 정보도 확인할 수 있다. 원격에서 웹서버를 모니터링 할 때 사용하면 좋을듯하다.

<img src="/blog/image/visualvm_3.png" alt="visualvm 설치 - 3">

<h3>Reference</h3>
- [VisualVM 다운로드](http://visualvm.java.net/download.html)
- [VisualVM 설치 및 Eclipse에 VisualVM 플러그인 설치 튜토리얼](http://linuxism.tistory.com/1838)
