---
layout: post
title:  "🚀 UiPath MSSQL 연동 (CRUD)"
subtitle: "MSSQL CRUD 개발"
date:   2020-03-23 21:17:21 +0900
categories: rpa update
author: labft3231
header-img: 'public/image/title/vba_background.jpg'
header-mask: true
published : false
tags:
    - MSSQL
    - UiPath
    - RPA
---
# UiPath MSSQL 연동 (CRUD)

## UiPath MSSQL 연동과 데이터 삽입, 읽기, 수정, 삭제 기능별 Sequance

#### Connetion - 연결
- DatabaseDB 연결 작업을 수행. 
- MSSQL로 지정되어있는데 DB연결 방식이나 다른 DB설정을 원하실때 변경가능. (RDB만 해당)
- 기본적으로 쿼리를 보내기 전에 Connection을 수행해줘야한다.

#### Connetion - 연결해제
- Database 연결 해제를 수행. 
- 기본적으로 DB사용 후 연결을 해제해줘야함.


#### 기본적인 쿼리(query) 필요 - 모든 쿼리(명령어) 실행 전후로 DB Connection과 DB Disconnection이 필요함

#### InsertData(Create)
- Data 삽입
- 원하는 컬럼에 따라 Assign 에서 지정가능
  - Argument값 변경해야함


#### SelectData(Read)
- Query 변경시 데이터 변경 가능
- 해당 예제에서의 output은 현재 xlsx로 나옵니다.(DataTable에서 다양하게 변형가능)


#### UpdateData(Update)
- assign과 argument값 적절하게 변경해야함


#### DeleteData(Delete)
- assign과 argument값 적절하게 변경해야함
