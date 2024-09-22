## Developed by: Pravin Raj A
## Register number: 212222240079
## Date:

# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)

 ### AIM:
To Compute the AutoCorrelation Function (ACF) of the vegetable price data for the first 35 lags to determine the model
type to fit the data.

### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Define a function to Compute Autocorrelation Function(ACF)
4. Implement the correlation using necessary logic and obtain the results
5. Store the results in an array
6. Represent the result in graphical representation as given below.

### PROGRAM:
```py
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

# Load the BitCoin price data
file_path = '/content/BTC-USD(1).csv'  # Ensure this is the correct path to your CSV file
Bitcoin_Price = pd.read_csv(file_path,nrows=50)

# Print the available columns to check for the correct name
print(Bitcoin_Price.columns)

# Extract the price data column (replace 'Close' with the actual column name from the output above)
price_data = Bitcoin_Price['Close'].values

# Calculate mean and variance
mean_price = np.mean(price_data)
var_price = np.var(price_data)

# Normalize the data (subtract mean and divide by standard deviation)
normalized_price = (price_data - mean_price) / np.sqrt(var_price)

# Compute the ACF for the first 35 lags
def compute_acf(data, max_lag):
    acf_values = []
    n = len(data)
    for lag in range(max_lag + 1):
        if lag == 0:
            acf_values.append(1)  # ACF at lag 0 is always 1
        else:
            acf = np.corrcoef(data[:-lag], data[lag:])[0, 1]
            acf_values.append(acf)
    return acf_values

lags = range(35)
acf_values = compute_acf(normalized_price, 34)

# Plot the ACF results
plt.figure(figsize=(10, 6))
plt.stem(lags, acf_values, use_line_collection=True)
plt.title('Autocorrelation Function (ACF) for Bitcoin Price')
plt.xlabel('Lag')
plt.ylabel('ACF')
plt.grid(True)
plt.show()
```

### OUTPUT:

![Screenshot 2024-09-22 125842](https://github.com/user-attachments/assets/8354b6e7-8246-4280-9b46-a3d345f78070)


### RESULT:
Thus the python code for implementing the auto correlation function is executed successfully.
