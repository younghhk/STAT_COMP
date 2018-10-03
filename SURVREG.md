# Survival models
[Note](https://app.box.com/s/kykg6pmjb757lhiuq3knawcakmsz4umc)

[Inverse sampling](https://app.box.com/s/rv8u5fa7btrluqzfo3k10wn10lk2kc45)

## Inclass Assignment #5

1. Write an `R` function that generates a data set (X,Z) with the size of `N`.

Covariates are Z=(1,z) where `z` is from uniform (0,1).
The latent time `X` follows a Cox model with the the baseline hazard that has a Weibull form with `lambda` (scale prameter) and `alpha` (shape parameter).
Censoring times are randomly drawn form an exponential distribution with the rate parameter `rateC`.

2. Test

Perform a simulation with `N=100`, `lambda=0.01`, `alpha=1`, `beta=-0.6`, `rateC=0.001`.
Then obtain the mean of betahat over 100 repetitions.


[Back](https://github.com/younghhk/STAT_COMP/)
