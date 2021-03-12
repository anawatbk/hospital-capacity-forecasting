# 🛏️📈 California's COVID-19 Hospitals Bed Capacity Forecasting
## Author: Anawat Putwanphen
## Project Goal
Forecast California COVID-19 Hospital bed capacity 1-month ahead (weekly average) using ML models in sklearn.
<br>
using dataset from Facility by Department of Health and Human Services
<br>
Links: https://healthdata.gov/dataset/covid-19-reported-patient-impact-and-hospital-capacity-facility 

## Highlight
### Feature Engineering
Create custom sklearn TransformerClass for
pipeline
<br>
1. Create custom calculated columns. 
2. Select only columns relevant for this project. 
3. Generate Lag features, and moving average. 
 
Example, lags = 5

create and append 5 new columns to dataframe.  

|x-5 | x-4 | x-3 | x-2 | x-1 | x-MA3 |

4. GroupbyImputer   
Impute missing values of each column by its hospital's median.


### Modeling Approach

1. Using RandomizedSearchCV to search across hyperparameters and models
2. Fit Stacking Ensemble model using linear models & RandomForest as base learners and using GradientBoosting as meta-learner.


### Summary
Best model: Stacking Ensemble model 
* base learners
    * LassoRegressor
    * RidgeRegressor
    * RandomForestRegressor
* meta-learner
    * GradientBoostingRegressor


The model has 23% lower RMSE compare to Naive method (using lastest week to forecast)
