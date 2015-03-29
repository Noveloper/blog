---
layout: post
title:  "img태그에 src의 참조가 없는 참조라면?"
categories: Javascript
---

<h2>Needs</h2>
최근에 들어온 요청이 사진이 없는 경우 해당 img 태그를 아예 안보이게 해달라는 요청이 있었다. 
아래와 같은 이미지 태그가 있을 때, 해당 src 어트리뷰트가 가리키고 있는 값이 없거나 잘못된 참조라면 화면에 보여지는 이미지 태그는 소위 말하는 엑박을 보여줄 것이다.

```javascript
<img src="---/---/---.png" />
```
