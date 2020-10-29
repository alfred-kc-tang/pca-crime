# [Principal Component Analysis on Crime Rates](https://alfred-kctang.github.io/pca-crime/)

## Table of Contents

* [Goal](#goal)
* [Data Source](#data-source)
* [Methodology](#methodology)
* [Findings](#findings)
* [Keywords](#keywords)
* [Coding Style](#coding-style)
* [License](#license)

## Goal

The objective of this project is to demonstrate the Principal Component Analysis (PCA) as a alternative technique to variable selection in linear regression model. PCA can be used for the removal of the correlations between the explanatory variables, in addition to the reduction of dimensionality.

## Data Source

The data set is obtained from the [StatSci.org](http://www.statsci.org/data/general/uscrime.html).

## Methodology

The prcomp function from the stats package is used for performing PCA. It is easy to do PCA with a single command, but it is harder to (1) interpret a given linear regression model using principal components as explanatory variables, and (2) to predict a given observation whose measurements are in terms of original variables rather than the principal components. Thus, we need to convert the linear regression model using principal components back into one in terms of original variables, so that we can have an idea of the weightings of each original variables and make predictions on new observations that are measured in original variables.

As usual, I use the hold-out method so as to have an unbiased estimate of the chosen model's performance; to put it simply, a test set is chosen from the data that is only used to estimate the performance of the best model.

Leave-one-out cross validation is adopted for model comparison, between (1) one using only the first principal component, (2) the other using both first and second principal components, as well as (3) the model selected via backward elimination from my previous project.

## Findings

In general, elbow diagram can be used to determine how many principal components should be used. The following elbow diagram shows the variance explained by each of the principal components.

<p align="center">
  <img src="https://github.com/alfred-kctang/pca-crime/blob/master/elbow_diagram.png?raw=true" alt="Elbow Diagram on Explained Variance"/>
</p>

As the elbow diagram indicates, there are signficant reduction of explained variance up to 3, after which explained variance are relatively small. So 3 principal components are used to build a linear regression model, but it turns out that the third principal component does not play a significant role in predicting crime rates, as shown by model output. Moreover, the p-value for the second principal component is 0.1, which is still above the significance level of 0.05. It is not clear whether the second principal component should be included in the linear model, and thus a model using only the first principal component and another one using both the first and second principal components are to be compared by leave-one-out cross validation.

It turns out that the model with the first principal component only performs better than the one using both the first and second principal components, which is consistent with p-value shown the model output. However, the performance of the former is still worse than the model selected via backward elimination from my previous work. A possible explanation for this case is that there are some of the explanatory variables are not useful for predicting crime rates but their noise are incorporated into the principal components, although PCA removed some of the correlations between the explanatory variables.

## Keywords

Holdout method, leave-one-out cross validation (LOOCV), leave-one-out cross validation score (LOOCV score), linear regression, Principal Component Analysis (PCA), regression, variable selection

## Coding Style

This projects follows [Google's R Style Guide](https://google.github.io/styleguide/Rguide.html), which is a fork of the [Tidyverse Style Guide](https://style.tidyverse.org/) by Hadley Wickham.

## License

This repository is covered under the [MIT License](https://github.com/alfred-kctang/pca-crime/blob/master/LICENSE).
