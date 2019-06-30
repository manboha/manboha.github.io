---
title:  "[R] Control Structures"
tags:
  - R Basic
  - ifelse
  - for
  - while
  - switch
  - repeat
toc: true
toc_label: "Table of contents"
---

## ifelse
```
# ifelse(test, yes, no)
ifelse(x <= 10, "less than 10", "greater than 10")
```

## if
```
if(x > 0){
   print("Positive number")
}
```
```
if (x <= 10) {
  print("less than 10")
} else {
  print("greater than 10")
}
```

## for
```
for (i in 1:10) {
    print(i)
}
```
```
for (i in 2:9) {
  for (j in 1:9) {
    print(i*j)
  }
}
```

## while
```
i <- 1
while (i < 10) {
    print(i)
    i <- i + 1
}
```

## break
To stop the iterations and flow the control outside of the loop.
```
for (x in 1:10) {
    if (x == 3){
        break
    }
    print(x)
}
```

## next
To skip the current iteration of a loop without terminating it.
```
for (x in 1:5) {
    if (x == 3){
        next
    }
    print(x)
}
```

## repeat
```
x <- 1
repeat {
   print(x)
   x = x+1
   if (x == 6){
       break
   }
}
```

## switch
```
switch(2, "red", "green", "blue")  # => "green"
switch("shape", 
       color = "red", 
       shape = "square", 
       length = 5)   # => "square"
```
```
choice <- "high"
switch(choice,
       high = {
         print("choice is high")
       },
       low = {
         print("choice is low")
       },
       {
         print("this is default")
       }
)
```
