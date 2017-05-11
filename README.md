# AmeliaIITest
---
title: "AmeliaII"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

Test
```{r}
library(Amelia)
require(Amelia)
data("freetrade")
freetrade$year
```
Test from other guy's paper
```{r}
id<-rep(1:15,each=10)
time<-rep(1:10,15)
set.seed(1234)
map.raw<-abs(round(rnorm(150,mean=50,sd=25)))
map<-round(ifelse(map.raw>=30,map.raw,map.raw+50))
set.seed(1234)
lac<-round(3-map*0.06+rnorm(150,mean=0,sd=0.4)-
0.4*time*time+4.3*time,1)
set.seed(1234)

lac.miss.tag<-rbinom(150, 1, 0.3)
lac.miss<-ifelse(lac.miss.tag==1,NA,lac)
set.seed(123456)
age<-rep(round(abs(rnorm(15, mean = 65, sd =
19))),each=10)
data<-data.frame(id,time,age,map,lac.miss)
data
data1 = cbind(id = data$id, time = data$time)
data1 = as.data.frame(data1)
data1[10:15,2] = NA
dim(data1)
# You can have three scores.  Have a time variable that is qualiative indicating the phase they are in so A1 B1 A2, and maybe the time as well, because more data doesn't really hurt (cite the Amelia guys)
# So figure out what the ts and cs are for.  I think TS is for time series variable and cs is for cross section variable
a.out <- amelia(data1, m = 5, ts = "time", idvars = "id")
```

