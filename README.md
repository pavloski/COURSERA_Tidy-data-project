# CourseProject_Get_Data
## Data for the course project downloaded from https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

## task 1: Merge the training and the test sets to create one data set
## read test set
X_test<- read.table("./UCI HAR Dataset/test/X_test.txt", quote="\"", comment.char="")
X_train<-read.table("./UCI HAR Dataset/train/X_train.txt", quote="\"", comment.char="")

## read activity labels
y_test<-read.table("./UCI HAR Dataset/test/y_test.txt", quote="\"", comment.char="")
y_train<-read.table("./UCI HAR Dataset/train/y_train.txt", quote="\"", comment.char="")

## read subjects
subject_test <- read.table("./UCI HAR Dataset/test/subject_test.txt", quote="\"", comment.char="")
subject_train <- read.table("./UCI HAR Dataset/train/subject_train.txt", quote="\"", comment.char="")

## join data frames
my.merged.data<-rbind(X_test, X_train)
my.merged.lables <-rbind(y_test, y_train)
my.merged.subjects <- rbind(subject_test, subject_train)
my.data <- cbind(my.merged.data, my.merged.lables, my.merged.subjects)

## add labels to dataset
##import features for column names
features <- read.table("./UCI HAR Dataset/features.txt", quote="\"", comment.char="")
colnames(my.data) <- features[,2]

## we also name the last columns with the activity labels and subjects
names(my.data)[562] <- "activity"
names(my.data)[563] <- "subject"

## task 2: Extract only the measurements on the mean and standard deviation for each measurement.
## select columns according to the data code book
colsToExtract <- c(1:6,41:46,81:86, 121:126,161:166, 201:202, 214:215, 227:228, 240:241, 253:254, 266:271, 345:350, 424:429, 503:504, 516:517, 529:530, 542:543, 562:563)

## extract the data
my.extract <- my.data[,colsToExtract]

## Task 3: Use descriptive activity names to name the activities in the data set
## get activity descriptions
activity_labels <- read.table("./UCI HAR Dataset/activity_labels.txt", quote="\"", comment.char="")

## create a new column "activity_description with values from activity_lables
my.extract$activity_description<- activity_labels[my.extract$activity,2]

## task 4: Appropriately labels the data set with descriptive variable names. 
## already accomplish on task 1

## task 5: From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

## create factors
my.extract$activity <- as.factor(my.extract$activity)
my.extract$subject <- as.factor(my.extract$subject)

## load dplr library
library(dplyr)
my.extract.grouped <- group_by(my.extract, activity, subject)
my.final <- summarise(my.extract.grouped, mean(`tBodyAcc-mean()-X`),
                    mean(`tBodyAcc-mean()-Y`),
                    mean(`tBodyAcc-mean()-Z`),
                    mean(`tBodyAcc-std()-X`),
                    mean(`tBodyAcc-std()-Y`),
                    mean(`tBodyAcc-std()-Z`),
                    mean(`tGravityAcc-mean()-X`),
                    mean(`tGravityAcc-mean()-Y`),
                    mean(`tGravityAcc-mean()-Z`),
                    mean(`tGravityAcc-std()-X`),
                    mean(`tGravityAcc-std()-Y`),
                    mean(`tGravityAcc-std()-Z`),
                    mean(`tBodyAccJerk-mean()-X`),
                    mean(`tBodyAccJerk-mean()-Y`),
                    mean(`tBodyAccJerk-mean()-Z`),
                    mean(`tBodyAccJerk-std()-X`),
                    mean(`tBodyAccJerk-std()-Y`),
                    mean(`tBodyAccJerk-std()-Z`),
                    mean(`tBodyGyro-mean()-X`),
                    mean(`tBodyGyro-mean()-Y`),
                    mean(`tBodyGyro-mean()-Z`),
                    mean(`tBodyGyro-std()-X`),
                    mean(`tBodyGyro-std()-Y`),
                    mean(`tBodyGyro-std()-Z`),
                    mean(`tBodyGyroJerk-mean()-X`),
                    mean(`tBodyGyroJerk-mean()-Y`),
                    mean(`tBodyGyroJerk-mean()-Z`),
                    mean(`tBodyGyroJerk-std()-X`),
                    mean(`tBodyGyroJerk-std()-Y`),
                    mean(`tBodyGyroJerk-std()-Y`),
                    mean(`tBodyGyroJerk-std()-Z`),
                    mean(`tBodyAccMag-mean()`),
                    mean(`tBodyAccMag-std()`),
                    mean(`tGravityAccMag-mean()`),
                    mean(`tGravityAccMag-std()`),
                    mean(`tBodyAccJerkMag-mean()`),
                    mean(`tBodyAccJerkMag-std()`),
                    mean(`tBodyGyroMag-mean()`),
                    mean(`tBodyGyroMag-std()`),
                    mean(`tBodyGyroJerkMag-mean()`),
                    mean(`tBodyGyroJerkMag-std()`),
                    mean(`fBodyAcc-mean()-X`),
                    mean(`fBodyAcc-mean()-Y`),
                    mean(`fBodyAcc-mean()-Z`),
                    mean(`fBodyAcc-std()-X`),
                    mean(`fBodyAcc-std()-Y`),
                    mean(`fBodyAcc-std()-Z`),
                    mean(`fBodyAccJerk-mean()-X`),
                    mean(`fBodyAccJerk-mean()-Y`),
                    mean(`fBodyAccJerk-mean()-Z`),
                    mean(`fBodyAccJerk-std()-X`),
                    mean(`fBodyAccJerk-std()-Y`),
                    mean(`fBodyAccJerk-std()-Z`),
                    mean(`fBodyGyro-mean()-X`),
                    mean(`fBodyGyro-mean()-Y`),
                    mean(`fBodyGyro-mean()-Z`),
                    mean(`fBodyGyro-std()-X`),
                    mean(`fBodyGyro-std()-Y`),
                    mean(`fBodyGyro-std()-Z`),
                    mean(`fBodyAccMag-mean()`),
                    mean(`fBodyAccMag-std()`),
                    mean(`fBodyBodyAccJerkMag-mean()`),
                    mean(`fBodyBodyAccJerkMag-std()`),
                    mean(`fBodyBodyGyroMag-mean()`),
                    mean(`fBodyBodyGyroMag-std()`),
                    mean(`fBodyBodyGyroJerkMag-mean()`),
                    mean(`fBodyBodyGyroJerkMag-std()`))
                    
