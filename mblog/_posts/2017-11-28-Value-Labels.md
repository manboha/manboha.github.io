---
title:  "[R] Value Labels"
last_modified_at: 2017-11-28 T22:50:00
tags:
  - R
  - Value Labels
toc: true
toc_label: "Table of contents"
---

## Value Labels

### factor
```
# variable x1 is coded 1, 2, 3
# value labels 1=one, 2=two, 3=three

df$x1 <- factor(df$x1, levels=c(1, 2, 3), 
                labels=c("one", "two", "three"))
```

### ordered
```
# variable x1 is coded 1, 2, 3
# value labels 1=low, 2=medium, 3=high

df$x1 <- ordered(df$x1, levels=c(1, 2, 3), 
                 labels=c("low", "medium", "high"))
```
