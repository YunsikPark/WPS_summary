# SQL 입문
>SQL은 데이터베이스를 액세스하고 조작하기 위한 표준 언어

## SQL 이란?
* SQL은 구조화 된 쿼리 언어
* SQL을 사용하면 데이터베이스에 액세스하고 조작 할 수 있다.
* SQL은 ANSI (American National Standards Institute) 표준이다.


## SQL은 무엇을 할 수 있는가?

* 데이터베이스에 대해 **쿼리를 실행**
* 데이터베이스에서 **데이터를 검색**
* 데이터베이스에 **레코드를 삽입**
* 데이터베이스의 **레코드를 업데이트**
* 데이터베이스에서 **레코드를 삭제**
* 새로운 데이터 베이스를 **생성**
* 데이터베이스에 새로운 테이블을 생성
* 데이터베이스에 저장 프로시저를 생성
* 데이터베이스에 뷰를 생성
* 테이블, 프로시저 및 뷰에 대한 사용권한 설정

## RDBMS
>RDBMS는 **관계형 데이터베이스 관리 시스템(Relational Database Management System)**의 약자입니다.

* RDBMS는 SQL과 MS SQL Server, IBM DB2, Oracle, MySQL 및 Microsoft Access와 같은 모든 최신 데이터베이스 시스템의 기초
* RDBMS의 데이터는 테이블이라는 데이터베이스 오브젝트에 저장되고, 테이블은 관련 데이터 항목의 모음이며 열과 행으로 구성된다.

```
select * from Customers;
```
# SQL 구문
## 데이터베이스 테이블
* 데이터베이스는 대개 하나 이상의 테이블을 포함한다.
* 각 테이블을 이름(예: "고객" 또는 "주문")으로 식별된다.
* 테이블은 데이터가 있는 레코드(행)를 포함한다.


## SQL 문
>데이터베이스에서 수행해야 하는 대부분의 작업은 SQL 문으로 수행된다.

다음 SQL 문은 "Customers"테이블의 모든 레코드를 선택한다.

```
select * from Customers;

```

## Keep in Mind
* SQL 키워드는 대소문자를 구분하지 않는다.
* select는 SELECT와 같다.

## 가장 중요한 SQL 명령
* SELECT - 데이터베이스에서 데이터를 추출
* UPDATE - 데이터베이서의 데이터를 업데이트
* DELETE - 데이터베이서에서 데이터를 삭제
* INSERT INTO - 새로운 데이터를 데이터베이서에 삽입
* CREATE DATEABASE - 새 데이터베이스를 만듬
* ALTER DATEABASE - 데이터베이스를 수정
* CREATE TABLE - 테이블을 수정
* DROP TABLE - 테이블을 삭제
* CREATE INDEX - 색인 (검색 키)을 생성
* DROP INDEX - 색인을 삭제


# SQL SELECT 문
> SELECT문은 데이터베이스에서 데이터를 선택하는데 사용된다.
> 리턴 된 데이터는 결과-세트(result-set)라고 하는 결과 테이블(result table)에 저장된다.

## SELECT 구문

```
>> SELECT column1, column2, ... FROM table_name;
```

여기에서 column1, column2,...는 데이터를 선택할 테이블의 필드 이름이다. 표에서 사용 가능한 모든 필드를 선택하려면 다음의 구문을 사용한다.

```
>> SELECT * FROM table_name;
```

# SQL SELECT DISTINCT 문

## SQL SELECT DISTINCT 문 
> SELECT DISTINCT는 고유한 (다른) 값만 리턴하는데 사용된다.
> 테이블 내에서 열은 종종 많은 중복 값을 포함한다. 때로는 서로 다른 (뚜렷한) 값만 나열하기를 원할 때가 있다.

## SELECT DISTINCT 구문

```
>> SELECT DISTINCT column1, column2, ... FROM table_name;
```

### DISTINCT 예제

```
# Customers 테이블의 "Country"열에서 DISTINCT 값만 선택

SELECT DISTINCT Country FROM Customers;



# 서로 다른 (별개의) 고객 국가의 수를 나열

SELECT COUNT(DISTINCT Country) FROM Customers;

```

#### MS Access

```
SELECT Count(*) AS DistinctCountries
FROM (SELECT DISTINCT Country FROM Customers);

```

