---
title       : Lifetime Income Estimator
subtitle    : A Data Products Production
author      : Wayne Carriker
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## It's Not About the Money, Money, Money...*

### OK, so actually it is about the money.

### Do you wonder about how much you can make?

### Are you curious about the value of your education?

### Do you believe women only earn 77 cents for every dollar that men earn?

### What do you think Data Science can do for you?

### Fire up the Lifetime Income Estimator and find out!

* Apologies to Jessie J...

---

## So What Does It Do?

The Lifetime Income Estimator uses US Census data from 1991 to 2014 to track
income by gender, education level, and age group. Based on your inputs, it
creates an appropriate subset of the data and then fits a linear model through
the years of data in order to extrapolate potential earnings over your
lifetime.

This provides an extraordinarily accurate model of your precise earning
potential. That, of course, is a total fabrication. What it does create is an
estimate of the median income of someone in your situation in the United
States. So, while you should NOT assume that the estimator can actually predict
your precise earning potential, it can provide some insight into the factors
that can influence your earning potential.

---

## Let's Look at an Example

Let's see what a 35 year old (in 2015) female with a Master's degree is likely
to earn working from 2005 (when she was 25) to 2030 (when she retires early at
50.) There isn't enough room in these slides to show the entire algorithm, but
it goes something like:


```r
data <- read.csv("../census.csv")
rows <- (data$Gender == "Female") & (data$Education == "Master's")
years <- data$Year[rows]; ages <- data$Ages[rows]; incomes <- data$Income[rows]
mdata <- data.frame(years, ages, incomes); fit <- lm(incomes ~ ., data = mdata)

years <- seq(from = 2005, to = 2030)
ages_yr <- seq(from = 25, to = 50); ages <- sapply(ages_yr, age_groups)
test <- data.frame(years, ages); earnings <- predict(fit, newdata = test)
sum(earnings)
```

The actual algorithm (not echoed here) produces:

```
## [1] 2063017
```

---

## If Only She Had Completed Data Science...

According to the census data, the best thing she could have done was actually
complete a professional degree. Let's assume that took an extra 3 years,
reducing her years of employment to 2008 to 2030, but earning her an extra
$881,807...


```
## [1] 2944824
```

But, that would also mean 3 more years of school and a job that she doesn't
enjoy. Instead, she can complete the Data Science specialization this year and
earn an extra $225,000 doing what she loves!


```
## [1] 2288017
```

Check it out at https://carriker.shinyapps.io/DataProducts
