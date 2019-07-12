Predicting demand 

https://www.kaggle.com/c/demand-forecasting-kernels-only/data

***********
https://slides.com/jvbw/sales-forecast
***********
*********** 1  Exploratory analysis

The data is for 10 stores, with 50 different items each.
It shows the number of sales for each item on a daily basis, from 01/01/2013 to 31/12/2017.

The dataset is clean, over 900000 rows for 4 columns.

As my computer is slow, I decided to work with data from items 1 to 25 (half of them).

Plotting the sales of 5 items over 5 years shows strong seasonality (yearly), and an upward trend over the years.

1.1  Creating columns

I created some extra columns, extracting from the 'date' info.
(I finally didn't use this additionnal data).

1.2  Some visualizing

I made different plots to visualize changes in time, and distribution of sales among items and stores.

***********
*********** 2  Modelling
The plots show a strong seasonality and trend, so I turned to SARIMA : SARIMA seems to be a good fit as this model takes trend and seasonality into account. 

For SARIMA, you have to set the date as the index, and explicitely set a frequency. To start with, I used daily data, grouping all the sales by day.

Using StatsModel, and plotting the decomposition, the trend and seasonality are obvious.
The ACF plots show seasonality of 7 (every week) and 365, every year.

2.0.1  Assumptions and data preparation 
Assumption : data is stationnary. If it isn't, make it.

Dickey-Fuller to check stationarity. The test is inconclusive, but the plots show that the data isn't stationary.
A simple one-time differentiation makes the data stationary.

Autocorrelation tests also show seasonality, again.

2.0.4  Determining coefficients for p, d, q (resampled monthly series)


Using SARIMA, you need to know what you use as p, d and q parameters. 
Making the data stationary, and looking at acf plots is a good way to get a feeling of these parameters.
The most precise way of choosing however is testing the AIC coefficient with different parameters and choosing those that return the lowest AIC.
I found some code that loops over all different parameter combinations to find the best AIC. 
This code is similar to StepWise in R.
I added to this to return the best combinations, instead of a long list with all parameters and AICs.

2.0.5  SARIMA
Using the most fitting parameters, I run Sarima.
Running SARIMA with daily sale values doesn't return very good results.
On a monthly basis, however, the model is nicely accurate.

I wrote a short interactive program, that takes a month and year as user input, and returns the forecast, including confidence interval.

2.0.6  Prophet
Prophet is a forecast model by facebook. It can take holidays into account.
It finds weekly and yearly trends by itself.


*********** 3 Comparing models
***********

Comparing purely based on the last year predictions (2017) errors, SARIMA is the best model. 
Prophet is also goood, but overpredicts slightly.

Prophet is much better with daily predictions and variations, and is easier to implement.