---
title       : Deleloping Data Products Week4
subtitle    : Miles Per Gallon App
author      : Raghu
job         : Software
framework   : io2012   # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
github:
    user: raghuu045
    repo: slidifyslideweek4
---


## Working of Shiny App

The Shiny application is build to display Miles per Gallon for the car. The application uses a linear regression model to find out miles per gallon for the selected features. 

* Fits a linear regression model on the mtcars dataset of "datasets" package.

        1. Identifies the predictors (numeric predictors) which have high 
        correlation (> 0.4) with the outcome (mpg).
        2. For the model then selects the predictor which has the highest 
        correlation from the identified list.
        3. Identifies the predictors which have low correlation (< 0.6) with 
        the selected one for the model, from the identified list.
        4. Adds these predictors to the model. 
        5. Fits the linear regression model.

> * Predicts miles per gallon for the selected features using the model fit. 
> * Displays predicted miles per gallon with a message saying if the mileage is low or good.
> * Provides an option to ON/OFF the display message. 

--- .class #id 

## Dataset for the model

All attributes on the dataset "mtcars" are numeric. Hence all attributes works with correlation function. 

```r
sapply(1:dim(mtcars)[2],function(x) {is.numeric(mtcars[,x])})
```

```
##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
```

```r
str(mtcars)
```

```
## 'data.frame':	32 obs. of  11 variables:
##  $ mpg : num  21 21 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 ...
##  $ cyl : num  6 6 4 6 8 6 8 4 4 6 ...
##  $ disp: num  160 160 108 258 360 ...
##  $ hp  : num  110 110 93 110 175 105 245 62 95 123 ...
##  $ drat: num  3.9 3.9 3.85 3.08 3.15 2.76 3.21 3.69 3.92 3.92 ...
##  $ wt  : num  2.62 2.88 2.32 3.21 3.44 ...
##  $ qsec: num  16.5 17 18.6 19.4 17 ...
##  $ vs  : num  0 0 1 1 0 1 0 1 1 1 ...
##  $ am  : num  1 1 1 0 0 0 0 0 0 0 ...
##  $ gear: num  4 4 4 3 3 3 3 4 4 4 ...
##  $ carb: num  4 4 1 1 2 1 4 2 2 4 ...
```

--- .class #id

## Server Calculation

```r
bestfit <- lm(mpg ~ qsec+drat+am+vs, data = mtcars) ## Model Fit
bestfit
```

```
## 
## Call:
## lm(formula = mpg ~ qsec + drat + am + vs, data = mtcars)
## 
## Coefficients:
## (Intercept)         qsec         drat           am           vs  
##     -10.658        1.103        2.015        6.091        3.073
```


```r
predict(bestfit,newdata) ## Prediction
```

--- .class #id 

## Resources

For the shiny application in Shiny server: Please visit [Miles Per Gallon App](https://raghuu045.shinyapps.io/week4app/)

For the source code in github: Please visit [ui.R and Server.R](https://github.com/raghuu045/DevelopingDataProductsWeek4)

### Notes:
1. The Application has a tab for the instructions on how to use the app. 
2. The Application has a tab for the process flow of the app. 
3. The application was initially built to show the history of prior inquires on the app. Since it has to retain the object between runs, seems it is not working in shiny server. It works locally. Hence commented codes related to this in the script. 

