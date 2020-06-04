---
layout: post
title:  "🐣 LINQ로 RPA datatable을 쿼리로 필터링 Basic"
subtitle: "LINQ로 data를 빠르게 필터링하자"
date:   2020-04-01 14:07:11 +0900
categories: rpa update
author: labft3231
header-img: 'public/image/title/LINQ_background.jpg'
header-mask: true
tags:
    - LINQ
    - UiPath
    - RPA
---

# UiPath LINQ Basic

LINQ는 Language Integrate Query의 약자로 쿼리를 사용해 데이터를 쉽게 필터링 할수있도록 도와줍니다.
해당 프로젝트는 조건값에 따라 필터링 하는것에 대한 3가지 예제가 포함되어 있습니다.

<!-- <https://github.com/labft3231/LINQ_Basic> 👈 LINQ 프로젝트 링크 -->


LINQ를 통해서 필요한 데이터를 빠르게 검출할 수 있으며 UiPath Certification 에서도 LINQ 사용을 권장하고 있습니다.


#### Main.xaml

- main에서는 간단한 Datatable을 만들고 이를 테이블명.Select("컬럼명 >3") 을 통의하여 데이터를 필터링하여 출력한다. 


#### ExcelToLINQ.xaml

- ExcelToLINQ에서는 (From r In 테이블명 Where cint(r("컬럼명")) > 300).CopyToDataTable 을 통해서 데이터를 필터링한다.


#### CollectionLINQ.xaml

- CollectionLINQ에서는 From name In Collection명 Where name.StartsWith("A") Select name 명령어로 데이터를 필터링한다.
<!-- (참고 : https://github.com/ufonlo/UIPath/blob/master/Library/Samples/Advanced/Filter%20Collection%20using%20LINQ.xaml) -->



