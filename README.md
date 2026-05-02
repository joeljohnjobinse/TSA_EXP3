# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
Date: 02/05/2026

### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("Walmart_sales.csv")

print(df.columns)

data = df['Fuel_Price']

data = data.astype(str)                     
data = data.str.replace(',', '')              
data = data.str.replace('$', '')           
data = pd.to_numeric(data, errors='coerce')
data = data.dropna().values

max_lag = 35
lags = range(max_lag)

mean = np.mean(data)
variance = np.var(data)

normalized_data = data - mean

acf_values = []

for lag in lags:
    numerator = 0
    denominator = 0
    
    for i in range(len(data) - lag):
        numerator += normalized_data[i] * normalized_data[i + lag]
    
    for i in range(len(data)):
        denominator += normalized_data[i] ** 2
    
    acf = numerator / denominator
    acf_values.append(acf)

plt.figure(figsize=(10, 5))
plt.stem(lags, acf_values)
plt.xlabel('Lag')
plt.ylabel('Autocorrelation')
plt.title('ACF of Walmart Sales')
plt.grid(True)
plt.show()
```
### OUTPUT:
<img width="1006" height="612" alt="image" src="https://github.com/user-attachments/assets/fb15b5b2-bbbe-48f8-adcf-fdbe656d8f0e" />

### RESULT:
        Thus we have successfully implemented the auto correlation function in python.
