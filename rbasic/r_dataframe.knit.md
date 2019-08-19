---
title: "R 데이터 프레임 Data frame"
author:
  - name: Bohak Maeng
    url: https://manboha.github.io
date: "2019-08-20"
output: 
  distill::distill_article:
    self_contained: false
    toc: true
    toc_depth: 2
---



 데이터 프레임은 다양한 형태의 데이터가 2차원으로 구성된 데이터 구조입니다. 행(케이스)과 열(변수)로 구성된 표와 같이 생겼습니다. 엑셀에서 이름 필드, 연령 필드, 성적 필드 등으로 이루어진 표와 같다고 보면 됩니다. 통계분석에 가장 많이 사용됩니다.


## 데이터 프레임 만들기 Create data frame

데이터 프레임을 생성하는 방법은 많습니다. 그 중에서 가장 많이 쓰이는 방법은 외부에서 만들어진 정리된 데이터를 R에서 읽어 들이는 방법입니다. 이 방법은 R 입출력에서 자세히 다루겠습니다. 

두 번째 방법은 벡터 형식의 자료를 묶어서 데이터 프레임을 만드는 것입니다. 아래 예제는 data.frame 함수를 이용하여 벡터 변수 name, age, sex, score를 하나로 묶어서 데이터 프레임 df를 만들어 보겠습니다.

<div class="layout-chunk" data-layout="l-body">

```r
name <- c("유재석", "홍진영", "송가인", "강호동", "이영자", "김종민", "김연아")
age <- c(24, 28, 31, 25, 27, 22, 29)
sex <- c("남", "여", "여", "남", "여", "남", "여")
score <- c(90, 80, 85, 75, 95, 80, 70)

# 'stringsAsFactors = FALSE' 옵션 : 문자 데이터를 팩터로 변환시키지 않음
df <- data.frame(name, age, sex, score, stringsAsFactors = FALSE)
df
```

```
    name age sex score
1 유재석  24  남    90
2 홍진영  28  여    80
3 송가인  31  여    85
4 강호동  25  남    75
5 이영자  27  여    95
6 김종민  22  남    80
7 김연아  29  여    70
```

</div>



## 데이터 프레임 구조 보기 Get the Structure of the Data Frame

<div class="layout-chunk" data-layout="l-body">

```r
# 데이터 프레임 구조
str(df)
```

```
'data.frame':	7 obs. of  4 variables:
 $ name : chr  "유재석" "홍진영" "송가인" "강호동" ...
 $ age  : num  24 28 31 25 27 22 29
 $ sex  : chr  "남" "여" "여" "남" ...
 $ score: num  90 80 85 75 95 80 70
```

</div>


<div class="layout-chunk" data-layout="l-body">

```r
# 행 개수
nrow(df)
```

```
[1] 7
```

```r
# 열 개수
ncol(df)
```

```
[1] 4
```

</div>



## 데이터 프레임 요약 보기 Summary of Data in Data Frame

<div class="layout-chunk" data-layout="l-body">

```r
summary(df)
```

```
     name                age            sex           
 Length:7           Min.   :22.00   Length:7          
 Class :character   1st Qu.:24.50   Class :character  
 Mode  :character   Median :27.00   Mode  :character  
                    Mean   :26.57                     
                    3rd Qu.:28.50                     
                    Max.   :31.00                     
     score      
 Min.   :70.00  
 1st Qu.:77.50  
 Median :80.00  
 Mean   :82.14  
 3rd Qu.:87.50  
 Max.   :95.00  
```

</div>




## 데이터 프레임에서 데이터 추출 Extract Data from Data Frame

### 특정 위치(행과 열 기준)에 있는 데이터 추출하기

<div class="layout-chunk" data-layout="l-body">

```r
# name 열(변수) 데이터 추출
# 데이터프레임과 컬럼사이에 $기호가 사용됨
df$name
```

```
[1] "유재석" "홍진영" "송가인" "강호동" "이영자" "김종민" "김연아"
```

</div>


<div class="layout-chunk" data-layout="l-body">

```r
# df$name 대신 아래처럼 사용 가능
df[, "name"]
```

```
[1] "유재석" "홍진영" "송가인" "강호동" "이영자" "김종민" "김연아"
```

</div>


<div class="layout-chunk" data-layout="l-body">

```r
# 첫번째 열(name) 추출
df[, 1]
```

```
[1] "유재석" "홍진영" "송가인" "강호동" "이영자" "김종민" "김연아"
```

</div>


<div class="layout-chunk" data-layout="l-body">

```r
# 1열과 3열 추출
df[, c(1, 3)]
```

```
    name sex
1 유재석  남
2 홍진영  여
3 송가인  여
4 강호동  남
5 이영자  여
6 김종민  남
7 김연아  여
```

</div>


<div class="layout-chunk" data-layout="l-body">

```r
# name 열(변수)의 3번째 데이터 추출
df$name[3]
```

```
[1] "송가인"
```

</div>



<div class="layout-chunk" data-layout="l-body">

```r
# 2~3번째 행 추출
df[2:3, ]
```

```
    name age sex score
2 홍진영  28  여    80
3 송가인  31  여    85
```

</div>


<div class="layout-chunk" data-layout="l-body">

```r
# 연령 변수의 데이터를 추출하여 평균을 구함
# na.rm = TRUE는 missing value를 제외하고 계산함
mean(df$age, na.rm = TRUE)
```

```
[1] 26.57143
```

</div>



### 마이너스 기호(-)를 이용하여 데이터 제외

<div class="layout-chunk" data-layout="l-body">

```r
# 3번째 열 제외
df[, -3]
```

```
    name age score
1 유재석  24    90
2 홍진영  28    80
3 송가인  31    85
4 강호동  25    75
5 이영자  27    95
6 김종민  22    80
7 김연아  29    70
```

</div>



### 조건으로 데이터 추출

특정 조건에 맞는 데이터만 추출할 때 대괄호 안에 조건식을 입력하여 추출하거나 subset 함수를 이용하여 추출할 수 있습니다. 데이터가 매우 많을 경우에는 대괄호 안에 조건식을 입력하여 추출하는 것이 subset 함수를 이용하는 것 보다 더 빠릅니다.

#### 대괄호 안에 조건식 입력하여 추출

<div class="layout-chunk" data-layout="l-body">

```r
# score가 90이상인 데이터 추출
df[df$score >= 90, ]
```

```
    name age sex score
1 유재석  24  남    90
5 이영자  27  여    95
```

</div>


<div class="layout-chunk" data-layout="l-body">

```r
# score가 90이상인 데이터의 name과 age만 추출
# 1:2 대신 c("name", "age")를 사용해도 됨
df[df$score >= 90, 1:2]
```

```
    name age
1 유재석  24
5 이영자  27
```

</div>



<div class="layout-chunk" data-layout="l-body">

```r
# 조건식과 출력 컬럼명을 변수에 입력하고 이를 활용
score90 <- df$score >= 90
cols <- c("name", "age")

df[score90, cols]
```

```
    name age
1 유재석  24
5 이영자  27
```

</div>



#### subset()을 이용하여 추출

<div class="layout-chunk" data-layout="l-body">

```r
# score가 90이상인 데이터 추출
subset(df, score >= 90)
```

```
    name age sex score
1 유재석  24  남    90
5 이영자  27  여    95
```

</div>


<div class="layout-chunk" data-layout="l-body">

```r
# score가 90이상인 데이터의 name과 age만 추출
subset(df, score >= 90, select = c("name", "age"))
```

```
    name age
1 유재석  24
5 이영자  27
```

</div>


<div class="layout-chunk" data-layout="l-body">

```r
# score가 90이상인 데이터에서 age와 sex만 제외하고 추출
subset(df, score >= 90, select = -(age:sex))
```

```
    name score
1 유재석    90
5 이영자    95
```

</div>



## 데이터 프레임의 데이터 수정

<div class="layout-chunk" data-layout="l-body">

```r
# 2번째 행에 있는 홍진영의 age를 29로 수정
df$age[2] <- 29
df
```

```
    name age sex score
1 유재석  24  남    90
2 홍진영  29  여    80
3 송가인  31  여    85
4 강호동  25  남    75
5 이영자  27  여    95
6 김종민  22  남    80
7 김연아  29  여    70
```

</div>


<div class="layout-chunk" data-layout="l-body">

```r
# 3행에 있는 송가인의 score를 95로 수정
df[3, "score"] <- 95
df
```

```
    name age sex score
1 유재석  24  남    90
2 홍진영  29  여    80
3 송가인  31  여    95
4 강호동  25  남    75
5 이영자  27  여    95
6 김종민  22  남    80
7 김연아  29  여    70
```

</div>



## 데이터 프레임 구조 수정 Modify the Structure of the Data Frame 

### 데이터 프레임 행열 추가 Adding Components

#### 행 추가 adding rows

<div class="layout-chunk" data-layout="l-body">

```r
new_data <- list("김남준", 24, "남", 92)
new_data
```

```
[[1]]
[1] "김남준"

[[2]]
[1] 24

[[3]]
[1] "남"

[[4]]
[1] 92
```

```r
df <- rbind(df, new_data)
df
```

```
    name age sex score
1 유재석  24  남    90
2 홍진영  29  여    80
3 송가인  31  여    95
4 강호동  25  남    75
5 이영자  27  여    95
6 김종민  22  남    80
7 김연아  29  여    70
8 김남준  24  남    92
```

</div>


<div class="layout-chunk" data-layout="l-body">

```r
new_data <- data.frame(
  name = "이지은",
  age = 26,
  sex = "여",
  score = 93)

df <- rbind(df, new_data)
df
```

```
    name age sex score
1 유재석  24  남    90
2 홍진영  29  여    80
3 송가인  31  여    95
4 강호동  25  남    75
5 이영자  27  여    95
6 김종민  22  남    80
7 김연아  29  여    70
8 김남준  24  남    92
9 이지은  26  여    93
```

</div>


#### 열 추가 adding columns

<div class="layout-chunk" data-layout="l-body">

```r
# salary 열 추가
df$salary <- c(220, 180, 250, 170, 220, 270, 250, 290, 210)
df
```

```
    name age sex score salary
1 유재석  24  남    90    220
2 홍진영  29  여    80    180
3 송가인  31  여    95    250
4 강호동  25  남    75    170
5 이영자  27  여    95    220
6 김종민  22  남    80    270
7 김연아  29  여    70    250
8 김남준  24  남    92    290
9 이지은  26  여    93    210
```

</div>


<div class="layout-chunk" data-layout="l-body">

```r
# 또는 cbind를 활용할 수 있음
# salary 열 추가
salary2 <- c(220, 180, 250, 170, 220, 270, 250, 290, 210)
df <- cbind(df, salary2)
df
```

```
    name age sex score salary salary2
1 유재석  24  남    90    220     220
2 홍진영  29  여    80    180     180
3 송가인  31  여    95    250     250
4 강호동  25  남    75    170     170
5 이영자  27  여    95    220     220
6 김종민  22  남    80    270     270
7 김연아  29  여    70    250     250
8 김남준  24  남    92    290     290
9 이지은  26  여    93    210     210
```

</div>


<div class="layout-chunk" data-layout="l-body">

```r
salary3 <- c(220, 180, 250, 170, 220, 270, 250, 290, 210)
new_data <- data.frame(salary3)

df <- cbind(df, new_data)
df
```

```
    name age sex score salary salary2 salary3
1 유재석  24  남    90    220     220     220
2 홍진영  29  여    80    180     180     180
3 송가인  31  여    95    250     250     250
4 강호동  25  남    75    170     170     170
5 이영자  27  여    95    220     220     220
6 김종민  22  남    80    270     270     270
7 김연아  29  여    70    250     250     250
8 김남준  24  남    92    290     290     290
9 이지은  26  여    93    210     210     210
```

</div>



### 데이터 프레임 행열 삭제 Deleting Component

#### 행 삭제

<div class="layout-chunk" data-layout="l-body">

```r
# 9행 삭제
df <- df[-9, ]
df
```

```
    name age sex score salary salary2 salary3
1 유재석  24  남    90    220     220     220
2 홍진영  29  여    80    180     180     180
3 송가인  31  여    95    250     250     250
4 강호동  25  남    75    170     170     170
5 이영자  27  여    95    220     220     220
6 김종민  22  남    80    270     270     270
7 김연아  29  여    70    250     250     250
8 김남준  24  남    92    290     290     290
```

</div>


<div class="layout-chunk" data-layout="l-body">

```r
# score 가 80이하 삭제 
df <- df[!df$score < 80, ]
df
```

```
    name age sex score salary salary2 salary3
1 유재석  24  남    90    220     220     220
2 홍진영  29  여    80    180     180     180
3 송가인  31  여    95    250     250     250
5 이영자  27  여    95    220     220     220
6 김종민  22  남    80    270     270     270
8 김남준  24  남    92    290     290     290
```

</div>



#### 열 삭제

<div class="layout-chunk" data-layout="l-body">

```r
# salary3 변수(열) 삭제
df$salary3 <- NULL
df
```

```
    name age sex score salary salary2
1 유재석  24  남    90    220     220
2 홍진영  29  여    80    180     180
3 송가인  31  여    95    250     250
5 이영자  27  여    95    220     220
6 김종민  22  남    80    270     270
8 김남준  24  남    92    290     290
```

</div>


<div class="layout-chunk" data-layout="l-body">

```r
# 5열(salary)과 6열(salary2) 삭제
df <- df[, -(5:6)]
df
```

```
    name age sex score
1 유재석  24  남    90
2 홍진영  29  여    80
3 송가인  31  여    95
5 이영자  27  여    95
6 김종민  22  남    80
8 김남준  24  남    92
```

</div>



## 데이터 프레임 연산

<div class="layout-chunk" data-layout="l-body">

```r
# rowSums(), colSums(), colMeans(), rowMeans()
df2 <- df[, -c(1, 3)]
df2
```

```
  age score
1  24    90
2  29    80
3  31    95
5  27    95
6  22    80
8  24    92
```

```r
colMeans(df2)
```

```
     age    score 
26.16667 88.66667 
```

</div>


