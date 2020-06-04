---
layout: post
title:  "⛵ UiPath On-Premise Orchestrator 서버 설치-3"
subtitle: "Orchestrator 설치 / 라이센스 적용" 
date:   2020-04-10 22:52:12 +0900
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

## 부가기능

부가적으로 필요에 따라서 그냥 넘어가도 되는 부분들에 대한 정리입니다. 

Elatic search의 기본 port는 9200이기 때문에 127.0.0.1:9200 입력후 넘어갑니다. elastic 안할거면 그냥 스킵해도 됩니다.

추후에 orchestrator 경로의 web.config 파일을 추가하여서 넣어줘도 괜찮습니다. 

또 그냥 넘어갈 수 있는 insights 입니다. 

insights도 혹시 설정할 일이 있다면 기존 UiPath DB를 생성한것처럼 UiPathInsights DB를 생성하여 입력해줍니다. 

해당 부분도 나중에 추가로 입력이 가능하지만 미리 해두면 insights 설치를 조금 더 편하게 할 수 있습니다. 

Insights 설치는 추후에 다루도록 하겠습니다. 


<br>
<br>

## Elastic search / Kibana 설치

먼저 `Elastic search`입니다. 

```
Elasticsearch는 텍스트, 숫자, 위치 기반 정보, 정형 및 비정형 데이터 등 모든 유형의 데이터를 위한 분산형 오픈 소스 검색 및 분석 엔진입니다. 
Elasticsearch는 Apache Lucene을 기반으로 구축되며, (현재 Elastic이라고 알려져 있는) Elasticsearch N.V.가 2010년에 최초로 출시했습니다. 
간단한 REST API, 분산형 특징, 속도, 확장성으로 유명한 Elasticsearch는 데이터 수집, 보강, 저장, 분석, 시각화를 위한 오픈 소스 도구 모음인 Elastic Stack의 중심 구성 요소입니다. 
보통 (Elasticsearch, Logstash, Kibana의 머리글자를 따서) ELK Stack이라고 하는 Elastic Stack에는 이제 데이터를 Elasticsearch로 전송하기 위한 경량의 데이터 수집 에이전트들이 풍부하게 제공되는 컬렉션인 Beats가 포함되어 있습니다.
```

그렇습니다. Elastic search는 각종 모든 데이터를 위한 분석엔진 입니다.
UiPath에서 생성되는 log 데이터를 받아 이것을 분석할 수 있을거 같네요.


그럼 이제 어떤 기능인지 알았으니 설치를 해보실까요.

https://www.elastic.co/kr/downloads/elasticsearch 에서 자신의 OS 환경에 맞는 elastic을 설치 합니다.

저는 7.6.2 버전이네요.

> elastic search나 orchestrator는 서버로 돌기 때문에 같은 서버에 설치해도 되고 독립적으로 구성해도 되고 상관없습니다.


C드라이브의 elastic 새폴더를 생성하여 다운로드 받은 압축파일을 옮겨줍니다.

bin folder로 이동하여 elasticsearch.bat 파일을 관리자 권한으로 실행해줍니다.

elastic search 실행시 java가 필요합니다. 다운 받은 elastic에 이미 jdk가 포함되어 있기 따로 설치를 해주시지 않아도 실행됩니다.

실행이 되면 http://127.0.0.1:9200으로 접속시 json형태의 데이터를 받을 수 있을것입니다. 


<br>

이제 `Kibana`입니다. 
 
```
Kibana는 Elastic Stack을 기반으로 구축된 오픈 소스 프론트엔드 애플리케이션으로, Elasticsearch에서 색인된 데이터를 검색하고 시각화하는 기능을 제공합니다. 
Elastic Stack(이전에는 Elasticsearch, Logstash, Kibana의 머리글자를 따서 ELK Stack이라고 함)의 차트 작성 도구로 널리 알려진 Kibana는 Elastic Stack 클러스터를 모니터링, 
관리 및 보호하기 위한 사용자 인터페이스의 역할과 Elastic Stack에서 개발된 기본 제공 솔루션의 중앙 집중식 허브 역할도 합니다. 
2013년 Elasticsearch 커뮤니티 내에서 개발된 Kibana는 사용자와 기업을 위한 포털을 제공하며 Elastic Stack을 들여다보는 창으로 성장했습니다.
```

Kibana는 elastic에서 색인화한 데이터를 검색하며 시각화 기능을 제공하네요
 
<!-- https://www.elastic.co/kr/downloads/kibana Kibana는 해당 경로에서 다운로드 가능합니다. -->

Kibana도 압축을 풀어서 C드라이브의 elastic파일로 옮겨줍니다. 

Kibana도 실행을 하려면 bin파일에서 kibana.bat을 관리자 권한으로 실행해주면 됩니다. 

실행이 되었다면 http://127.0.0.1:5601로 접속이 가능합니다. 



## Orchestrator 실행

Orchestrator를 설치를 마쳤으니 이제 Orchestrator를 사용할 수 있습니다.

ssl을 등록했던 호스팅 주소(https)로 접속하면 Orchestrator 실행을 볼 수 있습니다.

처음에 Orchstrator 설치시 tenant는 host, default와 두가지 tenant들로 접속이 가능합니다.

접속 아이디와 비밀번호는 Orchestrator 설치시 사용한 form을 입력해주면 됩니다.

 
 <br>
 <br>

 ## 라이센스 입력

 라이센스는 host tenant에서 입력 하시면 됩니다.
 
 host에 라이센스 입력시 각 tenant에 라이센스를 부가할 수 있습니다.

<br>

Orchestrator 설치에 대해서 마치겠습니다. Orchestrator 서버를 설치하는건데 생각보다 과정이 기네요.

문의사항이 있으시면 댓글이나 메일 주시면 되겠습니다. 감사합니다 ~