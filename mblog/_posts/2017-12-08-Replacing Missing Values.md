---
title:  "[R] Replacing Missing Values"
tags:
  - R
  - missing value
toc: true
toc_label: "Table of contents"
---

## Remove
```
# Removing cases with missing values
x <- c(1, 2, 3, 4, 5, 6, 7, 8, NA, NA, 11, 12)
df_no_missing <- na.omit(x)
```
```
mean(x, na.rm = T )
```

## With mean, median, mode
```
# Replacing missing values with the mean
x <- c(1, 2, 3, 4, 5, 6, 7, 8, NA, NA, 11, 12)
x_mean <- mean(x, na.rm=TRUE)
x <- ifelse(is.na(x), x_mean, x)
```
```
# Replacing missing values with the median
x_median <- median(x, na.rm = T)
df$v1 <- ifelse(is.na(x), x_median, x)
```
```
# package imputeTS
library(imputeTS)
na.mean(x, option="mean")
na.mean(x, option="median")
na.mean(x, option="mode")
```

## LOCF - Last Observation Carried Forward
```
library(imputeTS)
x2 <- c(NA,3,4,5,6,NA,7,8)

# Last Observation Carried Forward and reverse remaining NAs
na.locf(x2, option = "locf", na.remaining = "rev") # default

# Next Observation Carried Backward and reverse remaining NAs
na.locf(x2, option = "nocb")

# LOCF and remove remaining NAs
na.locf(x2, na.remaining = "rm")
```

## Mean of nearby points
```
library("zoo")
x <- c(1, 2, 3, 4, 5, 6, 7, 8, NA, NA, 11, 12)

(na.locf(x) + rev(na.locf(rev(x))))/2
```

## Interpolation
```
library(imputeTS)
x <- c(1, 2, 3, 4, 5, 6, 7, 8, NA, NA, 11, 12)

# linear interpolation
na.interpolation(x, option = "linear")

# spline interpolation
na.interpolation(x, option = "spline")

# Stineman interpolation
na.interpolation(x, option = "stine")
```

## Weighted Moving Average
```
library(imputeTS)
x <- c(1, 2, 3, 4, 5, 6, 7, 8, NA, NA, 11, 12)

# exponential weighted moving average, window size 4(2 left, 2 right)
na.ma(x, k = 4, weighting = "exponential")

# Simple Moving Averag
na.ma(x, k = 4, weighting = "simple")

# Linear Weighted Moving Average
na.ma(x, k = 6, weighting = "linear")
```

## Kalman Smoothing and State Space Models
```
library(imputeTS)
x <- c(1, 2, 3, 4, 5, 6, 7, 8, NA, NA, 11, 12)

# With KalmanSmooth and StructTS model
na.kalman(x, model = "StructTS", smooth = TRUE)

# With KalmanRun and StructTS model
na.kalman(x, model = "StructTS", smooth = FALSE)

# With KalmanSmooth and state space representation of arima model
na.kalman(x, model = "auto.arima", smooth = TRUE)

# With KalmanRun and state space representation of arima model
na.kalman(x, model = "auto.arima", smooth = FALSE)

# With KalmanSmooth and StructTS model with additional parameters 
na.kalman(x, model ="StructTS", smooth = TRUE, type ="trend") 
# The local level model, type = "level"
# The local linear trend model, type = "trend"
# The basic structural model, type = "BSM"
```

## Seasonally Decomposed Missing Value Imputation
```
# default (by Interpolation)
na.seadec(x, algorithm = "interpolation")

# Last Observation Carried Forward
na.seadec(x, algorithm = "locf")

# other algorithm : "mean", "random", "kalman", "ma" 
```

## Seasonally Splitted Missing Value Imputation
```
# default (by Interpolation)
na.seasplit(x, algorithm = "interpolation")

# other algorithm : "locf", mean", "random", "kalman", "ma" 
```





