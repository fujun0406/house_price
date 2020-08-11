# Project - House Price

## Contents
* [Overview](#overview)
* [Exploratory Data Analysis](#exploratory-data-analysis)
    * [Data](#data)
    * [Analyzing the target variable (sale_price)](#analyzing-the-target-variable-(sale_price))
    * [Preprocessing](preprocessing)
* [Building Models](#building-models)
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

### Analyzing the target variable (sale_price)
There are no negative values in the dataset for sale price and the distribution is right skewed, 
so we need to tranform this variable it or this will adversly impact our model in Figure 1. We try to transform the distribution 
by using log function and we can see the data simialr to normal.

<img src="/image/house_price1.png" width="410"/> <img src="/image/house_price2.png" width="410"/> 

<em>Figure 1: The distribution of sale price.</em>

<img src="/image/house_price3.png" width="410"/> <img src="/image/house_price4.png" width="410"/> 

<em>Figure 2: The distribution of log sale price.</em>

## Building Models

## Result

## Discussion
