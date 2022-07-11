tags:: [[Plotly]] [[Dashboards]] [[Python]] [[Library]]

- # Lazy Load Components
	- ## idk
		- ```python
		  @app.callback(Output('graph 1', 'figure'),
		                Input('my_Tabs', 'value'),
		                prevent_initial_call=True
		               )
		  ```
	- ## Lazy Load Plugin
		- `pip install dash-lazy-load`
		- To get simple lazy loading set up, the only change necessary is to wrap a Dash components with `dash_lazy_load.LazyLoad`
		- ```python
		  import dash_lazy_load
		  import dash
		  import dash_html_components as html
		  
		  app = dash.Dash('')
		  app.scripts.config.serve_locally = True
		  app.layout = html.Div([
		      html.Div('Testing', style=dict(height=1200)),
		      dash_lazy_load.LazyLoad(
		          html.Div('I loaded in lazily!!', style=dict(border='5px solid blue')),
		          height=500,
		          debounce=1000)
		  ])
		  
		  if __name__ == '__main__':
		  app.run_server(debug=True)
		  ```
- # Deployment
  collapsed:: true
	- {{video https://youtu.be/Gv910_b5ID0}}