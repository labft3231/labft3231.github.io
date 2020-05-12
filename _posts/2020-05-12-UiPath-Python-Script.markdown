---
layout: post
title:  "🐍 Python Scripts AND Pandas Basic"
subtitle: "호출, parameter전달, dataframe2datatable" 
date:   2020-05-12 21:03:54 +0900
categories: rpa update
author: labft3231
header-img: "public/image/title/pandas_background.jpg"
header-mask: true
hidden: false
published : true
tags:
    - Python
    - Pandas
    - RPA
    - UiPath
---


# pythonScript

사무업에 있어서 excel은 다양한 분야에서 활용되고 있고, 사무 자동화를 위한 RPA에서도 excel이 많이 사용됩니다.
UiPath에서도 다양한 excel 처리 기능이 있지만 방대한 데이터를 빠르게 처리해줄 수 있는 `Pandas`를 활용해보았습니다. 

해당 포스팅의 단계는 3단계로 나누어집니다.
1. python 스크립트 실행
2. python method에 파라미터 전달
3. pandas 활용

<br>

### webopen.xaml (uipath python script 실행)

![python_activity1](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/pandas0.JPG?raw=true)



> 단순히 실행을 위해서 python버전 정보와 경로등을 지정해야함 이것을 python scope에서 함
> 그 후 실행할 script를 설정하는데 이건 load python script에서 지정 가능함
> 단 메소드로 호출할 경우 아래 조건(main.xaml)의 activity가 필요함

<br>
<br>

### main.xaml (uipath python method 실행)


![python_activity2](https://github.com/labft3231/labft3231.github.io/blob/master/public/posts/pandas1.JPG?raw=true)


> Python Scope : 설치된 python 정보를 읽음(python설치경로, os버전, python version)
> Load Python script : 파이썬 script를 읽어 객체저장 (input: 코드나 실행할 python script명 / output: LoadedScript - python object형 결과)
> Invoked Python method : 객체를 받아 method와 파라미터 지정 하여 method 객체 리턴 (input: LoadedScript - python object형 결과, 실행할 python 함수에 parameter와 파일명과 함수명 / output : python object형 결과)
> Get python object : method 객체 받아서 return 타입과 return 변수에 지정 (input: MethodResult / 오브젝트에서 받을 데이터 형태, 데이터 형태에 맞는 result변수)


<br>
<br>

### testDF(uipath pandas 활용 DataFrame TO DataTable)

```python
import pandas as pd

def executionDF():
    s1 = pd.core.series.Series( [1, 2, 3, 4, 5] )
    s2 = pd.core.series.Series( ["one", "two", "three", "four", "five", "six", "seven"])
    df = pd.DataFrame(data=dict(num=s1, word=s2, a=''))
    return df.to_json(orient='records')

```


Pandas의 DataFrame을 바로 사용할 수 가 없어 .py에서 json을 리턴해주고 json으로 datatable로 변환

python에서 excel로 저장하고 excel파일을 uipath에서 읽어도 상관없음
(해당 프로젝트에서는 전자의 방법으로 했음)


(https://github.com/labft3231/pythonScript "🐍 Python Scripts AND Pandas Basic / UiPath에서 Pandas를 활용한 excel 데이터 조작입니다.")