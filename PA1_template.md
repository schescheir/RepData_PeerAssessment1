Peer Assessment Project 1- Reproducible Research
========================================================

This is an R Markdown document that will be used to completed Peer Assessment Project #1 for the Coursera Class "Reproducible Research."

The responses for this will be follow the evaluation tool inorder to more easily be evaluated by you, the evaluator.  Different sections will be identifed with astrixes (****).  

**** Reading and Processing  ****

This reads the .csv file into R and then (since the assignment asks us to ignore missing values), omits observations that have a NA value for steps.


```r
wal <- read.csv("activity.csv")
```

```
## Warning in file(file, "rt"): cannot open file 'activity.csv': No such file
## or directory
```

```
## Error in file(file, "rt"): cannot open the connection
```

```r
walk <- na.omit(wal)
```

```
## Error in na.omit(wal): object 'wal' not found
```

**** Histogram  ****


```r
hwalk <- tapply(walk$steps, walk$date, sum)
```

```
## Error in tapply(walk$steps, walk$date, sum): object 'walk' not found
```

```r
hist(hwalk)
```

```
## Error in hist(hwalk): object 'hwalk' not found
```


**** Mean and Median ****

Mean

```r
tapply(walk$steps, walk$date, mean)
```

```
## Error in tapply(walk$steps, walk$date, mean): object 'walk' not found
```

Median

```r
tapply(walk$steps, walk$date, median)
```

```
## Error in tapply(walk$steps, walk$date, median): object 'walk' not found
```

**** Time series plot **** 


```r
twalk <- tapply(walk$steps, walk$interval, mean)
```

```
## Error in tapply(walk$steps, walk$interval, mean): object 'walk' not found
```

```r
plot(levels(factor(walk$interval)), twalk, type = "l")
```

```
## Error in factor(walk$interval): object 'walk' not found
```

****  Point with maximum number of average (mean) steps per interval. **** 

To do this we used the which.max command.  The top is the begining of the interval and the section is the factor levlel associated with that interval.


```r
which.max(twalk)
```

```
## Error in which.max(twalk): object 'twalk' not found
```

**** Imputing missing values. **** 

The decision has been made to input all missing values with the median daily value for that day.  However there is an issue.  For 8 days the median is NA.  This is because for those days there are NO measured values through out the day, and thus, after NA's have been omitted they have zero value.  To deal with that those days much first be removed from the data set:

To this end days that were found to be NA after NA values were removed were idetified.  The were then isolated.  The labels for these values were then found and subsetted out of the original dataframe (before removal of na's as done by na.omit during processing).

The dates that now were removed were subsequently removed as factors.


```r
swalk <- tapply(walk$steps, walk$date, median)
```

```
## Error in tapply(walk$steps, walk$date, median): object 'walk' not found
```

```r
nswalk <- is.na(swalk)
```

```
## Error in eval(expr, envir, enclos): object 'swalk' not found
```

```r
toBeRemoved <- which(nswalk == TRUE)
```

```
## Error in which(nswalk == TRUE): object 'nswalk' not found
```

```r
brbr <- labels(toBeRemoved)
```

```
## Error in labels(toBeRemoved): object 'toBeRemoved' not found
```

```r
brbr
```

```
## Error in eval(expr, envir, enclos): object 'brbr' not found
```

```r
walk2 <-wal
```

```
## Error in eval(expr, envir, enclos): object 'wal' not found
```

```r
for(i in 1:8) {  
     walk2 <-subset(walk2, date != brbr[i])
     walk2
}
```

```
## Error in subset(walk2, date != brbr[i]): object 'walk2' not found
```

```r
walk2$date <- as.factor(as.character(walk2$date))
```

```
## Error in is.factor(x): object 'walk2' not found
```

```r
walk <- walk2
```

```
## Error in eval(expr, envir, enclos): object 'walk2' not found
```

Next the median of the remaining days was taken:


```r
tapply(walk$steps, walk$date, median)
```

```
## Error in tapply(walk$steps, walk$date, median): object 'walk' not found
```

And all medians were found to be zero.  As such remaining NA's were replaced with 0's.  While there are no more NA values that was accomplished by:


```r
walk2[is.na(walk2)] <- 0
```

```
## Error in walk2[is.na(walk2)] <- 0: object 'walk2' not found
```

****  Histogram of post-NA replacement **** 


```r
hwalk2 <- tapply(walk2$steps, walk2$date, sum)
```

```
## Error in tapply(walk2$steps, walk2$date, sum): object 'walk2' not found
```

```r
hist(hwalk2)
```

```
## Error in hist(hwalk2): object 'hwalk2' not found
```

****  Weekdays and Weekends **** 

Firstly we need to convert the date column to date.  Then assign them the day of the week.  Then create two data frames, ones with weekends days and one with week day days.  


```r
walk2$date <- as.Date(walk2$date)
```

```
## Error in as.Date(walk2$date): object 'walk2' not found
```

```r
walk2$wkdy <-weekdays(walk2$date)
```

```
## Error in weekdays(walk2$date): object 'walk2' not found
```

```r
walk2s <- subset(walk2, walk2$wkdy == "Sunday")
```

```
## Error in subset(walk2, walk2$wkdy == "Sunday"): object 'walk2' not found
```

```r
walk2ss <- subset(walk2, walk2$wkdy == "Saturday")
```

```
## Error in subset(walk2, walk2$wkdy == "Saturday"): object 'walk2' not found
```

```r
walk2weekends <- rbind(walk2s, walk2ss)
```

```
## Error in rbind(walk2s, walk2ss): object 'walk2s' not found
```

```r
walk2m <- subset(walk2, walk2$wkdy == "Monday")
```

```
## Error in subset(walk2, walk2$wkdy == "Monday"): object 'walk2' not found
```

```r
walk2t <- subset(walk2, walk2$wkdy == "Tuesday")
```

```
## Error in subset(walk2, walk2$wkdy == "Tuesday"): object 'walk2' not found
```

```r
walk2w <- subset(walk2, walk2$wkdy == "Wednesday")
```

```
## Error in subset(walk2, walk2$wkdy == "Wednesday"): object 'walk2' not found
```

```r
walk2th <- subset(walk2, walk2$wkdy == "Thursday")
```

```
## Error in subset(walk2, walk2$wkdy == "Thursday"): object 'walk2' not found
```

```r
walk2f <- subset(walk2, walk2$wkdy == "Friday")
```

```
## Error in subset(walk2, walk2$wkdy == "Friday"): object 'walk2' not found
```

```r
walk2weekdays <- rbind(walk2m, walk2t, walk2w, walk2th, walk2f)
```

```
## Error in rbind(walk2m, walk2t, walk2w, walk2th, walk2f): object 'walk2m' not found
```

Then we need to find the averages and make the graphs.


```r
twalkwd <- tapply(walk2weekdays$steps, walk2weekdays$interval, mean)
```

```
## Error in tapply(walk2weekdays$steps, walk2weekdays$interval, mean): object 'walk2weekdays' not found
```

```r
twalkwe <- tapply(walk2weekends$steps, walk2weekends$interval, mean)
```

```
## Error in tapply(walk2weekends$steps, walk2weekends$interval, mean): object 'walk2weekends' not found
```

```r
par(mfrow =c(1,2))
plot(levels(factor(walk2weekends$interval)), twalkwe, type = "l", main= "Weekends", xlab = "Intervals", ylab = "Steps")
```

```
## Error in factor(walk2weekends$interval): object 'walk2weekends' not found
```

```r
plot(levels(factor(walk2weekdays$interval)), twalkwd, type = "l", main= "Weekdays", xlab = "Intervals", ylab = "Steps")
```

```
## Error in factor(walk2weekdays$interval): object 'walk2weekdays' not found
```
