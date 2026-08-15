# Natural Gas Price Forecasting

An exploratory time-series model for estimating historical and near-term natural gas prices from a short series of monthly observations.

> J.P. Morgan Chase Forage Quantitative Research Job Simulation <br>
> Date: 09/2024

## Project overview

The exercise considers a simplified problem faced by a commodities desk: given monthly natural gas prices, estimate the price on a requested historical date and extrapolate prices over the following year.

The supplied dataset contains 48 month-end observations from October 2020 to September 2024. The notebook explores the series, checks stationarity and fits a seasonal ARIMA model before interpolating its monthly estimates to daily dates.

## Objectives

The task had four main aims:

- inspect the historical series and identify its broad trend and seasonal behaviour;
- estimate prices between the supplied month-end observations;
- forecast prices for the following 12 months; and
- provide a function that accepts a date and returns an estimated price where possible.

## Data and exploratory analysis

`Nat Gas.csv` contains two columns: `Dates` and `Prices`. The dates are parsed as a monthly time index and the prices are plotted to inspect the changing level and recurring annual pattern.

The notebook uses the Augmented Dickey-Fuller test to check stationarity. The original price series returns a p-value of approximately `0.973`, giving no evidence of stationarity. After first differencing, the p-value falls to approximately `1.75e-09`. This motivates setting the non-seasonal differencing order to $d=1$.

The autocorrelation and partial-autocorrelation plots of the differenced series are then used as a simple guide for the autoregressive and moving-average terms.

## Modelling approach

The notebook:

1. fits a SARIMAX model with order `(1, 1, 1)`;
2. uses seasonal order `(1, 1, 1, 12)` to represent the annual pattern in monthly data;
3. forecasts the next 12 monthly observations;
4. extracts confidence intervals for the forecast;
5. constructs a dated forecast series; and
6. interpolates month-end values to provide estimates on dates between observations.

### Date-specific price estimation

`estimate_price(date)` converts the requested date to a pandas timestamp and handles three cases:

- **Within the observed period:** the monthly series is converted to daily frequency and linearly interpolated.
- **Before October 2020:** the observed series is reversed and a second SARIMAX model is used to generate a backcast.
- **After September 2024:** the function returns an interpolated value when the date falls inside the 12-month forecast window. Dates beyond that window return no estimate.

In the saved notebook run, the function returns example estimates of `10.12` for 15 August 2020 and `12.21` for 1 August 2025. These values demonstrate the function rather than serving as externally validated price forecasts.

## Visual outputs

The notebook produces:

- a plot of the original monthly price series;
- ACF and PACF plots after differencing; and
- a historical-versus-forecast chart with a shaded confidence interval.

## Tools used

- pandas and NumPy for data handling;
- Matplotlib for visualisation; and
- statsmodels for the ADF test, diagnostic plots and SARIMAX model.

## Repository contents

```text
.
├── Nat Gas.csv    # Monthly prices supplied with the simulation
├── task1.ipynb    # Analysis, model fitting and price-estimation function
└── README.md
```

## Scope and limitations

This is a compact exercise built from only four years of monthly data. The SARIMAX specification is selected from basic diagnostics rather than a systematic model search, and the notebook does not include rolling backtests or out-of-sample error metrics. Daily values between month-end observations are interpolations, not observed daily market prices. The output should therefore be treated as a demonstration of time-series modelling rather than a trading or valuation model.
