---
layout: post
title:  "VisualVM 이란?"
categories: Java
---

<h3>VisualVM 이란?</h3>
먼저 VisualVM이 무엇인지에 대해 알아보겠다. [VisualVM](http://visualvm.java.net/) 공식 사이트에서 VisualVM의 소개는 다음과 같다.
- VisualVM은 여러 커맨드라인 JDK Tool과 경량의 프로파일링 기능을 통합하는 GUI Tool 이다. 
- VisualVM은 애플리케이션의 생산과 개발 시간 사용 모두를 위해 설계된 도구로서 JAVA SE 플랫폼의 성능 분석과 모니터링을 통해 기능을 더욱 향상시킨다. 


<h3>기능</h3>
VisualVM은 JDK 7이상의 환경에서 돌아가지만, 모니터링 대상이 되는 어플리케이션의 기반 JDK 버전은 1.4 이상 모두 지원하고있다. VisualVM은 모니터링 되는 어플리케이션에 아주 경미한 오버헤드를 부과하기 위해 자동적으로 데이터를 수집할 수 있고 빠르고 가볍게 이용이 가능한 jvmstat, JMX, SA, Attach API 등의 기능을 활용한다.

VisualVM이 제공하는 기능에 대해서 알아보자.

- Display local and remote Java applications, VisualVM은 실행중인 Java 어플리케이션을 로컬 및 원격에서 자동으로 감지하고 나열한다.
- Display application configuration and runtime environment, 각 어플리케이션에 대해 VisualVM은 다음과 같은 기본 런타임 정보를 보여준다. PID, Main class, JVM Home, JDK Home 등.
- Monitor application performance and memory consumption, 어플리케이션의 CPU 사용량, GC 활동량, Heap 영역 사용량, 실행중인 쓰레드와 로딩된 클래스의 개수 등을 알아볼 수 있다.
- Monitor application threads, 자바 프로세스에서 실행중인 모든 프로세스가 타임라인과 표로 표시된다. 쓰래드의 활동을 추적하고 사용하지 않는 비정상적인 패턴의 쓰래드를 찾아낼 수 있다. 
- Profile application performance or analyze memory allocation
- Take and display thread dumps, 마우스 클릭만으로 쓰래드 덤프를 캡쳐할 수 있다. 어플리케이션에서 일어나고 있는 상황에 대해서 사용자는 일일히 커맨드라인을 이용할 필요가 없다. 
- Take and browse heap dumps, 어플리케이션에서 메모리 내용이나 메모리 누수 현상을 찾아내야 할 때, 내장도구인 HeapWalker 를 이용하면 손쉽게 찾을 수 있다. 
- Analyze core dumps
- Analyze applications offline, 어플리케이션 구성 및 런타임 환경을 저장 할 수 있다.


<h3>확장성</h3>
만약 우리가 우리만의 특별한 기능이 필요하다면 VisualVM을 확장해서 고유의 모니터링 도구를 만드는것도 가능하다. 관련해서 많은 사용 정보와 Sample Code가 있다. [Developer Documentation](https://visualvm.java.net/api-quickstart.html)


<h3>정리</h3>
아직은 사용해 보지 않아서 정확히 위에서 정리한 기능들을 어떻게 보여줄지는 잘모르겠다. 일단 VisualVM에 대해서 정리해보면 개발자는 VisualVM만 잘 활용한다면 자신이 만든 어플리케이션의 성능 측정을 통해서 성능 향상을 꾀할 수 있다. VisualVM을 사용하기에 앞서 간략하게 VisualVM이 무엇이고 내포된 기능이 어떤것이 있는지 정리해 보았다. 


<h3>Reference</h3>
[VisualVM](http://visualvm.java.net/)
