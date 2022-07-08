tags:: [[Dashboards]], [[Plotly]]
title:: plotly.py

- Tutorials
	- https://youtu.be/hSPmj7mK6ng
	- https://youtu.be/pGMvvq7R1IM
	- https://youtu.be/8d7rArayuzc
	- https://youtu.be/_b2KXL0wHQg
- # Animated
	- ```python
	  px.scatter(data_frame = gapminder, 
	             x = 'gdpPercap',
	             y = 'lifeExp', 
	             size = 'pop', 
	             hover_name = 'country', 
	             color = 'country',
	             animation_frame = 'year',
	             animation_group = 'country',
	             range_x = [0,50000],
	             range_y = [20,90])
	  ```