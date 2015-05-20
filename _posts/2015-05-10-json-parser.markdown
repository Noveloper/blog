---
layout: post
title:  Java - JsonParser
categories: Spring
---

최근 내가 담당하는 시스템내에 주소 검색 API를 기존 것에서 새로운것으로 변경해야 될 니즈가 생겼는데 기존 API는 XML로 결과값을 반환하는 반면 새로운 API는 JSON 문자열로 반환하는 이슈가 있었다. 기존에 있던 코드 역시 [org.w3c.dom](http://docs.oracle.com/javase/7/docs/api/org/w3c/dom/package-summary.html) 패키지내에 클래스를 이용하여 XML을 Parsing 하는 예제 였기에 변경하려면 받아온 JSON 문자열을 알맞게 다시 포장하기 위해서는 어느 정도 소요가 필요했다.
<br>
<h2>org.json</h2>
먼저 생각한 방법은 그냥 이전에 써왔던대로 org.json 클래스들을 활용하여 작성하는 것이었다.

```java
import org.json.*;
...
...
public List<Address> parseAddressList(String jsonString) {
  List<Address> addresses = new List<Address>();
  
  JSONObject resultJSON = new JSONObject(jsonString);
  JSONObject headerJSON = resultJSON.getJSONObject("header");
  JSONObject bodyJSON = null;
  if (header.getBoolean("isSuccess")) {
    bodyJSON = resultJSON.getJSONObject("body");
    JSONArray addressesJSON = bodyJSON.getJSONArray("addresses");
    // parse and add address to addresses
  } else {
    // error 
  }
}
```
<br>
org.json 패키지에서 에서 제공하는 메서드는 굉장히 많기 때문에 가독성 좋은 코드를 짜기에 용이하다. 

<br>
<h2>JsonParser class</h2>
다른 방법을 찾아보다가 Java EE 7 버전부터 있는 [javax.json](https://docs.oracle.com/javaee/7/api/javax/json/package-summary.html) 패키지를 알게되었는데 새로운 JSON 처리 클래스들을 지원한다. <br>

```java
Json
JsonParser
JsonParser.Event
```
<br>
위에서 org.json 패키지를 활용해서 작성했던 코드를 이를 이용해서 변경하면 대충 다음과 같다.

```java
import javax.json.Json;
import javax.json.stream.JsonParser;
import javax.json.stream.JsonParser.Event;
...
...
public List<Address> parseAddressList(String jsonString) {
  List<Address> addresses = new List<Address>();
  
  JsonParser parser = Json.createParser(new StringReader(jsonString));
  String keyName = null;
  
  while (parser.hasNext()) {
    Event event = parser.next();
    Address address = new Address();
    
    switch (event) {
      case START_OBJECT:
        break;
      case START_ARRAY:
        break;
      case KEY_NAME:
        keyName = parser.getString();
        break;
      case VALUE_STRING:
        // process to String Value
        break;
      case VALUE_NUMBER:
        // process to Number Value
        break;
      case VALUE_FALSE:
        // process to boolean Value : False
        break;
      case VALUE_TRUE:
        // process to boolean Value : True
        break;
      case VALUE_NULL:
        // white space, don't anything
        break;
      case END_ARRAY:
        break;
      case END_OBJECT:
        break;
    }
    
    addresses.add(address);
  }
}
```
<br>
JsonParser 클래스 내부적으로 [JsonParser.Event](https://json-processing-spec.java.net/nonav/releases/1.0/pr-draft/javadocs/javax/json/stream/JsonParser.Event.html) 라는 enum을 갖는데 이 enum은 현재 JSON 문자열의 어느 지점인지를 알게 해준다. 단일 JSON 객체의 시작인지 배열의 시작인지, 키에 있는지 값에 있는지 등. 예를들어 이 JSON 문자열이 boolean 값을 오직 header에 isSuccess 한개라면 VALUE_FALSE 부분에 에러처리를 하면 된다. <br>
위와 같은 방법이 아니더라도 [JsonValue](https://docs.oracle.com/javaee/7/api/javax/json/JsonValue.html) 라는 인터페이스를 상속한 JsonObject 와 JsonArray를 이용하면 먼저 org.json 패키지를 사용해서 작성한 코드와 거의 유사하게 작성할 수 있는것 같다.

<br>
<h2>Conclusion</h2>
설명이 부족한데 나도 공부하면서 한거라 아직 사용법에 익숙치 않고 실제 프로젝트에는 JDK버전 호환 문제도 있어 위에서 org.json 패키지를 사용한 방법으로 구현하였다. switch 로 분기한 부분을 메서드로 잘 추출하면 그럴듯한 코드가 나오지 않을까라고 기대도 해보고 단지 Parser 뿐만 아니라 JsonWriter, JsonReader 같은 클래스도 지원하니 일단 이런게 있다는걸 알아두는 단계로 이번엔 넘어가야겠다.

<br>
<h2>Reference</h2>

- [javax.json Package](https://docs.oracle.com/javaee/7/api/javax/json/package-summary.html)
- [JsonParser class](http://docs.oracle.com/javaee/7/api/javax/json/stream/JsonParser.html)
- [org.json Package](http://www.json.org/javadoc/)
