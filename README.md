# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
### Date: 19-08-2025
### Developed By: K MADHAVA REDDY
### Register Number: 212223240064

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_csv("avocado.csv")

data['Date'] = pd.to_datetime(data['Date'])
data = data.groupby('Date')['Total Volume'].mean().reset_index()
data.set_index('Date', inplace=True)

data['volume_diff'] = data['Total Volume'] - data['Total Volume'].shift(1)

result = seasonal_decompose(data['Total Volume'], model='additive', period=52)
data['volume_sea_diff'] = result.resid

data['volume_log'] = np.log(data['Total Volume'])
data['volume_log_diff'] = data['volume_log'] - data['volume_log'].shift(1)

result = seasonal_decompose(data['volume_log_diff'].dropna(), model='additive', period=52)
data['volume_log_seasonal_diff'] = result.resid

plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data['Total Volume'], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('Year')
plt.ylabel('Total Volume')

plt.subplot(6, 1, 2)
plt.plot(data['volume_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced Volume')

plt.subplot(6, 1, 3)
plt.plot(data['volume_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Seasonally Adjusted Volume')

plt.subplot(6, 1, 4)
plt.plot(data['volume_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log(Total Volume)')

plt.subplot(6, 1, 5)
plt.plot(data['volume_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Year')
plt.ylabel('RDiff(Log(Total Volume))')

plt.subplot(6, 1, 6)
plt.plot(data['volume_log_seasonal_diff'], label='Log Transformation and Regular Differencing and Seasonal Differencing')
plt.legend(loc='best')
plt.title('Log Transformation + Regular Differencing + Seasonal Differencing')
plt.xlabel('Year')
plt.ylabel('SDiff(RDiff(Log(Total Volume)))')

plt.tight_layout()
plt.show()
```

### OUTPUT:

#### ORIGINAL DATA:
<img width="1228" height="205" alt="image" src="https://github.com/user-attachments/assets/e7c266c7-3c46-477c-b463-a34341752a9d" />


#### REGULAR DIFFERENCING:
<img width="1234" height="215" alt="image" src="https://github.com/user-attachments/assets/1ea9e1f2-61fb-4c94-9ef5-774da1ef6cf8" />



#### SEASONAL ADJUSTMENT:
<img width="1250" height="195" alt="image" src="https://github.com/user-attachments/assets/49873578-9c44-4ed1-a163-de97d99b3cbd" />


#### LOG TRANSFORMATION:
<img width="1222" height="197" alt="image" src="https://github.com/user-attachments/assets/5cf1864d-5993-4d2f-8555-2ff95245eaec" />

#### LOG TRANSFORMATION & REGULAR DIFFERENCING:
<img width="1219" height="209" alt="image" src="https://github.com/user-attachments/assets/a2d07bfa-169c-4ec1-af79-8aaa833ac40c" />

#### LOG TRANSFORMATION + REGULAR DIFFERENCING + SEASONAL DIFFERENCING:
<img width="1229" height="212" alt="image" src="https://github.com/user-attachments/assets/d5f0c2fc-dd42-45b0-bd94-27c3689eb9e8" />



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
