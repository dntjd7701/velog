### 👏 procedure ? 
>  **일련의 쿼리를 마치 하나의 함수처럼 실행하기 위한 쿼리의 집합**
> 
_A stored procedure is a prepared SQL code that you can save, so the code can be reused over and over again.
So if you have an SQL query that you write over and over again, save it as a stored procedure, and then just call it to execute it.
You can also pass parameters to a stored procedure, so that the stored procedure can act based on the parameter value(s) that is passed._

--- 
### 🎶 장/단점


#### 😉장점 

1. 하나의 요청으로 여러 SQL문을 실행 할 수 있다. (네트워크에 대한 부하를 줄일 수 있다.)
2. 미리 구문 분석 및 내부 중간 코드로 변환을 끝내야 하므로 처리 시간이 줄어든다.
3. 데이터베이스 트리거와 결합하여 복잡한 규칙에 의한 데이터의 참조무결성 유지가 가능하게 된다. 간단히 말하면 응용 프로그램 측 로직을 가지지 않고도 데이터베이스의 데이터 앞뒤가 맞게 될 수 있다.
4. JAVA 등의 호스트 언어와 SQL 문장이 확실하게 분리된 소스 코드의 전망이 좋아지는 것, 또한 웹사이트 등 운용 중에도 저장프로시저의 교체에 의한 수정이 가능하기 때문에 보수성이 뛰어나다.
5. 자주 사용되는 일반적인 쿼리를 모듈화 시켜 필요할 때만 호출하면 편리하다. 
6. 내가 필요한 만큼 응용해서 사용할 수 있기 때문에 MySQL 운영에 편리하다.

#### 😂단점

1. 유지 보수 복잡성이 증가한다.
2. 각 기능을 담당하는 프로그램 코드가 분산되어 관리하기 때문에 애플리케이션의 설치/배포가 더 복잡해진다. -> 적절한 사용이 요구된다.

---
### 🙌 사용 방법  

> 기본 문법

```sql 
CREATE PROCEDURE procedure_name
AS
sql_statement
GO;
```

> 실행

```sql
EXEC SelectAllCustomers;
```

> 파라미터가 있는 경우 

```sql 
CREATE PROCEDURE SelectAllCustomers @City nvarchar(30), @PostalCode nvarchar(10)
AS
SELECT * FROM Customers WHERE City = @City AND PostalCode = @PostalCode
GO;


EXEC SelectAllCustomers @City = 'London', @PostalCode = 'WA1 1DP';

```
---
#### ✔ 참고
[wiki](https://ko.wikipedia.org/wiki/%EC%A0%80%EC%9E%A5_%ED%94%84%EB%A1%9C%EC%8B%9C%EC%A0%80)
[W3Schools](https://www.w3schools.com/sql/sql_stored_procedures.asp)

