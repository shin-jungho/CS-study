# RDB (Relational Database)
구성된 테이블이 다른 테이블과 관계를 맺고 모여있는 집합체

- 관계를 나타내기 위해 <b><span style="blue">외래키(foreign key)</span></b>를 사용
- 테이블간의 관계에서 외래키를 이용해 테이블간 <b><span style="blue">Join</span></b>이 가능

### DBMS (Database Management System)
사용자와 db 사이에서 사용자의 요구에 따라 정보를 생성해주고 db를 관리해주는 소프트웨어

### RDBMS (Relational Database Management System)
사용자의 요구에 따라 정보를 생성해 관계형 db을 생성, 수정, 관리 할 수 있는 소프트웨어

### SQL (Structured Query Language)
RDBMS의 데이터를 관리하기 위해 설계된 프로그래밍 언어 <br>
db 스키마 생성과 수정을 위해 고안됨
<br>
ex) mysql, oracle etc..

> <b>스키마</b>
> <br>db에 저장되는 데이터 구조와 제약조건 정의
> <br> ex) 스키마 : db : 테이블 = 평면도: 집 : 방


# NoSQL (Not Only SQL)
SQL을 사용하지 않는 데이터베이스 관리 시스템을 지칭하는 단어 <br>
RDB 형태가 아닌 다른 형태의 데이터 저장 <br>
ex) mongoDB, Redis etc...

- <b><span style= "blue">테이블 간 관계를 정의하지 않음</span></b>
- 테이블 간의 관계를 정하지않아 Join도 불가능
- 여러 데이터에 분산해 저장하는 방식


|구분|NoSQL|RDBMS|
|---|---|---|
|장단점|데이터 무결성,<br> 정합성 보장 x,<br> 반정형 데이터 처리|데이터 무결성 보장, <br> 정규화된 데이터 처리, <br> 확장성 이슈|
|특징|일관성 x,<br> 변경에 용이|Join 가능, <br> ACID|
|사용케이스|대량 데이터 처리, <br> 빠른성능 요구|중요 트렌젝션처리 요구될 때|


## 📓 요약
🅐RDB(관계형 데이터베이스)를 🅑RDBMS(데이터베이스를 관리)로 생성하고 수정하고 관리 <br>
🅒SQL은 RDBMS를 관리하기 위해 설계된 특수 목적의 프로그래밍 언어이고,<br>

🅓NOSQL(비관계형 데이터베이스)는 RDB 형태의 관계형 데이터베이스가 아닌 다른 형태의 데이터 저장방식.