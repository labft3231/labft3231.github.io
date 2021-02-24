---
layout: post
title:  "🤒 UiPath Data 조작하기"
subtitle: "Back to the basic v1.0.4🚐" 
date:   2020-05-22 22:15:15 +0900
categories: rpa update
author: labft3231
header-img: "public/image/title/backToTheBasic_background.jpg"
header-mask: true
hidden: false
published : true
tags:
    - RPA
    - UiPath
---

UiPath 에서는 기존 프로그래밍 언어들과 다르게 초기화 및 사용 방법에 Activity 를 많이 활용하기 때문에 조작에 대해 헷갈릴 때가 많습니다.

참고이기도하고 기본을 되돌아 보고 더 탄탄한 기본을 다지기 위해 포스팅을 작성하게 되었습니다.

> 🗿 본 포스팅은 Data 기본 조작에 대해 정리 되어있습니다. 
> 계속 수정할 계획입니다. 


<br>

## UiPath Data Manipulation

<br>

### String

```c#
Contains : VarName.Contains ("text")

Format : String.Format("{0} is {1}", VarName1, VarName2)

IndexOf : VarName1.IndexOf("a")

Join : String.Join("|", CollVarName1)

Replace : VarName.Replace ("original", "replaced")

Split : VarName.Split("|"c)(index) 
ex) Varname.Split({","}, System.StringSplitOptions.None)
Varname.Split({",", " "}, System.StringSplitOptions.None)

- None	0	
> 문자열을 분할할 때 기본 옵션을 사용합니다.
- RemoveEmptyEntries	1	
> 결과의 빈 문자열을 포함하는 배열 요소를 생략합니다.
- TrimEntries	2	- uipath에선 옵션이 보이지 않음
> 결과의 각 부분 문자열에서 공백 문자를 자릅니다.

Trim : Trim(VarName)

Substring : VarName1.Substring(startIndex, length)
```

<br>

---

<br>

### List

>  배열은 여러 객체를 저장하기 위한 고정 크기 구조인 반면, 목록을 통해 항목을 추가, 삽입 및 제거할 수 있다.



##### 초기화

Array String 초기화
- new string(){}
Array String 추가
- 



New List (Of String)
my_List = new List(of string)(new string(){"value1","value2"})

Initialize Array
my_Array = new string(){"value1","value2"}
Array 첫번째 값
my_First = my_Array.first


##### List 요소 추가

- Add to collection이라는 activity로 요소를 추가할수 있음

- Invoked Method로 Sort나 Add도 가능함.



리스트끼리 합치기 위해서 Enumerable.Concat을 사용할 수 있다. 

```c#
Enumerable.Concat(SpainCities.AsEnumerable, UKCities.AsEnumerable).ToList
```

>  **.AsEnumerable** 를 사용하는 이유는 List를 Enumerable한것으로 바꿔주기 위해서 이다.



리스트를 String으로 변환

```c#
StrConv(item, VbStrConv.ProperCase)
```

<br>

---

<br>

### Dictionaries

- Key와 Value로 구성되어있음.



##### 초기화

```c#
new Dictionary(of String, List(Of String))

cities("US") = new List(of String) from {"New York", "Chicago", "Seattle","San Francisco"}

```



##### 요소 추가 제거 

Add to Collection, RemoveFromCollection 액티비티로 간단하게 사용 가능하며 아래 방법도 가능

- 요소 추가

  > VarName.Add(Key, Value)

- 요소 제거

  > VarName.Remove(Key)



##### 기타

- VarName.Item(Key) – key값으로 아이템 가져오기
- VarName.Count – 요소 갯수 가져오기
- VarName.ContainsKey(Key) – key가 포함되어있는지 확인(bolean형으로 return)
- VarName.TryGetValue(Key, Value) – key value확인

<br>

---

<br>

### DataRow 동적추가


배열은 크기가 정해져있기 때문에 List로 DataRow를 대체하여 DataTable에 삽입 가능.

System.Collections.Generic.List <System.String>

-> New List(Of String)(new String() {})

### Dict
New Dictionary(of string, string)
 
### Dict의 List
New List(Of Dictionary(Of String, String))()



Data Add

Invoke method사용

MethodName : AddRange

Parameter : IEnumerable<String>,   {""}

TargetObject : System.Collections.Generic.List <System.String>

TargetType : (null)
```

<br>

---

<br>

### DataTable 

- 행과 열을 표현할 수 있는 Type



##### 초기화

```c#
New System.Data.DataTable
```



##### 생성

일반적인 생성 방법은 BuildDataTable, Read Range, Read CSV, Data scraping이 있다고 함.

*Generate Data Table*을 통해서 동적으로도 생성도 가능함.



##### 서로 다른 DataTable 합치기

Join DataTables : JoinType 속성에 지정된 Join 규칙에 따라 서로 공통 값을 사용하여 두 테이블의 행을 결합 합니다.

Merge DataTable : 지정된 DataTable을 현재 DataTable과 병합하여 변경 내용을 보존할지 여부와 현재 DataTable에서 누락 된 스키마를 처리하는 방법을 나타냅니다.

<br>

---

<br>

### 기타

##### loop 지정 횟수 반복 

For Each 원하는 갯수 돌리고 싶을때(아래 예제는 3번 반복)

Enumerable.Range(0,  3)



##### Excel Read Range / Workbook Read Range 차이

Workbook은 Excel이 설치되지 않아도 실행이 가능하고 Excel은 Excel이 설치되어 있어야 실행이 가능함.
또한 Excel Read Range는 Excel scope안에서 실행되어야함

번외로..
Workbook은 DRM이 걸린 파일이 열리지도 않지만 DRM이 걸리지도 않아
Excel은 DRM 파일이 열리는데 저장하면 DRM이 걸림

##### Array 건너뛰기( index 값으로 지우는게 있을텐데 못찾았음)
arrayData.Skip(1).ToArray()


##### Datatime 포맷 정해주기 추가
System.DateTime.Now.ToString("yyyy_MM_dd")

DateTime.Now.AddMonths(-1).ToString("yyyy.MM.dd")


##### 현재 Directory (path) 가져오기

Directory.GetCurrentDirectory()



##### 정규표현식 찾은 값을 Array(Of String)으로 변경


Matches Type : System.Collections.Generic.IEnumable<System.Text.RegularExpressions.Match>
OfType(Of Match).Select(Function(m) m.Value.ToString).ToArray


##### 공백 문자처리 방법

"테스트" & vbLf & "입니다" Or "test"+ vbLf + "입니다"


##### 컬럼명 변경 

datatableVar.Columns("oldColumnName").ColumnName = New column Name


##### 중복되지 않은 사항 찾기

List1.Except(List2)

##### 중복 사항 

List1.Intersect(List2)
Distinct(), Union()


##### 유니코드 디코딩 (\u20)

System.Text.RegularExpressions.Regex.Unescape(unicodeString)


##### Get Excel Row index

Int value_row_index =yourdatatable.Rows.Indexof(row)

##### Get Folder Name

Directory.GetFiles(폴더명, "*.xls*", SearchOption.AllDirectories)

##### Datatable 중복제거

Datatable.DefaultView.Totable(true, list of column names)