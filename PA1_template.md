---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---

## Set default options and your working directory

```r
opts_chunk$set(echo=TRUE)
setwd("~/R Code/RepData_PeerAssessment1")
```

## Load the data in a usable form and display a summary of data

```r
RawData <- read.csv("activity.csv",header = TRUE)
summary(RawData)
```

```
##      steps                date          interval     
##  Min.   :  0.00   2012-10-01:  288   Min.   :   0.0  
##  1st Qu.:  0.00   2012-10-02:  288   1st Qu.: 588.8  
##  Median :  0.00   2012-10-03:  288   Median :1177.5  
##  Mean   : 37.38   2012-10-04:  288   Mean   :1177.5  
##  3rd Qu.: 12.00   2012-10-05:  288   3rd Qu.:1766.2  
##  Max.   :806.00   2012-10-06:  288   Max.   :2355.0  
##  NA's   :2304     (Other)   :15840
```


## What is mean total number of steps taken per day across all intervals?


```r
ProcessData <- na.omit(RawData) ## remove NA's
TotalStepsDay <- aggregate(.~date,data=ProcessData,FUN=sum) ## aggregate by date and sum steps
hist(ProcessData$steps, main = "Total Steps Each Day", xlab = "Steps")
```

![plot of chunk meansteps](figure/meansteps-1.png) 

```r
MeanSteps <- mean(TotalStepsDay$steps)
```
### The mean number of steps taken is 10766.


## What is the average daily activity pattern?

```r
AveStepsDay <- aggregate(.~interval,data=RawData,FUN=mean) ## find average steps each day for each by 5 minute interval
with(AveStepsDay,plot(interval,steps,type="l"))
title(main="Average Steps Taken per 5 minute Interval",xlab = "5MinInterval",ylab = "Ave Steps")
```

![plot of chunk dailypattern](figure/dailypattern-1.png) 

```r
MaxIdx <- which.max(AveStepsDay$steps) ## find index of max value
```

### The 835 is the 5 minute interval, on average over all days, that contains the maximum number of steps

## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
