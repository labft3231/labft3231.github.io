---
layout: post
title:  "🌱 UiPath Webhook"
date:   2020-04-03 18:13:11 +0900
categories: rpa update
author: labft3231
background: 'public/image/title/webhooks_background.png'
---

### UiPath Webhook.



1. webhook의 알아보고 싶은 계기

   - log에 따른 트리거 활용
   - 로그를 기록 및 프로젝트 관리

   

2. 삽질 과정 

   - RPA와 최근 go언어를 같이 병행하고 있어서 go언어의 다양한 프레임워크 중에 revel framework을 선택하여 test web 개발 (하지만 webhook에서 로그를 받아오질 못함.)

   - curl을 통해 http request를 날리면 서버는 정상적으로 동작하여 서버는 동작하지만 제대로 된 값이 들어오지 않음

   - 예시 검색하여 github를 통해 node.js 기반의 webhook 서비스 찾아 clone

   - 소스를 보고 rest swagger를 통해 필요한 url과 인자를 확인한 결과 처음 활성화를 위해서 다음 인자를 넣어야함

     [POST] /api/Account/Authenticate 에서 아래의 정보를 보냄
```json
     {
       "tenancyName": "",
       "usernameOrEmailAddress": "",
       "password": ""
     }
```
     

   - 위의 조건에 해당된다고 생각하는 인자들을 설정해봤지만 아래와 같은 에러뜸
```json
     {

     ​	"message":"Invalid credentials, failed to login.",

     ​	"errorCode":1000,

     ​	"resourceIds":null

     }
```
   - request하는 인자가 잘못되었다고 판단하여 다양한 인자를 바꿔가며 줘밨지만 실행되지 않았음

   - 구글링 한 결과 별로 정보가 없었지만 온프레미스 형태여야한다는 말이 있음

   - 일단 온프레미스 형태를 실행 해보기 위해 uipath에 free trial 신청한후 온프레미스 설치했지만. tanant ID설정과 비밀번호 설정이 있어 설정했지만 역시 node에서 실행이 되지 않음

   - orchestrator를 뿐아니라 studio도 엔터프라이즈급으로 신청이 되어야하나 싶어 trial key 발급

   - 발급 받은키로 활성화 하려했지만 라이센스 키가 잘못되었다는 에러가 뜸

   - UiPath에 문의 보냈지만 '-'를 없애고 등록해보라는 연락을 받음

   - 해결 후 알려준다 연락이 왔지만 주말이라 그런지 연락이 끊겼다.

   

3. 예상 

   - 내가 인자 잘못 입력했거나, 온프레미스 환경에서 동작이거나..

   - flask를 활용한 사람은 인자가 아무것도 없는 POST 메소드인데 log가 잘들어온단다.. (https://excelcult.com/2019/10/01/how-to-use-uipath-orchestrator-webhooks/)

   - uipath 온프레미스는 아마 studio에 라이센스 등록하고 cloud.uipath.com에 로봇을 등록하면서 얻은? 인자를 활용

   

4. 결론

   - 로그인이 안되는데 Studio커뮤니티 버전에서는 활성 불가능한지.

   - 아니면 post에 인자는 어떤 값을 어디서 보고 적어야하는지?


     

   

​	



