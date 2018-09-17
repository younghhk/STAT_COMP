# Quantile regression models

[Note]


## Data Preparation and Implementation

* Quantile regression can be implemented in various statistical software packages including R, using quantreg, 
SAS, using Proc Quantreg, and STATA, using Qreg.


* Standard errors and confidence limits for the quantile regression coefficient estimates can be obtained with
asymptotic and bootstrapping methods.

* Both methods provide robust results (Koenecker and Hallock 2001),
with the bootstrap method preferred as more practical (Hao and Naiman, 2007). 


## Application: Multiple Myeloma (MM) dataset

* Elevated beta-2 microglobulin (B2M, mg/L) in the blood is correlated with a larger amount of tumor (tumor mass) and reduced kidney function in multiple myeloma.

* We model B2M as a function of age, gender, race, hemoglobin (HGB, g/dL),  and albumin (ALB, g/L).
The summary statistics of MM is shown below.

 Variable      mean or %
 ---------     -------------
B2M       
Age     
Male          
Female    
White    
Others      
ALB
HGB        
---------     ------------- 



[Back](https://github.com/gdlc/STAT_COMP/)

