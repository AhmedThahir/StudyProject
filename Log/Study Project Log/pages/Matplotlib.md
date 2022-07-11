tags:: [[Python]] [[Library]] [[Data Visualization]]

- # Initialization
	- id:: 62c96cea-3de8-4027-b4fe-be20612e3204
	  ```python
	  import matplotlib.pyplot as plt
	  %config InlineBackend.figure_formats = ['svg'] # makes everything svg by default
	  %matplotlib inline
	  ```
	- ```python
	  plt.figure(
	    figsize=(6, 6),
	    dpi=80
	  )
	  ```
- # Example
  collapsed:: true
	- ```python
	  df = df.sort_values(x).reset_index(drop=True)
	  plt.plot(
	    df[x],
	    df[y],
	    'o'
	  )
	  plt.xlabel(x), plt.ylabel(y)
	  
	  #add linear regression line to scatterplot
	  m, b = np.polyfit(df[x], df[y], 1)
	  plt.plot(df[x], m*df[x] + b)
	  
	  plt.show()
	  ```
- # Regression Line
  collapsed:: true
	- ```python
	  m, b = np.polyfit(x, y, 1)
	  plt.plot(x, m*x + b)
	  ```