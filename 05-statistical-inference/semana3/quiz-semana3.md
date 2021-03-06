# Quiz Semana 3: Intervals, Testing, & Pvalues

In a population of interest, a sample of 9 men yielded a sample average brain volume of 1,100cc and a standard deviation of 30cc. What is a 95% Student's T confidence interval for the mean brain volume in this new population?

```RScript
n <- 9
μ <- 1100
σ <- 30
quantile = 0.975 # is 95% with 2.5% on both sides of the range
μ + c(-1, 1) * qt(quantile, df=n-1) * σ / sqrt(n)

## [1] 1077 1123
```

1. [1031, 1169]
2. [1080, 1120]
3. ```[1077, 1123]```
4. [1092, 1108]

A diet pill is given to 9 subjects over six weeks. The average difference in weight (follow up - baseline) is -2 pounds. What would the standard deviation of the difference in weight have to be for the upper endpoint of the 95% T confidence interval to touch 0?

```RScript
n <- 9
averageDifference <- -2
quantile = 0.975 # is 95% with 2.5% on both sides of the range
ci_up = 0
σ = (ci_up - averageDifference * sqrt(n))/qt(quantile, df=n-1)
round(σ, 2)

## [1] 2.6
```

1. ```2.60```
2. 2.10
3. 0.30
4. 1.50

In an effort to improve running performance, 5 runners were either given a protein supplement or placebo. Then, after a suitable washout period, they were given the opposite treatment. Their mile times were recorded under both the treatment and placebo, yielding 10 measurements with 2 per subject. The researchers intend to use a T test and interval to investigate the treatment. Should they use a paired or independent group T test and interval?

1. You could use either
2. Independent groups, since all subjects were seen under both systems
3. ```A paired interval```
4. It's necessary to use both

In a study of emergency room waiting times, investigators consider a new and the standard triage systems. To test the systems, administrators selected 20 nights and randomly assigned the new triage system to be used on 10 nights and the standard system on the remaining 10 nights. They calculated the nightly median waiting time (MWT) to see a physician. The average MWT for the new system was 3 hours with a variance of 0.60 while the average MWT for the old system was 5 hours with a variance of 0.68. Consider the 95% confidence interval estimate for the differences of the mean MWT associated with the new system. Assume a constant variance. What is the interval? Subtract in this order (New System - Old System).

```RScript
quantile = 0.975 # is 95% with 2.5% on both sides of the range

n_y <- 10 # nights new system
n_x <- 10 # nights old system
var_y <- 0.60 # variance new (sqrt of σ)
var_x <- 0.68 # variance old (sqrt of σ)
μ_y <- 3# average hours new system
μ_x <- 5# average hours old system

# calculate pooled standard deviation
σ_p <- sqrt(((n_x - 1) * var_x + (n_y - 1) * var_y)/(n_x + n_y - 2))

confidenceInterval <- μ_y - μ_x + c(-1, 1) * qt(quantile, df=n_y+n_x-2) * σ_p * (1 / n_x + 1 / n_y)^.5
round(confidenceInterval,2)

## [1] -2.75 -1.25
```

1. [1.25, 2.75]
2. [1.29, 2.70]
3. [-2,70, -1.29]
4. ```[-2.75, -1.25]```

Suppose that you create a 95% T confidence interval. You then create a 90% interval using the same data. What can be said about the 90% interval with respect to the 95% interval?

1. ```The interval will be narrower.```
2. The interval will be wider
3. The interval will be the same width, but shifted.
4. It is impossible to tell.

To further test the hospital triage system, administrators selected 200 nights and randomly assigned a new triage system to be used on 100 nights and a standard system on the remaining 100 nights. They calculated the nightly median waiting time (MWT) to see a physician. The average MWT for the new system was 4 hours with a standard deviation of 0.5 hours while the average MWT for the old system was 6 hours with a standard deviation of 2 hours. Consider the hypothesis of a decrease in the mean MWT associated with the new treatment.

What does the 95% independent group confidence interval with unequal variances suggest vis a vis this hypothesis? (Because there's so many observations per group, just use the Z quantile instead of the T.)

```RScript
quantile = 0.975 # is 95% with 2.5% on both sides of the range

n_y <- 100 # nights new system
n_x <- 100 # nights old system
σ_y <- 0.50# σ new
σ_x <- 2# σ old
μ_y <- 4# average hours new system
μ_x <- 6# average hours old system

# calculate pooled standard deviation
σ_p <- sqrt(((n_x - 1) * σ_x^2 + (n_y - 1) * σ_y^2)/(n_x + n_y - 2))

confidenceInterval <-  μ_x - μ_y + c(-1, 1) * qnorm(quantile) * σ_p * (1 / n_x + 1 / n_y)^.5
round(confidenceInterval,2)

## [1] 1.6 2.4
```

1. ```When subtracting (old - new) the interval is entirely above zero. The new system appears to be effective.```
2. When subtracting (old - new) the interval contains 0. There is not evidence suggesting that the new system is effective.
3. When subtracting (old - new) the interval contains 0. The new system appears to be effective.
4. When subtracting (old - new) the interval is entirely above zero. The new system does not appear to be effective.

Suppose that 18 obese subjects were randomized, 9 each, to a new diet pill and a placebo. Subjects’ body mass indices (BMIs) were measured at a baseline and again after having received the treatment or placebo for four weeks. The average difference from follow-up to the baseline (followup - baseline) was −3 kg/m2 for the treated group and 1 kg/m2 for the placebo group. The corresponding standard deviations of the differences was 1.5 kg/m2 for the treatment group and 1.8 kg/m2 for the placebo group. Does the change in BMI over the four week period appear to differ between the treated and placebo groups? Assuming normality of the underlying data and a common population variance, calculate the relevant *90%* t confidence interval. Subtract in the order of (Treated - Placebo) with the smaller (more negative) number first.

```RScript
quantile = 0.95 # is 90% with 5% on both sides of the range

n_y <- 9 # subjects treated
n_x <- 9 # subjects placebo
σ_y <- 1.5# kg/m2 std.dev. treated
σ_x <- 1.8# kg/m2 std.dev. placebo
μ_y <- -3#  kg/m2 average difference treated
μ_x <- 1#  kg/m2 average difference placebo

# calculate pooled standard deviation
σ_p <- sqrt(((n_x - 1) * σ_x^2 + (n_y - 1) * σ_y^2)/(n_x + n_y - 2))

confidenceInterval <-  μ_y - μ_x + c(-1, 1) * qt(quantile, df=n_y+n_x-2) * σ_p * (1 / n_x + 1 / n_y)^.5
round(confidenceInterval,3)

## [1] -5.364 -2.636
```

1. [-5.531, -2.469]
2. ```[-5.364, -2.636]```
3. [2.636, 5.364]
4. [2.469, 5.531]
