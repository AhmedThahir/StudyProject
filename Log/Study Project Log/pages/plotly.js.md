tags:: [[Dashboards]] [[Plotly]]
title:: plotly.js

- # Static
  collapsed:: true
	- ```html
	  <html>
	  
	  <head>
	  	<script src="plotly.min.js"></script>
	  </head>
	  
	  <body>
	  
	  	<div id="myPlot" style="width:100%;max-width:700px"></div>
	  
	  	<script>
	  		var xArray = [50, 60, 70, 80, 90, 100, 110, 120, 130, 140, 150];
	  		var yArray = [7, 8, 8, 9, 9, 9, 10, 11, 14, 14, 15];
	  
	  		// Define Data
	  		var data = [{
	  			x: xArray,
	  			y: yArray,
	  			mode:"scatter"
	  		}];
	  
	  		// Define Layout
	  		var layout = {
	  			xaxis: {
	  				range: [40, 160],
	  				title: "Square Meters"
	  			},
	  			yaxis: {
	  				range: [5, 16],
	  				title: "Price in Millions"
	  			},
	  			title: "House Prices vs. Size"
	  		};
	  
	  		// Display using Plotly
	  		Plotly.newPlot(
	  			"myPlot",
	  			data,
	  			layout
	  		);
	  	</script>
	  
	  </body>
	  
	  </html>
	  ```
- # Real-time
  collapsed:: true
	- ```html
	  <html>
	  
	  <head>
	  	<script src="plotly.min.js"></script>
	  </head>
	  
	  <body>
	  	<div id="chart"></div>
	  	<script>
	  		function getData() {
	  			return Math.random();
	  		}
	  
	  		var data = [{
	  			y: [getData()],
	  			//			mode: "markers"
	  		}];
	  
	  		Plotly.newPlot('chart', data);
	  
	  		var cnt = 0;
	  
	  		setInterval(function () {
	  			Plotly.extendTraces('chart', { y: [[getData()]] }, [0]);
	  			cnt++;
	  			if (cnt > 500) {
	  				Plotly.relayout('chart', {
	  					xaxis: {
	  						range: [cnt - 500, cnt]
	  					}
	  				});
	  			}
	  		}, 15);
	  	</script>
	  </body>
	  
	  </html>
	  ```