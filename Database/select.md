# SELECT

## 원하는 정보 가져오기

### 테이블의 모든 내용 보기

```sql
SELECT * FROM Customers;
```

### 원하는 열만 골라서 보기

```sql
SELECT 열이름 FROM Customers;

SELECT CustomerName FROM Customers;

-- 테이블의 컬럼이 아니여도 값을 선택할 수 있다.
SELECT CustomerName, 1, '1', NULL FROM Customers;
```

### 원하는 행만 걸러서 보기

**WHERE** 구문 뒤에 조건을 붙여 원하는 데이터만 가져올 수 있다.
**WHERE** 뒤에는 조건이 온다.

```sql
SELECT * FROM Orders
WHERE EmployeeID = 3;
```

### 원하는 순서로 데이터 가져오기

**ORDER BY** 를 사용해서 특정 컬럼 기준으로 데이터를 정렬할 수 있다.

ASC = 오름차순 (기본)
DESC = 내림차순

```sql
SELECT * FROM Customers
ORDER BY ContactName;
```

### 원하는 만큼만 데이터 가져오기

**LIMIT {가져올 갯수}** 또는 **LIMIT {건너뛸 갯수}, {가져올 갯수}**

```sql
-- 데이터를 10개까지만 가져온다.
SELECT * FROM Customers
LIMIT 10;

-- 데이터를 0개 건너뛰고 10개까지 가져온다.
SELECT * FROM Customers
LIMIT 0, 10;

-- 30개 건너뛰고 10개 가져온다.
SELECT * FROM Customers
LIMIT 30, 10;
```

### 원하는 별명으로 데이터 가져오기

**AS**를 사용해서 컬럼명 변경

```sql
SELECT
    CustomerId AS ID,
    CustomerName AS NAME,
    Address AS ADDR
FROM Customers;

-- 한글을 쓸때는 조심해서 사용 (나중에 더 자세히 알아보기)
```

---

## 각종 연산자

### 사칙연산

```sql
SELECT 1 + 2;

SELECT 5 - 2.5 AS DIFFERENCE;
```

결과
![Alt text](<스크린샷 2024-08-14 오후 5.20.24.png>)

```sql
SELECT 3 * (2 + 4) / 2, 'Hello';
```

결과
![Alt text](<스크린샷 2024-08-14 오후 5.20.24-1.png>)

**문자열에 사칙연산을 가하면 0으로 인식한다**

```sql
SELECT 'ABC' + 3;
-- 0 + 3
```

결과
![Alt text](<스크린샷 2024-08-14 오후 5.24.51.png>)

**숫자로 구성된 문자열은 숫자로 자동인식**

```sql
SELECT '1' + '002' + 3;
-- 1 + 2 + 3
```

### 참/거짓 관련 연산자

**TRUE = 1, FALSE = 0**

```sql
SELECT TRUE, FALSE;

SELECT !TRUE, NOT 1, !FALSE, NOT FALSE;
```

결과
![Alt text](<스크린샷 2024-08-14 오후 5.31.39.png>)

연산자

- **IS** = 양쪽이 모두 TRUE 또는 FALSE
- **IS NOT** = 한쪽은 TRUE, 한쪽은 FALSE

```sql
SELECT TRUE IS TRUE;
SELECT TRUE IS NOT FALSE;
SELECT (TRUE IS FALSE) IS NOT TRUE;
```

- **AND, &&** = 양쪽이 모두 TRUE일 때만 TRUE
- **OR, ||** = 한쪽은 TRUE면 TRUE

**MySQL의 기본 사칙연산자는 대소문자 구분을 하지 않는다.**

```sql
SELECT 'A' = 'a';
```

- **BETWEEN** {MIN} **AND** {MAX} = 두 값 사이에 있음
- **NOT BETWEEN** {MIN} **AND** {MAX} = 두 값 사이가 아닌 곳에 있음
