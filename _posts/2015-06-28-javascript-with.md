---
layout: post
title:  JavaScript - With
categories: javascript
---

이번에 레거시 자바스크립트 코드를 이해하고 기능을 추가해야 할 일이 있었는데 코드를 보던중 처음보는 키워드인 with 를 보게되었고 뭐하는 키워드이고 무슨 문법인지 공부를 해보았다.  <br>

<h2>With</h2>
C++ 을 공부해본 사람이라면 다음과 같은 코드가 익숙할 것이다

```c++
using namespace std;

int main() {
  cout << "test" << endl;
  return 0;
}
```

<br>
그리고 Java를 공부해본 사람이라면 다음과 같은 코드도 익숙할 것이다.

```java
import static org.junit.Assert

public class DommyTest {
  @Test
  public void test() {
    assertThat(...);
  }
}
```

<br>
두 코드의 공통점은 std::cout, Assert.assertThat 과 같은 함수를 사용할 때 namespace 와 static import 를 통해서 cout, assertThat 의 간단한 형태로 사용한다는 것이다. <br>

이 말을 하는 이유는 JavaScript 의 with 도 비슷한 역할을 수행하기 때문이다. <br>
다음 코드를 보자.

```javascript
function withTest() {
  with(console) {
    log("with");
    log("test");
  }
}
```

<br>
console 이라는 JavaScript 내장 객체를 with로 지정하여 log 같은 메서드를 console.log() 형태가 아닌 독립적으로 사용 가능하게 
하는 코드이다. <br>

```javascript
var monster = {
    hp: "100",
    name: "oger",
    weapon: "iron club"
}

function withTest2 () {
  with (monster) {
      console.log(hp);
      console.log(name);
      console.log(weapon);
  }
}
```

<br>
위와 같이 내장 객체 뿐만 아니라 사용자가 직접 정의한 객체들도 with로 컨트롤이 가능하다. 앞으로 수차례 재사용 되어질 코드가 있다면 with를 사용하면 상당량의 귀찮음을 덜어낼 수 있는것 같다. <br>

<h2>Conclusion</h2>
굉장히 편한 기능 같지만 대부분의 JavaScipt 개발자들은 with 문법을 사용하는 것을 좋아하지 않고 코드 컨벤션을 협의할 때 with를 금지하는 경우도 많다고 한다. <br>
왜 그런걸까 하고 찾아보다가 다음 문장을 읽게 되었다.

```java
People don’t like with, because it gives the illusion of working with the object.
```

객체를 다룸에 있어 굉장한 혼란을 줄 수 있다는 것이다. 사실 조금 생각해보면 위에서 예로 들었던 코드들을 보면 저게 지역 변수인지 전역변수인지 객체의 멤버인지 구분을 하기가 어렵다. 더군다나 딱히 var a; 와 같은 선언 코드를 넣지 않아도 처음 사용 될 때 자동 선언이 되어버리는 JavaScript 와 같은 경우에는 더더둑 가독성이 어려워 질 것 같다. 


<h2>Reference</h2>

- [JavasSript With - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/with)
- [With operator - JavaScript Tutorial](http://javascript.info/tutorial/with-operator)
