
[<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/banner.png" width="888" alt="Visit QuantNet">](http://quantlet.de/)

## [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **MVAboshousing** [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/)

```yaml

Name of Quantlet : MVAboshousing

Published in : Applied Multivariate Statistical Analysis

Description : 'Computes the ANCOVA model with Boston housing data. We add binary variable to the
ANCOVA model, and try to check the effect of the new factors on the dependent variable.'

Keywords : 'ANCOVA, anova, regression, financial, covariance, linear, linear-model,
linear-regression, test'

See also : SMSanovapull, SMSdete2pull

Author : Mengmeng Guo

Submitted : Mon, July 07 2014 by Philipp Gschoepf

Datafile : bostonh.dat

Output : The coefficients of the independent variables and dependent variable.

Example : The model is used for testing the interaction of x4 and x12, and also x4 and x15.

```


### R Code:
```r

# Clear variables and close windows
rm(list = ls(all = TRUE))
graphics.off()

# load data
data = read.table("bostonh.dat")

# First we use the ANOVA model to do the regression
x1  = data[, 1]
x2  = data[, 2]
x3  = data[, 3]
x4  = data[, 4]
x5  = data[, 5]
x6  = data[, 6]
x7  = data[, 7]
x8  = data[, 8]
x9  = data[, 9]
x10 = data[, 10]
x11 = data[, 11]
x12 = data[, 12]
x13 = data[, 13]
x14 = data[, 14]
fit = lm(x14 ~ x4 + x5 + x6 + x8 + x9 + x10 + x11 + x12 + x13)
summary(fit)

# We replace x9 by x15, and also transform x4.
x4  = data[, 4]
n   = length(x4)
for (i in 1:n) {
    if (x4[i] == 0) 
        x4[i] = -1
}
y   = 0
for (i in 1:n) {
    if (x9[i] >= median(x9)) 
        y[i] = 1 else y[i] = -1
}
x15  = y
fit2 = lm(x14 ~ x4 + x5 + x6 + x8 + x10 + x11 + x12 + x13 + x15)
summary(fit2)

# This is used for testing the interaction of x4 and x12, and also x4 and x15.
fit3 = lm(x14 ~ x4 + x5 + x6 + x8 + x10 + x11 + x12 + x13 + x15 + x4 * x12 + x4 * x15)
summary(fit3)

```
