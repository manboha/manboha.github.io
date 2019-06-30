---
title:  "[R] Basic Data Types"
tags:
  - R Basic
  - Vector
  - Data Type
toc: true
toc_label: "Table of contents"
---

## Numeric data

```
100000 # => 1e+05
150000000 # => 1.5e+08
5e+3 # => 5000
5e-3 # => 0.005
```

```
"3" * 2 # Error in "3" * 2 : non-numeric
as.numeric("3") * 2 # charater to nemeric
```

```
x <- 21
is.numeric(x)  # if x is nemeric

y <- 5L  
is.integer(y)  # if y is integer

class(4L)  # => integer
class(2.8)  # => numeric
4L * 2.8  # => 11.2
```
 
## Character data

```
han   # Error: object 'han' not found
"han"   # => "han"
한글   # Error: object '한글' not found
"한글"   # => "한글"
```

Count the Number of Characters
```
x <- "대한민국"
nchar(x)   # ⇒ 4
nchar("hello")  # ⇒ 5
nchar(3)  # ⇒ 1
nchar(532)  # ⇒ 3
```
 
## Logical data

```
3 >= 5   # ⇒ FALSE
2 != 3  # 2와 3은 다른가 ? ⇒ TRUE
```

TRUE is 1, FALSE is 0
```
TRUE * 3  # 1*3 = 3
FALSE * 3  # 0*3 = 0
```

## Date data 

```
today <- Sys.Date() 
now <- Sys.time()  

# the current system date and time in english "Sun Oct 23 14:00:25 2016"
today2 <- date() 
```

```
# as.Date( ) to convert strings to dates 
mydates <- as.Date(c("2016-07-21", "2015-03-15"))
mydates[1] - mydates[2]  # => Time difference of 494 days
```

Symbols to print dates by the foramt()

| Symbol | Meaning                | Example   |
|--------|------------------------|-----------|
| %d     | day as a number (0-31) | 01~31     |
| %m     | month (00-12)          | 00-12     |
| %y     | 2-digit year           | 16        |
| %Y     | 4-digit year           | 2017      |
| %a     | abbreviated weekday    | Mon       |
| %A     | unabbreviated weekday  | Monday    |
| %b     | abbreviated month      | Jan       |
| %B     | unabbreviated month    | January   |

```
today <- Sys.Date()
format(today, format="%Y년 %m월 %d일(%A)")
format(today, format="%Y.%m.%d(%a)")
```

as.Date(x, "format")
```
as.Date("2015-05-21")  # => "2015-05-21"
as.Date("02/05/2015", "%m/%d/%Y")  # => "2015-02-05"
as.Date("2015년 2월 5일", "%Y년 %m월 %d일") 
as.Date("161215", "%y%m%d") # => "2016-12-15"
as.Date("01-11-2016", "%d-%m-%Y")  # => "2016-11-01"
```

as.numeric() and as.character()
```
myday <- as.Date("2016-11-21")
as.numeric(myday)  # => 17126
as.character(myday)  # => "2016-11-21"
```

as.POSIXct()
```
as.POSIXct("2016-05-21 17:25") # => "2016-05-21 17:25:00 KST"
```

## Missing data

NA (not available) is the symbol of missing values

### Testing for missing values
```
x <- c(2, NA, 7, NA, 6)
is.na(x) # => FALSE  TRUE FALSE  TRUE FALSESE
s <- c("대한", NA, "민국")
is.na(s)  # => FALSE  TRUE FALSE
```
### Recoding values to missing
```
# recode 99 to missing for variable v1
df1$v1[df1$v1==99] <- NA
```

### Excluding missing values from analyses
```
x <- c(2, NA, 7, NA, 6)
mean(x) # => NA
mean(x, na.rm=TRUE) # => 5
```

### Deletion of missing values in data frame
```
x <- c(21, NA, 23, NA, 25)
y <- c(1, 2, NA, 4, 5)
df <- data.frame(x, y)

# All deletion of missing values
newdf <- df[!complete.cases(df),]
newdf <- na.omit(df)

# dletion of missing values by a variable
newdf <- df[complete.cases(df$x),]
df[complete.cases(df$y),]

library(dplyr) 
newdf <- df %>% filter(!is.na(x))
```

## NULL Object
```
str(df$x)  # => num [1:5] 21 NA 23 NA 25
df$x <- NULL   # delete df$x
str(df$x)  # => NULL
```
