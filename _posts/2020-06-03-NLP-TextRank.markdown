---
layout: post
title:  "📝 자연어처리 NLP"
subtitle: "자연어처리 학습하기" 
date:   2020-06-03 23:10:02 +0900
categories: nlp update
author: labft3231
header-img: "public/image/title/nlp_background.jpeg"
header-mask: true
hidden: false
published : true
tags:
    - NLP
---

### NLP(자연어처리)

> 사람의 언어를 기계가 이해하는 하기 위한 처리
>
> 한국어는 형태소 단위로 나누어져있으며 최소 단위는 자음과 모음
>
> 자연어 처리의 핵심은 분류에 있음

<br>


언어 모델을 만드는 가장 기초 기법은 마코프 체인 기법임

- 마코프체인 기법은 앞의 단어를 통해 다음 단어가 어떤게 나올지 예측함

<br>
<br>

### RNN

> RNN 히든 노드가 방향을 가진 엣지로 연결되어 순환구조를 이루는 인공신경망임
>
> 문자, 음성 등을 순차적으로 처리하기 적합한 모델

<br>

하지만 RNN은 길이가 문서 단위로 길어졌을 경우 앞의 데이터가 희석될 수 가 있어서 긴 문장일 경우 신뢰성이 떨어짐

또한 시계열이기 때문에 앞의 값을 기다려야해서 시간이 오래걸림.

접속어 같은 단어도 모두 가져오기 때문에 이러한 단어가 token에 영향을 줌

<br>
<br>

### Attention 

> Attention은 중요한 부분에 주목하는 모델임
>
> 사진에서 물체가 있고 배경이 있을때 물체가 있는곳을 중요 데이터라고 판단하여 분석
>
> AI 분야에서 대세 모듈로서 사용되고 있는 Transformer의 기반이 된다.

<br>

1. 추출적 요약

   > 대표적인 알고리즘으로 머신 러닝 알고리즘인 텍스트랭크(TextRank)가 있음

   <!-- 예시 : https://summariz3.herokuapp.com/ -->

2. 추상적요약

<br>
<br>

### Transformer

> **학습 속도가 무척 빠르다**는 장점을 갖고있다
>
> 전통적으로 써왔던 CNN, GRU를 버리고 Attention 하나로 모든것을 처리함
>
> 현재 대세임.



