---
layout: post
title:  Mybatis - association, collection
categories: spring
---

Database 에서 select 절을 이용해 데이터를 조회할 때 mybatis 의 resultMap 을 이용하면 사용자가 정의한 Model 객체로 값을 직접 받아올 수 있다. 그렇다면 Model 객체안에 멤버변수로 또 다른 Model 객체가 있다면 해당 객체에는 값을 어떻게 집어넣어 줄까? <br>
mybatis resultMap의 기능중 assocation 과 collection 에 대해서 알아보자. <br>

<h2>Association (has one)</h2>
Association은 has one 타입의 관계를 다룰 때 사용하는데 예를들어 어떤 시험지(Sheet)를 푸는학생(Stuent)은 한명이다. 해당 시험지를 조회하면서 그 학생을 조회하려고 association 관계를 걸어서 같이 조회하게 다음과 같이 코드를 작성할 수 있다.

```java
class Sheet {
  ...
  Student student;
}

class Student {
  int studentId;
  ...
}
```

```xml
<resultMap id="sheetResult" type="com.xxx.Sheet">
  <association property="student" column="stuendId" javaType="Student" select="selectStudent"/>
</resultMap>

<select id="selectSheet" resultMap="sheetResult">
  SELECT ..., student_id studentId, ... FROM sheet WHERE sheet_id = #{sheetId}
</select>

<select id="selectStudent" resultType="Student">
  SELECT student_id studentId, ... FROM student WHERE student_id = #{studentId}
</select>
```

association 태그에 column 은 조회할 selectStudent의 파라미터로 전달되고 sheet를 조회하면서 함께 student를 조회하여 Sheet 인스턴스 안에 멤버변수로 있는 Student 인스턴스의 내용도 채워지게 된다. <br>


<h2>Collection (has many)</h2>
Collection은 has many 타입의 관계를 다룰 때 사용한다. 위에 예에서 응용하여 하나의 Sheet에는 여러 문항(Pool)들이 들어있을 때 해당 문항 리스트를 얻어올 때 다음과 같이 작성할 수 있다.

```java
class Sheet {
  ...
  Student student;
  List<Pool> pools;
}

class Pool {
  ...
  int sheetId;
  ...
}
```

```xml
<resultMap id="sheetResult" type="Sheet">
  <collection property="pools" javaType="java.lang.ArrayList" column="sheetId" ofType="Pool" select="selectPools"/>
</resultMap>

<select id="selectSheet" resultMap="sheetResult">
  SELECT sheet_id sheetId, .... , FROM sheet WHERE sheet_id = #{sheetId}
</select>

<select id="selectPools" resultType="Pool">
  SELECT * FROM pool WHERE sheet_id = #{sheetId}
</select>
```

collection 태그에 javaType으로 ArrayList를 지정해주었고 해당 List의 제네릭 타이을 Pool 로 지정해준 코드이다. 이렇게하면 시험지(sheet)를 조회하면서 시험지에 해당하는 문항(pool)들을 List에 담을 수 있다.

<h2>Reference</h2>

- [Mybatis ResultMap](https://mybatis.github.io/mybatis-3/ko/sqlmap-xml.html)
