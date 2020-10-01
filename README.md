# oura-sleep-ring
The Oura sleep ring records several metrics during sleep including amount of REM sleep, deep sleep, and total sleep time. It spits out a daily Sleep Score metric
from 0-100, representing an overall indicator of how you slept (100 is the best possible score).

## Problem Summary (business question, expected output, motivation)
Can we reverse engineer Oura Sleep Ring's proprietary Sleep score metric? Doing this successfully could unveil a powerful algorithm that could help people with or without this ring understand the most critical factors in their sleep, and provide a formula for a holistic metric that lets you know the quality of your sleep. 

## Data Required
The following data fields were used:


## Analysis Procedure
My approach was to train supervised machine learning regression algorithms and attempt to predict the Sleep score metric accurately. By doing so, I can use feature weights and importances to reconstruct a formula that can be used to calculate the Sleep score metric. In particular, I tested:
* Linear regression (varying polynomial degree features)
* Ridge regression
* Lasso regression
* Random Forest


## Results

The test errors of the tuned algorithms were the following-

Since vanilla linear regression (with 1st degree polynomial features) was quite close, and didn’t involve confusing features to look at (e.g. x2^2 * x8), I will list the top 5 features and their weights:
…

The full analysis and weights of all the algorithms can be found in the notebooks”"

## Caveats and Improvements
* Due to a lack of data (~500 usable data points), the results of this analysis are less powerful.
