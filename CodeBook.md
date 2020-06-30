# Code Book
Coursera Data Science Specialization Course 
Getting and cleaning Data
Course project

### Data
This project is an exercise in acquiring and cleaning data. The project uses data from the UCI Machine Learning Repository: Human Activity Recognition and Smart Phone Data site.
This code book relies on the source code book listed in the README.txt of the zip archive and available at the UCI link for definitions and descriptions.

#### Processing

##### Step 1: Merge training and test sets to create one data set
Data was downloaded from the source files and read in with names corresponding to the source files. Test set data were combined together by columns. Train set data were combined in the same manner. Test and train set data were combined to created the full data set (fullSet).

##### Step 2: Extract only measurements on mean and standard deviation
A names variable (*allNames*) that included the subject, activity and all the feature names was created. This variable was subsetted to include only the subject, activity, and variables that included mean and standard deviation(std). This subsetted names variable was then used to extract the corresponding columns in the full data set. The result was saved as the *reducedSet*
