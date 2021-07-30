# California's Hospitals Bed Capacity Forecasting
## Objective
To create the Forecasting of California COVID-19 Hospital bed capacity 1-month ahead (weekly average) using pipeline and ML models in sklearn. Check out the notebook **[here]()**.
<br>
## Dataset
Hospitals Bed Capacity data from 2020-07-31 to 2021-02-19 by
[Facility by Department of Health and Human Services](https://healthdata.gov/dataset/covid-19-reported-patient-impact-and-hospital-capacity-facility )<br>
**Train/ Validation / Test Split**<br>
Train: 2020-07-31 to 2021-12-25 (5 months)<br>
Validation: 2021-01-01 to 2021-01-22 (1 month)<br>
Test: 2021-01-29 to 2021-02-19 (1 month)
![](images/split.png?raw=True)
<br>
<br>
## Modeling
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
![](images/approach1.png?raw=True)
2. Fit Stacking Ensemble model using linear models & RandomForest as base learners and using GradientBoosting as meta-learner.
![](images/approach2.png?raw=True)
<br>
<br>
## Summary<br>
![](images/summary.png?raw=True)

Best model: Stacking Ensemble model 
* base learners
    * LassoRegressor
    * RidgeRegressor
    * RandomForestRegressor
* meta-learner
    * GradientBoostingRegressor

The model has 23% lower RMSE compare to baseline
