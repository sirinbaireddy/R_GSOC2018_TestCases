
**Assignment Prompt:** The assigned task is to use glmnet to compute a L1-regularized linear model of the spam data in the  library "ElemStatLearn" and add what features are selected for the prediction function.

**My Answer:** 

**Importing the DataSet and glmnet:** The first step was importing the data from the internet to a dataset I can edit with R. 
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

**Data Explanation:** Before going into the commands of what I did, I will briefly explain the data. There are 58 distinct columns in the dataset, 57 of them measuring frequencies of various characters and words. 45 of those 57 columns measure the percentage of words in the email matching a specific word. Six of them measure the percentage of a certain character appearing. The remaining three of those 57 columns measure the average word length, longest word, and total number capital letters in each email. The 58th and last column of the dataset is a categorical variable having each email recorded as "Spam" or "Not Spam". If the email was spam, the email was recorded as a 1. If the email was not spam, it was recorded as a 0. There are 4601 distinct emails in this dataset, with approximately a third of the emails being spam.

**Features Selected for Prediction Function:** The next thing I needed to do was figure out my plan was to answer the question. The way I looked at it was I had a variety of factors including frequency counts of certain words and characters and a binary variable that stated whether the email was spam or not spam. I thought I could take several of the important factors listed and use them to predict if an email would be considered spam or not spam. To do this I had to figure out what the most important characteristics were in deciding whether or not an email would be spam. I had a lot of potential candidates but I decided to throw out a lot of extremely common words and symbols such as "all, or, you, :, #, your, ..." and many others. I spent a good amount of time narrowing it down to these final factors.
* frequency of word "order" 
* frequency of word "mail" 
* frequency of word "recieve" 
* frequency of word "free" 
* frequency of word "business" 
* frequency of word "credit" 
* frequency of word "money" 
* frequency of char "$" 

Unfortunately, when I imported the data set from the repository all of the column names were numeric and unordered so I converted the ones I wanted to easier variable names to work with.
```R
> order = as.matrix(dataSet$X0.5)
> mail = as.matrix(dataSet$X0.6)
> recieve = as.matrix(dataSet$X0.7)
> free = as.matrix(dataSet$X0.32.1)
> business = as.matrix(dataSet$X0.11)
> credit = as.matrix(dataSet$X0.12)
> money = as.matrix(dataSet$X0.15)
> dollarsign = as.matrix(dataSet$X0.44)
> xfactors = as.matrix(data.frame(order, mail, recieve, free, business, credit, money, dollarsign))
# the next variable isSpam is the response variable that has a 1 for spam and 0 for not spam
# it is not a predicting factor for the model
> isSpam = as.matrix(dataSet$X1) 
```

**Prediction Model:**
Now that we have all of our variables entered we can move on to the model. The prompt asked us to do a l1 regression model, so we choose a lasso regression with an alpha equal to 1. Since our response variable isSpam is a categorical variable with 0s and 1s, we use a binomial model.
```R
> glmod <- glmnet(xfactors,y= as.factor(isSpam),alpha = 1, family = "binomial")
> glmod
  Df      %Dev    Lambda
 [1,]  0 4.935e-14 0.1582000
 [2,]  1 1.309e-02 0.1441000
 [3,]  1 2.575e-02 0.1313000
 [4,]  3 4.682e-02 0.1197000
 [5,]  3 7.179e-02 0.1090000
 [6,]  4 9.602e-02 0.0993500
 [7,]  6 1.206e-01 0.0905300
 [8,]  6 1.446e-01 0.0824900
 [9,]  6 1.662e-01 0.0751600
[10,]  7 1.867e-01 0.0684800
[11,]  7 2.051e-01 0.0624000
[12,]  7 2.218e-01 0.0568500
[13,]  7 2.369e-01 0.0518000
[14,]  7 2.506e-01 0.0472000
[15,]  7 2.629e-01 0.0430100
[16,]  7 2.740e-01 0.0391900
[17,]  8 2.844e-01 0.0357100
[18,]  8 2.937e-01 0.0325300
[19,]  8 3.020e-01 0.0296400
....
[70,]  8 3.660e-01 0.0002578
[71,]  8 3.660e-01 0.0002349
[72,]  8 3.660e-01 0.0002141
[73,]  8 3.660e-01 0.0001950
```
I also plotted the variable coefficients versus the shrinking lambda.
```R
> plot(glmod, xvar="lambda")
```
I then displayed the coefficients and their intercepts
```R
> coef(glmod)[, 10]
(Intercept)       order        mail     recieve        free    business      credit       money 
 -0.8003488   0.2253186   0.0000000   0.4230139   0.3252347   0.3720801   0.0306762   0.1554286 
 dollarsign 
  2.4596797 
```




