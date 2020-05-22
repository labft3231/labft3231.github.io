---
layout: post
title:  "👊 자동화 RPA에서 중요한건 사람이 처리하고 싶다면 Action Center(웨비나)"
subtitle: "robot, studio, orchestrator 를 사용한 Action Center" 
date:   2020-05-08 19:50:37 +0900
categories: rpa update
author: labft3231
header-img: "public/image/title/actioncenter_background.jpg"
header-mask: true
hidden: false
published : True
tags:
    - Webinar
    - Action Center
    - RPA
    - UiPath
---


### UiPath 액션센터(human in the loop) 

액션센터는 사람이 로봇 프로세스에 사람이 승인하는 부분을 만들수 있습니다. 
이게 왜 필요하냐면..
결제와 같이 중요한 프로세스를 로봇 모두 처리한다면 의도치 않게 일이 잘못될 수 있기 때문입니다.
액션센터를 통해 사람이 처리할 것을 나눌 수 있죠.
원래의 이름은 human in the loop으로 쓰이다가 `Action center`로 변경되었습니다.
액션센터는 robot, studio, orchestrator 이 세가지가 한 박자가 되어서 사용된다고 합니다.




#### 액션 센터의 구성

- `attended`, `unattenended`, `human`가 Task마다 적절히 선택하여 사용할 수 있습니다.



#### 액션센터는 일종의 BPM

- task : 내가 해야되는 시점에 업무가 찾아옴(form)

  - 활성화를 시키기 위햐서 web.config 파일 수정해야함
  - ```<app setting></app setting>``` 이 추가 되어야함
  - host 테넌트 있을때 테스크가 활성화 될거임.
  - pakage 설치해야함, (UiPath.Persistense.Acrivities)
  - orchestrator process template 사용시 패키지 설치 되어있음
  - 사람의 개입이 필요한 부분에 Create Form Task 액티비티가 필요해
    - title, data 넣으면 form 데이터를 통해 값 바인딩함.
    - wait for task and resume 액티비티를 만나면 사람 반응까지 기다리기 가능


  
   ![actioncenter]({{ site.url }}/public/posts/actioncenter.JPG?raw=true)

  

  - Demo (기능)

    - 가격이 높을경우와 낮은 경우 나누어짐

    - web config에 app setting으로 테스크활성화하고 테스크에서 폼확인이 가능하고 여기서 human이 값 선택 가능 

    - 모바일 orchestrator로 task에 대한 푸시알림도 받을수 있음

    - task는 orchestrator말고 api로도 받을 수 잇음

    - 사용자의 입력이 있을때까지 기다림(최대 대기 시간은 없는걸로 알고있다고함)

    - unattended 형태이며 사용자 명령이 있기 전까지 로봇은 새로운 작업도 수행할 수 있음

    - 커뮤니티 기능에서도 사용이 가능함 (task 기능 가능) -패키지 설치가 필요함

      
