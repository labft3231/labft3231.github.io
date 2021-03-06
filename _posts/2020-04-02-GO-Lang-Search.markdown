---
layout: post
title:  "🏃 GO의 특징 살펴보기"
subtitle: "go lang"
date:   2020-04-02 15:07:11 +0900
categories: golang update
author: labft3231
header-img: 'public/image/title/go_background.jpg'
header-mask: true
tags:
    - Go
---

# 생각 정리를 위한 GO의 특징 살펴보기


1. go workspace  

   - go 설치시 기본 경로는 C:\go\bin 으로 설정되어 있으며 처음 시작할때 경로를 바꾸는게 좋다
   - go 같은 경우 bin안에 다양한 패키지가 설치되고 workspace 또한 bin안에 설정 된다. 경로를 바꾸어서 나중에 프로젝트가 많아졌을때 패키지가 꼬이는걸 방지할 수 있다.
   - python 같은 경우엔 virtual env를 통해서 프로젝트마다 패키지를 다르게 설정이 가능한데 go는 환경변수에 *GOPATH와 GOBIN*을 설정해줘야한다.

   

2. 변수 특징

   - 변수 선언시 var a int = 1 형태로 선언할 수 있다. 
   - js처럼 var a = "text" 형태로 datatype 설정 안해도 선언이 되긴함
   - 선언한 변수를 사용하지 않으면 에러가 난다.
   - 다양한 변수를 var i, j, k int로 한번에 선언도 가능
   - 함수 내부만 적용되는 := 를 통해서 빠르게 설정 가능
   - underscore 사용안함.
   - 상수 설정은 const로 설정 가능(바꿀 수 없는 값)

```go
package main

import "fmt"

func main() {
	var basicText string = "basic text"
	var text = "text"
	value := 3
	fmt.Println(basic_text)
	fmt.Println(text)
	fmt.Println(value)
}

```



3. 연산자 특징

   - 비트연산자, 할당연사자 등 사용가능
   - 포인터를 사용하여 주소 값을 얻을수 있다.

   

4. 조건문

   - while, do while 없음

   - for  (for i := 1; i <= 100; i++)

     - for문을 while처럼

       ```go
       for n < 10 {
               n *= 2         
           }
       ```

       

     - for문으로 무한루프

       ```go
       for {
               println("Infinite loop")        
           }
       ```

       

     - for range

       ```go
       names := []string{"홍길동", "이순신", "강감찬"}
        
       for index, name := range names {
           println(index, name)
       }
       ```

       

   

   

5. structure의 특징

   - 첫글자가 대문자인지 소문자인지에 따라 private인지 public인지 정해진다.
   - Java getter, setter 처럼 함수를 통해서 값을 외부에서 사용하는 방식을 권장
   - structure 선언시 해당 구조체가 어떤 일을 하는지에 대해 명시(주석 처리) 해주는걸 권장

