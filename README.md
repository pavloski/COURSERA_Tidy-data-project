# CourseProject_Get_Data
One of the most exciting areas in all of data science right now is wearable computing - see for example this article . Companies like Fitbit, Nike, and Jawbone Up are racing to develop the most advanced algorithms to attract new users. The data linked to from the course website represent data collected from the accelerometers from the Samsung Galaxy S smartphone. A full description is available at the site where the data was obtained:
http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones 

### Data for the course project downloaded from
https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

## TASK 1: Merge the training and the test sets to create one data set
After downloading the data into the local drive, the first step is to read the files into data frames. 
Test and train,  are read separately and then combined using rbind funtcion
The same goes for subject and activities. these two are joined to the data frame as new columns using cbind function
Finaly, columns are named according to the features file

## TASK 2: Extract only the measurements on the mean and standard deviation for each measurement.
We select required columns according to the data code book

## TASK 3: Use descriptive activity names to name the activities in the data set
We create a new column maping numbers 1 through 6 to activities according to the activity_labels description file

## task 4: Appropriately labels the data set with descriptive variable names. 
This task, for convenience was already accomplished during task 1

## task 5: From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
We first convert subjects and activities into factors
