run_analysis.R
Getting and Cleaning Data: Week 4 | Course Project
You should create one R script called run_analysis.R that does the following.
1. Merges the training and the test sets to create one data set.
2. Extracts only the measurements on the mean and standard deviation for each measurement.
3. Uses descriptive activity names to name the activities in the data set
4. Appropriately labels the data set with descriptive variable names.
5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
Load required libraries
library(data.table) library(reshape2)

Grab Data and Unzip to project directory
File URL to download
fileURL <- 'https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip'

Local Zipped data file
datasetZIP <- "./Dataset.zip"

Local Directory for Data
dirFile <- "./UCI HAR Dataset"

Download the dataset and unzip if necessary
if (file.exists(dataFileZIP) == FALSE) { download.file(fileURL, destfile = datasetZIP) } if (file.exists(dirFile) == FALSE) { unzip(datasetZIP) }

Directory and filename of final clean/tidy data:
tidyDatasetFile <- "./tidy-dataset.txt" tidyDatasetFileAVG <- "./tidy-datasetAVG.csv" tidyDatasetFileAVGtxt <- "./tidy-datasetAVG.txt"

1. Merges the training and the test sets to create one data set.
x_train <- read.table("./UCI HAR Dataset/train/X_train.txt", header = FALSE) X_test <- read.table("./UCI HAR Dataset/test/X_test.txt", header = FALSE)

y_train <- read.table("./UCI HAR Dataset/train/y_train.txt", header = FALSE) y_test <- read.table("./UCI HAR Dataset/test/y_test.txt", header = FALSE)

subject_train <- read.table("./UCI HAR Dataset/train/subject_train.txt", header = FALSE) subject_test <- read.table("./UCI HAR Dataset/test/subject_test.txt", header = FALSE)

Combines data table by (x, y, subject)_train vs (X,y, subject)_test by rows
x <- rbind(x_train, X_test) y <- rbind(y_train, y_test) s <- rbind(subject_train, subject_test)

2. Extracts only the measurements on the mean and standard deviation for each measurement.
Read features labels into R
features <- read.table("./UCI HAR Dataset/features.txt")

Features names to features column
names(features) <- c('feat_id', 'feat_name')

Searches each element of char vector for matches to the mean or std dev
index_features <- grep("-mean\(\)|-std\(\)", features$feat_name) x <- x[, index_features]

Replaces the matches from string
names(x) <- gsub("\(|\)", "", (features[index_features, 2]))

3. Uses descriptive activity names to name the activities in the data set
4. Appropriately labels the data set with descriptive variable names.
Read activity labels into R
activities <- read.table("./UCI HAR Dataset/activity_labels.txt")

Descriptive names to activities column
names(activities) <- c('act_id', 'act_name') y[, 1] = activities[y[, 1], 2]

names(y) <- "Activity" names(s) <- "Subject"

Combines data table by columns
tidyDataSet <- cbind(s, y, x)

5. From the data set in step 4, creates a second, independent tidy data set with
the average of each variable for each activity and each subject.
m <- tidyDataSet[, 3:dim(tidyDataSet)[2]] tidyDataAVGSet <- aggregate(m,list(tidyDataSet$Subject, tidyDataSet$Activity), mean)

Column Naming for Activity and Subject
names(tidyDataAVGSet)[1] <- "Subject" names(tidyDataAVGSet)[2] <- "Activity"

Created a tidy data set CSV in diretory | Tidy UCI-HAR Dataset that compares the Mean of each variable for each Activity with each Subject
write.table(tidyDataSet, tidyDatasetFile, sep="")

Created a tidy data set for Means CSV in diretory | Tidy UCI-HAR Dataset that compares the Mean of each variable for each Activity with each Subject
#write.csv(tidyDataAVGSet, tidyDatasetFileAVG, sep="")

Created a tidy data set for Means as a TXT in diretory | Tidy UCI-HAR Dataset that compares the Mean of each variable for each Activity with each Subject
write.table(tidyDataAVGSet, tidyDatasetFileAVGtxt, sep="", row.names=FALSE)
