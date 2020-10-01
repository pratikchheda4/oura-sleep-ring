# Introduction
The Oura sleep ring records several metrics during sleep including amount of REM sleep, deep sleep, and total sleep time. It outputs a daily Sleep Score metric
from 0-100, representing an overall indicator of how you slept (100 is the best).

In depth analysis can be found in the following notebooks:
* `sleep_data_linear_regression_ridge_lasso.ipynb`
* `sleep_data_random_forest.ipynb`

## Problem Summary (business question, expected output, motivation)
Can we reverse engineer Oura Sleep Ring's proprietary Sleep Score metric? Doing this successfully could unveil a powerful algorithm that could help people with or without this ring understand the most critical factors in their sleep, and provide a formula for a holistic metric that lets you know the quality of your sleep. 

## Data
The following data fields were included:
* sleep_score                   (float64)
* total_bedtime                 (float64)
* total_sleep_time              (float64)
* awake_time                    (float64)
* rem_sleep_time                (float64)
* light_sleep_time              (float64)
* deep_sleep_time               (float64)
* restless_sleep                (float64)
* sleep_efficiency              (float64)
* sleep_latency                 (float64)
* sleep_timing                  (float64)
* average_resting_heart_rate    (float64)
* lowest_resting_heart_rate     (float64)
* average_hrv                   (float64)
* temperature_deviation_(°c)    (float64)
* respiratory_rate              (float64)

Data sample screenshot:

Distribution of Sleep Scores:


## Analysis Procedure
My approach was to train supervised machine learning regression algorithms and attempt to predict the Sleep Score metric accurately. By doing so, I can use feature weights and importances to reconstruct a formula that can be used to calculate the Sleep Score metric. In particular, I tested:
* Linear regression (varying polynomial degree features)
* Ridge regression
* Lasso regression
* Random Forest


## Results

The test errors of the tuned algorithms were the following
 MAKE TABLE HERE

Since vanilla linear regression (with 1st degree polynomial features) was quite close, and didn’t involve confusing features to look at (e.g. x2^2 * x8), I will list the top 5 features and their weights:
MAKE TABLE HERE OR INCLUDE SCREENSHOT

The full analysis and weights of all the algorithms can be found in the following notebooks:
* `sleep_data_linear_regression_ridge_lasso.ipynb`
* `sleep_data_random_forest.ipynb`

## Caveats and Improvements
### Caveats
* Due to a lack of data (~500 usable data points), the results of this analysis are less powerful.
* I did not use other score metrics they provided such as 'rem_sleep_score' which is also not transparently calculated. Including features like this would defeat the purpose of the project.
* Computation constraints did not allow me to do a wider randomized and grid parameter search.

### Improvements
* Additional data would allow me to test more sophisticated algorithms like neural networks
* Trying some boosting algorithms (i.e. gradient boosting, extreme gradient boosting)

