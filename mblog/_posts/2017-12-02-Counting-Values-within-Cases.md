---
title:  "[R] Counting Values within Cases"
tags:
  - R
  - data transformation 
toc: true
toc_label: "Table of contents"
---

## Counting Values within Cases

```
df
```
```
# Result:
  x1 x2 x3 x4 x5
1  1  4  3  5  5
2  4  5  2  5  2
3  5  4  5  4  5
4  3  4  3  5  5
5  3  5  2  4  3
6  3  5 NA NA  5
7  2  3  3  3  4
```

```
# Counting number of value == 3 in each case
df$count_3 <- rowSums(df == 3, na.rm = TRUE)

# Counting number of value == 5 in each case
df$count_5 <- rowSums(df == 5, na.rm = TRUE)

df
```
```
# Result:
  x1 x2 x3 x4 x5 count_3 count_5
1  1  4  3  5  5       1       2
2  4  5  2  5  2       0       2
3  5  4  5  4  5       0       3
4  3  4  3  5  5       2       2
5  3  5  2  4  3       2       1
6  3  5 NA NA  5       1       2
7  2  3  3  3  4       3       0
```
