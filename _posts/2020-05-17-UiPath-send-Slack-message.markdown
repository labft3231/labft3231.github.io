---
layout: post
title:  "💬 RPA 자동화, UiPath로 Slack 메세지 전송하기"
subtitle: "RPA 자동화 도구로 슬랙 메세지 보내기" 
date:   2020-05-17 22:35:57 +0900
categories: rpa update
author: labft3231
header-img: "public/image/title/slack_background.jpg"
header-mask: true
hidden: false
published : true
tags:
    - Slack
    - RPA
    - UiPath
---

## 왜 Slack을 사용할까?

슬랙은 메신저 기능 뿐만아니라 다른 application과 connect가 가능하여 활용도가 무수히 많다. 
git이나 jira, trello등 업무적으로 사용하는 것들에 대해서 알림을 통합할수 있고 관리하기도 간편하다 
RPA 도구인 UiPath에서 slack의 메세지를 받는다거나 채널을 만든다거나 초대하거나 파일을 전송하는것들을 자동화할 수 있다.


## slack과 uipath 연동 및 개발 순서

![uipath,slack 연동](https://files.readme.io/81b00c3-Slack_Setup.png)

#### 사전 작업
- 슬랙 workspace 로그인

- 슬랙 app 생성 : https://api.slack.com/apps로 이동하여 create app

![slack app 생성](https://files.readme.io/49c45e5-Slack_CreateApp_1.png)
> `app name`과 `workspace`를 설정

![app info](https://files.readme.io/efaa234-Slack_AppCredentials.png)
> 기본정보에서 `ClientID`와 `Secret key`를 확인(Studio에서 slack과 연동할때 사용됩니다)

- app 퍼미션 등록
![permission apply](https://files.readme.io/f0127ec-Slack_RedirectURLs.png)
> Oauths & Permission 에서 redirect URL 등록

![scope setting](https://files.readme.io/f188720-Slack_SelectTokenScopes.png)
- workspace에 app 설치
![app install](https://files.readme.io/96d6195-Slack_InstallApptoWorkspace.png)
   

#### 프로젝트 개발(=채널에 메세지 보내기)
- Studio에서 프로젝트 개발
   1. pakage manager에서 uipath.slack.activity 설치
   2. slackscope생성 및 `ClientID`와 `Secret key` 설정
   3. send message 넣어서 원하는 상대 및 채널, 보낼메세지, 보낼파일 지정( 파일 안보낸다면 빈칸 )
![slack activity]({{ site.url }}/public/posts/slack.JPG?raw=true)


> Studio 실행시 등록한 slack에 메세지가 전송됩니다. 포스팅에선 slackbot에서 보내기 때문에 답변도 받을 수 있었습니다. (get messages)


### 결론
여기서는 간단하게 연동에 목적이 맞춰져 있기 때문에 프로젝트 개발 부분이 짧지만 
앞써 말했듯 채널생성 초대등 다양하게 활용가능합니다.

또한 slack뿐 아니라 MS의 teams도 자동화가 가능합니다. 
해당 부분에 대해 더 자세하게 알고 싶다면 아래 주소를 참조해주시면 되겠습니다.

https://docs.uipath.com/integrations/docs/slack
