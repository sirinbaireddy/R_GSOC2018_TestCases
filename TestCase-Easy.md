
**Assignment:** The assigned task is to use glmnet to compute a L1-regularized linear model of the spam data in the  library "ElemStatLearn" and add what features are selected for the prediction function.

The first step was importing the data from the internet to a dataset I can edit with R. 
I did this by accessing the UCI Machine Learning Repository (https://archive.ics.uci.edu/ml/machine-learning-databases/spambase/). I downloaded the data set with the command
```R
> dataSet <- read.table(file.choose(), header = T, sep = ",")
> View(dataSet)
```
Then I installed glmnet package which is needed in order to perform L1 regression models.
```R
> install.packages("glmnet", repos = "http://cran.us.r-project.org")
also installing the dependencies ‘iterators’, ‘foreach’
> 
> library(glmnet)
Loading required package: Matrix
Loading required package: foreach
Loaded glmnet 2.0-13
```

