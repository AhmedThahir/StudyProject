- Package to convert tables from pdf into pandas dataframes
- # Initialization
	- ```python
	  !pip install tabula-py
	  ```
	- ```python
	  import tabula as tb
	  from tabula.io import read_pdf
	  
	  import os
	  
	  import pandas as pd
	  ```
- # Read
	- ```python
	  rel = "data\\"
	  files = os.listdir("./data")
	  ```
	- ```python
	  def read_pdf(file):
	      df = tb.read_pdf(
	          "data/" + file,
	          pages='1',
	          pandas_options={
	              "names": [
	                  "Car",
	                  "City/University",
	                  "Cost",
	                  "BPP",
	                  "Design",
	                  "ACC",
	                  "SkidPad",
	                  "AutoX",
	                  "Endu",
	                  "Effic",
	                  "Penalties",
	                  "Overall Scores",
	                  "Overall Placing"
	              ]
	          }
	      )
	  
	      df[0]["Competition"] = file[:-4]        
	      return df[0]
	  ```
- # Write to CSV
	- ```python
	  df = pd.DataFrame()
	  for file in files:
	      if( ".pdf" == file[-4:] ):
	          df = read_pdf(file)
	          file_name = file[:-4] + ".csv"
	          df.to_csv(
	              os.getcwd() + "\\" + rel + file_name,
	              index = False
	          )
	  ```