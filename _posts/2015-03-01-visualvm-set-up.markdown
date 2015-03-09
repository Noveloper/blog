---
layout: post
title:  "VisualVM 설치 및 Eclipse 와의 연동"
categories: Java
---


VisualVM을 사용하기 위해 설치하는 방법을 알아보고 Eclipse와 같은 IDE와 어떻게 연동하는지도 알아본다.


<h3>직접 설치</h3>
먼저 아래의 링크를 클릭하여 다운받는 곳으로 이동 후 최상단에 있는 최신버전을 다운받는다. <br/>
(현재 글을 작성하고 있는 PC의 OS가 Windows 이므로 그에 맞춰서 설명하도록 하겠다) <br/>
[VisualVM 다운로드 받는 곳](http://visualvm.java.net/download.html) 

<img src="/blog/image/visualvm_1.png" alt="visualvm 설치 - 1">

다운받고 압축을 해제한 다음 bin 폴더에 있는 VisualVM 을 실행하면 현재 자신의 PC에서 실행중인 어플리케이션 중에 JDK 기반으로 작성된 어플리케이션의 목록을 확인할 수 있다. 

<img src="/blog/image/visualvm_2.png" alt="visualvm 설치 - 2">

Local 환경 뿐 아니라 Remote를 클릭하여 원격에서 실행중인 Java 어플리케이션의 정보도 확인할 수 있다. 원격에서 웹서버를 모니터링 할 때 사용하면 좋을듯하다.

<img src="/blog/image/visualvm_3.png" alt="visualvm 설치 - 3">

그 외에도 Overview 탭에서는 그 어플리케이션읙 기본정보(PID, Host, Main Class, Java version 등)을 확인할 수있고 Mornitor탭에서는 CPU 사용률, 로딩된 클래스의 개수, 쓰레드의 개수등을 살펴볼 수 있었다. <br/>
사용에 대한 얘기는 다음 포스트에서 작성할 생각이니 여기까지만 하겠다. 다음은 Eclipse 플러그인으로 설치하는 방법이다. 


<h3>Eclipse 연동</h3>

위에서 VisualVM 을 다운받았던 곳으로 다시 가보자.
[VisualVM 다운로드 받는 곳](http://visualvm.java.net/download.html) 

옆에 있는 IDE integration: Eclipse IDE 을 클릭해서 들어가 보면 Eclipse launcher for VisualVM 을 볼 수 있다. 다운받자.

<img src="/blog/image/visualvm_4.png" alt="visualvm 설치 - 4">

다운받은 파일을 압축을 풀고 Eclipse에서 Help > Install New Software 에서 location을 압축을 푼 폴더를 지정해서 설치하자.

<img src="/blog/image/visualvm_5.png" alt="visualvm 설치 - 5">

설치가 완료 됐다면 자신이 Eclipse 환경설정에서 <br/>
Run/Debug > Launching > VisualVM Configuration에서 VisualVM 실행파일의 위치를 잡아줘야 한다. 

<img src="/blog/image/visualvm_6.png" alt="visualvm 설치 - 6">

그 후 실행하려는 프로젝트를 실행할 때 <br/>
해당 프로젝트 > Run As > Run Cofigurations 에 들어가 

<img src="/blog/image/visualvm_7.png" alt="visualvm 설치 - 7">

이 부분을 클릭하여 해당 Launcher 를 VisualVM Launcher 로 변경해주면 끝이다.

사실, 설치된 VisualVM 을 실행해 놓으면 이런 번거로운 작업을 하지 않아도 알아서 VisualVM 목록에는 갱신되기 때문에 그냥 사용하면 되지만 Eclipse 에서 해당 프로젝트를 실행하였을때 모니터링 화면이 보이게 되면 좀 더 유기적인 작업으로 보여질 것 같아서 나름대로의 이점이 있는것 같다. 


<h3>정리</h3>
원래 목표인 VisualVM 플러그인 만들기에 앞서서 VisualVM 플러그인을 사용해 보기 위해 직접 설치하고 Eclispe 에 연동까지 해보았다. Eclipse 뿐 아니라 InteliJ 같은 다른 IDE에도 연동이 가능할거라 생각하고 이것에 관한 포스트는 추후에 다시 올리도록 하겠다. 


<h3>Reference</h3>
- [VisualVM 다운로드](http://visualvm.java.net/download.html)
- [VisualVM 설치 및 Eclipse에 VisualVM 플러그인 설치 튜토리얼](http://linuxism.tistory.com/1838)
