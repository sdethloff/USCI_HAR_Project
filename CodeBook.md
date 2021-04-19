# Introduction

This codebook describes the original datasets as well as the har_means.txt tidy dataset, which can be reproduced using the run_analysis.R script found in this repository.

# Original Datasets

Original datasets are found in the following files, once extracted from the zip file:

activity_labels.txt
features.txt
features_info.txt
train (folder): X_train.txt, Y_train.txt, and subject_train.txt
test (folder): X_test.txt, Y_test.txt, subject_test.txt 

Desctiptions of each original dataset can be found here:

activity_labels data includes two columns which denote specific activiteies (e.g. - Walking, Sitting, etc.) for each activity_number
features data represent variable names that can be used to name the columns from the x_ datasets
x_ files contain 561 columns containing measurements, including raw and statistical values (mean, st. dev., mean frequency, etc.) 
y_files data is composed of only one column, an activity_number, which a code representing the type of activity performed
subject_ files data is also composed of only one column, subject, which is a code of the specific user being observed
train data was recorded from 70% of participants from the study
test data was recorded from 70% of participants from the study

Further detail on each of these different measurements can be found here: [http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones].

# Transformations

1. Use the read.table function to read the activity_labels.txt and features.txt into RStudio
2. With the exceptiopn of features_info.txt, the remaining files noted above are read into in R with newly created column names. The x_ files were given the same column name was previously imported features.txt (using $). Otherwise, column names were simply assigned manually.
3. Use rbind() to merge the the test and train datasets for x_ files. Do the same for y_ files and subject_ files.
4. Then use cbind() to collate the three newly merged files into one dataset.
5. Next, create a subset from this one dataset using the select function, such that only columns that contain the word "mean" or "std". This subset should not contain "meanFreq".
6. Use the merge() function to combine this subset with activity_labels. This ensures that a desciption of the activity is included, not just an activity number.
7. Use the select() and arrange() functions. This step makes the dataset easier to read.
8. The first tidy data set is finally created by using the gather() function (pivot_longer function can also be used) is used to pivot the data from a wide to long format. New columns 'features' and 'measurement' are then piped in to finalize creation of the dataframe.
9. The next step is to create a summary, wherein the means of the measured data, grouped by activity and subject, are listed.
10. Lastly, each dataset is than written to a text file using the write.tabl function. Note: due to file size, only the har_means (summary) file is included in the repo.

# Solution Tidy Dataset

The solution tidy data set is called har_means.txt and contains the following columns:

subject - same desciption as with original dataset
activity_description - same desciption as with original dataset
features - represents the mean or std. deviation of the specific activity
mean_measurement - mean of datapoints (means and std. deviations) for each combination of user and observed activity
