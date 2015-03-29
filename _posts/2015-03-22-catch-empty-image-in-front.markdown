---
layout: post
title:  "img태그에 src의 참조가 없는 참조라면?"
categories: Javascript
---

<h2>Needs</h2>
최근에 들어온 요청이 사진이 없는 경우 해당 img 태그를 아예 안보이게 해달라는 요청이 있었다. 
아래와 같은 이미지 태그가 있을 때, 해당 src 어트리뷰트가 가리키고 있는 값이 없거나 잘못된 참조라면 화면에 보여지는 이미지 태그는 소위 말하는 엑박을 보여줄 것이다.

```javascript
<img src="test.png" />
```

사용자의 요청은 엑박도 아무 그림도 뜨지 않는 빈칸이 아닌 칸(img태그) 자체를 없애는 것이었다.

<h2>Try 1</h2>
처음 단순하게 생각하여 src의 값이 잘못됐다면 그냥 img 태그의 src 값이 null 이거나 공백이면 img 태그를 없애자 하는 생각으로 다음과 같은 코드를 작성했다.

```javascript
function hideImgIfSrcIsInvalid() {
  $("img").each(function() {
    var $imgTag = $(this);
    var imgSrc = $imgTag.attr("src").trim();
    
    if (imgSrc == null || imgSrc == '') {
      imgTag.hide();
    }
  });
}
```

하지만 이 방식은 완전히 잘못됐다. src의 값은 이미지의 존재 여부에 상관없이 위에 적혀있는 test.png 를 가져온다.


<h2>Try 2</h2>
이번에는 가져온 이미지의 크기가 0이거나 null일때를 체크해봤다.

```javascript
function hideImgIfSrcSizeIsInvalid() {
  $("img").each(function() {
    var $imgTag = $(this);
    var imgWidth = $imgTag.width();
    
    if (imgWidth == null || imgWidth == 0) {
      imgTag.hide();
    }
  });
}
```

꽤나 그럴듯한 방법이지만 이 방법은 실제 가져온 이미지의 크기가 아닌 img 태그 자체의 사이즈를 가져와서 의미가 없다. 


<h2>Try 3</h2>
html을 그려줄때 img태그에 src가 이상한 값이면 HTTP 4xx 에러를 내는것을 콘솔창에서 확인할 수 있다.
그래서 html을 그려줄때 try-catch 할 수 있는 방법을 찾기위해 자바스크립트나 JQuery가 아닌 EL이나 JSTL 쪽을 찾아보았는데 쓸만한것이 있어 적용해보았다. 


```javascript
<c:catch var="e">
  <c:import url="test.png" var="imgSrc" />
</c:catch>
<c:choose>
  <c:when test="${empty imgSrc}">
  </c:when>
  <c:otherwise>
    <td rowspan="3">
      <img src="test.png" width="100" height="100" alt="">
    </td>
  </c:otherwise>
</c:choose>
```

잘된다. 딱 원하는 액션을 보여주었기에 만족할만한 결과이지만 JSTL 태그 라이브러리가 아닌 자바스크립트나 JQuery 단에서 컨트롤 할 수 있다고 믿어 방법을 찾아보다가 Stackoverflow에서 Real Img Size를 구하는 방법을 찾았다.

```javascript
$("img").each(function() {
  var $imgTag = $(this);
  var real_width, real_height;
  
  $("<img/>") 
      .attr("src", $(img).attr("src"))
      .load(function() {
          real_width = this.width;   
          real_height = this.height;
      });
});
```

역시 이 방법도 잘된다. 상황에 따라서 JSTL을 이용한 방법을 사용할 지 자바스크립트를 이용한 방법을 사용할 지를 결정해야 될 것 같다. 어쨌든 미션 Clear.


<h2>Referencd</h2>
- [JSTL - catch](http://www.tutorialspoint.com/jsp/jstl_core_catch_tag.htm)
- [JSTL - import](http://www.tutorialspoint.com/jsp/jstl_core_import_tag.htm)
- [Get real image width and height with JavaScript in Safari/Chrome?](http://stackoverflow.com/questions/318630/get-real-image-width-and-height-with-javascript-in-safari-chrome)
