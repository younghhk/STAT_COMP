### Homework 1
**Due: Wednesday, 9/12/2018, in class.**

**Note:** Students are required to submit their homework as both PDF file and hardcopy by the due date of the assignment.
Please turn in code separately and electronically. All electronic submissions should be madevia D2L Dropbox and should follow the following naming convention: last name, first name, assignment number, proper extension. So, for example, if John Smith is turning in Homework 1, he would name the fileSmith_John1.pdf. The associated code would be Smith_John1.Rmd. If you wish to break up your code into separate files, you may submit them as Smith_John1a.Rmd, Smith_John1b.Rmd, and so on. There will be a 20% penalty per day that your homework is late. Homework in the wrong format will not be given credit.

**Problem 1.** Write a function which returns the  odds ratio, CI, and P value of the univariate logistic regression model.

**Problem 2.** Using the `recid.csv' dataset, fit the univariate logistic regression model with the response variable being "arrest".  Calculate the odds ratio, CI, and P value for financial, age, married, paroled, educ, and week variable.

The `recid.csv` data set contains information about 432 inmates who were released from Maryland state prisons in the early 1970s. The aim of this research was to determine the efficacy of financial aid to released inmates as a means of reducing recidivism. The data set used here contains the following variables. 

* arrest: has a value of 1 if arrested; otherwise, ARREST has a value of 0.
* week: is the week of first arrest; WEEK has a value of 52 if not arrested.
* financial: has a value of 1 if the inmate received financial aid after release; otherwise, FIN has a value of 0. 
* age: is the age in years at the time of release.
* race: has a value of 1 if the inmate is black: otherwise, RACE has a value of 0.
* paroled: has a value of 1 if released on parole: otherwise, PARO has a value of 0.
* married: has a value of 1 if the inmate was married at the time of release; otherwise, MAR has a value of 0.
* educ: is the highest level of completed schooling, coded as
          2=6th grade or less;
        3=7th 9th grade;
        4=10th to 11th grade;
        5=12th grade;
         6=some college;
