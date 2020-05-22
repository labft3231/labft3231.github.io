---
layout: post
title:  "🏄‍♂️ UiPath On-Premise Orchestrator 서버 설치-2"
subtitle: "Database 설정" 
date:   2020-04-08 22:43:55 +0900
categories: rpa update
author: labft3231
header-img: 'public/image/title/orchestrator_background.png'
header-mask: true
tags:
    - RPA
    - UiPath
    - Orchestrator
    - Kibana
    - Elastic Search
---

<br>

## Mssql 설치
사진 하단 첨부된 link에서 *Expresss* 설치 
![mssql Express](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/mssql.JPG?raw=true)
<https://www.microsoft.com/ko-kr/sql-server/sql-server-downloads>

<br>
<br>

## SSMS 설치
설치가 완료되었다면 이제 Mysql의 workbench와 같은 Mssql의 *SSMS* 를 설치를 시작합니다.

서버를 설치한 후 나오는 SSMS 설치하기 버튼을 누르거나 

<https://docs.microsoft.com/ko-kr/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver15&viewFallbackFrom=sql-server-ver15> 에서 설치 가능합니다.

<br>
<br>

## DB 설정
Mssql과 SSMS를 설치한 후에는 Orchestrator에서 사용할 `데이터베이스`와 이를 사용할 `user`를 생성해줘야합니다.

데이터베이스와 User를 생성하기 위해 SSMS을 실행합니다. 

![mssql login](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/db1.jpg?raw=true)


>> 현재 Authentication이 windows Auth로 설정이 되어있습니다. 아직 login할 user가 없기 때문에 이렇게 로그인합니다. 
>> server name은 그냥 기본값으로 로그인 하면 되겠습니다. *추후에 도메인명이나 ip로 외부 포트에서 접속 가능하게 만들수도 있습니다.*
>> 현재 SSMS 접속은 windows auth으로 했지만 windows auth 정보는 가변적이기 때문에 Orchestrator에서의 DB 접근을 위해 User를 따로 만들어야합니다.

<br>
<br>

## User 만들기


좌측 Object Exploer에서 Security 항목의 logins에서 우클릭 하여 New Login을 생성할 수 있습니다.

![create user](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/db3.JPG?raw=true)

>> 체크된 것들을 설정합니다. 
>> SQL Server authentucation을 선택하고 Login name과 비밀번호를 지정합니다.
>> 체크박스에서 다음 로그인때 비밀번호 변경은 해제합니다. 그리고 OK 버튼 클릭


그럼 유저만들기는 성공했네요 

<br>
<br>

## 데이터베이스 생성

테이블 설정은 위에서 보았던 Security 위에 Database에서 할수 있습니다. Database에서 우클릭 후 New Databases를 생성해보겠습니다.
![create database](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/db4.JPG?raw=true)

Database 이름을 입력하면 밑에 있는 데이터 베이스 file이름이 자동으로 변경됩니다. 
Database 이름은 UiPath로 지정합니다. 
이름 변경 후 해당 데이터베이스의 Owner를 설정해야합니다.
사진에서 보여지는 체크버튼쪽의 ...을 클릭하여 위에서 생성했던 Login name을 찾아 설정해줍니다.

##### Collection 부분은 생략 가능합니다.
이대로 DB를 생성을 해도 되지만 데이터베이스의 Collection 설정을 바꾸는게 좋습니다. 
Select a page의 Options에 들어가 Collection을 설정합니다. 한글 사용의 경우 보통 *Korean_Wansung_CI_AS* 을 많이 사용하며 *SQL_Latin1_General_CP1_CI_AS* 도 많이 쓰이는거 같습니다.


그럼 데이터베이스와 유저를 만들고 데이터베이스를 만들어 유저 권한을 주는 작업까지 완료했네요
다음 내용은 생성한 유저 이름으로 DB 접속을 하기 위한 내용입니다.


<br>
<br>

### 이제 Windows Authentication 방식의 로그인을 변경해줘야합니다. 

![change login](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/db5.JPG?raw=true)

<br>

위와 같이 이동하여 *SQL Server and Window Authentication mode*를 선택하고 OK

![change login2](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/db6.JPG?raw=true)

<br>
<br>

## Mssql 서버를 재실행
설정이 끝났습니다. 적용하려면 Mssql 서버를 재실행 해줘야 합니다.
재실행 방법은 작업관리자 서비스에서 MSSQLSERVER를 찾아서 우클릭하여 다시 시작해주시면 됩니다.

![reset mssql](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/db7.JPG?raw=true)


##### 서버가 다시 시작되면서 Auth 환경이 저장되고 Install 다음으로 넘어갈수 있습니다.

<br>

##### 다음편에 계속 이어서 쓰겠습니다. 

<br>
<br>


