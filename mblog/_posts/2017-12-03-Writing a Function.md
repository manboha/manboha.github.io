---
title:  "[R] Writing a Function"
tags:
  - R
  - Function  
toc: true
toc_label: "Table of contents"
---

```
# The function template
my_fun <- function(arg1, arg2) {
  # body
}
```

```
# Define ratio() function
ratio <- function(x, y) {
  x/y
}
ratio(3, 4) # => 0.75
```

```
# Function output
fu <- function(x) {
  if (TRUE) {
    return(x + 1)
  }
  x
}
fu(5) # => 6
```

```
ag <- function(a = 1, b = a * 2) {
  c(a, b)
}
ag() # [1] 1 2
ag(3, 2) # [1] 3 2
```
