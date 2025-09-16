# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
Date: 16/09/2025

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
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("GoldPrice(2013-2023).csv")

df["Price"] = df["Price"].str.replace(",", "").astype(float)
df["Date"] = pd.to_datetime(df["Date"])
df = df.sort_values("Date")
data = df["Price"].values
N = len(data)

lags = range(35)
autocorr_values = []

mean_data = np.mean(data)
variance_data = np.var(data)

for lag in lags:
    if lag == 0:
        autocorr_values.append(1)
    else:
        auto_cov = np.sum((data[:-lag] - mean_data) * (data[lag:] - mean_data)) / N
        autocorr_values.append(auto_cov / variance_data)

autocorr_values = np.array(autocorr_values)

markerline, stemlines, baseline = plt.stem(lags, autocorr_values)
plt.setp(markerline, 'markerfacecolor', 'blue')
plt.setp(stemlines, 'color', 'blue')
plt.setp(baseline, 'color', 'black')

plt.title("Autocorrelation of Gold Price (First 35 Lags)")
plt.xlabel("Lag")
plt.ylabel("Autocorrelation")
plt.grid(True)
plt.show()
```

### OUTPUT:
<img width="711" height="564" alt="image" src="https://github.com/user-attachments/assets/5bda89ef-0b60-4ad6-9cd9-956e78ab29ca" />


### RESULT:
Thus we have successfully implemented the auto correlation function in python.
