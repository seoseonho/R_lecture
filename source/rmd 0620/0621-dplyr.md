---
title: "0621 dplyr"
output:
  html_document:
    keep_md: true
date: '2022-06-21'
---



# p.98
# 분석 프로세스

# 데이터 전처리를 위한 도구 dplyr
# 데이터 전처리를 위한 도구 data.table

## 처리속도 차이
# dplyr : 10gb 이내
# data.table : 50gb 이상

# 배움의 측면
# dplyr 매우 쉬움
# data.table 어려움

# 라이브러리 불러오기
# install.packages("dplyr")

```r
library(dplyr)
```

```
## 
## 다음의 패키지를 부착합니다: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
mpg1 <- read.csv("mpg1.csv", stringsAsFactors = F)
```



```r
str(mpg1)
```

```
## 'data.frame':	234 obs. of  5 variables:
##  $ manufacturer: chr  "audi" "audi" "audi" "audi" ...
##  $ trans       : chr  "auto" "manual" "manual" "auto" ...
##  $ drv         : chr  "f" "f" "f" "f" ...
##  $ cty         : int  18 21 20 21 16 18 18 18 16 20 ...
##  $ hwy         : int  29 29 31 30 26 26 27 26 25 28 ...
```

```r
data2 <- mpg1 %>%
  select(drv, cty, hwy) %>% 
  filter(drv == "f")
```





```r
str(mpg1)
```

```
## 'data.frame':	234 obs. of  5 variables:
##  $ manufacturer: chr  "audi" "audi" "audi" "audi" ...
##  $ trans       : chr  "auto" "manual" "manual" "auto" ...
##  $ drv         : chr  "f" "f" "f" "f" ...
##  $ cty         : int  18 21 20 21 16 18 18 18 16 20 ...
##  $ hwy         : int  29 29 31 30 26 26 27 26 25 28 ...
```

```r
data2 <- mpg1 %>%
  select(drv, cty, hwy) %>% 
  filter(drv == "f")
```
 
  #select : 컬러명 추출
  #filter : 행 추출 (조건식)
  # group by :
  # summarize() :
   


```r
data3 <- select(mpg1, drv, cty, hwy)
data3 <- filter(data3, drv == "f")
```

%>% <- 컨트롤+쉽프트+m


# 교재 p99 ~ p120
# 파생변수 만들기
# filter, select, rename, mutate
 glimpse(iris)
 


```r
iris %>% 
  # species, setosa versicolor
  filter(Species != "virginica") %>% 
  select(Sepal.Length, Sepal.Width) %>% 
  filter(Sepal.Length > 5.0) %>% 
  mutate(total = Sepal.Length + Sepal.Width) ->data2
```
  


```r
iris %>% 
  # species, setosa versicolor
  filter(Species != "Virginica"& Sepal.Length> 5.0) %>%   
  select(Sepal.Length, Sepal.Width) %>% 
  mutate(total = Sepal.Length + Sepal.Width) ->data3
```
 
 # p.121 집단별 통계량
 # p.122
   
   

```r
mpg1 %>%  
    group_by(trans) %>% 
    summarise(avg = mean(cty)     # 평균
           ,total = sum(cty)      # 총합
           ,med   = median(cty)  
           ,count = n()) # 중간값
```

```
## # A tibble: 2 × 5
##   trans    avg total   med count
##   <chr>  <dbl> <int> <int> <int>
## 1 auto    16.0  2507    16   157
## 2 manual  18.7  1438    18    77
```




 
 
 
 
 
 
 
 
 
 빈도분석 p.99
 count (데이터세트, 변수)
 table (데이터세트 $변수)

 

count(mpg1, trans)

trans n
1 auto 157
2 manual 77

# class() 함수 안에 count () 함수를 바로 넣음




```r
class(count(mpg1, trans))
```

```
## [1] "data.frame"
```

"data. frame"





```r
table(mpg1$trans)
```

```
## 
##   auto manual 
##    157     77
```

 auto manual 
   157     77 
   
p102

방법1 새 데이터세트 <- 데이터세트 %>% select(열1,열2,열3)

방법2 새 데이터세트 <- select(데이터세트,열1,열2,열3)



```r
mpg1_1 <- mpg1 %>%  select(manufacturer,trans,cty) 

mpg1_2 <- select(mpg1,manufacturer, trans, cty)
```

str(mpg1_1) #str(mpg1_2)의 결과도 같음
'data.frame' : 234obs. of 3 variables:
$maunfacturer: chr "audi" "audi"....
$trans       : chr "auto" "manual" "manual""auto"
$cty         : int 18 21 20 21 16 18 18 18 16 20
