---
layout: post
title:  "Javascript - Form 전송시 특정 태그 제외시키기"
categories: Javascript
---

<h3>Needs</h3>
- 전송 페이지를 구현 하다보면 각 상태 값에 따라서 전송되는 파라미터들을 분기해야할 상황이 생긴다. 
- 네이밍 규칙만 잘 지켰다면 함께 보내도 상관은 없지만 보다 좋은 성능을 위해서 필요없는 값을 넘길 필요가 없다.
- 전송(submit)시에 특정 태그만 제외 시키는 방법을 알아본다.

<h3>Solution</h3>
- 예상외로 방법은 간단하게 찾을 수 있었다. 
- 각 태그의 속성에 disabled 를 추가하면 끝.

```Javascript
<form>
  <input name="targetId" />
  <input name="targetDescription" disabled />
  ...
</form>
```

- 위와 같이 작성하면 전송시에 targetId 만 넘어가게 되고 disabled 처리된 targetDescription은 전달되지 않는다.

<h3>Reference</h3>
- [Stackoverflow : Exclude hidden form fields from submit](http://stackoverflow.com/questions/16808799/exclude-hidden-form-fields-from-submit)
- [w3schools : disabled Attribute](http://www.w3schools.com/tags/att_input_disabled.asp)
