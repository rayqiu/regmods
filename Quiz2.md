# Regression Models (Quiz 2)
Ray Qiu  
October 14, 2015  

1. Consider the following data with x as the predictor and y as as the outcome.

    x <- c(0.61, 0.93, 0.83, 0.35, 0.54, 0.16, 0.91, 0.62, 0.62)  
    y <- c(0.67, 0.84, 0.6, 0.18, 0.85, 0.47, 1.1, 0.65, 0.36)  
    Give a P-value for the two sided hypothesis test of whether β1 from a linear regression model is 0 or not.


```r
x <- c(0.61, 0.93, 0.83, 0.35, 0.54, 0.16, 0.91, 0.62, 0.62)
y <- c(0.67, 0.84, 0.6, 0.18, 0.85, 0.47, 1.1, 0.65, 0.36)
fit <- lm(y~x)
summary(fit)
```

```
## 
## Call:
## lm(formula = y ~ x)
## 
## Residuals:
##      Min       1Q   Median       3Q      Max 
## -0.27636 -0.18807  0.01364  0.16595  0.27143 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)  
## (Intercept)   0.1885     0.2061   0.914    0.391  
## x             0.7224     0.3107   2.325    0.053 .
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 0.223 on 7 degrees of freedom
## Multiple R-squared:  0.4358,	Adjusted R-squared:  0.3552 
## F-statistic: 5.408 on 1 and 7 DF,  p-value: 0.05296
```

* p-value: 0.05296

2. Consider the previous problem, give the estimate of the residual standard deviation

* Residual standard error: 0.223 on 7 degrees of freedom

3. In the mtcars data set, fit a linear regression model of weight (predictor) on mpg (outcome). Get a 95% confidence interval for the expected mpg at the average weight. What is the lower endpoint?


```r
x <- mtcars$wt
y <- mtcars$mpg
fit <- lm(y ~ x)
predict.lm(fit, data.frame(x = mean(x)), interval = "confidence", level = 0.95)
```

```
##        fit      lwr      upr
## 1 20.09062 18.99098 21.19027
```

* lwr: 18.99098

4. Refer to the previous question. Read the help file for mtcars. What is the weight coefficient interpreted as?

* The estimated expected change in mpg per 1,000 lb increase in weight

5. Consider again the mtcars data set and a linear regression model with mpg as predicted by weight (1,000 lbs). A new car is coming weighing 3000 pounds. Construct a 95% prediction interval for its mpg. What is the upper endpoint?


```r
x <- mtcars$wt
y <- mtcars$mpg
fit <- lm(y ~ x)
predict.lm(fit, data.frame(x = 3), interval = "prediction", level = 0.95)
```

```
##        fit      lwr      upr
## 1 21.25171 14.92987 27.57355
```

* upr: 27.57355

6. Consider again the mtcars data set and a linear regression model with mpg as predicted by weight (in 1,000 lbs). A “short” ton is defined as 2,000 lbs. Construct a 95% confidence interval for the expected change in mpg per 1 short ton increase in weight. Give the lower endpoint.


```r
x <- mtcars$wt
y <- mtcars$mpg
fit <- lm(y ~ I(x/2))
sumCoef <- summary(fit)$coefficients
sumCoef[2,1] + c(-1, 1) * qt(.975, df = fit$df) * sumCoef[2, 2]
```

```
## [1] -12.97262  -8.40527
```

7. If my X from a linear regression is measured in centimeters and I convert it to meters what would happen to the slope coefficient?

* It would get multiplied by 100.

8. I have an outcome, Y, and a predictor, X and fit a linear regression model with Y=β0+β1X+ϵ to obtain β^0 and β^1. What would be the consequence to the subsequent slope and intercept if I were to refit the model with a new regressor, X+c for some constant, c?

* The new intercept would be β^0−cβ^1

9. Refer back to the mtcars data set with mpg as an outcome and weight (wt) as the predictor. About what is the ratio of the the sum of the squared errors, ∑ni=1(Yi−Y^i)2 when comparing a model with just an intercept (denominator) to the model with the intercept and slope (numerator)?


```r
x <- mtcars$wt
y <- mtcars$mpg
fit <- lm(y ~ 1)
fit2 <- lm(y ~ x)
anova(fit2)$"Sum Sq"[2] / anova(fit)$"Sum Sq"[1]
```

```
## [1] 0.2471672
```

10. Do the residuals always have to sum to 0 in linear regression?

* If an intercept is included, then they will sum to 0.

