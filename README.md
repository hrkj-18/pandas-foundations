## Pandas Foundations

### Chapter 1

###

```python
df.head()
df.tail()
df.info()
```
>>prints first five entries <br> prints last five entries <br> prints the info of all columns

### NumPy and pandas working together

```python
import numpy as np

# Create array of DataFrame values: np_vals
np_vals = df.values
```

### Building DataFrames from scratch

```python
list_keys = ['Country', 'Total']
list_values = [['United States', 'Soviet Union', 'United Kingdom'], [1118, 473, 273]]

zipped = list(zip(list_keys , list_values))
print(zipped)
data = dict(zipped)
df = pd.DataFrame(data)
print(df)
```
>>[ ( 'Country', [ 'United States', 'Soviet Union', 'United Kingdom' ] ), ( 'Total', [1118, 473, 273] ) ] <br>

>>| |         Country|  Total|
>>|---|---|---|
>>|0|   United States|   1118|
>>|1|    Soviet Union|    473|
>>|2|  United Kingdom|    273|

### Building DataFrames with broadcasting
```python
state = "PA"
cities=['Manheim','Preston park','Biglerville']

data = {'state':state, 'city':cities}

df = pd.DataFrame(data)
print(df)
```
>>| |  state|             city|
>>|---|---|---|
>>|0|     PA|          Manheim|
>>|1|     PA|     Preston park|
>>|2|     PA|      Biglerville|

### Importing & exporting data

### Reading a flat file

```python
df1 = pd.read_csv(data_file)
print(df1)
```
>>| |  Year|  Total Population|
>>|---|---|---|
>>|0|  1960|      3.034971e+09|
>>|1|  1970|      3.684823e+09|
>>|2|  1980|      4.436590e+09|
>>|3|  1990|      5.282716e+09|
>>|4|  2000|      6.115974e+09|
>>|5|  2010|      6.924283e+09|

```python
new_labels = ['year', 'population']

df2 = pd.read_csv(data_file, header=0, names=new_labels)
print(df2)
```
>>| |  year|    population|
>>|---|---|---|
>>|0|  1960|  3.034971e+09|
>>|1|  1970|  3.684823e+09|
>>|2|  1980|  4.436590e+09|
>>|3|  1990|  5.282716e+09|
>>|4|  2000|  6.115974e+09|
>>|5|  2010|  6.924283e+09|

### Delimiters, headers, and extensions

```python
df1 = pd.read_csv(file_messy)
print(df1.head())

df2 = pd.read_csv(file_messy, delimiter=' ', header=3, comment='#')
print(df2.head())

df2.to_csv(file_clean, index=False)
df2.to_excel('file_clean.xlsx', index=False)
```
>> The following stock data was collect on 2016-AUG-25 from an unknown source <br>
>>These kind of comments are not very useful are they? <br>                        
>>Probably should just throw this line away too but not the next since those are column labels <br> 
>>name Jan Feb Mar Apr May Jun Jul Aug SepOct No...NaN <br>                        
>>\# So that line you just read has all the column...NaN <br>                        
>>IBM 156.08 160.01 159.81 165.22 172.25 167.15 1...NaN <br>  

>>| |    name|     Jan|     Feb|  ...|     Nov|     Dec|
>>|---|---|---|---|---|---|---|
>>|0|     IBM|  156.08|  160.01|  ...|  137.21|  137.96|
>>|1|    MSFT|   45.51|   43.08|  ...|   53.88|   55.40|
>>|2|  GOOGLE|  512.42|  537.99|  ...|  735.39|  755.35|
>>|3|   APPLE|  110.64|  125.43|  ...|  118.16|  111.73|
>> <br>
>>[4 rows x 13 columns]

### Plotting series using pandas
```python
df.plot(color='red')

plt.title('Temperature in Austin')
plt.xlabel('Hours since midnight August 1, 2010')
plt.ylabel('Temperature (degrees F)')

print(df.head(3))
plt.show()
```
>>| |    Temperature (deg F)|
>>|---|---|
>>|0|                   79.0|
>>|1|                   77.4|
>>|2|                   76.4|

>>![Plotting Series with Pandas Example Sample Graph](/img/plotting-series-using-pandas-example.png)

### Plotting DataFrames

```python
print(df.head())
```
>>| |  Temperature (deg F)|  Dew Point (deg F)|  Pressure (atm)|
>>|---|---|---|---|
>>|0|                 79.0|               70.8|             1.0|
>>|1|                 77.4|               71.2|             1.0|
>>|2|                 76.4|               71.3|             1.0|
>>|3|                 75.7|               71.4|             1.0|
>>|4|                 75.1|               71.4|             1.0|

```python
df.plot()
plt.show()
```
>>![Plotting the whole DataFrame](/img/plotting-dataframes-1.png)

```python
df.plot(subplots=True)
plt.show()
```
>>![Plotting the columns separately](/img/plotting-dataframes-2.png)

```python
column_list1 = ['Dew Point (deg F)']
df[column_list1].plot()
plt.show()
```
>>![Plotting only one column](/img/plotting-dataframes-3.png)

```python
column_list2 = ['Temperature (deg F)','Dew Point (deg F)']
df[column_list2].plot()
plt.show()
```
>>![Plotting multiple columns together](/img/plotting-dataframes-4.png)

### Chapter 2

### Visual exploratory data analysis

### pandas line plots

```python
df.plot(x='column_name' , y='column_name or list of column_names')

plt.xlabel('Xaxis description')
plt.ylabel('Yaxis description')
plt.title('Title')

plt.show()
```
### pandas scatter plots

```python
df.plot(kind='scatter', x ='column_name', y ='column_name', s=size)
```
### pandas box plots
```python
cols = ['requiured','columns']
df[cols].plot(kind='box',subplots=True)
plt.show()
```

### pandas hist, pdf and cdf

```python
# This formats the plots such that they appear on separate rows
fig, axes = plt.subplots(nrows=2, ncols=1)

# Plot the PDF
df.fraction.plot(ax=axes[0], kind='hist', normed=True, bins=30, range=(0,.3))
plt.show()

# Plot the CDF
df.fraction.plot(ax=axes[1], kind='hist', normed=True, bins=30, cumulative=True, range=(0,.3))
plt.show()
```
### Statistical exploratory data analysis
#### Describe
```python
df.describe()
```
>>Prints all the min max and quartiles of all the columns
 #### Min & Max
```python
df.min() or df.max()
```
>>Gives min or max of all the columns

#### Count
```python
print(df.count())
```
>>prints the number of non missing values in all columns


#### Quantiles
```python
print(df.quantile([0.05, 0.95]))
```
### Separating populations with Boolean indexing

```python
filtered_df=df.loc[df[column_name]='Value']
```
### Creating and using a DatetimeIndex
```python
# Prepare a format string: time_format
time_format = '%Y-%m-%d %H:%M'

# Convert date_list into a datetime object: my_datetimes
my_datetimes = pd.to_datetime(date_list, format=time_format)  

# Construct a pandas Series using temperature_list and my_datetimes: time_series
time_series = pd.Series(temperature_list, index=my_datetimes)

['20100101 00:00',
 '20100101 01:00',
 '20100101 02:00',
 '20100101 03:00',]
 
 2010-01-01 00:00:00    46.2
2010-01-01 01:00:00    44.6
2010-01-01 02:00:00    44.1
```
### Partial string indexing and slicing
```python
# Extract the hour from 9pm to 10pm on '2010-10-11': ts1
ts1 = ts0.loc['2010-10-11 21:00:00':'2010-10-11 22:00:00']

# Extract '2010-07-04' from ts0: ts2
ts2 = ts0.loc['2010-07-04']

# Extract data from '2010-12-15' to '2010-12-31': ts3
ts3 = ts0.loc['2010-12-15':'2010-12-31']
```
### Reindexing the Index
```python
ts4 = ts2.reindex(ts1.index, method='ffill')
```
### Resampling and frequency
```python
df1 = df['Temperature'].resample('6h').mean()

# Downsample to daily data and count the number of data points: df2
df2 = df['Temperature'].resample('D').count()
```

### Separating and resampling
```python
february = df['Temperature']['2010-Feb']

# Downsample to obtain the daily lowest temperatures in February: february_lows
february_lows = february.resample('D').min()
```
### Rolling mean and frequency
```python
# Extract data from 2010-Aug-01 to 2010-Aug-15: unsmoothed
unsmoothed = df['Temperature']['2010-Aug-01':'2010-Aug-15']

# Apply a rolling mean with a 24 hour window: smoothed
smoothed = unsmoothed.rolling(window=24).mean()

# Create a new DataFrame with columns smoothed and unsmoothed: august
august = pd.DataFrame({'smoothed':smoothed, 'unsmoothed':unsmoothed}
```
### Manipulating pandas time series
### Method chaining and filtering
```python
# Strip extra whitespace from the column names: df.columns
df.columns = df.columns.str.strip()

# Extract data for which the destination airport is Dallas: dallas
dallas = df['Destination Airport'].str.contains('DAL')

# Compute the total number of Dallas departures each day: daily_departures
daily_departures = dallas.resample('D').sum()

# Generate the summary statistics for daily Dallas departures: stats
stats = daily_departures.describe()
```
```python
ts2_interp = ts2.reindex(ts1.index).interpolate(how='linear')

# Compute the absolute difference of ts1 and ts2_interp: differences 
differences = np.abs(ts1 - ts2_interp)

# Generate and print summary statistics of the differences
print(differences.describe())
```

### Time zones and conversion

```python
mask = df['Destination Airport'] == 'LAX'

# Use the mask to subset the data: la
la = df[mask]

# Combine two columns of data to create a datetime series: times_tz_none 
times_tz_none = pd.to_datetime( la['Date (MM/DD/YYYY)'] + ' ' + la['Wheels-off Time'] )

# Localize the time to US/Central: times_tz_central
times_tz_central = times_tz_none.dt.tz_localize('US/Central')

# Convert the datetimes from US/Central to US/Pacific
times_tz_pacific = times_tz_central.dt.tz_convert('US/Pacific')
```

### Plotting time series, datetime indexing
```python
df.plot()
plt.show()

# Convert the 'Date' column into a collection of datetime objects: df.Date
df.Date = pd.to_datetime(df.Date)

# Set the index to be the converted 'Date' column
df.set_index('Date', inplace=True)

# Re-plot the DataFrame to see that the axis is now datetime aware!
df.plot()
plt.show()
```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
