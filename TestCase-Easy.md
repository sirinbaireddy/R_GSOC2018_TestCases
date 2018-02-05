
**Assignment:** The assigned task is to use glmnet to compute a L1-regularized linear model of the spam data in the  library "ElemStatLearn" and add what features are selected for the prediction function.


The first step was importing the data from the internet to a dataset I can edit with R. 
I did this by accessing the UCI Machine Learning Repository (https://archive.ics.uci.edu/ml/machine-learning-databases/spambase/). I downloaded the data set with the command

'''R
> dataSet <- read.table(file.choose(), header = T, sep = ",")
> View(dataSet)
'''

Then installed glmnet
'''
> install.packages("glmnet", repos = "http://cran.us.r-project.org")
also installing the dependencies ‘iterators’, ‘foreach’
'''
trying URL 'http://cran.us.r-project.org/bin/macosx/mavericks/contrib/3.3/iterators_1.0.9.tgz'
Content type 'application/x-gzip' length 309783 bytes (302 KB)
==================================================
downloaded 302 KB

trying URL 'http://cran.us.r-project.org/bin/macosx/mavericks/contrib/3.3/foreach_1.4.4.tgz'
Content type 'application/x-gzip' length 381405 bytes (372 KB)
==================================================
downloaded 372 KB

trying URL 'http://cran.us.r-project.org/bin/macosx/mavericks/contrib/3.3/glmnet_2.0-13.tgz'
Content type 'application/x-gzip' length 1508797 bytes (1.4 MB)
==================================================
downloaded 1.4 MB


The downloaded binary packages are in
	/var/folders/90/0351r_zs5w5dyp9pmgj4fmv80000gn/T//RtmpSAT6MN/downloaded_packages
> 
> library(glmnet)
Loading required package: Matrix
Loading required package: foreach
Loaded glmnet 2.0-13

glmnet is good because it can take advantage of sparsity
we want l1 linear regression which is "lasso regression"
