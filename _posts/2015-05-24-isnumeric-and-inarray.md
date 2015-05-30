---
layout: post
title:  jQuery - isNumeric(), inArray()
categories: Javascript
---

프론트 작업을 하면서 숫자를 처리할 때 자주 생기는 이슈는 다음과 같다. <br>

1. 어떤 입력에 대해서 숫자만을 입력 받아야한다.
2. 리스트형의 데이터일때 중복되는 값이 있으면 안된다.

jQuery의 함수를 사용해서 이를 해결해보자. <br>

<h2>isNumeric</h2>

이름만 봐도 어떤 함수인지 알 수 있듯이 파라미터로 넘어온 값이 '수' 인지 아닌지를 판단할 수 있는 함수다. 

```javascript
$.isNumeric(23) // true
$.isNumeric("23") // true
$.isNumeric("23.0") // true
$.isNumeric("이십삼") // false
```
<br> 
사용예는 다음과 같다. 

```javascript
if ($.isNumeric($("#ordNo").val())) {
  // success process
} else {
  // error process
}
  
```

<br>
<h2>inArray</h2>

중복된 값을 처리하기 위해서 Java의 Collection 클래스의 contains 메서드와 같은것이 분명히 있을거라고 생각하고 찾아보았는데 역시나 있었다. 어떤 소설에서 본 문장이지만 있지 않을까 하며 찾기 보다 반드시 있다라며 찾는건 검색 속도도 효율도 다르단다.
<br>

다시 본론으로 넘어가서 jQuery의 inArray 함수를 사용하면 중복 처리를 다음과 같이 할 수 있다.

```javascript
var ordNos = [];
var realCnt = 0;

$("input[name='ordNo']").each(function (i, v) {
  ++realCnt;
  if ($.inArray(v, ordNos) != -1) {
    ordNos.put(v);
  } else {
    // error process
  }
};
```

<br>
inArray 는 존재하면 해당 값의 인덱스를, 없으면 -1을 반환한다.
 
<br>
<h2>Reference</h2>

- [isNuemric Documentation](https://api.jquery.com/jQuery.isNumeric/)
- [inArray Documentation](https://api.jquery.com/jQuery.inArray/)
