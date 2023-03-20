https://hongong.hanbit.co.kr/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-databasedb-dbms-sql%EC%9D%98-%EA%B0%9C%EB%85%90/
DB 동향 랭킹 알기

VO 클래스 : DB테이블의 record를 인스턴스화시킨 클래스

[Web architecture 3티어 구조]

![image](https://user-images.githubusercontent.com/101415950/226226393-17f2af03-2faf-4921-98a7-ad6a1d5e6d18.png)

1. client
요청을 보내는 side
웹 브라우저의 화면이 3티어 구조가 동작하는 시발점

2. middle server
client가 보낸 요청을 처리하는 side 즉 프로그램

client ---(request(HTTP))----> server ----(JDBC)-----> DB

controller가 처리
model이 요청에 따른 값이나 처리된 값을 받아 vo클래스로 정리

3. DB
처리된 데이터가 저장되고 관리되는 장소
