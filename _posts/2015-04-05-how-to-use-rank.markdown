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

<h2>Reference</h2>
- [Oracle - Rank](http://docs.oracle.com/cd/B19306_01/server.102/b14200/functions123.htm)
- [Mssql - Rank](https://msdn.microsoft.com/ko-kr/library/ms176102.aspx)
- [Cubrid - Rank](http://www.cubrid.org/ko_manual90/entry/RANK%20%ED%95%A8%EC%88%98)
