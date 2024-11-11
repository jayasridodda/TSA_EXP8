## Name: DODDA JAYASRI
## Reg No: 212222240028
## Date: 

# Ex.No: 08 MOVINTG AVERAGE MODEL AND EXPONENTIAL SMOOTHING

## AIM:

To implement Moving Average Model and Exponential smoothing Using Python on Salesforcehistory

## ALGORITHM:

1. Import necessary libraries
2. Read the electricity time series data from a CSV file,Display the shape and the first 20 rows of
the dataset
3. Set the figure size for plots
4. Suppress warnings
5. Plot the first 50 values of the 'volume' column
6. Perform rolling average transformation with a window size of 5
7. Display the first 10 values of the rolling mean
8. Perform rolling average transformation with a window size of 10
9. Create a new figure for plotting,Plot the original data and fitted value
10. Show the plot
11. Also perform exponential smoothing and plot the graph
    
## PROGRAM:

```
# Import necessary libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import warnings
from statsmodels.tsa.holtwinters import ExponentialSmoothing

# Suppress warnings
warnings.filterwarnings('ignore')

# Read the dataset (adjust the path accordingly)
data = pd.read_csv('/content/Salesforcehistory.csv')

# Convert 'date' to datetime format and set it as the index
data['Date'] = pd.to_datetime(data['Date'], format='%Y-%m-%d')
data.set_index('Date', inplace=True)

# Focus on the 'Adj Close' column
adj_close_data = data[['Open']]

# Display the shape and the first 5 rows of the dataset
print("Shape of the dataset:", adj_close_data.shape)
print("First 5 rows of the dataset:")
print(adj_close_data.head())

# Plot Original Dataset (Adj Close Data)
plt.figure(figsize=(8, 4))
plt.plot(adj_close_data['Open'], label='Original Adj Close Data', color='blue')
plt.title('Original dataset')
plt.xlabel('Date')
plt.ylabel('Open')
plt.legend()
plt.grid()
plt.show()

# Moving Average
# Perform rolling average transformation with a window size of 10
rolling_mean_10 = adj_close_data['Open'].rolling(window=10).mean()

# Plot Moving Average
plt.figure(figsize=(8, 4))
plt.plot(adj_close_data['Open'], label='Original Adj Close Data', color='blue')
plt.plot(rolling_mean_10, label='Moving Average (window=10)', color='orange')
plt.title('Moving Average')
plt.xlabel('Date')
plt.ylabel('Open')
plt.legend()
plt.grid()
plt.show()

# Exponential Smoothing
model = ExponentialSmoothing(adj_close_data['Open'], trend='add', seasonal=None)
model_fit = model.fit()

# Make predictions for the next 30 periods (you can adjust this)
predictions = model_fit.predict(start=len(adj_close_data), end=len(adj_close_data) + 30)

# Plot the original data and Exponential Smoothing predictions
plt.figure(figsize=(8, 4))
plt.plot(adj_close_data['Open'], label='Original Adj Close Data', color='blue')
plt.plot(predictions, label='Exponential Smoothing', color='orange')
plt.title('Exponential Smoothing')
plt.xlabel('Date')
plt.ylabel('Open')
plt.legend()
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()
```

## OUTPUT:

Given dataset

![image](https://github.com/user-attachments/assets/5ea0f326-8163-4aab-a880-238fdbc2bffa)


Original dataset

![image](https://github.com/user-attachments/assets/7652803c-9db3-447f-a68b-933e8542fe81)


Moving Average

![image](https://github.com/user-attachments/assets/8601fda3-8497-4a24-8dbb-463f7a069c97)


Exponential Smoothing

![image](https://github.com/user-attachments/assets/8ecadf5d-d4ac-4988-9e97-0b1ed535077a)



## RESULT:
Thus we have successfully implemented the Moving Average Model and Exponential smoothing using python.
