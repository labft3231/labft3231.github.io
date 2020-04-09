---
layout: post
title:  "UiPath Webhook Auth 문제해결"
date:   2020-04-06 19:10:11 +0900
categories: rpa update
author: labft3231
background: 'public/image/title/webhooks_background.png'
---

### UiPath Webhook 회고

webhook을 하다 막힌 부분이 있어 도움을 청했고, 그 결과 해답을 얻을수 있었다. 



일단 내가 접근하는 방식이 cloud 방식인지 On-Premise 방식인지 구분을 할줄 알아야했다.
  
  
| On-Premise                           | Cloud                                                |
| ------------------------------------ | ---------------------------------------------------- |
| Orchestrator를 다운 받아 설치한 환경 | UiPath에서 제공되는 웹 환경<br /> (cloud.uipath.com) |
  

예상했던 것은 On-premise만 가능한줄 알았는데 Cloud도 가능하다는 이야기 였고, 

Cloud 방식으로 접근했다. 

api의 인증에서 오류가 났었는데 document를 확인한 결과 내가 시도했던 URL과 전혀 다른 URL이라는 것을 알 수 있었다. 

URL을 통해서 또한 인자와 리턴값 모두 달랐다. 
  
  
|        | On-Premise                                                   | Cloud                                                        |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| URL    | {{url}}/api/Account/Authenticate                             | https://account.uipath.com/oauth/token                       |
| Method | POST                                                         | POST                                                         |
| Header | Content-Type:application/json                                | Content-Type:application/json<br />X-UIPATH-TenantName:{{tenantName}} |
| Return | <code>{"usernameOrEmailAddress": "{{usernameOrEmailAddress}}","tenancyName": "{{tenancyName}}","password": "{{password}}"}</code> | <code>{     "grant_type": "refresh_token",     "client_id": "{{clientId}}",     "refresh_token": "{{userKey}}" }</code> |
  

 위와 같이 값을 바꾸어 제대로 값을 받을 수 있었다.

이렇게 삽질을 하는 와중에 좋은 사이트를 찾았다. 

<https://postman.uipath.rocks/?version=latest>

해당 사이트는 언어별로 설정을 변경하여 원하는 환경에서 테스트 및 활용이 가능하게끔 되어있다.





