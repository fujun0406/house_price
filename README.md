# Project - House Price

## Contents
* [Overview](#overview)
* [Exploratory Data Analysis](#exploratory-data-analysis)
    * [Data](#data)
    * [Analyzing the Target Variable](#analyzing-the-target-variable)
    * [Relationship about Continuous Features](#relationship-about-continuous-features)
    * [Relationship about Categorical Features](#relationship-about-categorical-features)
    * [Preprocessing](preprocessing)
* [Building Models](#building-models)
    * [Lasso Regression](#lasso-regression)
    * [Rasso Regression](#ridge-regression)
* [Result](#result)
* [Discussion](#discussion)

## Overview
We will be using data on house sales from a large city in the United States with the goal of developing a predictive model for the sale price of homes in this city.
The primary goal is for the model to accurately predict the price of a new house coming to market, something that is clearly of use to both buyers and sellers. In this project,

* Utilizing Lasso regression and ridge regression.
* Measuring which model is more suitable for this dataset.
* Trying to do variable selection in order to simplify model.

## Exploratory Data Analysis

### Data
In this dataset, we have 15 features in Table 1 which consist of continuous variabls and categorical variables and total samples is 1584. There is no missing values in the dataset.

<table>
<tr><th>Continuous Variabls </th><th>Categorical Variables</th></tr>
<tr><td>
  
| Column | Non-Null Count | Dtype |
|--|--|--|
| sale_price |       1584 non-null | int64 | 
| year_sold |        1584 non-null | int64 | 
| year_built |       1584 non-null | int64 | 
| lot_area |         1584 non-null | int64 | 
| basement_area |    1584 non-null | int64 | 
| living_area |      1584 non-null | int64 | 
| full_bath |        1584 non-null | int64 | 
| half_bath |        1584 non-null | int64 | 
| bedroom |          1584 non-null | int64 | 
| garage_cars |      1584 non-null | int64 | 
| garage_area |      1584 non-null | int64 | 

</td><td>

| Column | Non-Null Count | Dtype |
|--|--|--|
| ac |               1584 non-null | object | 
| zoning |           1584 non-null | object | 
| neighborhood |     1584 non-null | object | 
| quality |          1584 non-null | object | 
| condition |        1584 non-null | object | 

</td></tr> </table>

<em>Table 1: The attribute for datasets of dataset.</em>

### Analyzing the Target Variable
There are no negative values in the dataset for sale price and the distribution is right skewed, 
so we need to tranform this variable it or this will adversly impact our model in Figure 1. We try to transform the distribution 
by using log function and we can see the data simialr to normal.

<img src="/image/house_price1.png" width="410"/> <img src="/image/house_price2.png" width="410"/> 

<em>Figure 1: The distribution of sale price.</em>

<img src="/image/house_price3.png" width="410"/> <img src="/image/house_price4.png" width="410"/> 

<em>Figure 2: The distribution of log sale price.</em>

### Relationship about Continuous Features
According to Figure 3, we can notice that the correaltion of `sale_price` is lower with `year_sold`, `lot_area`, `half_bath` and `bedroom` since there correlation under 0.5. The variable of `living_area` has high correaltion with `full_bath` and `bedroom` and `garage_cars` has high correlation with `garage_area` and `year_build`.

<img src="/image/correlation.png" width="600"/> 

<em>Figure 3: The correlation matrix.</em>

We can see that the variable of `year_built`, `lot_area`, `basement_area`, `living_area`, `half_bath` they are skewed so we need to handle it.
<table>
<tr><td>
   
| Variables | Skewness |
| ------ | -------|
| lot_area |         11.782904 | 
| living_area |       1.008922 | 
| half_bath |         0.727706 | 
| basement_area |     0.529231 | 
| full_bath |         0.348596 | 

</td><td>
   
 | Variables | Skewness |
| ------ | -------|
| garage_area |       0.221875 | 
| bedroom |           0.211698 | 
| year_sold |         0.073479 | 
| garage_cars |      -0.050316 | 
| year_built |        -0.556842 | 

</td></tr> </table>

<em>Table 2: The skewness of continuous variables.</em>

### Relationship about Categorical Features
It seems sale_price will be influenced by all of categorical variables. We can try to check Figure 4 and Figure 5 which are about
quality and condition respetively. More deatils about other features can check on jupyter notebook.

<img src="/image/quality.png" width="600"/> 

<em>Figure 4: The distribution of quality variable.</em>

<img src="/image/condition.png" width="600"/> 

<em>Figure 5: The distribution of condition variable.</em>

### Preprocessing
Based on previous analysis, we will use log to transform the variables of `sale_price`, `year_built`, `lot_area` and `living_area` which can make the distribtion to be more normal. In terms of categorical variables, we will use the module pandas in Python to transform categorical variables into dummy variables.

## Building Models
In this project, we try to use lasso regression and ridge regression to explore this datset because this dataset is high dimensional input. 

### Lasso Regression
The result of $\alpha$ and RMSE plot in Figure 6.

<img src="/image/condition.png" width="600"/> 

<em>Figure 6: $\alpha$ and RMSE plot.</em>

### Ridge Regression
## Result

## Discussion
