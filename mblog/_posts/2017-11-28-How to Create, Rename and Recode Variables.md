---
title:  "[R] How to Create, Rename and Recode Variables"
tags:
  - R Basic
  - Data Manipulation
  - variable
  - recode
  - rename
toc: true
toc_label: "Table of contents"
---

## Create New Variables

```
df$sum <- df$x1 + df$x2
df$mean <- (df$x1 + df$x2)/2
```
```
library(dplyr)
df <- df %>% 
  mutate(sum = x1 + x2,
         mean = (x1 + x2)/2)
```

## Rename variables

```
names(df)  # => "x1"   "x2"   "sum"  "mean"
names(df)[1] <- "v1"   # x1 -> v1
```
```
library(dplyr)
df <- df %>% rename(v1 = x1,
                    v2 = x2)
```

## Recode Into Different Variables

```
# ifelse function
df$ageg <- ifelse(df$age < 30, "young",
                  ifelse(df$age < 60, "middle", "old"))
```
```
# on vector
df$ageg[df$age < 30] <- "young"
df$ageg[df$age >= 30 & df$age < 60] <- "middle"
df$ageg[df$age >= 60] <- "old"
```
```
# dplyr package
library(dplyr)
df <- df %>% 
  mutate(ageg = ifelse(age < 30, "young",
                        ifelse(age < 60, "middle", "old")))
```
```
# create new variables containing ranks
df$v1_rank <- rank(v1)
```

## Recode into Same Variables

```
# Replace all the data in a variable with a number
df$grade <- 5

# Replace all the data in a variable with text
df$grade <- "Five"

# Replace all the data in a variable with NA (missing data)
df$grade <- NA
```
```
# Replace the data in a variable based on equal to some value
df$x1[df$x1 == 99] <- NA

# Replace based on greater than or equal to some value
df$x1[df$x1 <= 5] <- "Low"

# Replace only missing data
df$x1[is.na(df$x1)] <- "Missing"
```

## Delete Variables

```
df$ageg <- NULL
```
