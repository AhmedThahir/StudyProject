tags:: [[Python]] [[Library]] [[Plotly]]

- Research Paper
	- ![Plotly-Resampler_Effective Visual Analytics for Large Time Series.pdf](../assets/Plotly-Resampler_Effective_Visual_Analytics_for_Large_Time_Series_1657463840000_0.pdf)
- `pip install plotly-resampler`
- Individual figure
	- ```python
	  from plotly_resampler import FigureResampler
	  
	  fig = FigureResampler(px.scatter()) #putting empty constructor is the fastest
	  fig.update_layout(title="Testing", xaxis_title='Year', yaxis_title='Dollars USD')
	  
	  fig.add_trace(
	      px.scatter(x=x, y=noisy_sin, render_mode="webgl")
	      .data[0]
	  )
	  ```
	- ```python
	  fig.show() # doesn't resample when zooming in
	  fig.show_dash(mode="inline") # requires server
	  ```
	- #+BEGIN_WARNING
	  Output will be missing in exported HTML when using `FigureWidgetResampler`
	  #+END_WARNING
- All figures
  collapsed:: true
	- collapsed:: true
	  ```python
	  from plotly_resampler import register_plotly_resampler
	  
	  register_plotly_resampler(mode='auto')
	  ```
	- #+BEGIN_NOTE
	  This wraps all plotly graph object figures with a FigureResampler | FigureWidgetResampler. This can thus also be used for the plotly.express interface.
	  #+END_NOTE