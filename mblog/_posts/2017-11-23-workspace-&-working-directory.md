---
title:  "[R] Workspace & Working Directory"
last_modified_at: 2017-11-22 T19:00:00
tags:
  - R Basic
  - workspace
  - working directory
toc: true
toc_label: "Table of contents"
---

## workspace

```
# save the workspace to the file .RData in the current working directory 
save.image()

# save the workspace to the file "ws2.RData"
save.image(file = "ws2.RData")
load("ws2.RData")  # load workspace into the current session

ls()  # present objetcs in current workspace
```

## working directory

> [Note] for Windows Users (path :  \ –> / )
> (X) c:\mydocuments\myfile.txt
> (O) c:/mydocuments/myfile.txt

```
getwd() # print the current working directory

setwd(mydirectory)      # change to working directory
setwd("c:/docs/mydir") 
setwd("/usr/rob/mydir")

dir()  # list the files in the current working directory
dir(all.files = TRUE)  
list.files()  # dir()
```

## options

```
help(options) 
options() 
options(digits=3) 
```

## command history

```
history() # recall the last 25 used commands
history(max.show=Inf)  # recall the last all used commands

savehistory(file="myfile")  # save the commands history
loadhistory(file="myfile") # load the commands history

savehistory()  # save to ".Rhistory"
loadhistory()  # load from ".Rhistory"
```

## save & load objects

```
save(object list, file="myfile.RData")  # save objects
load("myfile.RData")  # load objets
```
