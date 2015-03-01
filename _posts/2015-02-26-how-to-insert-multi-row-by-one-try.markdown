---
layout: post
title:  "DB - INSERT INTO SELECT"
categories: Database
---

<h3>서론</h3>
- 운영 업무를 하다가 간혹 생기는 일인것 같으면서 자주 생기는 일인데 업무담당자의 실수 혹은 다른 시스템 외부적인 문제로 데이터를 수작업으로 입력해야 하는 상황이 생긴다. 이때 프로세스를 전단계로 돌려서 업무담당자로 하여금 재작업하게 하던가 이미 시스템에 간단히 데이터를 수정할 수 있는 관리자 메뉴가 있다면 작업소요가 크지 않겠지만, 프로세스를 전 단계로 돌리기 난해한 상황이거나 잘마련된 관리자 시스템이 없는데 시스템을 만들자니 코딩 소요도 분명 조금이지만 있을것이고 운영서버에 배포까지 해야하기 때문에 긴급한 요청이라면 시스템을 수정하는건 어렵다. 그러면 결국 이걸 다 데이터베이스 일일히 INSERT를 해야하나하고 미간에 주름이 잡히기 마련이다. 절대 어려운건 아니지만 귀찮고 아트하지 못하다. 나 역시 그랬으며 개발자는 보통 이런상황을 가장 싫어할거라 믿어 의심치 않는다.

<h3>본론</h3>
- 최근에 나에게도 이런 상황이 발생하였는데 당시의 상황은 이렇다
    1. 몇단계에 걸쳐서 프로세스가 진행되는 시스템인데 각 단계마다 입력해야할 값은 동일하다.
    2. 단계는 A단계까지만 진행된 상태이며 요청자는 A단계 데이터를 특정 몇개의 필드를 제외하고는 추후 단계에 동일하게 입력하고 싶어한다. 
- 그렇다면 A단계까지 입력된 정보를 이용해서 INSERT 작업을 그나마 간소화 하기 위한 방법은 뭐가 있을까
- 이미 입력된 여러행의 데이터를 한번의 쿼리로 INSERT 가능하게 하는 SQL 에서 제공되는 INSERT INTO SELECT 에 대해서 소개한다.
- 기본 구문은 다음과 같다.

```sql
INSERT INTO table_name SELECT * FROM table_name WHERE target_id = ?
```

- 위에서 언급한 상황에서의 해결은 다음과 같이 컬럼명을 나열해주며 해결한다.
- 테이블 스키마에 정의된 컬럼 순서대로 입력을 해줘야 한다.

```java
INSERT INTO table_name SELECT 'noveloper' target_id, target_name, ... FROM table_name WHERE step = 'A' 
```

- 이 구문을 이용하면 같은 테이블이 아닌 곳에서 필요한 키값을 얻어올 수 있다면 그거대로 이용이 가능하다.

```java
INSERT INTO table1 (field1,field3,field9)
SELECT table2.field3,table2.field1,table2.field4
FROM table2;
```

<h3>결론</h3>
비록, 개발자가 INSERT 작업을 해주는건 똑같지만 이 구문을 이용하면 쿼리 한번으로 해결이 가능하기 때문에 작업 소요가 엄청 줄어든것은 분명해서 나름 만족할만한 결과이다. 게다가 수작업이 아닌 시스템에 기능으로 적용하기에도 이 SQL 구문은 굉장히 좋다. 예를들어 특정 기능의 복사 기능을 만들때, 그 기능의 모든 파라미터를 받는게 아닌 해당 데이터의 키값만 받아서 그대로 이 구문을 이용하여 INSERT 하면 가장 아트한 복사 기능을 만들 수 있다. 


<h3>참고자료</h3>
- [MySql : INSERT INTO SELECT](http://dev.mysql.com/doc/refman/5.7/en/insert-select.html)
- [CUBRID : INSERT INTO SELECT](http://www.cubrid.org/manual/92/ko/sql/query/insert.html)
