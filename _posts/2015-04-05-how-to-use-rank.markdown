---
layout: post
title:  SQL - Rank 함수
categories: Database
---


거의 모든 업무에서 사용될 것 같은 기능은 '정렬' 이다. 대표적인 정렬 알고리즘들이 있지만 여전히 각각의 특정 데이터에 '순위'를 부여하여 정렬하는것은 꽤나 골치아픈 작업이다. 좋은 Ranking 알고리즘을 찾지 못한 사람은 코드단에서 어느 정도 귀찮은 작업을 해야 할 것이다.


<h2>RANK 함수</h2>
ANSI 표준 SQL에서 정의된 RANK 함수가 있다. RANK 함수는 레코드단위로 특정 컬럼에대한 순위를 1부터 순차적으로 부여하고 같은 값에 대해서는 동일한 순위를 부여한다. 동일한 순위가 있을 경우에 하위 순위는 동일순위의 개수를 더한 다음 순위이다. 

```sql
----------------------
1
1
3
4
5
5
5
8
----------------------
```

RANK 함수의 문법은 다음과 같다.

```sql
SELECT 
  user_id
  , point
  , RANK() OVER (ORDER BY point DESC) AS point_rank
FROM 
  point_user
```

이 질의는 포인트와 아이디를 갖고있는 point_user라는 테이블에서 포인트가 많은 사람을 순위별로 정렬하는 질의이다.
얼핏보면 어렵지만 우리가 잘알고있는 ORDER BY 절을 보면 point로 내림차순한다는 것을 알 수 있다.
그렇다면 이번에 사용자가 포인트를 사용한 이력이 담긴 point_use_his 란 테이블이 있다고 하면 여기서 각 사용자별로 포인트를 가장 많이 쓴 날을 조회해야한다면 어떨까?

```sql 
SELECT
  user_id
  , use_point
  , use_date
  , RANK() OVER (PARTITION BY user_id ORDER BY use_point DESC) AS point_use_rank
FROM
  point_use_his
```

```
// 결과
noveloper 3000  2015/04/02  1
noveloper 2000  2015/04/03  2
noveloper 1000  2015/03/23  3
```

PARTITION BY 절을 이용하면 PARTITION BY에 사용된 컬럼을 기준으로 개별로 순위를 부여하게 된다. 

문법을 정리해보면 
- OVER는 필수요소이다.
- ORDER BY 필수요소이며 이 절에 사용되는 컬럼이 순위를 부여하는 기준이 된다.
- PARTITION BY 는 선택요소이며 이 절에 사용되는 컬럼을 기준으로 개별적으로 순위를 부여하게 된다.



<h2>Conclusion</h2>
업무에 당장 투입되고 보았던 SQL질의문에서 RANK 함수가 빈번하게 사용된다는 것을 알았다. 기존에 있던 질의들을 잘 이해할 수 없었는데 알고나니 생각보다 어려운 질의문이 아니었다는 생각이 들고 앞으로도 자주 써먹을 것 같다는 강한 느낌을 받았다. 



<h2>Reference</h2>
- [Oracle - Rank](http://docs.oracle.com/cd/B19306_01/server.102/b14200/functions123.htm)
- [Mssql - Rank](https://msdn.microsoft.com/ko-kr/library/ms176102.aspx)
- [Cubrid - Rank](http://www.cubrid.org/ko_manual90/entry/RANK%20%ED%95%A8%EC%88%98)
