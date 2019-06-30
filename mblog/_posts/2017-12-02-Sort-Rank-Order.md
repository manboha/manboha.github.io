---
title:  "[R] Sort, Rank and Order"
tags:
  - R
  - Sort
  - Rank
  - Order
toc: true
toc_label: "Table of contents"
---

## Sort

```
# sample variable
df$v1
# [1] 16 13 39 88 67  4 51 98 56 61 NA

# Sort a variable. NA is removed(default).
sort(df$v1)
# [1]  4 13 16 39 51 56 61 67 88 98

# Sort a variable in descresing order
sort(df$v1, decreasing = T)
# [1] 98 88 67 61 56 51 39 16 13  4

# NAs are put in the end 
sort(df$v1, decreasing = T, na.last = T)
# [1] 98 88 67 61 56 51 39 16 13  4 NA

# NAs are put in the front
sort(df$v1, decreasing = T, na.last = F)
# [1] NA 98 88 67 61 56 51 39 16 13  4
```
```
# ordered levels in factor
df$v2 <- factor(df$v2, levels = c("high", "middle", "low"))
df$v2
# [1] high   middle low    high   high   middle high  
# [8] high   middle high   <NA>  
# Levels: high middle low

# Sort the factor
sort(df$v2)
# [1] high   high   high   high   high   high   middle
# [8] middle middle low   
# Levels: high middle low
```

## Rank

```
df$v1
# [1] 16 13 39 88 67  4 51 98 56 61 NA

# Return the ranks of elements in increasing order 
rank(df$v1)
# [1]  3  2  4  9  8  1  5 10  6  7 11

# Return the ranks of elements in descresing order 
rank(-df$v1)
# [1]  8  9  7  2  3 10  6  1  5  4 11

# NA is removed 
rank(df$v1, na.last = NA)
# [1]  3  2  4  9  8  1  5 10  6  7

# NAs are put in the end
rank(df$v1, na.last = T)
# [1]  3  2  4  9  8  1  5 10  6  7 11

# NAs are put in the front
rank(df$v1, na.last = F)
# [1]  4  3  5 10  9  2  6 11  7  8  1

# NAs are keep
rank(df$v1, na.last = "keep")
# [1]  3  2  4  9  8  1  5 10  6  7 NA
```

## order

```
# the ranked position of each element
order(df$v1)
# [1]  6  2  1  3  7  9 10  5  4  8 11
# 6th element(== 1) is first

# NA is removed
order(df$v1, na.last = NA)

# Sort a variable in ordered index
df$v1[order(df$v1, na.last = NA)]
# [1]  4 13 16 39 51 56 61 67 88 98  == sort(df$v1)
```
