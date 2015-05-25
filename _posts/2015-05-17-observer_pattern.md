---
layout: post
title:  Observer Pattern
categories: Desginpattern
---

이번에 디자인패턴 스터디에서 Observer 패턴에 대하여 정리할 기회가 있어서 '나무키우기' 라는 내가 예전에 진행했던 Android 프로젝트에 Observer 패턴을 적용 했더라면 어떤식으로 코드가 바뀌었을지에 대해서 간략하게 정리해 보고자한다.

<h2>Project 개요</h2>
먼저 프로젝트에 대해 소개하자면 사용자가 처음 어플리케이션을 실행하면 화면에 어린 나무가 나타나고 화면에 있는 '물주기', '가지치기' 라는 버튼을 통해서 나무를 점차 키워가고 마지막에 자신이 얼마나 잘 키웠는가에 나무의 가치가 판단된다.
<br>
사용자의 액션에 따라 나무의 속성이 변하게 되고 이 나무의 모습이 변경되야 하기 때문에 그때 내가 생각했던 방법은 메인 스레드 뒤에서 나무의 속성에 따라 나무의 모습을 변경해주는 데몬 스레드를 돌리는 것이었다. 이 스레드는 어플리케이션의 실행을 종료하거나 나무의 성장이 다하기 전까지 멈추지 않는다. 사실 이때도 굉장히 안좋은 방법이란걸 느낄수 있었지만 그때의 나로 돌아간다면 아마도 같은 선택을 할 것이다. 


<h2>Observer 패턴이란?</h2>
- 스터디 교재인 [Java 언어로 배우는 디자인 패턴 입문](http://book.naver.com/bookdb/book_detail.nhn?bid=4529127)에서 소개하는 Observer 패턴은 '관찰자' 와 '관찰 대상' 을 객체로 보고 관찰 대상의 상태가 변화하면 관찰자에게 알려주는 것이라 한다. 더 나아가 관찰자는 관찰 대상의 상태값에 따라 다른 엮여있는 객체들의 상태를 **update** 해주는 것이 Observer 패턴이라고 정의한다.
- [Wiki](http://en.wikipedia.org/wiki/Observer_pattern) 에서는 Observer 패턴이 어떤 한 객체의 상태가 변경되면 그 객체에 의존하는 다른 객체들에게 **Notify** 해주어 자동으로 상태를 변경하는 방식이라고 기술되어 있다.


![Observer Pattern](http://upload.wikimedia.org/wikipedia/commons/thumb/8/8d/Observer.svg/854px-Observer.svg.png "출처: http://en.wikipedia.org/wiki/Observer_pattern")

<br>
<h2>적용</h2>
그럼 한번 적용해보자. <br>
이전에 스레드로 돌렸다는 코드가 있었다는것만 알아두고 Observer 패턴을 어떤식으로 적용했을지에 대해서만 얘기하겠다. 

```java
public interface Observer {
 public abstract void update(Tree tree);
}
```

Observer 인터페이스는 Tree 라는 객체를 관찰하는 인터페이스고 관찰하며 구체적으로 어떻게 상태를 업데이트 할 것인지는 이 인터페이스를 구현해서 작성한다. <br>

```java
public abstract class Tree {
 private ArrayList<Observer> observers = new ArrayList<Observer>();
 public addObserver(Observer observer) {
  observers.add(observer);
 }
 public void notifyObservers() {
  Interator iter = observers.iterator();
  while (iter.hasNext()) {
   Observer o = (Observer)iter.next();
   o.update(this);
  }
 }
 public abstract void giveWater();
 public abstract void cutBranch();
}
```

이 나무(Tree) 클래스는 실제로 생략된 부분이 많지만 스마트폰 화면에 보여지는 나무에 대한 상태를 표현한 추상 클래스이다. 하위클래스로 복숭아나무(PeachTree)와 상록수(EvergreenTree) 등이 있으며 물을 주는 행위(giveWater)와 가지치는 행위(cutBranch)는 하위 클래스에서 구현되도록 한다. <br>

```java
public vlass PeachTree extends Tree {
  public void giveWater() {
    // change state : amount of water in tree
    notifyObservers();
  }
  public void cutBranch() {
    // change state : amount of branch in tree
    notifyObservers();
  }
}

public vlass EvergreenTree extends Tree {
  public void giveWater() {
    // change state : amount of water in tree
    notifyObservers();
  }
  public void cutBranch() {
    // change state : amount of branch in tree
    notifyObservers();
  }
}
```

화면에서 사용자의 Action 으로 인해 giveWater 와 cutBranch 가 수행되고 나무의 수분 상태나 가지 상태에 따라 특정한 사건이 발생된다. 복숭아 나무(PeachTree)는 각 상태에 민감하고 상록수(EvergreenTree)는 각 상태에 둔감하여 키우기가 복숭아 나무보다 용이하다는 설정이다. <br>

```java
public class DisasterObserver implements Observer {
  public void update(Tree tree) {
    // occur disaster
  }
}

public class SellerObserver implements Observer {
  public void update(Tree tree) {
    // cacluate value of tree
  }
}
```

DisasterObserver 클래스는 이름 그대로 나무의 현재 정보에 따라 재난을 발생시키는 Observer 클래스이다. 나무에 현재 수분이 적으면 말라 비틀어진다거나 친구들에게 푸쉬로 도움을 달라는 요청을 보내기도 한다. 또한, 가지 상태와 수분 상태에 따라 병충해가 발생하기도 한다.

SellerObserver 클래스는 나무의 현재 정보에 따라 그 나무의 가치를 갱신하는 Observer 클래스이다. 현재 이 나무가 건강한 상태인지 앞으로 기대되는 성장률은 얼마인지를 판단하여 가치를 갱신한다. 복숭아 나무의 기본가치가 상록수의 기본가치보다 높은 대신 건강한 상태와 높은 성장률을 기대하기 어렵다는 설정이다. <br>

```java
Tree peachTree = new PeachTree();
Tree evergreenTree = new EvergreenTree();
peachTree.addObserver(new DisasterObserver());
peachTree.addObserver(new SellerObserver());
evergreenTree.addObserver(new DisasterObserver());
evergreenTree.addObserver(new SellerObserver());
```

나무에 Observer 들을 등록하는 부분이다. 이제 스레드를 대신하여 Observer 들로 인하여 나무의 속성이 변경 될 때마다 사건이 발생될 것이다. <br>

<h2>Conclusion</h2>
약간은 어거지로 적용한 감이 있기도 하지만 약간의 이해를 돕기 위해서 하나의 예제를 더 소개하자면, Java Swing 컴포넌트와 Anroid  레이아웃을 구성해본 사람이라면 위 코드와 같은 방식이 익숙할텐데 이벤트 소스에 이벤트 리스너를 등록하는 코드와 아주 유사하다. <br>

```java
Button btnGiveWater = new Button();
btnGiveWater.onClickListener(new MyClickListener());
```

바로 이 이벤트 리스너를 등록하는 방식이 이 Observer 패턴으로부터 비롯되었기 때문이다.
<br>
Observer 패턴에 대해서 마지막으로 정리하자면,

- 메모리 리소스 활용 : 언제 일어날지 모르는 사건에 대하여 계속 돌고 있는 스레드를 만드는것보다 사건이 일어났을때마다 객체에게 알려주어(Notify) 상태를 변경(Update) 해주는 면에서 효율적이다. 
- 사실은 수동적이다 : Observer 패턴은 '관찰자' 라는 의미이지만 실제로는 우리가 구현한것처럼 '전달받는 역할' 이다. 관찰 대상이 되는 객체로 부터 상태값이 변경 되었다는것을 수동적으로 기다리고 있기 때문에 Observer 패턴은 Publish-Subscribe 패턴이라고도 하는데 명확한 이해를 위해서는 개인적으로 더 좋은 표현이라고 생각한다. <br>

<h2>Reference</h2>

 - [Java 언어로 배우는 디자인 패턴 입문](http://book.naver.com/bookdb/book_detail.nhn?bid=4529127)
 - [Wiki - Observer Pattern](http://en.wikipedia.org/wiki/Observer_pattern)
