---
title:  "[R] Create Time Series"
tags:
  - R
  - difference
  - moving average
  - running median
  - lag
  - lead
toc: true
toc_label: "Table of contents"
---

Methods of creating time series variables are differences, moving averages, running medians, lag, lead, etc.

## Differences

```
x <- c(2, 3, 5, 7, 10, 15)

# lag : an integer indicating how many lags to use
diff(x, lag = 1, differences = 1) # [1] 1 2 2 3 5
diff(x, lag = 2, differences = 1) # [1] 3 4 5 8

# Difference : order of difference
diff(x, lag = 1, differences = 1) # [1] 1 2 2 3 5
diff(x, lag = 1, differences = 2) # [1] 1 0 1 2

diff(x, lag = 1, differences = 1) # default
diff(x, lag = 2, differences = 2) # [1] 2 4
```

## Moving averages

```
library(zoo)
x <- 1:10

rollmean(x, 5, fill = NA, align = "right")
# [1] NA NA NA NA  3  4  5  6  7  8

rollmeanr(x, 5, fill = NA)
# [1] NA NA NA NA  3  4  5  6  7  8
```
```
rollmean(x, 5, fill = NA, align = "left")
# [1]  3  4  5  6  7  8 NA NA NA NA

rollmean(x, 5, fill = NA, align = "center")
# [1] NA NA  3  4  5  6  7  8 NA NA
```

## Running medians

```
library(zoo)
x <- 1:10

rollmedian(x, 5, fill = NA, align = "right")
# [1] NA NA NA NA  3  4  5  6  7  8

rollmedian(x, 5, fill = NA, align = "center")
# [1] NA NA  3  4  5  6  7  8 NA NA

rollmedian(x, 5, fill = NA, align = "left")
# [1]  3  4  5  6  7  8 NA NA NA NA
```

## Lag

```
library(data.table)
df$x2_lag1 <- shift(x2, n=1, fill=NA, type="lag")  
```
```
library(dplyr)
df <- df %>%
  mutate(x3_lag2 = lag(x3, n=2, default=NA))

df <- df %>% 
  mutate(x5_lag1 = data.table::shift(x5, n=1, fill=NA, type="lag"))
```

## Lead

```
library(data.table)
df$x2_lead2 <- shift(x2, n=2, fill=NA, type="lead")
```
```
library(dplyr)
df <- df %>% 
  mutate(x3_lead1 = lead(x3, n=1, default=NA))
```
