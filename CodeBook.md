Data Introduction
This project will use six data, which are x_train.txt, x_test.txt, y_train.txt, y_test.txt, subject_train.txt and subject_test.txt, they can all be found inside the downloaded dataset, namely URI HAR Dataset.
The features.txt contains the correct variable name, which corresponds to each column of x_train.txt and x_test.txt. Further explanation of each feature is in the features_info.txt.
The activity_labels.txt contains the desciptive names for each activity label, which corresponds to each number in the y_train.txt and y_test.txt.
The README.txt is the overall desciption about the overall process of how publishers of this dataset did the experiment and got the data result.
Course Project Introduction
The script run_analysis.R uses the data.table package for renaming column and reading in files. It performs 5 major steps including:

Merges the training and the test sets to create one data set. (In the following the word data means both train and test). The x_data.txt, y_data.txt, subject_data.txt should be binded by row, and after that all three of them should binded by column.

Extracts only the measurements on the mean and standard deviation for each measurement. For the column of x_data.txt, extract only the ones that have mean() or std() in their names, compare it with feature.txt.

Uses descriptive activity names to name the activities in the data set. Match each number in the y_data column with activity_labels.txt.

Appropriately labels the data set with descriptive variable names. Rename the column of y_data and subject_data, instead of using the default name given by R.

From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
Write out the tidy dataset to averagedata.txt.

Final Tidy Data Description
The final tidy data is produced inside the run_analysis.R, which I simply named it data3 and data4.

data3 is the tidy data produced after going through the first 4 steps of the course project. It contains 10299 observations and 68 variables.
The first column refers to each subject that did the experiment.
Column 2~67 are the feature variables(mean and std of the whole feature variables).
The last column is refers to the activity that the subjects were doing, including WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING.
data4 is the tidy data produced after going through all 5 steps of the course project. It contains 180 observations and 68 variables. Where the first column is the subject id, second column is the activity and the rest are the average of each feature variables.
