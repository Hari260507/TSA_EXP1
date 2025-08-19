# Ex.No: 01A PLOT A TIME SERIES DATA
###  Date: 19/08/2025

# AIM:
To Develop a python program to Plot a time series data (population/ market price of a commodity
/temperature.
# ALGORITHM:
1. Import the required packages like pandas and matplot
2. Read the dataset using the pandas
3. Calculate the mean for the respective column.
4. Plot the data according to need and can be altered monthly, or yearly.
5. Display the graph.
# PROGRAM:
 ```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Load dataset
data = pd.read_csv("/content/Tomato.csv")

# Convert Date column to datetime
data['Date'] = pd.to_datetime(data['Date'])

# Set Date as index
data.set_index('Date', inplace=True)

# Use Average price as the main series
data['price'] = data['Average']

# Regular Differencing
data['price_diff'] = data['price'] - data['price'].shift(1)

# Seasonal Decomposition (additive model, monthly seasonality)
result = seasonal_decompose(data['price'], model='additive', period=30)
data['price_seasonal_diff'] = result.resid

# Log Transformation
data['price_log'] = np.log(data['price'])
data['price_log_diff'] = data['price_log'] - data['price_log'].shift(1)

# Seasonal Decomposition on log-differenced series
result_log = seasonal_decompose(data['price_log_diff'].dropna(), model='additive', period=30)
data['price_log_seasonal_diff'] = result_log.resid

# Plotting
plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data['price'], label='Original')
plt.legend(loc='best')
plt.title('Original Tomato Price (Average)')
plt.xlabel('Date')
plt.ylabel('Price')

plt.subplot(6, 1, 2)
plt.plot(data['price_diff'], label='Regular Differencing')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Date')
plt.ylabel('Differenced Price')

plt.subplot(6, 1, 3)
plt.plot(data['price_seasonal_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Date')
plt.ylabel('Seasonally Adjusted Price')

plt.subplot(6, 1, 4)
plt.plot(data['price_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Date')
plt.ylabel('Log Price')

plt.subplot(6, 1, 5)
plt.plot(data['price_log_diff'], label='Log Transformation + Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation + Regular Differencing')
plt.xlabel('Date')
plt.ylabel('Diff(Log Price)')

plt.subplot(6, 1, 6)
plt.plot(data['price_log_seasonal_diff'], label='Log Transformation + Differencing + Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Log Transformation + Regular Differencing + Seasonal Adjustment')
plt.xlabel('Date')
plt.ylabel('Sdiff(RDiff(Log Price)))')

plt.tight_layout()
plt.show()
 ```










# OUTPUT:

<img width="1904" height="315" alt="image" src="https://github.com/user-attachments/assets/e58ec23e-ee09-4f17-949a-4b2f49f477d3" />
<img width="1686" height="281" alt="image" src="https://github.com/user-attachments/assets/9beaf2e5-7105-448c-9444-5bcfc54f0099" />
<img width="1675" height="271" alt="image" src="https://github.com/user-attachments/assets/c25a784d-2075-4584-85fa-b85c54b40fe6" />
<img width="1673" height="268" alt="image" src="https://github.com/user-attachments/assets/52f6a7cc-a7b3-42b6-a616-b5d405ad7de1" />
<img width="1678" height="275" alt="image" src="https://github.com/user-attachments/assets/1717cb8d-0d51-47fe-906d-121d04562ca1" />
<img width="1684" height="257" alt="image" src="https://github.com/user-attachments/assets/d68fc9aa-3871-4614-a130-f5de86798061" />



# RESULT:
Thus we have created the python code for plotting the time series of given data.
