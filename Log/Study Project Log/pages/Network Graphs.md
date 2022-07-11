tags:: [[Python]] [[Library]] [[Networks]]

- # Purpose
	- Helps visualize networks (obviously)
- # Visualization
	- ```python
	  import networkx as nx
	  import numpy as np
	  
	  import matplotlib.pyplot as plt
	  %config InlineBackend.figure_formats = ['svg'] # makes everything svg by default
	  %matplotlib inline
	  ```
	- ## Graph Generation
		- ```python
		  def subgraph(n):
		      vertices = np.arange(1, n+1)
		  
		      edges = []
		      for i in range(1, n+1):
		          for j in range(i+1, n+1):
		              if(i != j):
		                  edges.append(
		                      (i, j)
		                  )
		      no_of_edges = len(edges)
		                  
		      graph = nx.Graph()
		      graph.add_nodes_from(vertices)
		      graph.add_edges_from(edges)
		      
		      plt.figure(
		        figsize=(0.5+n/4, 0.5+n/4),
		        dpi=80
		      )
		      
		      if(n<=12):
		          node_color = "tab:blue"
		          edge_color = "lightblue"
		      else:
		          node_color = "darkred"
		          edge_color = "lightpink"
		      
		      nx.draw(
		          graph,
		          
		          node_size = 30,
		          node_color = node_color,
		          
		          width = 0.75,
		          edge_color = edge_color
		      )
		      
		      title = "Team of " + str(n) + " members"
		      if(n==1):
		          title = title[:-1]
		      title += " - " + str(no_of_edges) + " interactions"
		      if(no_of_edges==1):
		          title = title[:-1]
		      
		      plt.title(title)
		      plt.show()
		  ```
		- ```python
		  def create_graph(n, divisions=1):
		      division_size = int(n/divisions)
		  
		      if(divisions != 1):       
		          interactions_per_team = int(division_size*(division_size - 1)/2)
		          total_interactions = interactions_per_team * divisions
		              
		          message = (
		              "Team of " + str(n) +
		              " divided into " + str(divisions) + " divisions " +
		              "with " + str(division_size) + " members each" +
		              "\n\n" + 
		              "Total interactions = " + str(total_interactions) + "\n" +
		              "Interactions per team = " + str(interactions_per_team) +
		              "\n\n" +
		              "Each team will look like this"
		          )
		          print(message)
		          
		      subgraph(division_size)
		  ```
		- ```python
		  # def customized_graph(graph):
		  #     pos = nx.spring_layout(graph)
		  #     nx.draw_networkx_nodes(
		  #         graph,
		  #         pos = pos,
		  #         nodelist=vertices
		  #     )
		  #     nx.draw_networkx_edges(
		  #         graph,
		  #         pos = pos,
		  #         edgelist=edges,
		  #         alpha = 0.5
		  #     )
		  #     return graph
		  ```
	- ## Calling
		- ```python
		  sizes = [1, 2, 3, 6, 12, 15]
		  for i in sizes:
		      create_graph(i)
		  ```
		- ```python
		  total = 100
		  divisions = [5, 20]
		  
		  for i in divisions:
		      create_graph(total, i)
		  ```