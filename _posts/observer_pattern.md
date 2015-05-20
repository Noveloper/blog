<h1>Observer 패턴</h1>

<h2>Observer 패턴이란?</h2>
- 스터디 교재인 [Java 언어로 배우는 디자인 패턴 입문](http://book.naver.com/bookdb/book_detail.nhn?bid=4529127)에서 소개하는 Observer 패턴은 '관찰자' 와 '관찰 대상' 을 객체로 보고 관찰 대상의 상태가 변화하면 관찰자에게 알려주는 것이라 한다. 더 나아가 관찰자는 관찰 대상의 상태값에 따라 다른 엮여있는 객체들의 상태를 **update** 해주는 것이 Observer 패턴이라고 정의한다.
- [Wiki](http://en.wikipedia.org/wiki/Observer_pattern) 에서는 Observer 패턴이 어떤 한 객체의 상태가 변경되면 그 객체에 의존하는 다른 객체들에게 **Notify** 해주어 자동으로 상태를 변경하는 방식이라고 기술되어 있다.


![Observer Pattern](http://upload.wikimedia.org/wikipedia/commons/thumb/8/8d/Observer.svg/854px-Observer.svg.png "출처: http://en.wikipedia.org/wiki/Observer_pattern")



<h2>예제</h2>
내가 예전에 '증강현실 식물키우기' 라는 Android App을 개발하다가 중간에 중단했었는데 그 프로젝트에 쓰였던 클래스들과 책에 나온 예제를 섞어서 예제로 들어보겠다. 

<br>
```java
public interface Observer {
 public abstract void update(Tree tree);
}
```
Observer 인터페이스는 Tree 라는 객체를 관찰하는 인터페이스고 구체적으로 관찰하며 어떻게 상태를 업데이트 할 것인지는 이 인터페이스를 구현해서 작성한다.

<br>
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

이 나무(Tree) 클래스는 실제로 생략된 부분이 많지만 스마트폰 화면에 보여지는 나무에 대한 상태를 표현한 추상 클래스이다. 물을 주는 행위(giveWater)와 가지치는 행위(cutBranch)는 하위 클래스에서 구현되도록 한다.

<br>
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

PeachTree는 복숭아 나무를 뜻하고 EvergreenTree 는 상록수를 뜻하는 클래스로서 화면에서 사용자의 Action 으로 인해 giveWater 와 cutBranch 가 수행되고 나무의 수분 상태나 가지 상태에 따라 특정한 사건이 발생된다.

<br>
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

DisasterObserver 클래스는 이름 그대로 나무의 현재 정보에 따라 재난을 발생시키는 Observer 클래스이다. 나무에 현재 수분이 적으면 말라 비틀어진다거나 친구들에게 푸쉬로 도움을 달라는 요청을 보내기도 한다. 또한, 가지 상태와 수분 상태에 따라 병충해가 발생하기도 한다. 복숭아 나무(PeachTree)는 각 상태에 민감하고 상록수(EvergreenTree)는 각 상태에 둔감하여 키우기가 복숭아 나무 보다 용이하다는 설정이다.

SellerObserver 클래스는 나무의 현재 정보에 따라 그 나무의 가치를 갱신하는 Observer 클래스이다. 현재 이 나무가 건강한 상태인지 앞으로 기대되는 성장률은 얼마인지를 판단하여 가치를 갱신한다. 복숭아 나무의 가치가 상록수의 가치보다 높은 대신 건강한 상태와 높은 성장률을 기대하기 어렵다는 설정이다.

<br>
```java
Tree peachTree = new PeachTree();
Tree evergreenTree = new EvergreenTree();
peachTree.addObserver(new DiasterObserver());
peachTree.addObserver(new SellerObserver());
evergreenTree.addObserver(new DiasterObserver());
evergreenTree.addObserver(new SellerObserver());
```

나무에 Observer 들을 등록하는 부분이다. 위에서 Android 를 잠깐 언급했지만 Android나 Java Swing 을 해본사람이라면 위와 같은 형태의 코드를 많이 접했을 것이다.

그렇다. 바로 UI 컴포넌트들에 이벤트 리스너를 등록하는 코드와 아주 흡사하다.

<br>
```java
Button btnGiveWater = new Button();
btnGiveWater.onClickListener(new MyClickListener());
```

바로 이 이벤트 리스너를 등록하는 방식이 이 Observer 패턴으로부터 비롯되었기 때문이다.


<h2>정리</h2>
만약, Observer 패턴을 모르고서 저 Disaster 와 Seller 같은 처리를 하기 위해서 내가 가장 처음 생각했을 방법은 메인 스레드 뒤에서 계속해서 돌면서 나무의 상태를 체크하며 사건을 발생시키는 데몬 스레드들로 만드는 것이다. 실제로 저 프로젝트를 진행할 때 Observer 패턴을 몰랐기 때문에 리소스를 많이 잡아먹는 문제에도 불구하고 그렇게 작성했었다. 

Observer 패턴은 사실 '관찰자' 라는 의미이지만 실제로는 우리가 이해하고 구현한것처럼 '전달받는 역할' 이다. 관찰 대상이 되는 객체로 부터 상태값이 변경 되었다는것을 수동적으로 기다리고 있기 때문에 Observer 패턴은 Publish-Subscribe 패턴이라고도 한다. 명확한 이해를 위해서 더 좋은 표현이라고 개인적으로 생각한다.



<h2>Reference</h2>
 - [Java 언어로 배우는 디자인 패턴 입문](http://book.naver.com/bookdb/book_detail.nhn?bid=4529127)
 - [Wiki - Observer Pattern](http://en.wikipedia.org/wiki/Observer_pattern)
