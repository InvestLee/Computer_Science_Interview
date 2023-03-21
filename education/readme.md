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

-- EMP 테이블에서 어떤 부서번호가 있는지를 검색....
-- 중복을 없애고 정렬된 값으로
-- DISTINCT는 10g 버전부터 정렬이 기본으로 안들어가 있음
SELECT DISTINCT DEPTNO 
FROM EMP
ORDER BY DEPTNO;

-- DISTINCT는 성능을 많이 잡아먹어서 EXISTS로 대체하거나 테이블 최소화 후 수행 권장
SELECT DEPTNO 
FROM DEPT D
WHERE EXISTS
(
 SELECT * 
 FROM EMP E
 WHERE D.DEPTNO = E.DEPTNO
);

-- 연결 연산자 ||
-- 컬럼과 컬럼을 연결 / 컬럼과 문자열 / 문자열과 문자열
-- MySQL 제공 안된...CONCAT()
-- SMITH씨의 월급은 1100달러 입니다.
SELECT ENAME || '씨의 월급은 ' || SAL || '달러 입니다.' 문장 FROM EMP;
```

BETWEEN 200 AND 100 = 200이상 100이하인 수가 없어서 아무것도 검색이 안됨 


```
-- IN 연산자 (비교 연산자 중 하나)
-- <, >, <>, = 

-- STEP1
-- DB서버를 3번이나 찝적거림
SELECT EMPNO, ENAME, JOB, SAL, HIREDATE FROM EMP WHERE EMPNO = 7369; 
SELECT EMPNO, ENAME, JOB, SAL, HIREDATE FROM EMP WHERE EMPNO = 7521; 
SELECT EMPNO, ENAME, JOB, SAL, HIREDATE FROM EMP WHERE EMPNO = 7782; 

-- STEP2
-- OR로 연결
SELECT EMPNO, ENAME, JOB, SAL, HIREDATE
FROM EMP
WHERE EMPNO = 7369 
OR EMPNO = 7521 
OR EMPNO = 7782;

-- STEP3
-- 이를 IN연산자로 한번에 정리 그러므로 IN연산자는 비교 연산자이다.
SELECT EMPNO, ENAME, JOB, SAL, HIREDATE
FROM EMP
WHERE EMPNO IN 
(
 7369, 
 7521, 
 7782
);
```

오라클 테이블은 2차원 구조 = 엑셀 파일의 2차원 구조 => csv파일로 변환한 후 적재하면 처리가 빠름 

```
-- 문자함수
-- CONCAT() :: 문자열 혹은 컬럼 연결, 붙일때 사용
SELECT CONCAT('Good',' Morning') FROM dual;
SELECT CONCAT(ename,JOB) FROM emp;
SELECT ename, JOB, CONCAT(CONCAT(ename, ' is a '), JOB) INFO FROM emp;

-- INITCAP(CHAR)
SELECT INITCAP(ENAME), ENAME, DEPTNO 
FROM EMP
WHERE LOWER(ENAME) = 'scott';

-- SUBSTR('문자열',시작위치,글자수)
-- 음수는 뒤에서 찾음
SELECT SUBSTR('HelloWorld',6) from dual;
SELECT SUBSTR('HelloWorld',6,4) from dual;
SELECT SUBSTR('HelloWorld',-4,2) from dual;

-- emp 테이블에서 사원의 이름이 N으로 끝나는 사원들을 검색
SELECT ENAME, DEPTNO
FROM EMP
WHERE SUBSTR(ENAME,-1) = 'N';

-- 날짜 추출 YEAR(), MONTH(), DAY() X
-- 오라클은 날짜...년,월,일 같은 것들을 "추출"기법으로 리턴
-- EMP테이블에서 년도 2자리만 추출되도록
SELECT ENAME, DEPTNO, CONCAT(SUBSTR(HIREDATE,1,2), '년') 입사년도
FROM EMP;

-- 암시적 형변환 : 날짜와 문자는 상호 호환이 될 때
-- 명시적 형변환 : 날짜와 문자는 상호 호환이 안될 때 직접 변환해줘야 됨
SELECT SYSDATE FROM DUAL;

-- EMP테이블에서 사원의 이름 중에 LL가 포함된 사원을 검색..
-- LIKE, INSTR(특정한 문자열을 못찾으면 0, 찾으면 위치 반환)
SELECT ENAME, DEPTNO, INSTR(ENAME, 'LL')
FROM EMP
--WHERE ENAME LIKE '%LL%'
WHERE INSTR(ENAME, 'LL') > 0;
```

```
SELECT GREATEST(1,2,3) FROM DUAL
UNION ALL
SELECT LEAST(1,2,3) FROM DUAL;

SELECT MAX(SAL) FROM EMP;

-- 지금까지 살아온 일수를 검색
SELECT SYSDATE-(TO_DATE('93/02/16')) FROM DUAL;
SELECT TRUNC(SYSDATE-TO_DATE('93/02/16')) FROM DUAL;

-- 날짜 추출 EXTRACT(년,월,일)
SELECT EXTRACT(YEAR FROM HIREDATE) "Year", 
       EXTRACT(MONTH FROM HIREDATE) "Month", 
       EXTRACT(DAY FROM HIREDATE) "DAY" 
FROM EMP;
```
