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
console 이라는 JavaScript 내장 객체를 with로 지정하여 log 같은 메서드를 console.log() 형태가 아닌 독립적으로 사용 가능하게 하는 코드이다. <br>

<h2>Reference</h2>

- [JavasSript With - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/with)
- [With operator - JavaScript Tutorial](http://javascript.info/tutorial/with-operator)
