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
    * [Model Comparison](#model-comparison)
    * [Variable Selection](#variable-selection)
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

### Model Comparison

#### Lasso Regression
The result of alpha and RMSE plot in Figure 6. In this case it appears that the model's rmses nearly monotonically increase as alpha  increases. This indicates that the CV proceedure is exhibiting a preference for the linear regression mode. However, one of the suggestions employed by Hastie, et al. in their glmnet R package is instead of using the with the smallest mean rmse to instead use the largest value of that has an error metric (rmse) that is within 1 standard error of the minimum value of the error metric (rmse). We can find this value using the lasso_cv_res data frame we previously constructed. RMSE of validation dataset in Figure 7.

<img src="/image/lasso1.png" width="600"/> 
<em>Figure 6: alpha and RMSE plot.</em>

<img src="/image/lasso3.png" width="600"/> 
<em>Figure 7: RMSE of validation dataset for lasso regression.</em>

#### Ridge Regression
The result of alpha and mean test score plot in Figure 8. This plot clearly shows that the value between 6 and 8 is obtained as the minimum of this curve. However, this plot gives us an overly confident view of this choice of this particular value of aplha. RMSE of validation dataset in Figure 9.

<img src="/image/ridge1.png" width="400"/> 

<em>Figure 8: alpha and mean test score plot.</em>

<img src="/image/ridge3.png" width="600"/> 

<em>Figure 9: RMSE of validation dataset for ridge regression.</em>

In all variables case, the RMSE of validation dataset is smaller thn training dataset. Therefore, I will choose to use ridge regression model to fit this dataset.

| Method | Traning dataset RMSE | Validation dataset RMSE |
| ------ | ------ | ------ |
| Lasso | 20736.2| 20967.1|
| Ridge | 20085.9 | 20396.3 |

<em>Table 3: The performance of lasso regression and ridge regression.</em>

### Variable Selection
Since the variable of `garage_cars` and `garage_area` have high correlation and the coefficient of `garage_area` is high. And the variable of `living_area` has high correaltion with `full_bath` and `bedroom`. In order to prevent multicollinearity, we will omit the variable of `garage_cars`, `full_bath` and `bedroom`. The coefficient of `ac` and `zoning` also small. That means the influence of those variables may not strong. We also try to omit those variable to see the impact.

The result of alpha and mean test score plot in Figure 9 shows that the value between 6 and 8 is obtained as the minimum in this model and RMSE of validation dataset in Figure 10.

<img src="/image/select_ridge.png" width="400"/> 

<em>Figure 9: alpha and mean test score plot.</em>

<img src="/image/select_ridge2.png" width="400"/> 

<em>Figure 10: RMSE of validation dataset for selected variables.</em>

According to the above, we can notice that this dataset is high dimensional input. And there are some variables are continuous variables. In this project, we consider use ridge regression and lasso regression. Using the Ridge regression can shrink some  𝛽  tend to  0  but still need to consider all of varibales. Using lasso regression can shrink coefficient to 0 but according to the performance of validation dataset, it shows the ridge regression is more better. Then, we base on the reslut of all variables to omit some variables which can prevent multicollinearity issue and simplify the complexity of model.

## Result

## Discussion
