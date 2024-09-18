# GasPriceForecasting

09/2024<br>
JPMorgan Chase Forage Quantitative Research

# The Task

The objective of this project is to analyze historical natural gas price data and build a forecasting model. The focus is on estimating natural gas prices for both past and future dates, helping a commodity trading desk price long-term storage contracts.

The project uses time series forecasting techniques, specifically the ARIMA model, to predict future prices and estimate past prices based on the historical data provided.

### Data

The dataset consists of monthly natural gas prices from October 2020 to September 2024, stored in a CSV file. Each data point corresponds to the market price of natural gas at the end of each month.

### Project Goals

- **Analyze historical data** to estimate past prices.
- **Build a forecasting model** to predict prices for the upcoming year.
- **Visualize the data** to identify patterns and forecast results.
- **Allow date-specific price estimates**, returning an estimated price for any input date.

### Steps Involved

1. **Data Preprocessing**: Clean and prepare the data for time series analysis.
2. **Model Selection**: Apply ARIMA for seasonal trend and pattern detection.
3. **Forecasting**: Predict prices for the upcoming year.
4. **Price Estimation**: Estimate historical and future prices for specific dates.

# The Code

Key components of the code include:

- `estimate_price(date)`: Returns the estimated price for a given past or future date.
- Time series forecasting model implementation using the ARIMA model from the `statsmodels` library.
- Visualization of historical and forecasted prices, with confidence intervals to show prediction accuracy.


