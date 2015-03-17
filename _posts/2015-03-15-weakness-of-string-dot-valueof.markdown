---
layout: post
title:  "String.valueOf() 사용시 생길 수 있는일 및 주의사항"
categories: Java
---


뷰단에서 넘어온 데이터를 데이터베이스에 저장하기 전에 비즈니스 로직단에서 한번 더 가공한 후 데이터를 넘길때 일반적으로 작성하는 방법은 뷰단에서 바라볼 수 있는 URL을 맵핑시킨 Controller와, 비즈니스로직을 담당하는 Service, 데이터베이스 접근에 관여하는 DAO 를 작성하는 것이다. 프론트단에서 데이터를 받을때 Model 객체가 아닌 Map 객체로 받아야만 하는 상황에서 비즈니스 로직에서 해당 데이터를 가공할때는 Map 컬렉션 클래스의 get메서드를 사용해야 한다. 

```java
@Override
void updateBlog(Map<String, Object> paramMap) {
  Blog blog = new Blog();
  ...
  blog.setPostId(paramMap.get("postId"));
  ...
  blogDAO.updateBlog(blog);
}
```

Blog라는 Model이 다음과 같이 정의되어 있다고하자.

```java
class Blog {
  private String postId;
  private String postName;
  private String postCategory;
  private String postContent;
  ...
}
```

프론트단에서 넘어오는 postId 값이 굉장히 길어질 수 있음을 고려하여 postId를 String으로 선언하였다. 받아온 paramMap의 Map 제네릭은 [String, Object] 였으므로 blog객체에 넘겨줄라면 형변환을 하거나 String.valueOf를 쓰면된다.

```java
@Override
void updateBlog(Map<String, Object> paramMap) {
  Blog blog = new Blog();
  ...
  blog.setPostId(String.valueOf(paramMap.get("postId")));
  ...
  blogDAO.updateBlog(blog);
}
```


<h3>What is problem?</h3>
- 시스템에서 에러가 났는데 이유를 모르겠다. 아니 정확히 말하자면 이유는 알 수 있었는데 왜? 라는 의문이 들었다. 분명히 데이터케이스 스키마정보에 post_id라는 컬럼은 NOT NULL이 지정되고 있었기 때문에 null 값이 들어오면 진즉에 SqlException을 냈어야 정상인데 이 컬럼에 널값이 들어가서 이 테이블을 참조하는 다른시스템에서 오류가 나고 있었다. (심지어 Mapper 파일에서 if태그문을 걸어 not null 에다가 ''와 같은 빈문자열도 거르고 있었다.)
- 자세히 깊게 들여다보니 NULL 값이 들어간게 아니라 "null" 이라는 문자열이 들어간것이다.
- String.valueOf(null)은 문자열 "null"을 반환한다. 
- 이 문제를 해결하기위해 다음과 같이 stringValueOf(Object)라는 메서드를 만들어서 상황을 해결했다.

```java
private stringValueOf(Object object) {
  return object == null ? "" : String.valueOf(object);
}

@Override
public void updateBlog(Map<String, Object> paramMap) {
  Blog blog = new Blog();
  ...
  blog.setPostId(stringValueOf(paramMap.get("postId"));
  ...
  blogDAO.updateBlog(blog);
}
```


<h3>Conclusion</h3>
사실 이와 같은 문제는 프론트단에서 컨트롤러로 값을 받을때 Validation 체크하는 로직이 제대로 만들어져 있었다면 애초에 컨트롤러에서 잡았을 문제이다. 허나 분명히 위와 같은 상황이 벌어질 수 밖에 없는 이유가 있었고 String.valueOf 와 같은 기본적인 메서드를 사용할때에도 한번 더 생각할 필요가 있다는것을 알게되었다.



<h3>Reference</h3>
- [String.valueOf 소스코드](http://grepcode.com/file/repository.grepcode.com/java/root/jdk/openjdk/6-b14/java/lang/String.java#2837)
