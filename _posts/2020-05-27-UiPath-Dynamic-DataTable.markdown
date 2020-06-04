---
layout: post
title:  "🔮 UiPath 동적으로 Datatable 생성하여 환율 구하기"
subtitle: "UiPath Dynamic Datatable" 
date:   2020-05-27 21:27:12 +0900
categories: rpa update
author: labft3231
header-img: "public/image/title/exchangeRate_background.jpg"
header-mask: true
hidden: false
published : true
tags:
    - RPA
    - UiPath
---


## UiPath Dynamic Datatable 



> 🔮 본 글은 Datatable을 동적으로 생성하는 프로젝트에 대한 리뷰와 설명입니다.
>
> 실행 시 로봇이 입력한 금액과 입력한 나라의 환율을 구해서 Excel로 저장해줍니다.
> Data/Input/inputData.xlsx 경로에서 KRW 기준에서 원하는 금액과 원하는 나라 환율을 계산해줍니다.
>
> 기준 나라 변경을 원할 경우 URL 변경해주면 A1 셀과 url을 변경해주면 됩니다. 👍
> (아니면 환율 바꾸는 부분을 추가해줘도 됩니다.)



순서대로 설명하자면..



### Excel_DataExtract.xaml

Excel에서 사용할 데이터를 추출합니다. (Row : 환율 검색할 화폐 종류, Column: 검색할 금액)



### OpenWeb.xaml 

환율 검색할 사이트 열기 (특별한게 없습니다.)



### ✨ DataTable_Create.xaml 

위에서 추출한 Excel데이터를 받아 인수로 완성된 Excel Datatable을 생성합니다.

- 실질적으로 `Dynamic`하게 만드는 부분입니다.
  - 값을 통해서 Column 만큼 반복합니다.  반복하는 이유는 Column 값들을 하나의 문자열을 생성하기 위해서 인데 문자열이 필요한 이유는 `Generate DataTable` 액티비티를 사용하기 위해서 입니다.
  - 보통 Build Datable 액티비티를 통해서  DataTable을 초기화 해주는데 Column 값을 알고 있을때는 편하고 좋지만 동적으로 생성하기엔 한계가 있는걸로 보입니다. 뭐 그냥 계속 컬럼 추가 해주면서 하면 가능도 하겠지만 엄청 번거러워 보입니다.
- 그 후 받은 데이터를 바탕으로 웹에서 검색하여 list을 생성해줍니다.
- list를 array로 변형하여 AddDataRow 액티비티로 동적으로 생성한 DataTable에 넣어주면 값이 채워집니다.



### Excel_DataInsert.xaml

Excel에 생성된 DataTable 값 입력



<!-- <https://github.com/labft3231/DynamicDatatable> 👈 "🔮 UiPath 동적으로 Datatable 생성하여 환율구하기" -->