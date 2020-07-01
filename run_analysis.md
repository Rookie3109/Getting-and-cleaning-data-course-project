# Getting and cleaning data course project

## Data description & Source file URLs

```
dataDescription <- "http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones"
dataUrl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
```
Download and Extract the Zip archive
```
# download.file(dataUrl, destfile = "data.zip")
# unzip("data.zip")
```

## Merge training and test sets to create one dataset
Read activity and feature labels
```
activity_labels <- read.table("./UCI HAR Dataset/activity_labels.txt") #V2 contains label
features <- read.table("./UCI HAR Dataset/features.txt")               #V2 contains feature labels
```
Read Test data
```
subject_test <- read.table("./UCI HAR Dataset/test/subject_test.txt")
X_test <- read.table("./UCI HAR Dataset/test/X_test.txt")
y_test <- read.table("./UCI HAR Dataset/test/y_test.txt")
```
Read train data
```
subject_train <- read.table("./UCI HAR Dataset/train/subject_train.txt")
X_train <- read.table("./UCI HAR Dataset/train/X_train.txt")
y_train <- read.table("./UCI HAR Dataset/train/y_train.txt")
```
Combine subjects, activity labels, and features into test and train sets
```
test  <- cbind(subject_test, y_test, X_test)
train <- cbind(subject_train, y_train, X_train)
```
Combine test and train sets to full dataset
```
fullSet <- rbind(test, train)
```
## Extract only measurements on mean and standard deviation
Subset, keeping mean, std columns; also keep subject, activity columns
```
allNames <- c("subject", "activity", as.character(features$V2))
meanStdColumns <- grep("subject|activity|[Mm]ean|std", allNames, value = FALSE)
reducedSet <- fullSet[ ,meanStdColumns]
```
## Use descriptive activities names for activity measurements
Use indexing to apply activity names to corresponding activity number
```
names(activity_labels) <- c("activityNumber", "activityName")
reducedSet$V1.1 <- activity_labels$activityName[reducedSet$V1.1]
```
## Appropriately Label the dataset with descriptive variable names
Use series of substitutions to rename variables
```
reducedNames <- allNames[meanStdColumns]    # Names after subsetting
reducedNames <- gsub("mean", "Mean", reducedNames)
reducedNames <- gsub("std", "Std", reducedNames)
reducedNames <- gsub("gravity", "Gravity", reducedNames)
reducedNames <- gsub("[[:punct:]]", "", reducedNames)
reducedNames <- gsub("^t", "time", reducedNames)
reducedNames <- gsub("^f", "frequency", reducedNames)
reducedNames <- gsub("^anglet", "angleTime", reducedNames)
names(reducedSet) <- reducedNames   # Apply new names to dataframe
```

