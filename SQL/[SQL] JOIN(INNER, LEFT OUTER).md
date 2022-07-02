> JOIN 정리

<img src="http://3.bp.blogspot.com/-jEXZZAq_FY8/VIfXun7s2rI/AAAAAAAAAIY/qyb2hMyEwOo/s1600/LEFT%2Bvs%2BRight%2BOuter%2BJoin%2Bin%2BSQL.png" witdh="10%" height="10%">


## INDEX
- 조인(Join)이란?
- 조인의 목적
- 조인(INNER/LEFT)
- 조인의 사용 예시 

## JOIN 이란?

<span style="background-color: rgba(242,179,188,0.5)">조인(JOIN) 또는 결합 구문 : DB 내의 여러 테이블의 레코드를 조합하여 하나의 열로 표현한 것 </span>


- <span style="color: red">즉, 조인이란 두 개 이상의 테이블을 서로 묶어 하나의 결과 집합을 만들어 내는 것을 말한다.</span> 따라서 조인은 테이블로서 저장되거나, 그 자체로 이용할 수 있는 결과 셋을 만들어 낸다.

> ANSI 표준 SQL 유형

- INNER JOIN
- OUTER JOIN
- LEFT JOIN
- OUTER JOIN
- 특별한 경우 테이블(기본 테이블, 뷰 또는 조인된 테이블)은 자기 자신에게 JOIN 할 수 있다. 


## 조인의 목적

 SQL JOIN은 기본적으로 RDB(관계형 데이터베이스)의 본질적인 기능을 가진 핵심 SQL명령어이다. 관계형 데이터베이스에서는 중복된 데이터를 피하기 위해 데이터를 쪼개 여러 테이블로 나눠 저장한다. 이렇게 분리되어 저장된 데이터에서 원하는 결과셋을 얻기 위해서는 다시 테이블을 조합하여 결과를 추출할 필요가 있다. JOIN은 이러한 배경에서 각 테이블을 적절하게 조합하여 결과를 도출하기 위한 SQL 명령어이다. **<span style="color: red">즉, 조인은 독립된 객체 테이블 혹은 집합객체를 상호연관성에 의해 연결하게 만들어 하나의 결과 셋을 보여주는 명령어이다.</span>** 


## 조인(INNER/LEFT)
> 예시를 위한 예제 테이블

![](https://images.velog.io/images/dntjd7701/post/2cf73d5f-46d2-4d83-a962-f7e9e5152bd1/%ED%99%94%EB%A9%B4%20%EC%BA%A1%EC%B2%98%202021-12-28%20101232.png)

[DDL 쿼리 참조(WIKI)](https://ko.wikipedia.org/wiki/Join_(SQL))

---
### 내부 조인(INNER JOIN)
![](https://images.velog.io/images/dntjd7701/post/d48333a6-10c3-4a88-bbcc-f61bececfb5d/image.png)

>**기준 테이블과 조인 테이블에 조건을 만족하는 값이 모두 존재하는 경우의 데이터만 조회** 

---

- LEFT JOIN과 더불어 가장 흔한 결합 방식
- 2개 이상의 테이블의 컬럼 값을 결합함으로써 새로운 결과 테이블 반환
- ON절의 조건을 충족하는 모든 결과 열을 찾기 위해 각 테이블의 조인 대상과 비교 진행
- 조인 구문 충족시 일치된 각 열의 컬럼 값은 결과 열로 결합(조인 테이블 각각의 모든 레코드 결합)

> 조인문은 테이블의 존재하는 모든 레코드의 최초 곱집합의 결과값에서 조인 구문을 충족시키는 모든 레코드 값을 반환한다. 실제 SQL의 실행에서 보통 곱집합의 연산은 매우 비효율적이므로 실행 가능한 **해시 조인** 혹은 **소트-머지 조인**과 같은 다른 접근법을 사용한다.
[해시 조인](http://wiki.gurubee.net/pages/viewpage.action?pageId=26740416)
[소트 머지 조인](http://wiki.gurubee.net/pages/viewpage.action?pageId=26740413)


>** Explicit ex **
```sql
SELECT *
FROM employee INNER JOIN department
  ON employee.DepartmentID = department.DepartmentID;
```

> Implicit ex
```sql
SELECT *
FROM employee, department
WHERE employee.DepartmentID = department.DepartmentID;
```

> using 
```sql
SELECT *
FROM employee INNER JOIN department
USING (DepartmentID);
```

> Result![](https://images.velog.io/images/dntjd7701/post/829fd932-428a-4428-aa4c-ffc40d6719ff/image.png)
_조인 조건에서 명시적으로 IS NULL 또는 IS NOT NULL과 같은 구문을 사용하지 않는다면 NULL은 어떠한 값도 일치하지 않으므로(NULL 자체 포함) NULL값은 포함되지 않는다._ 이와 같은 문제를 해결하기 위해 **외부 조인**을 사용할 수 있다.


### 외부 조인(OUTER JOIN)

![](https://images.velog.io/images/dntjd7701/post/961fc2eb-ffc9-4493-b27a-98eafb4de636/image.png)
- **LEFT OUTER JOIN**
- RIGTH OUTER JOIN
- FULL OUTER JOIN

> **기존 테이블을 기준으로 조인 테이블에 데이터가 존재하지 않더라도 기준 테이블의 모든 데이터가 조회되고, 데이터가 존재할 경우 해당 데이터를 참조할 수 있다.**

---

- **기준 테이블의 데이터를 누락 없이 모두 조회하고 참조 테이블의 값이 있을 경우 해당 값을 사용하기 위해서 사용한다. **
- LEFT JOIN, 왼쪽(먼저 나타나는)  테이블에서 조인 조건에 맞지 않는 모든 행을 결과 집합에 포함시키고 내부 조인에서 반환된 모든 행과 오른쪽 테이블의 출력 열을 NULL로 설정하도록 지정한다.
- RIGHT JOIN, 오른쪽(나중에 나타나는) 테이블에서 조인 조건에 맞지 않는 모든 행을 결과 집합에 포함하고 내부 조인에서 반환된 모든 행과 다른 테이블에 해당되는 출력 열을 NULL로 설정하도록 지정한다.
- FULL JOIN, 조인 조건에 맞지 않는 왼쪽 또는 오른쪽 테이블의 행을 결과 집합에 포함시키고 다른 테이블에 해당되는 출력 열을 NULL로 설정하도록 지정한다. 여기에는 INNER JOIN에서 일반적으로 반환되는 모든 행도 포함된다.

---
> INTERSECT
```sql
SELECT * FROM TableA INTERSET SELECT * FROM TableB
```
- 교집합 개념

> EXCEPT
```sql
SELECT * FROM TableA EXCEPT SELECT * FROM TableB
```
- 차집합 개념

	Table A와 Table B의 컬럼의 갯수와 순서가 동일해야 하며 
    각 상호 비교되는 컬럼들의 데이터 형식이 호환이여야한다.

---


### 조인의 사용 예시 (INNER, LEFT)

> **성능 향상을 위한 조인문(JOIN과 LEFT OUTER JOIN)**

- 조인을 사용하는 경우 INNER JOIN을 되도록 사용한다. 
	- 동일한 효과를 가지는 쿼리를 작성할 경우  LEFT OUTER JOIN의 습관적 사용보단 INNER JOIN을 사용하는 것이 속도 측면에서 효과적이다.

- 서브쿼리를 통해 필요 컬럼과 조인에 필요한 컬럼을 뽑아 사용하고, where 절과 group by를 통해 불러오는 데이터양을 감소시킬 수도 있다. 

> 예시
```sql
SELECT
     TblA.A
    ,TblB.B   
    ,TblC.B
FROM
    tbl_A TblA   
    LEFT OUTER JOIN tbl_B TblB    
            ON TblB.join_value = TblA.join_value
    LEFT OUTER JOIN tbl_C TblC
            ON TblC.join_value = TblA.join_value
```
> 다중 테이블을 사용할 경우 위와 같은 방법은 모든 테이블의 모든 컬럼과 모든 데이터들을 전부 조회하기 때문에 속도 측면에서 떨어진다.
```sql
SELECT
     TblA.A
    ,TblB.B
    ,TblC.C
FROM
    (SELECT  A ,join_value   FROM  tbl_A  )   TblA   
LEFT OUTER JOIN 
    (SELECT  B ,join_value   FROM  tbl_B  )   TblB    
        ON TblB.join_value = TblA.join_value
LEFT OUTER JOIN 
    (SELECT  C ,join_value   FROM  tbl_C  )   TblC
        ON TblC.join_value = TblA.join_value
```
위와 같이 서브쿼리를 통해 필요 컬럼과 조인에 필요한 컬럼을 뽑아 사용하고, where 절과 group by를 통해 불러오는 데이터양을 감소시킬 수도 있다. 

---

#### INNER JOIN

[INNER JOIN EX1](https://www.w3schools.com/sql/sql_join_inner.asp)
[INNER JOIN EX2
](https://www.mysqltutorial.org/mysql-inner-join.aspx)

> **with GROUP BY** 
![](https://images.velog.io/images/dntjd7701/post/6b2ea377-b585-4b83-8080-71b8cca62d28/image.png)
```sql
SELECT 
    t1.orderNumber,
    t1.status,
    SUM(quantityOrdered * priceEach) total
FROM
    orders t1
INNER JOIN orderdetails t2 
    ON t1.orderNumber = t2.orderNumber
GROUP BY orderNumber;
```
- order number, order status, total sales 반환
- 조인을 위한 조건으로 각 테이블의 pk값인 orderNumber사용
- orders 테이블을 기준으로 조인하여 orderdetails의 quantityOrdered와 priceEach 컬럼을 이용
- GROUP BY 절을 통해 orderNumber로 그룹을 짓고, SUM 집계함수를 이용해 (quantityOrdered * priceEach)값을 각 그룹마다 각자 더해 total이라는 컬럼으로 반환한다. 
- 결과
![](https://images.velog.io/images/dntjd7701/post/941797bf-747d-45f5-826f-a9dd3b985e82/image.png)


> **Using other operators**
![](https://images.velog.io/images/dntjd7701/post/f2867aad-f9d8-4e48-aea5-f73839766b20/image.png)
```sql
SELECT 
    orderNumber, 
    productName, 
    msrp, 
    priceEach
FROM
    products p
INNER JOIN orderdetails o 
   ON p.productcode = o.productcode
      AND p.msrp > o.priceEach
WHERE
    p.productcode = 'S10_1678';
```
- 다양한 operators 사용이 가능하다.
- 각 테이블의 pk값이 productCode로 조인을 하고, productCode가 같으면서 products 테이블의 MSRP컬럼이 orderdetails의 priceEach값보다 큰 컬럼만 가져온다.
- 위의 결과로 나온 테이블 중 Where조건의 productcode값이 'S10_1678'인 컬럼만 반환한다.
- 결과
![](https://images.velog.io/images/dntjd7701/post/54f17d40-aa9f-4e03-bd2c-c5e3faa155f7/image.png)


#### LEFT OUTER JOIN

[LEFT OUTER JOIN EX1](https://www.w3schools.com/sql/sql_join_left.asp)
[LEFT OUTER JOIN EX2](https://www.mysqltutorial.org/mysql-left-join.aspx)


> **Find unmatched rows**
![](https://images.velog.io/images/dntjd7701/post/846c38bf-47ab-4a5a-948c-03b0126f690c/image.png)
```sql
SELECT 
    c.customerNumber, 
    c.customerName, 
    o.orderNumber, 
    o.status
FROM
    customers c
LEFT OUTER JOIN orders o 
    ON c.customerNumber = o.customerNumber
WHERE
    orderNumber IS NULL;
```
- LEFT OUTER JOIN은 한 테이블을 기준으로 매치되지 않는 다른 테이블을 찾는데에 매우 유용하다.
- 위와 같이 customer 테이블을 기준으로 orderNumber가 없는 즉, 주문하지 않은 고객들에 대한 데이터 정보를 쉽게 추출할 수 있다. 
- 이는 기준 테이블을 기준으로 조건에 일치하는 조인된 테이블의 데이터와 일치되지 않는 데이터를 NULL로써 가져올 수 있기 때문이다.
- 결과 
![](https://images.velog.io/images/dntjd7701/post/c52318f8-901f-4ca4-a54e-8f0aa23bdb0d/image.png)


> **WHERE vs ON**
![](https://images.velog.io/images/dntjd7701/post/0b93a271-2f04-4542-989d-8e20ec1973b2/image.png)
- WHERE
```sql
SELECT 
    o.orderNumber, 
    customerNumber, 
    productCode
FROM
    orders o
LEFT JOIN orderDetails 
    USING (orderNumber)
WHERE
    orderNumber = 10123;
```
![](https://images.velog.io/images/dntjd7701/post/b1724d91-81e0-4c8c-819f-2d6c2636aaf0/image.png)
- ON
```sql
SELECT 
    o.orderNumber, 
    customerNumber, 
    productCode
FROM
    orders o
LEFT JOIN orderDetails d 
    ON o.orderNumber = d.orderNumber AND 
       o.orderNumber = 10123;
```
![](https://images.velog.io/images/dntjd7701/post/0c3a4118-0ba4-42e0-a2c7-923b3e027694/image.png)
- Where절을 사용한 첫번째 쿼리의 경우 조인된 테이블에서 Where조건에 맞는 테이블을 다시 추출하여 반환한다. 즉, orders, orderDetails 테이블에서 orders을 기준으로 조인된 테이블의 결과값에서 Where절의 조건을 통해 필터링을 거쳐 최종 결과값을 추출한다.ㅣ
- ON절에서 사용한 쿼리의 경우 조금 다른 결과값을 반환한다. 이는 조인 조건이 마무리되고 그 다음 필터링되듯 Where조건이 처리되는 방식이 아닌 조인 조건 자체에 포함되어있으므로 기준 테이블을 기준으로 orderNumber값이 같고, orderNumber값이 '10123'인 테이블만 값을 가지게 된다. 그 외의 테이블은 기준 테이블은 모두 나오되, 조인된 컬럼 부분의 경우는 NULL값으로 채워져 추출되게 된다. 
- INNER JOIN의 경우엔 ON절과 WHERE절의 조건에 의한 결과값이 동일하다.



---
> <span style="color: red">주의</span>
USING의 경우 조인하는 각 테이블이 공통으로 가지고 있는 키 컬럼을 통해 조인을 실행하는 하나의 구문이다. 하지만, 사용 시 컬럼의 이름이 정확히 일치해야하고, 이로 인한 alias의 사용 등 쿼리의 작성에 불편한 요소가 있어 ANSI표준 JOIN~ON의 형식으로 사용하는 것을 권장한다.

