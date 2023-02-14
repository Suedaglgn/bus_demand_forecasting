# Forecasting Bus Demand in Banana Republic Municipalities with Time Series

## Problem Definition

The central urban planning commitee of Banana Republic asked you to help them with the forecast of bus demands of municipalities. And they provide a nice dataset to support you. 
The dataset includes two measurements for an hour for the number of used buses in each municipality, each measurement is timestamped. The dataset format is as follows (comma separated values):

- MUNICIPALITY_ID: where municipality_id is an anonymization to disguise the actual names,There are 10 municipalities (ids from 0 to 9)
- TIMESTAMP: represents the exact time of the measurement,
- USAGE: is the number of buses in use at the time of measurement
- TOTAL_CAPACITY: represents the total number of buses in the municipality two measurements for an hour.

The committee asks you to forecast the hourly bus usages for next week for each municipality. 
Hence you can aggregate the two measurements for an hour by taking the max value (sum would not be a nice idea for the obvious reasons) for each hour, and you should model this data with a time series model of your selection. 

The committee says that they will use the last two weeks (starting from 2017-08-05 to 2017-08-19) as assessment (test) data, hence your code should report the error (in the criterion you chose for the task) for the last two weeks. You may use true values for the prediction of the last week of test data, then combine the error of the first and last week of the test separately.

Keep in mind that the dataset has missing data, hence a suitable missing data interpolation would be useful.


## Methods

- Simple Moving Average
- Prophet
- LSTM Encoder-Decoder

## Results

|                |        |  Models   |    |
|:--------------:|:------:|:---------:|:--:|
| Municipalities |  SMA   |  Prophet  | LSTM |
|       0        |  0,24  |   0,23    | 0,22 |
|       1        |  0,28  |   0,56    | 0,24 |
|       2        |  0,23  |   0,57    | 0,18 |
|       3        |  0,30  |   0,20    | 0,15 |
|       4        |  0,33  |   0,22    | 0,25 |
|       5        |  2,47  |   8,05    | 0,75 |
|       6        |  0,17  |   0,19    | 0,13 |
|       7        |  0,21  |   0,11    | 0,16 |
|       8        |  0,23  |   0,19    | 0,20 |
|       9        |  0,24  |   0,26    | 0,18 |


## Usage

- Run preprocess.ipynb to create preprocced_data.csv
- Run desired model's notebook

## Hyperparameters

**General Parameters**
```
forecast_start = "2017-08-05 06"
forecast_end = "2017-08-19 16"
working_hours_start = 7
working_hours_end = 16
```


- **Simple Moving Average**
  - window: 11
- **Prophet**
  - yearly_seasonality=False,
  - weekly_seasonality=True,
  - daily_seasonality='auto',
  - interval_width=0.95
- **LSTM**
  - EarlyStopping
    - monitor="val_loss",
    - min_delta=0.005,
    - patience=10,
    - mode="min"
  - ReduceLROnPlateau
    - monitor="val_loss"
    - factor=0.2
    - mode="min"
    - patience=3
    - min_lr=0.01
  - LOOK_BACK = 7 
  - FORECAST_RANGE = 1
  - epochs = 100 
  - batch_size = 32 
  - validation = 0.1
  - optimizer='rmsprop'
  - loss='mae'
  - run_eagerly=True
  - activation='relu'
