---
title:  "[R] Shift Values - Lag & Lead"
tags:
  - R
  - data transformation
toc: true
toc_label: "Table of contents"
---

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
