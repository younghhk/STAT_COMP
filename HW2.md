### Homework 2
**Due: Monday, 10/8/2018, in class.**

**Note:** Students are required to submit their homework as both RMD and PDF file via D2L and bring the hardcopy by the due date of the assignment.
All electronic submissions should follow the following naming convention: last name, first name, assignment number, proper extension. So, for example, if John Smith is turning in Homework 1, he would name the fileSmith_John1.pdf. The associated code would be Smith_John1.Rmd. If you wish to break up your code into separate files, you may submit them as Smith_John1a.Rmd, Smith_John1b.Rmd, and so on. There will be a 20% penalty per day that your homework is late. Homework in the wrong format will not be given credit.



**Problem 1 (Linear regression models).** Write an R code to construct the 95% CI for beta manually. Using the dataset from Inlcass 2, give the CI for beta.



**Problem 2. (Quantile regression models)** Using 'bwt' dataset from Inclass 3, fit quantile regression model to explore the relationship between baby weight and covariates including     Black, Married, Boy, Visit, MomEdLevel, MomSmoke, CigsPerDay, MomAge, MomAge^2,  MomWtGain, MomWtGain^2 at quantile levels from 0.05 to 0.95 by 0.05. Provide the coefficient tables with confidence interval and interpret the results. 

**Problem 3. (Generalized linear models)**
Let  *yi* be a  random variable and **xi** a vector of covariates for the ith individual, then we model log mu=**xi'b**, where here **b** is a vector of regression coefficient.

1. Construct small data set (X,y): 

* n=1000
* **X**=(X1,X2), where X1 is  a vector, all filled with ones and X2~runif(n)
* **b**=(.2,.25)
* log(mu)=**Xb**
* y~poisson(mu)


2.  Estimate using `glm` function using the log link.


3. Obtain ML estimates of beta using your function via grid-search and using optimize.

* Develop an `R`-function to evaluate the log-likelihood of a poisson regression given X, y, and **b**.

* Estimation using `optim()`

**Problem 4. (Survival models) (TBA)
