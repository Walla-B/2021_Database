#데이터베이스 

DBMS : Data Base Management System

통일한 특징/속성을 가지고 있는 entity, instance들이 모여있는것이 DB

Instance : 고유한 객체

RDBMS : Relational DBMS

학생이라는 DB가 있을떄, 학생의 속성으로는 학년,성적 등이 있으며s



MariaDB (on WSL2 Ubuntu)

셸에서 실행시 다음 오류와 함꼐 실행되지 않는 경우가 발생한다.

```
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2)
```
이는 mysql 서버가 자동으로 실행되지 않았기 떄문에 발생하는 오류이므로 다음 명령어를 통해 mysql 서버를 수동으로 실행해 준뒤 실행하면 잘 동작한다.
```
$ sudo /etc/init.d/mysql start
$ sudo mariadb
```

기본 사용법

[SQL  Documentation](https://www.w3schools.com/sql/sql_syntax.asp)

모든 명령의 단위는 ;로 끝나게 되며, 이떄 ;가 입력되지 않았다면
아랫줄에 계속해서 -> 표시로 명령이 입력중임을 나타내게 된다.

1. 기존 데이터베이스 목록 출력  : 
   ```sql
   SHOW DATABASE; //모든 데이터베이스 출력
   ```

2. 데이터베이스 만들기 :
   ```sql
   CREATE DATABASE database_name;
   ```
3. 데이터베이스 선택  : 
   ```sql
   USE database_name; //위의 데이터베이스 목록에서 데이터베이스 목록을 출력하게 된다.
   ```
   데이터베이스에서 '나간다' 라는 개념이 아닌, 위 명령어를 통해 데이터베이스들을 선택하여 사용하게 된다
4. (데이터베이스 선택 후) 테이블 생성  : 
   ```sql
   CREATE TABLE table_name ( field_name DOMAIN(LENGHT))

   //예시
   CREATE TABLE students ( sid CHAR(20), name CHAR(20), age INTEGER, gpa REAL );
   ```

5. (데이터베이스 선택 후) 테이블 목록 출력  : 
   ```sql
   SHOW TABLES;
   ```

6. (데이터베이스 선택 후) 테이블 전체 출력 : 
   ```sql
   SELECT * FROM table_name;
   ```
   
7. (데이터베이스 선택 후) 테이블에 인스턴스 삽입: 
   ```sql
   INSERT INTO table_name
   VALUES ( 'non-integer_values', integer_value);
   // 모든 정수형 타입이 아닌 타입들은 aphostropies 안에 들어가 있어야 함을 명심하자.
   ```
8. (데이터베이스 선택 후) 테이블에서 인스턴스 삭제: 
   ```sql
   DELETE FROM table_name instance_var
   WHERE instance_var.instance_attribute = something;
   // 위 질의문은 어떤 인스턴스의 속성을 규정해 해당 조건에 부합하는 인스턴스들을 삭제한다.
   ```
9. 테이블 구조 보기:
   ```sql
   DESC table_name; // Describe
   ```
10. 데이터베이스 삭제 :
    ```sql
    DROP DATABASE database_name;
    ```
11. 테이블 삭제 :
    ```sql
    DROP TABLE table_name;
    ```
12. 테이블 열 추가/삭제 :
    ```sql
    ALTER TABLE table_name
    ADD column_name data_type,
    DROP COLUMN comlun_name;
    ```

```sql
INSERT INTO Employees
VALUES 
('10001','Bryan','120000'),
('10002','Joe','80000'),
('10003','Jack','200000'),
('10004','James','75000'),
('10005','Charlie','230000');
```
```sql
INSERT INTO Aircraft 
VALUES 
('20001','A380','5000'),
('20002','A390','6000'),
('20003','A747','2000'),
('20004','A130','1500'),
('20005','A242','3400');
```
```sql
INSERT INTO Flights
VALUES
('30001','SEOUL','BUSAN','300','12:00:00','13:00:00'),
('30002','SEOUL','TOKYO','700','13:00:00','15:00:00'),
('30003','GIMPO','BUSAN','270','14:00:00','14:50:00'),
('30004','GIMPO','HONGKONG','820','11:30:00','13:45:00'),
('30005','BUSAN','TOKYO','520','15:30:00','17:45:00');
```
```sql
INSERT INTO Certifies
VALUES
('10001','20002'),
('10003','20003'),
('1005','20005');
```



```sql
//4.5.1
SELECT C.eid
FROM Aircraft A, Certified C
WHERE A.aid = C.aid AND A.aname = ‘Boeing’

//4.5.2
SELECT E.ename
FROM Aircraft A, Certified C, Employees E
WHERE A.aid = C.aid AND A.aname = ‘Boeing’ AND E.eid = C.eid

//4.5.3
SELECT A.aid
FROM Aircraft A, Flights F
WHERE F.from = ‘Bonn’ AND F.to = ‘Madrid’ AND
A.cruisingrange > F.distance

//4.5.4
SELECT E.ename
FROM Aircraft A, Certified C, Employees E, Flights F
WHERE A.aid = C.aid AND E.eid = C.eid AND
distance < cruisingrange AND salary > 100,000

//4.5.5
SELECT E.ename
FROM Certified C, Employees E, Aircraft A
WHERE A.aid = C.aid AND E.eid = C.eid AND A.cruisingrange > 3000
AND E.eid NOT IN ( SELECT C2.eid
FROM Certified C2, Aircraft A2
WHERE C2.aid = A2.aid AND A2.aname = ‘Boeing’ )```