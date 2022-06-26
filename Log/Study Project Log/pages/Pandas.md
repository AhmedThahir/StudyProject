tags:: [[Python]] [[Exploratory Data Analysis]]

- Try using [[numpy]] for operations whenever possible
- # Importing
  collapsed:: true
	- ```python
	  import pandas as pd
	  ```
- # Creating Dataframe
  collapsed:: true
	- ## Dataset
	  collapsed:: true
		- ```python
		  df = pd.read_csv("dataset.csv")
		  ```
	- ## Manual
	  collapsed:: true
		- ```python
		  perf = pd.DataFrame(
		      columns = ['Season', 'Appearances', 'Goals', 'Assists'],
		      data = [
		          ["2021/2022", 39, 24, 3],
		          ["2020/2021", 44, 36, 4],
		          ["2019/2020", 46, 37, 7]
		      ]
		  )
		  ```
- # Editing Values
  collapsed:: true
	- ```python
	  prediction[['Rating', 'Value']] = prediction[['Rating', 'Value']].values * 100
	  ```
	- ((628335df-cf72-43d1-8989-7990834f12b4))
- # Read/Write
  collapsed:: true
	- Single File
	  collapsed:: true
		- ```python
		  dataset = pd.read_csv(file)
		  ```
		- ```python
		  file_name = file[:-4] + ".csv"
		  df.to_csv(
		    os.getcwd() + "\\" + rel + file_name,
		    index = False
		  )
		  ```
	- ## Multiple Files
	  collapsed:: true
		- ```python
		  raw_formula_student = pd.DataFrame()
		  for file in files:
		      if( ".csv" == file[-4:] ):
		          raw_formula_student = pd.concat(
		              [raw_formula_student, read_file(file)]
		          )
		  ```
- # Useful Functions
  collapsed:: true
	- ```python
	  df.head()
	  df.tail()
	  
	  df.describe()
	  df = df.dropna()
	  ```
	- alias:: re-index reindex
	  ```python
	  df = df.set_index(
	      "Season",
	      "Player Name"
	  )
	  ```
	- ```python
	  df.unique()
	  df.value_counts()
	  100 * df['col'].value_counts() / df['col'].shape[0]
	  ```
	- ```python
	  df['Age'].avg()
	  ```
	- | Function | Function Application |
	  |---|---|
	  | `pipe()` | Table-wise |
	  | `apply()` | Row/column-wise |
	  | `applymap()` | Element-wise |
	- ```python
	  df.iloc[:, 2:11] = (
	          df.iloc[:, 2:11]
	          .apply(lambda x: x.str.replace(',', '.'))
	          .values.astype(float)
	          )
	  ```
	- ## View null values
	  collapsed:: true
		- ```python
		  formula_student[
		      formula_student.isna().any(axis=1)
		  ]
		  ```
- # Correlation
  collapsed:: true
	- ## Correlation Matrix
	  collapsed:: true
		- ```python
		  (
		    formula_student
		    [['Cost', 'Design', 'Overall Scores']]
		    .corr()
		  )
		  ```
	- ## Correlation Ranking
	  collapsed:: true
		- ```python
		  (
		      formula_student
		      .iloc[:, 1:11]
		      .corr("Overall Scores")
		      .sort_values("Correlation", ascending=False)
		      .iloc[1:, :] # remove the obvious overall scores = 1.00
		  )
		  ```
		- ```python
		  # this is unnecessarily complicated way i used before
		  (
		      formula_student
		      .iloc[:, 1:11]
		      .corr()
		      .rename(columns={"Overall Scores":"Correlation"})
		      [["Correlation"]]
		      .sort_values("Correlation", ascending=False)
		      .iloc[1:, :] # remove the obvious overall scores = 1.00
		  )
		  ```
- # Deleting
  collapsed:: true
	- Drop first $n$ records
	  collapsed:: true
		- ```python
		  df = df.iloc[n: , : ]
		  ```
- # Sorting
  collapsed:: true
	- ```python
	  (
	    perf
	    .sort_values("Season")
	    .reset_index(drop=True)
	  )
	  ```
	- ```python
	  (
	    perf
	    .sort_values([
	      "Season",
	      "Rating",
	      "Value"
	    ], ascending=[
	      True,
	      True,
	      False
	    ])
	    .reset_index(drop=True)
	  )
	  ```
	- Different approach
	  collapsed:: true
		- ```python
		  (
		    formula_student[["Cost", "Overall Placing"]]
		    .sort_values("Cost", ascending = False)
		    .head(10)
		    .sort_values("Overall Placing")
		  )
		  ```
- # Grouping/Aggregation
  collapsed:: true
	- ```python
	  meanCols = {
	      "Value": "MeanValue",
	      "Overall": "MeanOverall",
	      "CPIValue": "MeanCPIValue"
	  }
	  ```
	- ## Single Aggregation Function
	  collapsed:: true
		- ### All Columns
		  collapsed:: true
			- collapsed:: true
			  ```python
			  (
			    merged
			    .groupby(
			    	["Year"],
			    	as_index=False # if Year should not become index of dataframe
			    )
			    .mean()
			    .rename(columns={
			      "Value": "MeanValue",
			      "Overall": "MeanOverall",
			      "CPIValue": "MeanCPIValue"
			    })
			  )
			  # or mean = merged.groupby(["Year"]).mean().reset_index()
			  ```
				- Renaming is for obvious reasons
		- ### Particular Columns
		  collapsed:: true
			- ```python
			  mean = merged[["Year","Value"]].groupby(
			    ["Year"],
			    as_index=False
			  ).mean().rename(columns=meanCols)
			  ```
	- ## Multiple Aggregation Function
	  collapsed:: true
		- ``` python
		  (
		    merged.groupby(
		    	["Year"],
		    	as_index=False
		    )
		    .agg(
		      ['mean', 'sum']
		    )
		  )
		  ```
		- ```python
		  (
		    formula_student[["Car", "Overall Scores"]]
		    .groupby(
		      ["Competition"]
		    )
		    .agg({
		      'Car' : ["count"],
		      'Overall Scores' : ["mean", "min", "max"]
		    })
		  )
		  ```
		- Round-off all results
		  collapsed:: true
			- ```python
			  formula_student[["Car", "Overall Scores"]]
			      .groupby(
			          ["Competition"]
			      )
			      .agg({
			          'Car' : ["count"],
			          'Overall Scores' : ["mean", "min", "max"]
			      })
			      .round(1)
			  ```
		- Round-off specific results
		  collapsed:: true
			- ```python
			  def mean_func(x):
			      return round(x.mean(), 1)
			  
			  formula_student[["Car", "Overall Scores"]]
			      .groupby(
			          ["Competition"]
			      )
			      .agg({
			          'Car' : ["count"],
			          'Overall Scores' : [mean_func, "min", "max"]
			      })
			  ```
- # Merging
  collapsed:: true
	- ```python
	  merged = pd.merge(
	      ratings[ratings["Value"] >= 10000],
	      cpi
	  ).sort_values("Value").reset_index(drop=True)
	  ```
- # Plotting
  collapsed:: true
	- ```python
	  merged.plot(
	    x="Season",
	    ylabel="Feature",
	    title="Features over Time"
	  )
	  ```
- # Type Casting
  collapsed:: true
	- ```python
	  df['Fee'] = df['Fee'].values.astype(float)
	  # df['Fee'] = df['Fee'].astype(float)
	  ```
- # Lagged Value
	- ```python
	  nba["wpc_lag"] = (
	    nba
	    .groupby("Team")
	    ["wpc"]
	    .shift(1)
	  )
	  ```
- # Performance Optimization
  collapsed:: true
	- ## Selectively-load columns
	  collapsed:: true
		- ```python
		  df = pd.read_csv(
		    "dataset.csv",
		    usecols = [
		      "First Name",
		      "Last Name"
		    ]
		  )
		  ```
	- ## Selectively-load rows
	  collapsed:: true
		- ```python
		  df = pd.read_csv(
		    "dataset.csv",
		    nrows = 10
		  )
		  ```
	- Use correct `dtypes`
		- ```python
		  df = pd.read_csv(
		    "dataset.csv",
		    dtype = {
		      "Age": "uint8",
		      "Year": "uint16",
		      "Time": "datetime"
		      "Salary": "ufloat32",
		      "Gender": "category",
		      "Name": "string[pyarrow]"
		    }
		  )
		  ```
		- #+BEGIN_WARNING
		  ~~`float16`~~
		  there's no hardware support for float16 on a typical processor (at least outside the GPU). NumPy converts the float16 operands to float32, perform the scalar operation on the float32 values, then round the float32 result back to float16.
		  #+END_WARNING
	- Use `pyarrow` engine
	  collapsed:: true
		- ```python
		  df = pd.read_csv(
		    "dataset.csv",
		    engine = "pyarrow"
		  )
		  ```
	- Use [[Modin]]