tags:: [[Time Series]]
company:: Facebook

- > Prophet is a procedure for forecasting time series data based on an additive model where non-linear trends are fit with yearly, weekly, and daily seasonality, plus holiday effects. It works best with time series that have strong seasonal effects and several seasons of historical data. Prophet is robust to missing data and shifts in the trend, and typically handles outliers well.
- [Good Tutorial](https://youtu.be/KvLG1uTC-KU)
- # Step 0 - Import Packages
	- ```python
	  # Install pystan with pip before using pip to install prophet
	  # pystan>=3.0 is currently not supported
	  pip install pystan==2.19.1.1
	  pip install prophet
	  
	  import pandas as pd
	  from prophet import Prophet
	  ```
- # Step 1 - Import Data
	- ```python
	  df = pd.read_csv('dataset.csv')
	  
	  df['Year'] = df['Time Date'].apply(lambda x: str(x)[-4:])
	  df['Month'] = df['Time Date'].apply(lambda x: str(x)[-6:-4])
	  df['Day'] = df['Time Date'].apply(lambda x: str(x)[:-6])
	  df['ds'] = pd.DatetimeIndex(df['Year']+'-'+df['Month']+'-'+df['Day'])
	  
	  df = df.loc[(df['Product']==2667437) & (df['Store']=='QLD_CW_ST0203')]
	  df.drop(['Time Date', 'Product', 'Store', 'Year', 'Month', 'Day'], axis=1, inplace=True)
	  df.columns = ['y', 'ds']
	  
	  df.head()
	  ```
- # Step 2 - Train Model
	- ```python
	  m = Prophet(interval_width=0.95, daily_seasonality=True)
	  model = m.fit(df)
	  ```
- # Step 3 - Forecast
	- ```python
	  future = m.make_future_dataframe(periods=100,freq='D')
	  forecast = m.predict(future)
	  
	  forecast.head()
	  ```
	- ```python
	  plot1 = m.plot(forecast)
	  plt2 = m.plot_components(forecast)
	  ```
	-