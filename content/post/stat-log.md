---
title: "Prediction and Classification Modeling"
date: 2019-09-08T18:23:14-04:00
draft: false
markup: mmark
---
## Population parameters
- **population mean**  
μ = (Σ * X)/ N 平均值
- **population variance**  方差
$\sigma^{2}$ is population variance 
$$\sigma^{2}=\frac{\sum_{1}^{n}(x_{i}-\mu)^{2}}{N}$$
- **population standard deviation** 标准差
$$\sigma=\sqrt{\frac{\sum(x_{i}-\mu)^{2}}{N}}$$
Sample standard deviation:
$$s_x=\sqrt{\frac{\sum(x_{i}-\bar{x})^{2}}{n-1}}$$

**Z-score** represents a value's relationship to the mean (average) of a group of values,measured in terms of standard deviations away from the mean.[Reference](https://mathbitsnotebook.com/Algebra2/Statistics/STzScores.html)

$$z=(x-\mu)/\sigma$$

The range of Z is -3 to 3.

- if Z-score = 0: the data value should same with the population mean;
- if Z-score = 1: the value is one standard deviation away from the mean.

Z-scores may be positive or negative, with a positive value indicating the score is above the mean and a negative score indicating it is below the mean.
![Normal distribution and Z values](/img/normaldistribution.png)
Reject H<sub>0</sub> when you have a relatively large |Z<sub>calc</sub>|; that is |Z<sub>calc</sub>| > |Z<sub>critical</sub>|.
In this situation, you reject H<sub>0</sub> when the value is a relatively large number of standard deviations away from the hypothesized value.

**frenquency** of an event: how many times this even occured in an experiment or study.

**central limited theorem** states that as the sample size gets larger(>30), the sampling distribution of the sample means approaches a normal distribution. Application: the average of the sample means will be the population mean.[Reference](https://www.statisticshowto.datasciencecentral.com/probability-and-statistics/normal-distributions/central-limit-theorem-definition-examples/)

**P-Value** [Reference](https://www.statisticshowto.datasciencecentral.com/p-value/)

Z值越大，P值越小,越要拒绝H<sub>0</sub>。

|Z<sub>calc</sub>| > |Z<sub>critical</sub>| ⇒ p-value < α ⇒ reject H<sub>0</sub>  ⇒accept H<sub>a</sub>

|Z<sub>calc</sub>| <= |Z<sub>critical</sub>| ⇒ p-value ≥ α ⇒ fail to reject H<sub>0</sub> 
​	 
​**RSquare** (0~1)

**correlation**: square root of rsquare

**Chi-square** test independence

**Fundamental Concepts**
- Always take a **random** and **representative** sample
- Remember that statistics is not an exact science
- Understand a Z-Score
- Understand the central limit theorem?
- Understand one-sample hypothesis testing
- Understand that few approaches/techniques are

**Data Mining**
- Formulate the problem
- Accumulate data
- Transform and select data
- Train models
- Evaluate models
- Deploy models
- Monitor results

## Reference
[1] Klimberg and McCullough, 2013
R. Klimberg, B.D. McCullough
Fundamentals of predictive analytics with JMP®
SAS Institute, Inc., Cary, NC (2013)

[2] https://www.statisticshowto.datasciencecentral.com/probability-and-statistics/normal-distributions/central-limit-theorem-definition-examples/

[3] https://www.statisticshowto.datasciencecentral.com/p-value/

[4] https://mathbitsnotebook.com/Algebra2/Statistics/STzScores.html