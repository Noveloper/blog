<h1>Observer 패턴</h1>

<h2>Observer 패턴이란?</h2>
- 스터디 교재인 [Java 언어로 배우는 디자인 패턴 입문](http://book.naver.com/bookdb/book_detail.nhn?bid=4529127)에서 소개하는 Observer 패턴은 '관찰자' 와 '관찰 대상' 을 객체로 보고 관찰 대상의 상태가 변화하면 관찰자에게 알려주는 것이라 한다. 더 나아가 관찰자는 관찰 대상의 상태값에 따라 다른 엮여있는 객체들의 상태를 update 해주는 것이 Observer 패턴이라고 정의한다.
- [Wiki](http://en.wikipedia.org/wiki/Observer_pattern) 에서는 Observer 패턴이 어떤 한 객체의 상태가 변경되면 그 객체에 의존하는 다른 객체들에게 Notify 해주어 자동으로 상태를 변경하는 방식이라고 기술되어 있다.
- 여기서 Update 와 Notify 는 동일한 맥락이다.


![Observer Pattern](http://upload.wikimedia.org/wikipedia/commons/thumb/8/8d/Observer.svg/854px-Observer.svg.png "출처: http://en.wikipedia.org/wiki/Observer_pattern")



<h2>Example</h2>


<h2>Reference</h2>
 - [Java 언어로 배우는 디자인 패턴 입문](http://book.naver.com/bookdb/book_detail.nhn?bid=4529127)
 - [Wiki - Observer Pattern](http://en.wikipedia.org/wiki/Observer_pattern)
