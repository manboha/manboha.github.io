---
title:  "[R] Importing Data"
tags:
  - Importing data
  - CSV
  - Excel
  - SPSS
  - SAS
toc: true
toc_label: "Table of contents"
---

## From CSV

```
df <- read.csv("myfile.csv")

# the strings aren’t converted factors
df <- read.csv("myfile.csv", stringsAsFactors = F)
```

## From Excel

```
# install.packages("readxl")
library(readxl)
df <- read_excel("myfile.xlsx")
df <- read_excel("myfile.xlsx", col_names = F)
df <- read_excel("myfile.xlsx", sheet = 3)
df <- read_excel("myfile.xlsx", sheet = "my_sheet")
```

## From SPSS
```
# install.packages("Hmisc")
library(Hmisc)
df <- spss.get("mydata.sav")
```
or
```
# install.packages("foreign")
library(foreign)
df <- read.spss(file = "mydata.sav", to.data.frame = T)
```

## From SAS
```
# install.packages("Hmisc")
library(Hmisc)
df <- sasxport.get("mydata.xpt")
```
or
```
# install.packages("sas7bdat))
library(sas7bdat))
df <- read.sas7bdat("mydata.sas7bdat")
```
