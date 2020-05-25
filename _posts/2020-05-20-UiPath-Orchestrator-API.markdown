---
layout: post
title:  "🌠 UiPath, Orchestraor API로 Robot 실행하기(Cloud Server)"
subtitle: "Web API로 UiPath 실행하기" 
date:   2020-05-20 23:20:15 +0900
categories: rpa update
author: labft3231
header-img: "public/image/title/rest_background.jpeg"
header-mask: true
hidden: false
published : true
tags:
    - Orchestrator
    - RPA
    - UiPath
---

## Orchestrator API를 쓰는 이유?
Orchestrator는 Cloud 웹 환경이 잘구성되어 있고 App도 따로 구현되어 있어서 사실 현재 사용함에 있어서는 불편함이 없습니다.
하지만 제한적인 기능을 주거나 관리 측면에서 API를 사용하면 더 유용할 것이며, 또 API를 이용하여 개발을 한다면 다른 API나 내가 원하는 기능을 
빠르게 적용하고 활용할 수 있기 때문에 API를 이용해봤습니다. 

> 본 포스팅은 인증부터 Robot 실행까지의 내용이 담겨있습니다.


## Cloud 서버에서 Orchestrator API를 사용하는 이유?
원래 On-premiss 형태에서 개발해보고 싶었지만 현재 On-premise가 만료되어서 Cloud 서버로 실행하였습니다.
인증부분 빼고 나머지 부분이 같기 때문에 인증 부분만 바꿔주면 어디서든 사용가능합니다.




## 순서
1. `POST` Auth - 계정 인증
2. `GET` Account Logical Name - 계정 이름 가져오기
3. `GET` serviceInstanceLogicalName - 서비스명 가져오기
4. `GET` Process Key - 프로세스 Key 가져오기
5. `POST` Robot - 로봇실행하기


로봇을 실행하기 까지 가져와야할 데이터가 많습니다. 인증의 token은 24시간 유지 됩니다. 
사용전에 인증 key를 새로 발급 받는다면 인증시간에 크게 신경 안써도 될거 같아요. 
(보안을 생각한다면 인증서 발급하여 사용하고 바로 지우는게 제일 좋을거 같습니다. 근데 다른사람과 같이 사용한다면 transaction 부분도 생각해줘야겠네여.)

<br>

UiPath Doc에서는 Postman을 사용하는거 같습니다. <br>
(저도 API 테스트 할 때 Postman 써왔는데 insomnia를 쓰고 나서는 insomnia만 쓰게 되네요)
암튼 API만 보내면 되기 때문에 postman, curl, insomnia 아무거나 상관없습니다. 


### 1. Auth - 계정 인증 (Cloud 환경에서의 인증)
- cloud는 인증부분의 base url이 다름

```HTTP
POST /oauth/token HTTP/1.1
Accept: application/json
Host: account.uipath.com/
Content-Type: apllication/json

Reqeust
{
	"grant_type":"refresh_token",
	"client_id":"{{clientId}}",
	"refresh_token":"{{userKey}}"
}

Response
{
  "access_token": "xxxxxxxxxxxxxxxxxxxxx",
  "id_token": "xxxxxxxxxxx",
  "scope": "openid profile email offline_access",
  "expires_in": 86400,
  "token_type": "Bearer"
}
```
> access_token과 id_token 획득

### 2. Account Logical Name - 계정 이름 가져오기
- access_token으로 request 전송

```HTTP
GET /cloudrpa/api/getAccountsForUser HTTP/1.1
Accept: application/json
Host: platform.uipath.com/
Content-Type: apllication/json
Authorization : Bearer {{ access_token }}


Response
{
  "userEmail": "labft3231@gmail.com",
  "accounts": [
    {
      "accountName": "xxx",
      "accountLogicalName": "xx"
    },
    {
      "accountName": "xx",
      "accountLogicalName": "xxx"
    }
  ]
}
```


> accountLogicalName 획득



### 3. serviceInstanceLogicalName - 서비스 이름 가져오기

- accountLogicalName으로 request 전송

```HTTP
GET /cloudrpa/api/account/{{ accountLogicalName }}/getAllServiceInstances HTTP/1.1
Accept: application/json
Host: platform.uipath.com/
Content-Type: apllication/json
Authorization : Bearer {{ access_token }}


Response
{
  [
    {
      "serviceInstanceName": "xx",
      "serviceInstanceLogicalName": "xxx",
      "serviceType": "xxx",
      "serviceUrl": "xxx",
      "serviceState": "ENABLED",
      "userRolesInService": [
        "Administrator"
      ]
    },
  ]
}
```


> serviceInstanceLogicalName 획득


### 4. Process Key - 프로세스 Key 가져오기
- Process key 가져오기

https://platform.uipath.com/

```HTTP
GET /{{ accountLogicalName }}/{{ serviceInstanceLogicalName }}/odata/Releases HTTP/1.1
Accept: application/json
Host: platform.uipath.com/
Content-Type: apllication/json
Authorization : Bearer {{ access_token }}


Response
{
  "@odata.context": "https://platform.uipath.com/xxxx/xxxxxxx/odata/$metadata#Releases",
  "@odata.count": 9,
  "value": [
    {
      "Key": "xxxxx-xx-xx-xx-xxxxxxx",
      "ProcessKey": "xxxxxxx",
      "ProcessVersion": "1.0.3",
      "IsLatestVersion": false,
      "IsProcessDeleted": false,
      "Description": "",
      "Name": "xx_xxxxx",
      "EnvironmentId": xxxx,
      "EnvironmentName": "xxxxx-xx",
      "InputArguments": null,
      "ProcessType": "Process",
      "SupportsMultipleEntryPoints": false,
      "RequiresUserInteraction": true,
      "AutoUpdate": false,
      "_FeedId": "00000000-0000-0000-0000-000000000000",
      "JobPriority": "Normal",
      "Id": xxx,
      "Arguments": {
        "Input": null,
        "Output": null
      },
      "ProcessSettings": null
    },
    ...
    ...
}
```

> Process Key 획득


### 5. Robot - 로봇실행하기
- Process key로 로봇 실행



```HTTP
GET /{{ accountLogicalName }}/{{ serviceInstanceLogicalName }}/odata/Jobs/UiPath.Server.Configuration.OData.StartJobs HTTP/1.1
Accept: application/json
Host: platform.uipath.com/
Content-Type: apllication/json
Authorization : Bearer {{ access_token }}
X-UIPATH-TenantName : {{ serviceInstanceLogicalName }}
X-UIPATH-OrganizationUnitId : {{웹 orche에서 참조}}

Request
{
"startInfo": {
	"ReleaseKey": {{ Key }},
	"Strategy": "All",
	"RobotIds": [],
	"NoOfRobots": 0
	}
}


Response
{
  "@odata.context": "https://platform.uipath.com/xxxx/xxxx/odata/$metadata#Jobs",
  "value": [
    {
      "Key": "xxx-xx-xxx-xx-xxxxx",
      "StartTime": null,
      "EndTime": null,
      "State": "Pending",
      "JobPriority": "Normal",
      "Source": "Manual",
      "SourceType": "Manual",
      "BatchExecutionKey": "xx-xx-xxx-xx-xxxxx",
      "Info": null,
      "CreationTime": "2020-xx-xxTxx:49:37.9692211Z",
      "StartingScheduleId": null,
      "ReleaseName": "xxxx-xxxxxx",
      "Type": "Unattended",
      "InputArguments": null,
      "OutputArguments": null,
      "HostMachineName": "xx-xxxxxx",
      "HasMediaRecorded": false,
      "PersistenceId": null,
      "ResumeVersion": null,
      "StopStrategy": null,
      "RuntimeType": null,
      "RequiresUserInteraction": true,
      "ReleaseVersionId": null,
      "EntryPointPath": null,
      "Id": xxxx
    }
  ]
}
```

> 실행할 Key 입력하여서 전송시 실행됩니다.



### 결론 
현재 포스팅에서는 Robot 프로세스 실행에 대해 다루었지만 기타 orchestrator에서 사용되는 다른 API도 만들수 있습니다.
더 다양한 API는 아래의 주소를 참고하시면 되겠습니다. <br>


https://docs.uipath.com/orchestrator/reference/authenticating


