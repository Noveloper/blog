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

<h2>Reference</h2>

- [isNuemric Documentation](https://api.jquery.com/jQuery.isNumeric/)
- [inArray Documentation](https://api.jquery.com/jQuery.inArray/)
