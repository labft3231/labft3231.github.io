---
layout: post
title:  "UiPath On-Premise Orchestrator 설치-1"
date:   2020-04-07 17:35:11 +0900
categories: RPA update
author: labft3231
background: 'public/image/title/orchestrator_background.png'
---

## UiPath On-Premise Orchestrator 설치 시작


- 앞서 webhook 과정에서 스쳐지나갔던 On-premise Orchestrator를 설치 과정에 대해 정리해보았습니다.

<br>
<br>

## On-premise Orchestrator의 특징

- 업데이트 마다 사항이 바뀔 수 있기 때문에 설명 대신에 아래의 링크를 첨부 

- [on-premise 와 cloud 차이점](https://docs.uipath.com/cloudplatform/docs/on-premises-vs-cloud-platform-orchestrator-features)

- 큰 특징으로 봤을때 insights 사용이 가능하고 Elasticsearch도 사용가능하고 DB에 로그등을 저장할 수 있고 등의 특징을 가진거 같다.

<br>
<br>

------------------------------------------

### 그럼 설치를 해보자.

<br>
<br>

#### 다운로드

- Orchestrator installer Download 링크(아래 추천 링크와 둘중에 맘에 드는걸로 다운로드 가능)  <https://download.uipath.com/UiPathOrchestrator.msi

- 혹시 다운로드가 되지 않을경우나 exe 파일이 필요한 경우 UiPath 공식 홈페이지에서 Trial 버전(위에 것도 Trial 임)을 다운로드 받을 수 있다 <https://www.uipath.com/start-trial>

<br>
<br>

#### Orchestrator install 은 IIS 환경을 설정을 요구합니다. 

![UiPath Orchestrator 시스템 요구사항](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/%EC%BA%A1%EC%B2%98.PNG?raw=true)

<br>

##### IIS 환경 설정

   - 7.5 이상의 버전을 설치 하기 위해 아래의 링크를 참조
      - <https://docs.microsoft.com/en-us/iis/install/installing-iis-7/installing-iis-7-and-above-on-windows-server-2008-or-windows-server-2008-r2>

   - 위와 같이 설정하면 또 아래와 같이 IIS URL Rewrite Module 에러가 납니다.

      ![IIS URL Rewrite Module](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/%EC%BA%A1%EC%B2%982.PNG?raw=true)

      - 해당 링크를 통해 해결가능 <https://www.microsoft.com/en-us/download/details.aspx?id=47337>

   - 아직 설정이 더 남았습니다. 아래처럼 필요한 IIS Module이 나타나는데 환경마다 다를 수 있으니 자신의 에러 메세지를 확인하여 설치하도록 한다.

      ![IIS Module](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/%EC%BA%A1%EC%B2%983.PNG?raw=true)

      ![IIS Module Solution](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/%EC%BA%A1%EC%B2%984.PNG?raw=true)



   - 설치가 완료되면 드디러 다음화면으로 넘어갈 수 있다. 

      ![Orchestrator install page](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/%EC%BA%A1%EC%B2%985.PNG?raw=true)

<br>
<br>

#### 인증서 인증

- 해당 글은 기존 인증서를 통해 인증을 하는데 혹시 도메인을 발급 받고 하고 싶다면 도메인에 따른 ssl 인증서를 받아서 설치하면 됩니다.

- 인증서가 필요한데 default로 씌여 있는 인증서 이름으로 설정 시 next가 되지 않습니다. 

- 등록할 인증서를 알기 위해 windows 검색에서 IIS 관리자에 들어간다. (IIS Manager)

   ![IIS](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/%EC%BA%A1%EC%B2%986.PNG?raw=true)

   ![IIS2](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/%EC%BA%A1%EC%B2%987.PNG?raw=true)

   ![IIS3](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/%EC%BA%A1%EC%B2%988.PNG?raw=true)

- 성명 복사 해서 넣고 Next

<br>

##### 다음페이지에서는 스샷은 없지만 Application Pool Identity 설정 후 Next를 클릭하면 다음으로 넘어가집니다.

##### 다음은 DB 설정입니다. 길게 쓰면 지루하니 다음 포스팅에 이어서 쓰도록 해야겠습니다.







