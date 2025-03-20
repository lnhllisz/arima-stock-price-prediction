# arima-stock-price-prediction
**Data Preparation**

The dataset collected consists of six different Vietnamese stocks: ANV, DAT, HAH, KDC, NAF, and PVT. The selected features used for training the model include:
- Technical indicators: 200-day SMA, RSI, stochastic oscillators.
- Macroeconomic factors: GDP, interest rates.
- Target variable: Closing price of each stock.

Data preparation is of paramount importance in financial time-series forecasting since this is the phase when the dataset is properly formatted, clean, and optimized for deep learning models. The process begins with loading the dataset, where financial data is imported as a Pandas DataFrame. The 'Date' column is parsed as a datetime index which allows the model to recognize the sequential nature of the data. This is crucial for time-series forecasting.

The next step is when the dataset undergoes missing value handling to ensure data integrity. Financial datasets often contain missing values due to market holidays, reporting delays, or data collection issues. These gaps can distort predictions if not addressed properly. To handle missing values, there are some common techniques, namely forward-filling (using the last available data point), interpolation (estimating values based on surrounding data), or removing rows with excessive gaps. Identifying and addressing anomalies, such as extreme outliers caused by errors or market shocks, is also important to prevent the model from learning misleading patterns from data that do not conform to the usually expected behaviour. As a result, we align the macroeconomic data on a daily frequency as stock prices are believed to be available daily whilst GDP and interest rate data are reported less frequently.

In the preprocessing step, the stock price data is re-ordered chronologically and filtered to the period from January 22, 2020, to January 14, 2025. Our inputs including technical and macroeconomic indicators are also processed. Technical indicators (SMA200, RSI, Stochastic Oscillator) are computed from the daily stock data. GDP data (with quarters formatted as “Q1 2020”, etc.) is converted by replacing the quarter identifier with a representative month–day (e.g., “Q1” → “-01-01”) and then merged with the daily stock data using forward-fill. Similarly, the monthly interest rate data is merged with the stock data by forward-filling the latest available value.

**Model Configuration**

The ARIMAX model is configured using an optimal (p, d, q) structure, selected through autoarima based on the AIC supported in the Python library. Instead of manually testing different combinations of parameters, autoarima automates this process by evaluating multiple models and selecting the one that minimizes the AIC, which enables us to keep a balance between model sophistication and forecasting accuracy.

**Data Processing**

Firstly, the dataset is splitted 80:20, with 80 percent of the data used for training while the rest is for testing. This process is called splitting the dataset. There are cases that the dataset is divided with different proportions, however; this separation is highly recommended due to its accuracy and reliability.

Secondly, when it comes to model training, the ARIMAX model is fitted to the training set using the closing price as the dependent variable, which, accordingly, creates the trained model to generate predictions for the test set based on past data.

The actual and predicted closing prices are then plotted to analyze performance trends. At the same time, the three evaluation metrics, namely, RMSE, MSE, and Accuracy are computed for us to quantify the forecast accuracy to assess the model’s performance.
