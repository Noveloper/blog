---
layout: post
title:  "Javascript - input 태그에서 multi-line 이 가능할까?"
categories: Javascript
---

<h3>Needs</h3>
- 최근에 원래 input 태그를 사용했던 곳 중에서 사용자가 여러줄 입력이 가능하게 변경해달라는 요청이 있었다.
- 간단한 작업일거라 생각했지만 꽤나 골머리를 썩혔다.


<h3>Solution ?</h3>
- 사실 결론부터 말하자면 input 태그에서 multi-line 구현은 불가능하다. 고민하지 말고 그냥 textarea를 쓰면 된다. 
- 애초에 input 태그는 single-line 전용으로 구현 되었고 form 엘리먼트에서 multi-line 이 가능한 엘리먼트는 textarea 밖에 없다는 졍보를 접했다.
- 그럼에도 사용자의 요청에 맞게 작업하기 위해서는 textarea를 억지로 input 처럼 보이게 해야한다. 
- 나느 스크롤 바를 안보이게 하고 크기를 맞추는 등의 CSS 작업을 해줘야 했다.


<h3>Reference</h3>
- [Stackoverflow : MultiLine Form in HTML?](http://stackoverflow.com/questions/1931332/multiline-form-in-html)
- [w3schools : textarea tag](http://www.w3schools.com/tags/tag_textarea.asp)
