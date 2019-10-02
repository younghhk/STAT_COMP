# Survival models
[Note](https://younghhk.github.io/STAT_COMP/M2_Surv.html#1)

[Inverse sampling](https://app.box.com/s/rv8u5fa7btrluqzfo3k10wn10lk2kc45)
## Inclass Assignment #4 

```{r}
1. Write an `R` function that generates the time to event outcome from Cox model.
To generate X from the Cox model, we can use the inverse sampling method.
If U is uniform on (0,1) and S(x|z) is the conditional survival function derived from the Cox model.

Assume that the baseline hazard has the exponential form,
h0(x)=lambda and z has the Bernoulli distribution with parameter p=0.5 and beta=1.

Obtain the summary statistics and draw the distribution of 100 randomly generated X.
```

[Back](https://github.com/younghhk/STAT_COMP/)
