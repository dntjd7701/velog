### π procedure ? 
>  **μΌλ ¨μ μΏΌλ¦¬λ₯Ό λ§μΉ νλμ ν¨μμ²λΌ μ€ννκΈ° μν μΏΌλ¦¬μ μ§ν©**
> 
_A stored procedure is a prepared SQL code that you can save, so the code can be reused over and over again.
So if you have an SQL query that you write over and over again, save it as a stored procedure, and then just call it to execute it.
You can also pass parameters to a stored procedure, so that the stored procedure can act based on the parameter value(s) that is passed._

--- 
### πΆ μ₯/λ¨μ 


#### πμ₯μ  

1. νλμ μμ²­μΌλ‘ μ¬λ¬ SQLλ¬Έμ μ€ν ν  μ μλ€. (λ€νΈμν¬μ λν λΆνλ₯Ό μ€μΌ μ μλ€.)
2. λ―Έλ¦¬ κ΅¬λ¬Έ λΆμ λ° λ΄λΆ μ€κ° μ½λλ‘ λ³νμ λλ΄μΌ νλ―λ‘ μ²λ¦¬ μκ°μ΄ μ€μ΄λ λ€.
3. λ°μ΄ν°λ² μ΄μ€ νΈλ¦¬κ±°μ κ²°ν©νμ¬ λ³΅μ‘ν κ·μΉμ μν λ°μ΄ν°μ μ°Έμ‘°λ¬΄κ²°μ± μ μ§κ° κ°λ₯νκ² λλ€. κ°λ¨ν λ§νλ©΄ μμ© νλ‘κ·Έλ¨ μΈ‘ λ‘μ§μ κ°μ§μ§ μκ³ λ λ°μ΄ν°λ² μ΄μ€μ λ°μ΄ν° μλ€κ° λ§κ² λ  μ μλ€.
4. JAVA λ±μ νΈμ€νΈ μΈμ΄μ SQL λ¬Έμ₯μ΄ νμ€νκ² λΆλ¦¬λ μμ€ μ½λμ μ λ§μ΄ μ’μμ§λ κ², λν μΉμ¬μ΄νΈ λ± μ΄μ© μ€μλ μ μ₯νλ‘μμ μ κ΅μ²΄μ μν μμ μ΄ κ°λ₯νκΈ° λλ¬Έμ λ³΄μμ±μ΄ λ°μ΄λλ€.
5. μμ£Ό μ¬μ©λλ μΌλ°μ μΈ μΏΌλ¦¬λ₯Ό λͺ¨λν μμΌ νμν  λλ§ νΈμΆνλ©΄ νΈλ¦¬νλ€. 
6. λ΄κ° νμν λ§νΌ μμ©ν΄μ μ¬μ©ν  μ μκΈ° λλ¬Έμ MySQL μ΄μμ νΈλ¦¬νλ€.

#### πλ¨μ 

1. μ μ§ λ³΄μ λ³΅μ‘μ±μ΄ μ¦κ°νλ€.
2. κ° κΈ°λ₯μ λ΄λΉνλ νλ‘κ·Έλ¨ μ½λκ° λΆμ°λμ΄ κ΄λ¦¬νκΈ° λλ¬Έμ μ νλ¦¬μΌμ΄μμ μ€μΉ/λ°°ν¬κ° λ λ³΅μ‘ν΄μ§λ€. -> μ μ ν μ¬μ©μ΄ μκ΅¬λλ€.

---
### π μ¬μ© λ°©λ²  

> κΈ°λ³Έ λ¬Έλ²

```sql 
CREATE PROCEDURE procedure_name
AS
sql_statement
GO;
```

> μ€ν

```sql
EXEC SelectAllCustomers;
```

> νλΌλ―Έν°κ° μλ κ²½μ° 

```sql 
CREATE PROCEDURE SelectAllCustomers @City nvarchar(30), @PostalCode nvarchar(10)
AS
SELECT * FROM Customers WHERE City = @City AND PostalCode = @PostalCode
GO;


EXEC SelectAllCustomers @City = 'London', @PostalCode = 'WA1 1DP';

```
---
#### β μ°Έκ³ 
[wiki](https://ko.wikipedia.org/wiki/%EC%A0%80%EC%9E%A5_%ED%94%84%EB%A1%9C%EC%8B%9C%EC%A0%80)
[W3Schools](https://www.w3schools.com/sql/sql_stored_procedures.asp)

