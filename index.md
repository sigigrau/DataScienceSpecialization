Practical Machine Learning Project
========================================================

The quantified self is a movement of people that uses technological gadgets to measure themselves for different reasons, such us improving their health, learn about their habits or testing brand new technology. For this study, we are going to use a dataset of measures of a group of volunteers who measured themselves doing barbell lifts correctly and incorrectly in 5 different ways. Using a machine learning algorithm, we are going to predict the manner in which the participants did the exercice.

For the data subsetting we are going to use the Caret package.
 

```r
library(caret)
```

```
## Warning: package 'caret' was built under R version 3.1.2
```

```
## Loading required package: lattice
## Loading required package: ggplot2
```

```r
library(data.table)
```

# Data download

First of all, we are going to download the training and test data:


```r
downloadData <- function() {
    download.file("http://d396qusza40orc.cloudfront.net/predmachlearn/pml-training.csv", "pml-training.csv")
    download.file("http://d396qusza40orc.cloudfront.net/predmachlearn/pml-testing.csv", "pml-testing.csv")
}
```

# Data process

We remove the corrupted data.


```r
data <- read.csv("./pml-training.csv", na.strings = c("NA", ""))
data = data[,-c(1:7)]
```

# Prediction 

Then we split the data into a train and a test set:


```r
inTrain <- createDataPartition(y=data$classe, p=0.6, list=FALSE)
training <- data[inTrain,]
testing <- data[-inTrain,]
```

And we predict the classe variable using random forest:


```r
model <- train(classe~., method="rf", data=training)
```

```
## Error: contrasts can be applied only to factors with 2 or more levels
```















