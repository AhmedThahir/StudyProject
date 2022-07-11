tags:: [[Python]]

- Use `.values` whenever possible
  collapsed:: true
	- speeds up operations
	- converting `Pandas` series into `numpy` array
- id:: 62cac844-e087-4d20-92b6-9521d2aecfcb
  ```python
  import numpy as np
  ```
- # Find-Replace
  collapsed:: true
	- `if`
	  collapsed:: true
		- id:: 628335df-cf72-43d1-8989-7990834f12b4
		  ```python
		  prediction['Rating'] = np.where(
		    prediction['Rating'].values > 100,
		    100,
		    prediction['Rating'].values
		  )
		  ```
	- `if-else`
	  collapsed:: true
		- ```python
		  prediction['Rating'] = np.where(
		    prediction['Rating'].values > 100,
		    100,
		    0
		  )
		  ```
	- `if-elseif-else`
	  collapsed:: true
		- ```python
		  conditions = [
		    prediction['Rating'].values > 100,
		    prediction['Rating'].values > 50,
		    prediction['Rating'].values > 20
		  ]
		  
		  values = [
		    100,
		    50,
		    20  
		  ]
		  
		  default = 0
		  
		  prediction['Rating'] = np.select(
		    conditions,
		    values
		    default = default
		  )
		  ```
	- nested
	  collapsed:: true
		- ```python
		  conditions = [
		    (prediction['Rating'].values > 100 & prediction['Rating'].values % 2 == 0),
		    (prediction['Rating'].values > 100 & prediction['Rating'].values % 3 == 0),
		    (prediction['Rating'].values > 100 & prediction['Rating'].values % 4 == 0),
		    
		    prediction['Rating'].values > 50,
		    prediction['Rating'].values > 20
		  ]
		  
		  values = [
		    102,
		    103,
		    104,
		    
		    50,
		    20  
		  ]
		  
		  default = 0
		  
		  prediction['Rating'] = np.select(
		    conditions,
		    values
		    default = default
		  )
		  ```
- # Rounding
  collapsed:: true
	- ## Round to Integer
	  collapsed:: true
		- id:: 628335df-fb78-486a-b86e-8fc4ad113cf9
		  ```python
		  np.around(prediction)
		  
		  # instead of
		  # prediction = ( round(element) for element in prediction )
		  ```
	- Round to $n$ places
	  collapsed:: true
		- ```python
		  np.around(prediction, n)
		  ```