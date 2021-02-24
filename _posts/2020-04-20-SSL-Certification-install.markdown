---
layout: post
title:  "🐌 DNS 설정 및 SSL 발급"
subtitle: "DNS 설정, SSL 발급" 
date:   2020-04-20 21:43:36 +0900
categories: rpa update
author: labft3231
header-img: 'public/image/title/ssl_background.jpg'
header-mask: true
tags:
    - RPA
    - UiPath
    - Orchestrator
    - SSL
    - DNS
---


> 이전에 포스팅에서 자체 생성으로 만든 인증서로 설치하였지만 다른 PC에서 접근이 불가하여 인증서를 다시 구성하였습니다.
> ssl 인증서는 domain을 바탕으로 구성해야 다른 웹에서 Orchestrator 접근이 가능합니다. 


## 도메인 주소 발급과 DNS 레코드 등록

전 기존에 구매한 도메인이 있어서 만들었던 도메인을 활용하였습니다. 

https://www.freenom.com/en/index.html?lang=en여기서 무료로 발급 받을 수 있다네요! :smile:

https://opentutorials.org/module/4092/24965 생활코딩 사이트에 자세한 설명이 있습니다.


도메인을 발급 받았다면 내 서버 ip와 연결하여 내 서버 ip에 좀 더 편하게 접근할 수 있도록 DNS 레코드를 등록해줍니다.

연결이 되었다면 해당 도메인으로 접근시 내 ip가 연결되는 것을 확인할 수 있다. 


## ssl을 만들어야 한다.

내 ip와 연결된 dns를 얻었다면 이제 ssl을 발급 받아야한다.
ssl 내 주소가 안전하다는 것을 증명해주는 인증서이다. 

ssl를 만들기 위해서 다양한 프로그램이 있다 여기선 무료 인증서(let's encript)를 활용한다.

<https://certifytheweb.com/> 에서 setup 파일을 다운로드 합니다.

setup파일을 통해 설치하면 CertifyTheWeb 프로그램이 생성된다. 
해당 프로그램 실행 시 email을 입력하는 화면이 나오는데 이메일을 입력해준다. 

~~~
해당 프로그램은 기본기간에서 추가로 자동 갱신해주는 기능에 최대 갯수 제한이 있습니다.

다른 인증서 발급시 다른 이메일 주소를 사용하면 됩니다.
~~~

이메일을 등록하고 이제 새로운 인증서를 만들어 보자





ssl을 받았으면 
> 이제 인증서를 활용하면 `http` 연결에서 -> `https` 이 가능합니다.


Domain name service를 통해서 발급받은 도메인과 ip오 



wmic product where name="Elasticsearch 7.6.2" call uninstall