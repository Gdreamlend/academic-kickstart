---
title: "Stat Dirty Data"
date: 2019-09-10T11:00:46-04:00
draft: true
---

When we get a new data set, one of the first steps is to perform **descriptive statistics** on most of the variables. By doing that we can (1) check on the quality of the data, (2) start to get a basic understanding of the data set.

Error Detection (categorical variables): analyze -> distribution -> select [variables] -> OK (If there are some typographical in content may use Recode tool to change the errors)

Outlier Detection (continuous variables): analyze -> distribution -> select [variables] -> OK
Outliers:?  analyze -> screening -> explore outliers -> select [variables] -> Y -> OK -> Quantile Range Outliers -> click [variables] -> select rows

Missing values, four primary methods for dealing with this problem:
- Listwist deletion methon. Romove rows with missing values.
- Variable removal method. Eliminate any variable/column with missing values.
- Conventional estimate values methods. Replace missing values using typical statistical methods to estimated values.
- Model-based methods. Impute missing values by using medel-based correction methods.