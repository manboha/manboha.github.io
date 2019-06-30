---
title: "[R] Random Number Generators"
tags:
  - R
  - random number  
toc: true
toc_label: "Table of contents"
---

## Seed
```
# an exact replication of random numbers
set.seed(1)
runif(2) # => 0.2655087 0.3721239

set.seed(1)
runif(2) # => 0.2655087 0.3721239
```
    
## Uniformly distributed random numbers
```
# Generate a number

runif(1)

# Generate a vector of 5 numbers
runif(5)

# Generate a vector of 5 numbers from 0 to 100
runif(5, min=0, max=100)

# Generate 5 integers from 0 to 100
# max=101 : because of floor function
floor(runif(500, min=0, max=101))

# Generate 5 integers from 0 to 100
sample(1:100, 5, replace=TRUE)

# Generate 5 integers from 0 to 100 without replacement
sample(1:100, 5, replace=FALSE)

# Generate integers from 1 to 5 in a multinomial distribution
sample(1:5, 100, rep=TRUE, prob=c(.2, .25, .2, .25, .1))

# Random items from a list
sample(state.name, 10)
```

## Normal distributed random numbers
```
# Generate 5 noram random vector(mean=0, sd=1)
rnorm(5)

# different mean and standard deviation
rnorm(5, mean=30, sd=5)

# make a histogram of a normal distributed numbers
x <- rnorm(500, mean=0, sd=10)
hist(x)
```

