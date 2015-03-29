---
layout: post
title:  Mybatis - foreach
categories: Spring
---

이전에 작성했던 포스트중에 INSERT INTO SELECT 에 대해 다뤘던적이 있다. <br>
>>> [INSERT INTO SELECT](http://noveloper.github.io/blog/database/2015/02/26/how-to-insert-multi-row-by-one-try.html)

해당 방법은 INSERT를 할 때 기존에 있던 데이터들과 같은 값들을 넣을때 값을 조회하면서 INSERT 하는 다중 INSERT 하는 방식이었다. 
하지만 매번 다른 값이 들어가야하는 다중 INSERT 를 해야한다면? 그 값은 DAO를 통해서 넘어온다면? 
일반적으로 생각하는 방법은 다음과같이 Java단에서 List의 forEach 문법을 이용하여 INSERT 함수를 반복 호출하는것이다.

```java
@Override
public void insertUserList(List<User> users) {
  for (User user : users) {
    insertUser("insertUser", user);
  }
}
```
```xml
<insert id ="insertUser" parameterType="User">
  INSERT INTO User 
    (user_id
    , user_name
    , user_passwd
    , user_note)
    VALUES
    (#{userId}
    ,#{userName}
    ,#{userPasswd}
    ,#{userNote})
</insert>
```

<h2>What is problem?</h2>
생각해보면 코드도 깔끔하고 의미가 명확하여 좋은것같다. 하지만 이 작업을 수행하기 위해서는 예를들어 만약 1000명의 User를 삽입해야 한다면 다음과 같은 작업이 1000번 일어날 것이다.

[ DAO 함수호출 - Mapper 검색 - DB 오픈 - Query 수행 ] x 1000

사실 굵직한 작업으로 많이 간소화해서 그렇지 이거보다 더 많은 작업이 이루어지게 된다. 위에 프로세스에서 오로지 Query 수행만 1000번하게 할 수 업을까?

<h2>Mabatis - foreach</h2>
Mybatis에서 제공하는 문법중 foreach를 이용하여 다음과 같이 바꿔보았다.

```xml
<insert id ="insertUser" parameterType="User">
<foreach item="user" index="index" collection="users">
  INSERT INTO User 
    (user_id
    , user_name
    , user_passwd
    , user_note)
    VALUES
    (#{user.userId}
    ,#{user.userName}
    ,#{user.userPasswd}
    ,#{user.userNote})
</foreach>
</insert>
```

이렇게 하면 위에서 정의한 프로세스중 Query 수행만 1000번 돌아간다는 신뢰가 생긴다. <br>
<br>
foreach는 INSERT 뿐만 아니라 SELECT 시 에도 쓰인다. <br>
user_type이라는 컬럼이 있고 해당 값이 특정한 값일때만 조회를 해야하고 List를 통해서 넘어올 때 다음과 같이 mapper를 작성해주면 된다.

```xml
<select id="xxx" parameterType="User" resultType="User">
  SELECT 
    *
  FROM
    user
  WHERE
    user_type IN 
      <foreach item="user" index="index" collection="users" open="(" separator="," close=")">
        #{user.userType}
      </foreach>
</select>
```

위와 같이 foreach를 작성하면 결과는 다음과 같이 나온다

```xml
user_type IN
  ("admin", "designer", "normal")
```

<h2>conclusion</h2>
mybatis의 foreach를 이용하면 쟈바단에서의 퍼포먼스 시간을 줄일 수 있다. 만약 한번의 INSERT 트 후에 제대로 값이 들어갔는지 확인하여 제대로 안들어갔을때 Rollback 시키기 위해서는 처음 일반적으로 Java단에서 호출하는 방법을 이용해야 할 것이다.


<h2>Reference</h2>
- [Mybatis - foreach](https://mybatis.github.io/mybatis-3/ko/dynamic-sql.html)
