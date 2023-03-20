https://hongong.hanbit.co.kr/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-databasedb-dbms-sql%EC%9D%98-%EA%B0%9C%EB%85%90/

DB 동향 랭킹 알기

VO 클래스 : DB테이블의 record를 인스턴스화시킨 클래스

[Web architecture 3티어 구조]

![image](https://user-images.githubusercontent.com/101415950/226226393-17f2af03-2faf-4921-98a7-ad6a1d5e6d18.png)

1. client

요청을 보내는 side

웹 브라우저의 화면이 3티어 구조가 동작하는 시발점

보통 브라우저 화면에서 HTTP를 통해 통신하지만

홈쇼핑일 경우 고객이 휴대폰으로 전화 걸어 회사 내 통신할 경우에도

데이터는 서버 한 곳에 합쳐져야 됨

2. middle server

client가 보낸 요청을 처리하는 side 즉 프로그램

client(인터넷 브라우저) ---(request(HTTP))----> server ----(JDBC)-----> DB
   
핸드폰 ---(request(rmi))----> server ----(JDBC)-----> DB ==> DAO가 다른 디바이스 요청에도 모델링함

controller가 처리

model이 요청에 따른 값이나 처리된 값을 받아 vo클래스로 정리

즉 고객 정보에 모델에 저장되어 DAO 프로그램 함수에 의해 DB에 전송됨

3. DB

처리된 데이터가 저장되고 관리되는 장소


sueupdaum profile image	
강사 하승현
오전 10:44
ALTER SESSION SET “_ORACLE_SCRIPT”=true;

sueupdaum profile image	
강사 하승현
오전 10:49
alter user lotteuser default tablespace users quota unlimited on users;

sueupdaum profile image	
강사 하승현
오전 10:57
#######

SQLPLUS system/system;
ALTER SESSION SET “_ORACLE_SCRIPT”=true;
CREATE USER lotteuser IDENTIFIED BY 1234;
GRANT CONNECT, RESOURCE TO lotteuser; 
alter user lotteuser default tablespace users quota unlimited on users;
CONN lotteuser /1234;
@ C:\경로\emp.sql (바로 엔터)

[DML]

SERVER <---------(SELECT)----------- DB

SERVER --(INSERT, UPDATE, DELETE)--> DB

[DB엔진랭킹]

https://db-engines.com/en/ranking 

추세가 관계형DB에서 비정형DB(DOCUMENT)로 변경되는 추세

파이썬의 장고 프레임워크에 내장된 DB : SQLite

[오라클 실행 순서]

FROM(테이블) ---> WHERE(행 제한) --> SELECT(컬럼 추출) --> ROWNUM --> ORDER BY

[MYSQL]

FROM(테이블) ---> WHERE(행 제한) --> SELECT(컬럼 추출) ---> ORDER BY ---> LIMIT 

```
-- 별칭에 공백, 특수문자, 대소문자 구분시 " "로 쌓여야 한다.
SELECT ENAME, JOB, SAL, SAL*2+100 "인상된 급여"
FROM EMP
ORDER BY "인상된 급여" DESC;

-- EMP 테이블에서 급여를 가장 많이 받는 직원 상위 3명을 검색
SELECT ENAME, JOB, SAL, ROWNUM RANKING, DENSE_RANK() OVER(ORDER BY SAL DESC)
FROM
(
 SELECT ENAME, JOB, SAL
 FROM EMP
 ORDER BY SAL DESC
)
WHERE ROWNUM <= 3;

```
