---
layout: post
title:  "UiPath On-Premise Orchestrator 설치-1"
date:   2020-04-07 17:35:11 +0900
categories: RPA update
author: labft3231
background: 'public/image/title/rpa_background.jpg'
---

## UiPath On-Premise Orchestrator 설치 시작


- 앞서 webhook 과정에서 스쳐지나갔던 On-premise Orchestrator를 설치 과정에 대해 정리해보았다.

<br>
<br>

## On-premise Orchestrator의 특징

- 업데이트 마다 바뀔 수 있기 때문에 설명 대신에 아래의 링크를 첨부했다. 

- [on-premise 와 cloud 차이점](https://docs.uipath.com/cloudplatform/docs/on-premises-vs-cloud-platform-orchestrator-features)

- 큰 특징으로 봤을때 insights 사용이 가능하고 Elasticsearch도 사용가능하고 DB에 로그등을 저장할 수 있고 등의 특징을 가진거 같다.

<br>
<br>

------------------------------------------

### 그럼 설치를 해보자.

<br>
<br>

#### 다운로드

- Orchestrator installer Download 링크(둘중에 맘에 드는걸로 다운로드 가능) [https://download.uipath.com/UiPathOrchestrator.msi](https://download.uipath.com/UiPathOrchestrator.msi)

- 혹시 다운로드가 되지 않을경우나 exe 파일이 필요한 경우 UiPath 공식 홈페이지에서 Trial 버전(위에 것도 Trial 임)을 다운로드 받을 수 있다 [추천](https://www.uipath.com/start-trial)

<br>
<br>

#### Orchestrator install을 시작하면 처음 IIS 환경을 설정해야한다. 

- 처음 설치 시 IIS 설정을 요구한다.

![UiPath Orchestrator 시스템 요구사항](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/%EC%BA%A1%EC%B2%98.PNG?raw=true)

<br>
<br>

1. IIS 환경 설정

   - 7.5 이상의 버전을 설치 하기 위해 아래의 링크를 참조
      - https://docs.microsoft.com/en-us/iis/install/installing-iis-7/installing-iis-7-and-above-on-windows-server-2008-or-windows-server-2008-r2

   - 위와 같이 설정하면 또 아래와 같이 IIS URL Rewrite Module 에러가 난다.

![캡처2](C:\Users\ksc31\Desktop\설치error 정리\캡처2.PNG)

   - https://www.microsoft.com/en-us/download/details.aspx?id=47337

   - 아직 설정이 더 남았다. 필요한 IIS Module이 다를 수 있으니 자신의 에러 메세지를 확인하여 설치하도록 하자.

![캡처3](C:\Users\ksc31\Desktop\설치error 정리\캡처3.PNG)



![캡처4](C:\Users\ksc31\Desktop\설치error 정리\캡처4.PNG)



설치가 완료되면 드디러 다음화면으로 넘어갈 수 있다. 

![캡처5](C:\Users\ksc31\Desktop\설치error 정리\캡처5.PNG)

여기서 인증서가 필요한데 default로 씌여 있는 인증서 이름이 올바르지 않다.

인증서 이름을 알기 위해 window 검색에서 IIS 관리자에 들어간다. (IIS Manager)

![캡처6](C:\Users\ksc31\Desktop\설치error 정리\캡처6.PNG)



![캡처7](C:\Users\ksc31\Desktop\설치error 정리\캡처7.PNG)

![캡처8](C:\Users\ksc31\Desktop\설치error 정리\캡처8.PNG)

성명 복사 해서 넣으면 다음으로 진행 가능



다음에선 Application Pool  Identity 설정 후 DB를 설정해주면 된다. 

길게 쓰면 지루하니 다음편에서 이어서 작성







