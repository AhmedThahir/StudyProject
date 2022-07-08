alias:: Graphs

- # Pie Chart
	- ||Good|Bad|
	  |--|--|--|
	  |Showing|only single category relative to the whole|multiple categorical data|
	  |Example|![good_pie_chart.png](../assets/good_pie_chart_1656753857286_0.png)|![bad_pie_chart.png](../assets/bad_pie_chart_1656753847796_0.png)|
	  |Solution||![bar_chart_instead_of_pie_chart.png](../assets/bar_chart_instead_of_pie_chart_1656754108008_0.png) <br />Use **sorted** bar chart instead|
	- Try to avoid, but if you have to use
		- Make sure sum(categories)=100
		- Categories should be sorted
		- Concise labels
		- $\le 5$ categories
			- If there are more, make it 'others'
		- Do not compare pie-charts side by side