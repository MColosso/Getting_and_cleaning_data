### **README**

Based on Human Activity Recognition Using Smartphones Dataset project (Smartlab - Non Linear Complex Systems Laboratory, DITEN - Università degli Studi di Genova, Italy), data collected by Anguita et al [1] where, with a group of 30 volunteers within an age bracket of 19-48 years, each one performing six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist, captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz using its embedded accelerometer and gyroscope. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. (Original data of the project can be found at https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip)

With this data we build a [tidy dataset](https://github.com/MColosso/Getting_and_cleaning_data/blob/master/tidy_dataset.txt) with an average of every mean and standard deviation of the given features, grouped by subject and activity.

[run_analysis.R](https://github.com/MColosso/Getting_and_cleaning_data/blob/master/run_analysis.R)
==============
The script to make this tidy dataset is packed in a function named run_analysis, and is located in the same directory (folder) as the **UCI HAR Dataset**.

It starts defining the paths to the UCI HAR Dataset folder and results folder, as to the "train" (training) and "test" folder where original data were splited.

In the first step, we merged the training and the test sets to create one data set of data, subjects and activites, via rbind function.

In the second step, we read the features names (which will be the columns names with appropiated transformations), selected only those which contains 'mean()' and 'std()' and selected only the data corresponding to these.

In the third step, transformed the activity code in the data into a descriptive name ('1' -> 'WALKING', '2' -> 'WALKING_UPSTAIRS', etc.)

In the fourth step, we convert selected features names into standard, discarding spaces, parenthesis, dots, commas, minus and underscore signs, concatenates subjects, activities and data read into a single data frame, and added column names.

In the fifth and last step, we created a second, independent tidy data set with the average of each variable for each activity and each subject. The strategy will be to use 'tapply' function to calculate the mean of each column of data of the previous dataset:

- First of all, we need to create a list of factors to be used in tapply function combining subject code (as 3 digits, zero padded) and activiy label: '025 WALKING_DOWNSTAIRS'
- Then, calculate the average for first data column (column 3 of previous dataset). It give us, not only the averages for each subject and activity, but the subjects and activities as row names.
- Create initial tidy dataset splitting subjects and activities from row names and binding with the average for first data column.
- Calculate average for following columns binding the result with the new dataset
- Change the names of the columns this dataset to those used in intermediate dataset (step 4) and write the resulting dataset.

Codebook
=========
The codebook of resulting dataset can be found at [CodeBook.md](https://github.com/MColosso/Getting_and_cleaning_data/blob/master/CodeBook.md)


Notes
=====
[1] Davide Anguita, Alessandro Ghio, Luca Oneto, Xavier Parra and Jorge L. Reyes-Ortiz. Human Activity Recognition on Smartphones using a Multiclass Hardware-Friendly Support Vector Machine. International Workshop of Ambient Assisted Living (IWAAL 2012). Vitoria-Gasteiz, Spain. Dec 2012
