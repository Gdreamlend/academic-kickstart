---
title: "Linear Regression"
date: 2019-09-16T15:47:55-04:00
draft: false
---

The level of measurement of a variable can be either nominal, ordinal,
interval or ratio.

Nominal:
Unordered categorical variables. These can be either binary (only two categories, like gender: male or female) or multinomial (more than two categories, like marital status: married, divorced, never married, widowed, separated). The key thing here is that there is no logical order to the categories.

Ordinal:
Ordered categories. Still categorical, but in an order. Likert items with responses like: “Never, Sometimes, Often, Always” are ordinal.

Interval:
Numerical values without a true zero point. The idea here is the intervals between the values are equal and meaningful, but the numbers themselves are arbitrary. 0 does not indicate a complete lack of the quantity being measured. IQ and degrees Celsius or Fahrenheit are both interval.

Ratio:
Numerical values with a true zero point.

## Conditions for a simple linear model
- **Linearity** The average values of the response Y for each value of X fall on a common straight line.
- **Zero Mean** The error distribution is centered at zero.(Note: By using least squares regression, we force the residual mean to be zero. Other techniques would not necessarily satisfy this condition.)
- **Constant Variance** The variability in the errors is the same for all values of the predictor variable. This means that the spread of points around the line remains fairly constant.
- **Independence** The errors are assumed to be independent from one another.
- **Random** The data are obtained using a random process. 
- **Normality** In order to use standard distributions for confidence intervals and hypothesis tests, we often need to assume that the random errors follow a normal distribution.

![regression standard error](/img/regression_standard_error.png)

**outliers** and **Influential Points**:An outlier is a data point that diverges from an overall pattern in a sample. An outlier has a large residual (the distance between the predicted value and the observed value). Outliers lower the significance of the fit of a statistical model because they do not coincide with the model's prediction. An influential point is any point that has a large effect on the slope of a regression line fitting the data. They are generally extreme values. The process to identify an influential point begins by removing the suspected influential point from the data set. If this removal significantly changes the slope of the regression line, then the point is considered an influential point.[reference](https://www.chegg.com/homework-help/definitions/outliers-and-influential-points-31)

## Inference for Regression Slope
**sum of squares**

$$SSQ(x)=\sum(x-\bar{x})^{2}=\sum(x)^{2}-\frac{(\sum{x})^{2}}{n}$$

$$SSQ(y)=\sum(y-\bar{y})^{2}=\sum(y)^{2}-\frac{(\sum{y})^{2}}{n}$$

Total SSQ = SSQ(y)
$$SSQ(reg)={\hat{\beta_1}}^{2}\cdot{SSQ(x)}$$

$$SSQ(xy)=\sum(x-\bar{x})(y-\bar{y})=\sum{xy}-\frac{\sum{x}\sum{y}}{n}$$

$$\hat{\beta_1}=\frac{SSQ(xy)}{SSQ(x)}$$

$$\hat{\beta_0}=\bar{y}-\hat{\beta_1}\bar{x}$$

estimate of $$\sigma^{2}=S_{y|x}^{2}$$

$$\sigma^{2}=S_{y|x}^{2}=\frac{\sum(y_i-\hat{y_i})^{2}}{n-2}=\frac{SSE}{n-2}$$ 

The standard error of the slope or standard error of estimate $$SE_{\hat{\beta_1}}$$ represents the average distance that your observed values deviate from the regression line.

$$S_{\hat{\beta_1}}=SE_{\hat{\beta_1}}$$

$$SE_{\hat{\beta_1}}=\sqrt{\frac{1}{n-2}\frac{{\sum(y_i-\hat{y_i})}^2}{\sum(x_i-\bar{x})^2}}=\sqrt{\frac{SSE}{(n-2)SSQ(x)}}$$ 

定义存疑？？？

Total SSQ = SSQ(y)

SSQ(Reg) = $${\hat{\beta_1}}^{2}(SSQ(x))$$

SSQ(error) = SSE = SSQ(y) - SSQ(Reg)

T-test

**Find α/2**

Level of Confidence = 95%

α = 100% - (Level of Confidence) = 5%

α/2 = 2.5% = 0.025

**Find t_{α/2}**

Calculate tα/2 by using t-distribution with degrees of freedom (df) as n - 2 and α/2 as right-tailed area.

Confidence Interval(CI):

CI for the mean value of Y ($\mu_{Y|X}$):

$$\hat{Y}_{X_0}\pm{t_{n-2,1-{\alpha}/2}}S_{\hat{Y}_{X_0}}$$

$$S_{\hat{Y}_{X_0}}=S_{Y|X}\sqrt{\frac{1}{n}+{\frac{(X_0-\bar{X})^2}{(n-1)SSQ(x)}}}$$
