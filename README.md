### NAME: Praveen.K
### REG.NO:212223040152

## EXP 3 - Delhi Air Quality Analysis

## Aim

To compare air quality parameters in Delhi across different stations and analyze the relationship between pollutants (e.g., PM2.5 and NO₂) using scatter plots and correlation analysis.


## Procedure / Algorithm

1)Load the dataset using pandas.

2)Preprocess the data:

3)Convert the date column (period.datetimeFrom.utc) to datetime format.

4)Drop missing or invalid values.

5)Pivot the dataset so each pollutant (parameter) becomes a separate column.

6)Plot scatter plot between PM2.5 and NO₂ to study their relationship.

7)Plot correlation heatmap between all pollutants to identify relationships.

8)Interpret the results — identify which pollutants are correlated and which stations are most polluted.


## Program
## 1)Load the dataset and show summary (head, data types, null counts).
```

```

## Output:

## 2)Clean the data: parse datetime, convert pm2.5 to numeric, drop invalid rows.
```


```

## Output:


## 3)Add date, month, hour columns.
```


```


## Output:


## 4)Plot monthly boxplots of PM2.5 (as above).
```


```

## Output:


## 5)Compute monthly average PM2.5, and plot a bar or line chart.
```


```

## Output:


## 6)Compute how many days exceed WHO PM2.5 limit (25 µg/m³) and percentage.
```


```

## Output:



## 7)Plot average PM2.5 vs hour-of-day.
```



```


## Output:

## 8)Find the top 5 worst-polluted days (highest daily averages) and their values/dates.
```


```


## Output:


## 9)Write a brief paragraph interpreting seasonal and daily trends and what those imply for public health.
```




```


## Output


## Result

The dataset was successfully loaded and processed to extract pollutant-wise and station-wise air quality data for Delhi.


