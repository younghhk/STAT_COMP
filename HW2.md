### Homework 2
**Due: Monday, 10/8/2018, in class.**

**Note:** Students are required to submit their homework as both RMD and PDF file via D2L and bring the hardcopy by the due date of the assignment.
All electronic submissions should follow the following naming convention: last name, first name, assignment number, proper extension. So, for example, if John Smith is turning in Homework 1, he would name the fileSmith_John1.pdf. The associated code would be Smith_John1.Rmd. If you wish to break up your code into separate files, you may submit them as Smith_John1a.Rmd, Smith_John1b.Rmd, and so on. There will be a 20% penalty per day that your homework is late. Homework in the wrong format will not be given credit.



**Problem 1 (Linear regression models).** Write an R code to construct the 95% CI for beta manually. Using the dataset from Inlcass 2, give the CI for beta.



**Problem 2. (Quantile regression models)** Using 'bwt' dataset from Inclass 3, fit quantile regression model to explore the relationship between baby weight and covariates including     Black, Married, Boy, Visit, MomEdLevel, MomSmoke, CigsPerDay, MomAge, MomAge^2,  MomWtGain, MomWtGain^2 at quantile levels **(0.1,0.5,0.9)**. Provide the coefficient tables with confidence interval (**or p-value**) and interpret the results. 

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

**Problem 4. (Survival models)**
Write an R function that generates a (latent) survival time X.
To generate X from the Cox model, we can use the inverse sampling method.
If U is uniform on (0,1) and S(x|z) is the conditional survival function derived from the Cox model.

I.e.,
S(x|z)=exp(-H_0(x)exp(z'beta))

Then, X=S^{-1}(U|z)=H_0^{-1}(-log U/exp(z'beta)) has survival function S(x|z). 


The Gompertz distribution represents another extension of the exponential distribution.
Like the Weibull, the Gompertz distribution is characterized by two parameters. 
Assume that the baseline hazard function h_0(x) follows the Gompertz distribution,
I.e., h_0(x)=lambda \times exp(alpha \times x)

(1) Derive the baseline cumulative hazard function, H_0(x).

(2) Derive the inverse of the baseline cumulative hazard function, H_0^{-1}(x).

  
(3) Using the inverse sampling method and (2), express X w.r.t. U, where U~Unif(0,1).


(4) Write an `R` code to generate 100 X's assuming z is a single bivaraite covariate (ex. treatments), beta=0.6 and lambda=1 and alpha=1.

[HW2 solution](https://app.box.com/s/7tx0r16ej5py6jvanheshgrzue28jmb8)
