
**Assignment Prompt:** The assigned task is to use glmnet to compute a L1-regularized linear model of the spam data in the  library "ElemStatLearn" and add what features are selected for the prediction function.

**My Answer:** The first step was importing the data from the internet to a dataset I can edit with R. 
I did this by accessing the UCI Machine Learning Repository (https://archive.ics.uci.edu/ml/machine-learning-databases/spambase/). I first downloaded the required files, then I imported the data set with the command
```R
> dataSet <- read.table(file.choose(), header = T, sep = ",")
> View(dataSet)
```
Then I installed glmnet package which is needed in order to perform this following type of regression model.
```R
> install.packages("glmnet", repos = "http://cran.us.r-project.org")
also installing the dependencies ‘iterators’, ‘foreach’
> 
> library(glmnet)
Loading required package: Matrix
Loading required package: foreach
Loaded glmnet 2.0-13
```
Before going into the commands of what I did, I will briefly explain the data. There are 58 distinct columns in the dataset, 57 of them measuring frequencies of various characters and words. 45 of those 57 columns measure the percentage of words in the email matching a specific word. Six of them measure the percentage of a certain character appearing. The remaining three of those 57 columns measure the average word length, longest word, and total number capital letters in each email. The 58th and last column of the dataset is a categorical variable having each email recorded as "Spam" or "Not Spam". If the email was spam, the email was recorded as a 1. If the email was not spam, it was recorded as a 0. There are 4601 distinct emails in this dataset, with approximately a third of the emails being spam.


