# Forecasting Bus Demand in Banana Republic Municipalities with Time Series

## Problem Definition

The central urban planning commitee of Banana Republic asked you to help them with the forecast of bus demands of municipalities. And they provide a nice dataset to support you (https://pi.works/3w8IJbV). 
The dataset includes two measurements for an hour for the number of used buses in each municipality, each measurement is timestamped. The dataset format is as follows (comma separated values):

- MUNICIPALITY_ID: where municipality_id is an anonymization to disguise the actual names,There are 10 municipalities (ids from 0 to 9)
- TIMESTAMP: represents the exact time of the measurement,
- USAGE: is the number of buses in use at the time of measurement
- TOTAL_CAPACITY: represents the total number of buses in the municipality two measurements for an hour.

The committee asks you to forecast the hourly bus usages for next week for each municipality. 
Hence you can aggregate the two measurements for an hour by taking the max value (sum would not be a nice idea for the obvious reasons) for each hour, and you should model this data with a time series model of your selection. 

The committee says that they will use the last two weeks (starting from 2017-08-05 to 2017-08-19) as assessment (test) data, hence your code should report the error (in the criterion you chose for the task) for the last two weeks. You may use true values for the prediction of the last week of test data, then combine the error of the first and last week of the test separately.

Keep in mind that the dataset has missing data, hence a suitable missing data interpolation would be useful.


