# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION
### Date: 11-05-2026


### AIM:
To Illustrates how to perform time series analysis and decomposition on the monthly average temperature of a city/country and for airline passengers.

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the decomposition process for the required data.
4. Plot the data according to need, either seasonal_decomposition or trend plot.
5. Display the overall results.

### PROGRAM:
```
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
import pandas as pd

data = pd.read_csv("C:/Users/admin/OneDrive/Desktop/index_1.csv")

data['datetime'] = pd.to_datetime(
    data['date'] + ' ' + data['datetime'],
    errors='coerce'
)

data = data.dropna(subset=['datetime'])

data = data.set_index('datetime')

data = data.sort_index()

daily_sales = data['money'].resample('D').mean()

daily_sales = daily_sales.dropna()

decomposition = seasonal_decompose(
    daily_sales,
    model='additive',
    period=30
)

plt.figure(figsize=(12, 12))

decomposition.plot()

plt.subplot(411)

plt.plot(daily_sales, label='Daily Coffee Sales')

plt.legend(loc='upper left')

plt.title('Daily Coffee Sales')

plt.subplot(412)

plt.plot(
    decomposition.trend,
    label='Trend',
    color='orange'
)

plt.legend(loc='upper left')

plt.title('Trend Plot')

plt.subplot(413)

plt.plot(
    decomposition.seasonal,
    label='Seasonality',
    color='green'
)

plt.legend(loc='upper left')

plt.title('Seasonality Plot')

plt.subplot(414)

plt.plot(
    decomposition.resid,
    label='Residual',
    color='red'
)

plt.legend(loc='upper left')

plt.title('Residual Plot')

plt.tight_layout()

plt.show()
```



### OUTPUT:
FIRST FIVE ROWS:

<img width="573" height="318" alt="image" src="https://github.com/user-attachments/assets/960fe021-e2eb-46b1-86d3-8a187987e669" />


PLOTTING THE DATA:
<img width="657" height="140" alt="image" src="https://github.com/user-attachments/assets/082cb05b-3dfd-4c5f-a93e-3f46e6d1e528" />


SEASONAL PLOT REPRESENTATION :

<img width="642" height="117" alt="image" src="https://github.com/user-attachments/assets/4eaa1be5-a8e0-4823-83fc-9c05a9951c50" />


TREND PLOT REPRESENTATION :
<img width="659" height="111" alt="image" src="https://github.com/user-attachments/assets/109357ec-bbed-496d-baa1-ad6ed715e99b" />


OVERALL REPRESENTATION:

<img width="672" height="501" alt="image" src="https://github.com/user-attachments/assets/b16a7c79-9f4c-467e-bf3f-7c60a008ef9e" />


### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
