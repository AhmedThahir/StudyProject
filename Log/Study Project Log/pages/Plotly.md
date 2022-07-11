tags:: [[Dashboards]] [[Python]] [[Library]] [[Data Visualization]]

# Importing
collapsed:: true
	- ```python
	  import plotly.express as px
	  
	  import plotly.io as pio
	  pio.templates.default = "ggplot2"
	  ```
# Plots
collapsed:: true
	- ```python
	  px.scatter()
	  px.line()
	  px.imshow(df, text_auto=True) # heatmap with value
	  ```
# Useful Configuration
collapsed:: true
	- Only 2 series as colored
	  collapsed:: true
		- ```python
		  fig.update_traces({"line":{"color":"lightgrey"}})
		  
		  fig.update_traces(patch={"line":{"color":"blue", "width":5}}, 
		                    selector={"legendgroup":"Turkey"})
		  fig.update_traces(patch={"line":{"color":"red", "width":5}}, 
		                    selector={"legendgroup":"Japan"})
		  ```
		- ```python
		  sorted_df = long_df.copy()
		  # map the value order
		  sorted_df["order"] = sorted_df["Country Name"].map({"Japan": 1, "Turkey": 2}).fillna(3)
		  # sort by this order
		  sorted_df.sort_values(by=["order","years"], ascending=False, inplace=True)
		  
		  # The line which comes the latest, is drawn on the top.
		  ```
	- ```python
	  fig.update_layout(
	      legend=dict(
	          # Adjust click behavior
	          itemclick="toggleothers",
	          itemdoubleclick="toggle",
	      )
	  )
	  
	  fig.show(config={"displayModeBar": False, "showTips": False})
	  ```
	- Grey out unselected
	  collapsed:: true
		- ```python
		  scatter = px.scatter_matrix(df)
		  scatter.data[0].update(selected=dict(marker=dict(color='red')),
		                         unselected=dict(marker=dict(color='blue',
		                                                     opacity=0.001)))
		  ```
# Animated
collapsed:: true
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
- # Performance
  collapsed:: true
	- ## Lazy Plot
	  collapsed:: true
		- ```python
		  # initialize empty plots, then just fill in data in the update function
		  fig = px.scatter()
		  fig.add_trace(
		    px.scatter()
		    .data[0]
		  )
		  fig.add_trace(
		    px.line()
		    .data[0]
		  )
		  ```
	- ## Webgl renderer
	  collapsed:: true
		- ```python
		  px.scatter(df, x="x", y="y", render_mode='webgl')
		  px.scatter_polar(df, x="x", y="y", render_mode='webgl')
		  
		  px.line(df, x="x", y="y", render_mode='webgl')
		  px.line_polar(df, x="x", y="y", render_mode='webgl')
		  
		  # heatmapgl
		  ```
	- ## [[Plotly Resampler]]
	- ## [[Datashader]]
	- ## Specify range
	  collapsed:: true
		- Letting plotly autorange means it needs to do relayouts often and requires it to calculate the range each time.
		- ```python
		  fig = px.scatter(df, x="x", y="y", range_x=[2, 3], range_y=[10, 20])
		  ```
	- ## Caching
	  collapsed:: true
		- This example is for streamlit(Dash alternative). Try to use the concept and update this note
		- ```python
		  # caching all the figures objects themselves in a dict or list:
		  
		  @st.cache(hash_funcs={dict: lambda _: None}) # hash_funcs because dict can't be hashed
		  def get_dic_of_fig():
		      dico_of_fig = {}
		      for param in list_of_params: 
		          plotly_fig = plot_plotly_fig(param)
		          dico_of_fig [param] = plotly_fig 
		      return dico_of_fig 
		  
		  dico_of_fig = get_dic_of_fig() # this dic is cached
		  
		  # for plotting
		  st.plotly_chart(dico[param_chosen])
		  ```
	- ## use Plotly.react instead of Plotly.newPlot (only for [[plotly.js]])
- # Tutorials
  collapsed:: true
	- https://youtu.be/hSPmj7mK6ng
	- https://youtu.be/pGMvvq7R1IM
	- https://youtu.be/8d7rArayuzc
	- https://youtu.be/_b2KXL0wHQg