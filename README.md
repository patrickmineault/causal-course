# Notes on Causal Course

Notes from course on causal inference: https://www.bradyneal.com/causal-inference-course

# Chapter 1

* Fundamental problem of causal inference: you only measure factuals, not counterfactuals.
  * There's the treated and the untreated. To measure the effect of the treatment, you need to estimate $Y(1) - Y(0)$, the effect of the treatment on both the treated and untreated minus the effect of no treatment on both the treated and untreated. However, you can only measure the effect of treatment on the treated and no treatment on the untreated - you have empty entries in your matrix.

* The associational difference $E[Y|T=1] - E[Y|T=0]$ is not the causal effect of the treatment. However, it can be a stand-in for the causal effect if:
  * The treatment is ignoreable: If E[Y|T=1] = E[Y(1)], the treatment is said to be ignoreable. This condition is equivalent to exchangeability, which means that the population which received the treatment and the one which didn't can be swapped, and the expected associational difference in these two cases would be the same.
  * This is the case, by construction, if we have an RCT.

* We can define a notion of conditional exchangeability, $E[Y(1)|W] = E[Y|X, T=1]$, meaning that the causal quantity Y(1) becomes the same as the statistical quantity $E[Y|W, T=1]$, provided that we condition on W. 
  * We can use this to define the average conditional treatment effect, $E[Y|X, T=1] - E[Y|X, T=0]$. From this, we can estimate the average treatment effect by marginalizing out $X$: $ATE = E_X[E[Y|X, T=1] - E[Y|X, T=0]]$. 
  * This works if the effect is identifiable: when we can estimate a causal quantity by using purely statistical quantities.
  * Requires 
    1. positivity: that the probability of treatment is greater than 0 for every value of $W$.
    2. unconfoundedness: the variables X are exhaustive
    3. no interference: treatment on some units does not affect   other units
    4. consistency: no multiple versions of the treatment

* Example of estimation:
  * $E[Y|X, T=1]$, for X discrete can be estimated via binning.
  * %E[Y|X, T=1]$ for X continuous can be estimated via linear regression. In fact, we can tie confounder weights and bundle up into a single regression, such that $Y ~ \alpha T + \beta X$ and estimate via linear regression. This is a very common surgery (*controlling for*, *adjusting for* in epidemiology settings).


