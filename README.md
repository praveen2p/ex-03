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
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("/content/delhi_pm25_aqi.csv")

# Preview data
df.head()
df.dtypes
# Null value count
df.isnull().sum()
```

## Output:
<img width="773" height="342" alt="image" src="https://github.com/user-attachments/assets/68a8f52d-3efb-48a7-b5c0-d954b7832fab" />
<img width="1597" height="637" alt="image" src="https://github.com/user-attachments/assets/5afc255c-765a-435f-ba90-b2f967591ca5" />


## 2)Clean the data: parse datetime, convert pm2.5 to numeric, drop invalid rows.
```
 #Convert datetime column
df['datetime'] = pd.to_datetime(
df['period.datetimeFrom.utc'],
errors='coerce'
)
# Ensure PM2.5 values are numeric
df['value'] = pd.to_numeric(df['value'], errors='coerce')
# Drop rows with missing datetime or PM2.5
df = df.dropna(subset=['datetime', 'value'])

```

## Output:
<img width="723" height="288" alt="image" src="https://github.com/user-attachments/assets/72773f45-3b57-404f-96a0-fd93e567698d" />


## 3)Add date, month, hour columns.
```
df['date'] = df['datetime'].dt.date
df['month'] = df['datetime'].dt.month_name()
df['hour'] = df['datetime'].dt.hour
print(df[['datetime', 'value', 'date', 'month', 'hour']].head())

```


## Output:
<img width="755" height="253" alt="image" src="https://github.com/user-attachments/assets/0f68a538-0d41-4773-b914-e44a74cc98ea" />


## 4)Plot monthly boxplots of PM2.5 (as above).
```
import seaborn as sns
plt.figure(figsize=(12,6))
month_order = [
'January','February','March','April','May','June',
'July','August','September','October','November','December'
]
sns.boxplot(x='month',y='value',data=df,order=month_order)
plt.xticks(rotation=45)
plt.title("Monthly Distribution of PM2.5 – Delhi")
plt.xlabel("Month")
plt.ylabel("PM2.5 (µg/m³)")
plt.tight_layout()
plt.show()

```

## Output:
<img width="1663" height="673" alt="image" src="https://github.com/user-attachments/assets/e72100f6-7fad-4968-8b90-9e1a96984adf" />



## 5)Compute monthly average PM2.5, and plot a bar or line chart.
```

monthly_avg = df.groupby('month')['value'].mean().reindex(month_order)
plt.figure(figsize=(10,5))
monthly_avg.plot(kind='bar')
plt.title("Monthly Average PM2.5 – Delhi")
plt.xlabel("Month")
plt.ylabel("Average PM2.5 (µg/m³)")
plt.tight_layout()
plt.show()
```

## Output:
<img width="1256" height="597" alt="image" src="https://github.com/user-attachments/assets/6323eca7-e4c9-4de1-9ed1-d324e57d9f3f" />


## 6)Compute how many days exceed WHO PM2.5 limit (25 µg/m³) and percentage.

## 7)Plot average PM2.5 vs hour-of-day.

## 8)Find the top 5 worst-polluted days (highest daily averages) and their values/dates.

## 9)Write a brief paragraph interpreting seasonal and daily trends and what those imply for public health.
```

WHO_LIMIT = 25
# Daily average PM2.5
daily_avg = df.groupby('date')['value'].mean()
total_days = daily_avg.shape[0]
exceed_days = (daily_avg > WHO_LIMIT).sum()
percentage_exceed = (exceed_days / total_days) * 100
print(f"Total days: {total_days}")
print(f"Days exceeding WHO limit: {exceed_days}")
print(f"Percentage of unsafe days: {percentage_exceed:.2f}%")
hourly_avg = df.groupby('hour')['value'].mean().reset_index()
plt.figure(figsize=(10,5))
sns.lineplot(x='hour', y='value', data=hourly_avg, marker='o')
plt.title("Average PM2.5 by Hour of Day – Delhi")
plt.xlabel("Hour of Day")
plt.ylabel("PM2.5 (µg/m³)")
plt.xticks(range(0,24))
plt.tight_layout()
plt.show()


```


## Output

<img width="763" height="295" alt="image" src="https://github.com/user-attachments/assets/8f66be61-4bbe-4645-bb15-19668f940821" />

<img width="1300" height="559" alt="image" src="https://github.com/user-attachments/assets/5e78f1a7-558f-4dc5-ba4a-2a62ccea6d43" />




## Result

The dataset was successfully loaded and processed to extract pollutant-wise and station-wise air quality data for Delhi.


