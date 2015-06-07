---
layout: post
title:  Mybatis - association, collection
categories: spring
---

Database 에서 select 절을 이용해 데이터를 조회할 때 mybatis 의 resultMap 을 이용하면 사용자가 정의한 Model 객체로 값을 직접 받아올 수 있다. 그렇다면 Model 객체안에 멤버변수로 또 다른 Model 객체가 있다면 해당 객체에는 값을 어떻게 집어넣어 줄까?
