### NAME : KARTHIKEYAN R
### REG NUM: 212222240045
### Date : 

# Ex.No: 1B  CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on Rainfall Rate
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller
%matplotlib inline

train = pd.read_csv("/content/rainfall.csv")
# Change 'Date' to 'date' to match the actual column name
train['date'] = pd.to_datetime(train['date'], format='%Y-%m-%d')  
train.set_index('date', inplace=True)  
train.head()

# Change 'Price' to 'rainfall' to match the actual column name
train['rainfall'].plot(title='Rainfall') 

def adf_test(timeseries):
    print('Results of Dickey-Fuller Test:')
    dftest = adfuller(timeseries, autolag='AIC')
    dfoutput = pd.Series(dftest[0:4], index=['Test Statistic', 'p-value', '#Lags Used', 'Number of Observations Used'])
    for key, value in dftest[4].items():
        dfoutput['Critical Value (%s)' % key] = value
    print(dfoutput)

# Change 'Price' to 'rainfall' to match the actual column name
adf_test(train['rainfall'])
```
### REGULAR DIFFERENCING:
```
train['Rainfall_diff'] = train['rainfall'] - train['rainfall'].shift(1) # Changed 'Price' to 'rainfall' to match the actual column name
train['Rainfall_diff'].dropna().plot(title='Differenced Rainfall Rate ')
```
### SEASONAL ADJUSTMENT:
```
n = 7
# Changed 'Price' to 'rainfall' to match the actual column name
train['Rainfall_seasonal_diff'] = train['rainfall'] - train['rainfall'].shift(n) 
train['Rainfall_seasonal_diff'].dropna().plot(title='Seasonally Differenced Rainfall Rate')
```
### LOG TRANSFORMATION:
```
# Calculate the logarithm of the 'rainfall' column 
train['rainfall_log'] = np.log(train['rainfall'])

# Calculate the log difference using the 'rainfall_log' column
train['rainfall_log_diff'] = train['rainfall_log'] - train['rainfall_log'].shift(1)

# Plot the log differences with an appropriate title
train['rainfall_log_diff'].dropna().plot(title='Log Differenced Rainfall')
```

### OUTPUT:

![image](https://github.com/user-attachments/assets/1b14f355-9e3d-4219-891b-d89bb3f633fe)


### REGULAR DIFFERENCING:

![image](https://github.com/user-attachments/assets/03942739-6c54-4c50-baef-15fced8b9392)



### SEASONAL ADJUSTMENT:

![image](https://github.com/user-attachments/assets/0b779373-53a5-4b2f-a6df-c977781a8ef7)

### LOG TRANSFORMATION:

![image](https://github.com/user-attachments/assets/9407c2e1-2b35-488f-a8c3-336e82bde23e)



### RESULT:

Thus The python code has been created for the conversion of non stationary to stationary data on Rainfall Rate.
