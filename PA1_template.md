# Reproducible Research: Peer Assessment 1
## Loading and preprocessing the data
Show any code that is needed to.

1. Load the data.


```r
da<-read.csv("activity.csv")
```

2. Process/transform the data (if necessary) into a format suitable for your analysis

```r
library(ggplot2)
da$date<-as.Date(da$date)
datime<-as.POSIXlt(da$date)
```

## What is mean total number of steps taken per day?
1. Calculate the total number of steps taken per day.

The mean total number of steps taken per day is:

```r
mean(with(da, tapply(steps, date, sum)),na.rm=T)
```

```
## [1] 10766.19
```

2. If you do not understand the difference between a histogram and a barplot, research the difference between them. Make a histogram of the total number of steps taken each day.


```r
hist(with(da, tapply(steps, date, sum))
     ,main="Histogram: Total number of steps taken each day"
     ,xlab="Number of Steps"
     ,col="gray"
     ,breaks=8)
```

![](PA1_template_files/figure-html/unnamed-chunk-5-1.png) 

3. Calculate and report the mean and median of the total number of steps taken per day.


```r
summary(with(da, tapply(steps, date, sum)))
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
##      41    8841   10760   10770   13290   21190       8
```


## What is the average daily activity pattern?
1. Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)

```r
y<-with(da, tapply(steps, date, mean))
x<-with(da, tapply(date, date, max))
x<-as.POSIXlt(names(x))
##plot(x,y,main="Daily Activity Pattern",type="l",xlab="date",ylab="steps")
qplot(x,y)
```

```
## Warning: Removed 8 rows containing missing values (geom_point).
```

![](PA1_template_files/figure-html/unnamed-chunk-7-1.png) 

## Imputing missing values
If we imput missing values the mean of the values is NA:

```r
mean(with(da, tapply(steps, date, sum)),na.rm=F)
```

```
## [1] NA
```

## Are there differences in activity patterns between weekdays and weekends?
For that, we do:
* Extract the week's days.

```r
wd<-weekdays(da$date)
```


