- Ensure Reproducibility
- Tips
	- Label sections using markdown
	- Sections
		- Import libraries
		- Import datasets
	- Functions for every operation
		- Use `pipe()` when working with datasets
		- ```python
		  import datetime as dt
		  
		  def loggg(f):
		    def wrapper(df, *args, **kwargs):
		      tic = dt.datatime.now()
		      result = f(df, *args, **kwargs)
		      toc = dt.datatime.now()
		      
		      duration = toc - tic
		      print(f.__name__, "took", duration)
		      
		      return result
		    return wrapper
		  
		  @loggg
		  def start_pipeline(df):
		    return df.copy()
		  
		  @loggg
		  def clean_dataset(df):
		    df.columns = [
		      c.replace(" ", "") for c in df
		    ]
		    return df
		  
		  @loggg
		  def remove_outliers(df):
		    return df
		  
		  cleaned_df = 
		  (my_dataset
		   .pipe(start_pipeline)
		   .pipe(clean_dataset)
		   .pipe(remove_outliers)
		  )
		  ```
			- The dataset will first make a copy using `start_pipeline()`, then `clean_dataset()` and then `remove_outliers()`
			-