---
layout: post
title:  "🚢 UiPath Log 데이터 시각화"
subtitle: "Elastic search와 Kibana를 활용한 데이터 시각화" 
date:   2020-04-27 17:43:55 +0900
categories: rpa update
author: labft3231
header-img: "public/image/title/orchestrator_background.png"
hidden: false
header-mask: true
published : true
tags:
    - RPA
    - UiPath
    - Orchestrator
    - Kibana
    - Meatric Beat
    - Elastic Search
---

On-premise 형태의 Orchestrator 서버 환경을 구축하였다면 이제 cloud환경보다 더 다양한 것을 해볼 수 있습니다.
- UiPath에서 유료로 제공하는 insights 를 사용 가능
- Orchestrator 로그인 Custom
- tenant 관리
- SSL을 통한 독립된 환경 조성
- log 데이터 관리(db, elasticsearch 등.)

서버를 어떻게 운용하고 데이터를 얼마나 활용하는지에 따라 많은 것을 할 수 있을 것입니다.

해당 포스팅에서는 UiPath 로그 데이터와 Metricbeat(server log) 수집 데이터에 대한 설명입니다.

<br>

### 각 기능 및 특징

![각각의_특징](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/monitoring2.JPG?raw=true)

<br>

### 순서
로그의 전송 순서는 아래와 같습니다.

![log_data_flow](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/monitoring1.JPG?raw=true)

Orchestrator에서 log를 받으면 Orchestrator는 web.config 설정에 따라 로그를 전송.
Orchestrator 설치 당시에 정보를 정확하게 기입하였다면 `DB`와 `Elastic search`로 데이터가 저장이 될 것입니다.
> 혹시 데이터가 저장이 되지 않는다면 web.config 파일을 수정해줘야합니다.



<br>

### 결과

![데이터결과](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/monitoring3.JPG?raw=true)

Orchestrator 서버를 통해 받아온 log 데이터와 Meatric beat를 통해 받아온 데이터를 Kibana를 통해 시각적으로 표현한 화면입니다.
