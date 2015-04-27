---
layout: post
title:  CSS - Print 영역을 분할하자
categories: CSS
---

이번에 개발하게 된건 기존의 기능에서 어떤 문서를 출력하고 있다면, 그 문서가 출력될 때 다른 문서 2장을 추가로 출력되게 해달라는 요청이었다. 또한, 특정 경우에는 기존의 그 문서만, 다른 경우에는 두장의 문서만 출력하게 하는 둥 여러케이스를 요청받았다. 출력될 문서는 HTML 코드로 작성되어 있었고 해당 문서를 출력할 때는 브라우저의 기본 인쇄 기능을 사용하고 있었기에 다른 문서 2장을 추가하기 위해서는 해당 양식대로 HTML 코드를 작성해야 했다. 그리고 케이스에 맞춰서 출력이 되야했기 때문에 한 페이지에 내용을 담아서 div로 분할시켰다.

```html
<body>
<div class="sector1">
...
</div>
<div class="sector2">
...
</div>
<div class="sector3">
...
</div>
</body>
```

<h2>문제의 시작</h2>
사실 어찌보면 당연한 문제였다. div의 사이즈가 일정하지 않을 수 있었기 때문에 div 크기에 따라서 출력되는 페이지에 내용이 겹칠 염려가 있었기 때문이다. 그렇다고 div의 크기를 절대 사이즈로 딱 A4용지의 크기 만큼 설정하는것도 좋은 방법이 아니라고 생각했다. 당장의 니즈는 없었지만 추후 sector 한개의 크기가 A4 용지를 넘어버릴 가능성이 충분히 존재했기 때문이다.
(여기서 '충분히' 란 표현은 개발에서 굉장히 중요하다. 다른 기능도 마찬가지겠지만 저 표현이 들어가는 기능의 개발은 '무조건' 확장이 용이하게 개발해야 되기 때문이다.)

<h2>CSS Media Print type</h2>
이전과 달리 html은 웹페이지에 국한되지 않는다. 요즈음은 각 장치에 대응을 하여 표현할 수 있게 CSS에 Media 라는 타입이 존재한다. 이 Media 타입중 print 타입을 이용하여 print 영역을 분할할 수 있다.

```css
@media print {
    page-divide {
        page-break-after: auto|always|left|right;
        page-break-beforer: auto|always|left|right;
    }
}
```

page-break-after 는 일단 페이지 영역을 어떻게 분할할 지 정할 수 있다. 
각 속성은 참고자료로 첨부된 페이지에서 확인을 할 수 있고 가장 많이 쓰일 것 같은건 before와 after이다.

```css
@media print {
    page-divide {
        page-break-after: always;
    }
}
```

```html
<div class="sector1">
...
</div>
<div class="page-divide" />
<div class="sector2">
...
</div>
<div class="page-divide" />
```

위와 같이 작성하면 page-divide 를 클래스로 하는 div 이후 무조건 printing 영역을 분할 하겠다는 뜻이다. 반대로 page-break-before을 사용했다면 page-divide 이전 영역까지 printing 영역을 분할하기 때문에 다양하게 사용이 가능할 것 같다.


<h2>특정부분 출력에서 제외시키기</h2>
div 로만 쭈욱 작성했다면 출력시에는 나뉘어져 깔끔할지 몰라도 사용자들이 보이는 html 페이지는 div가 서로 여백없이 연결되어 있어 보기 불편할 수 있다. 이때 여백이나 영역을 구분하는 태그를 집어 넣으면 보기 좋을 수 있지만 또 반대로 출력시에 해당부분이 같이 출력되는 문제가 있다. 

```css
@media print {
    page-divide {
        page-break-after: always;
    }
    
    no-print-page {
        display: none;
    }
}
```

```html
<div class="no-print-page">
============================================================
</div>
<div class="sector1">
...
</div>
...
<div class="no-print-page">
============================================================
</div>
```

이런식으로 no-print-page 라는 클래스를 정의해서 넣어놓으면 이 no-print-page 의 속성은 printing을 할 때만 동작하기 때문에 printing 시에 깔끔하게 해당 영역이 사라진다.


<h2>Conclusion</h2>
더 욕심이 나서 정렬이 안되어 있던 각 영역을 printing 시에 가운데로 정렬한다던지 하는 기능을 추가하고 싶었지만 해당 부분은 찾지못하여 여백 영역을 조금 넣어 기능을 구현하였기 때문에 100% 깔끔하게 해결하진 못했다. 찜찜하긴 하지만 프린트 영역에만 여백넣는 방법을 찾아서 해당 방법을 참고한다면 추후 보완할 수 있을거라 생각하고 글을 마친다.


<h2>Reference</h2>
- [CSS Media types - w3schools.com](http://www.w3schools.com/css/css_mediatypes.asp)
- [CSS page-break-after Property - w3schools.com](http://www.w3schools.com/cssref/pr_print_pageba.asp)
- [프린트 영역에만 여백 넣기 - Stackoverflow](http://stackoverflow.com/questions/1542320/margin-while-printing-html-page)
