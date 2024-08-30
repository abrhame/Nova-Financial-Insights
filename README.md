# Financial Data Analysis

This repository contains a comprehensive analysis of financial news and stock price data, focusing on Apple Inc. (AAPL). The project explores correlations between news sentiment and stock market movements, applies technical indicators to stock data, and includes seasonal decomposition of news headline lengths.

## Table of Contents

- [Executive Summary](#executive-summary)
- [Introduction](#introduction)
- [Problem Definition](#problem-definition)
- [Project Challenges](#project-challenges)
- [Project Limitations](#project-limitations)
- [Data Collection Overview](#data-collection-overview)
- [Seasonal Decomposition of Headline Length](#seasonal-decomposition-of-headline-length)
- [Technical Indicators and Stock Performance Analysis](#technical-indicators-and-stock-performance-analysis)
- [Cumulative Returns Analysis](#cumulative-returns-analysis)
- [Conclusion](#conclusion)
- [Key Achievements](#key-achievements)
- [Future Directions](#future-directions)
- [How to Use](#how-to-use)
- [Requirements](#requirements)

## Executive Summary

This report analyzes financial news and stock data to uncover correlations between news sentiment and stock movements. It utilizes technical indicators and seasonal decomposition to provide insights into trends and patterns in the data.

## Introduction

The analysis focuses on Apple Inc. (AAPL) stock, examining the relationship between news headlines and stock prices. Key analyses include seasonal decomposition of headline lengths and calculation of technical indicators like SMA, RSI, and MACD.

## Problem Definition

The main objectives are:
1. Analyze seasonality and trends in financial news headline lengths.
2. Compute and visualize key financial indicators for AAPL stock.
3. Assess the impact of daily and cumulative returns on stock performance.

## Project Challenges

- **Data Quality:** Managing missing values and ensuring data integrity.
- **Complexity:** Integrating diverse datasets.
- **Time Constraints:** Limited time for developing comprehensive models.
- **Visualization:** Presenting complex financial analyses effectively.

## Project Limitations

- **Incomplete Data:** Potential missing records affecting accuracy.
- **Limited Context:** Lack of contextual data for news articles.
- **Data Integration:** Challenges in harmonizing data from different sources.

## Data Collection Overview

Data includes:
- **Financial News Dataset:** Headlines, publication dates, stock symbols, etc.
- **AAPL Stock Data:** Historical stock prices (Open, High, Low, Close, Volume).

## Seasonal Decomposition of Headline Length

Seasonal decomposition of news headline lengths identifies observed, trend, seasonal, and residual components. The analysis is performed using the `seasonal_decompose` function.

```python
from statsmodels.tsa.seasonal import seasonal_decompose
import matplotlib.pyplot as plt

# Perform seasonal decomposition
decomposition = seasonal_decompose(data['headline_length'], model='additive', period=4)

# Plot the decomposition
decomposition.plot()
plt.show()
```

## Technical Indicators and Stock Performance Analysis

Technical indicators for AAPL stock include SMA, RSI, MACD, Daily Returns, and Cumulative Returns. Analysis code:

```python
import pandas as pd
import yfinance as yf
import talib as ta
import plotly.express as px

# Load stock data
ticker = 'AAPL'
start_date = '2010-01-01'
end_date = '2020-01-01'
data = yf.download(ticker, start=start_date, end=end_date)

# Calculate SMA, RSI, MACD
data['SMA_20'] = ta.SMA(data['Close'], timeperiod=20)
data['RSI_14'] = ta.RSI(data['Close'], timeperiod=14)
data['MACD'], data['MACD_Signal'], data['MACD_Hist'] = ta.MACD(data['Close'])

# Calculate Daily and Cumulative Returns
data['Daily_Return'] = data['Close'].pct_change()
data['Cumulative_Return'] = (1 + data['Daily_Return']).cumprod() - 1
```

## Cumulative Returns Analysis

Cumulative returns for AAPL are visualized to show overall investment growth over the period.

```python
# Plotting Cumulative Returns
fig = px.line(data, x=data.index, y='Cumulative_Return', title='AAPL Cumulative Returns')
fig.show()
```

## Conclusion

The analysis provides valuable insights into trends in financial news and stock performance. Seasonal decomposition and technical indicators offer a comprehensive view of AAPL stock's behavior over time.

## Key Achievements

- Decomposed and analyzed headline length data.
- Computed and visualized key financial indicators for AAPL stock.
- Analyzed cumulative returns.

## Future Directions

- **Enhanced Analysis:** Develop complex models for predicting stock movements based on news sentiment.
- **Data Expansion:** Include additional stocks and time periods.
- **Advanced Visualization:** Create interactive dashboards for dynamic data exploration.

## How to Use

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/abrhame/Nova-Financial-Insights.git
   cd Nova-Financial-Insights
   ```

2. **Install Dependencies:**
   Make sure you have Python 3.x installed. Use `pip` to install the required packages.
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the Analysis:**
   Execute the Jupyter Notebook
   

4. **View Results:**
   Check the generated plots and reports in the specified output directory.

## Requirements

- Python 3.x
- `pandas`
- `yfinance`
- `ta-lib`
- `statsmodels`
- `matplotlib`
- `plotly`

Create a `requirements.txt` file with the following content:

```
pandas
yfinance
ta-lib
statsmodels
matplotlib
plotly
```


