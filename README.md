## Introduction
The Oura sleep ring records several metrics during sleep including amount of REM sleep, deep sleep, and total sleep time. It outputs a daily Sleep Score metric
from 0-100, representing an overall indicator of how you slept (100 is the best).

In depth analysis can be found in the following notebooks:
* `sleep_data_linear_regression_ridge_lasso.ipynb`
* `sleep_data_random_forest.ipynb`

## Problem Summary (business question, expected output, motivation)
Can we reverse engineer Oura Sleep Ring's proprietary Sleep Score metric? Doing this successfully could unveil a powerful algorithm that could help people with or without this ring understand the most critical factors in their sleep, and provide a formula for a holistic metric that lets you know the quality of your sleep. 

## Data

The data was sourced from my personal ring as well as anonymous friends

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

Performance of the algorithms:
| Name                         | Test Error (MSE) | R^2  |
|------------------------------|------------------|------|
| Linear Regression (1st poly) | 7.82             | .833 |
| Linear Regression (2nd poly) | 9.29             | .812 |
| Ridge Regression (2nd poly)  | 7.02             | .853 |
| Lasso Regression (2nd poly)  | 6.91             | .846 |
| Random Forest                | 9.22             | .777 |

In terms of test error, Lasso regression performed the best.
The top 5 features and their weights:

| Feature                                | Coefficient | Coefficient (absolute value) |
|----------------------------------------|-------------|------------------------------|
| total_sleep_time                       | 25.26       | 25.26                        |
| sleep_latency                          | 12.14       | 12.14                        |
| awake_time * lowest_resting_heart_rate | -10.30      | 10.30                        |
| sleep_latency^2                        | -9.49       | 9.49                         |
| rem_sleep_time                         | 7.56        | 7.56                         |

The full analysis and weights of all the algorithms can be found in the following notebooks:
* `sleep_data_linear_regression_ridge_lasso.ipynb`
* `sleep_data_random_forest.ipynb`

## Caveats and Improvements
### Caveats
* Due to a lack of data (~500 usable data points), the results of this analysis are less powerful.
* I did not use other score metrics they provided such as 'rem_sleep_score' which is also not transparently calculated. Including features like this would defeat the purpose of the project.
* Computation constraints did not allow me to do a wider randomized and grid parameter search.
* The data only consists of 3 different peoples' data. It might not generalize well without a significant sample of the population.

### Improvements
* Additional data would allow me to test more sophisticated algorithms like neural networks
* Trying some boosting algorithms (i.e. gradient boosting, extreme gradient boosting)
* Ensembling multiple models could help reduce variance and improve performance
