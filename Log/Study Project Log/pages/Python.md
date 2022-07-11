tags:: programmingLanguage

- general purpose, statistical computing and machine learning
- since it is an interpreted language, it is slow for very large-scale projects, but should be fine for me
- # Libraries
  collapsed:: true
	- [[Pandas]]
	- [[Sci-Kit Learn]]
	- [[Numpy]]
	- [[Matplotlib]]
- # Misc
  collapsed:: true
	- [[Animation]]
	- [[Interactive Plots]]
	- [[Dashboards]]
- # Text Formatting
  collapsed:: true
	- ```python
	  class color:
	     PURPLE = '\033[95m'
	     CYAN = '\033[96m'
	     DARKCYAN = '\033[36m'
	     BLUE = '\033[94m'
	     GREEN = '\033[92m'
	     YELLOW = '\033[93m'
	     RED = '\033[91m'
	     BOLD = '\033[1m'
	     UNDERLINE = '\033[4m'
	     END = '\033[0m'
	  
	  print(color.BOLD + 'Hello World !' + color.END)
	  ```
- # Functions
  collapsed:: true
	- Date-Time
	  collapsed:: true
		- Refer to [[Python Date Formats]]
		- ```python
		  dob = '05/02/1985'
		  dob = datetime.strptime(dob, '%d/%m/%Y')
		  ```
	- ## Files
	  collapsed:: true
		- ```python
		  import os
		  
		  files = os.listdir("./data")
		  files
		  ```
		- ```python
		  from os import walk
		  files = []
		  
		  # specific directory
		  files = []
		  for (dirpath, dirnames, filenames) in walk("./data"):
		      files.extend(filenames)
		      break
		  
		  # directory and subdirectories
		  for (dirpath, dirnames, filenames) in walk("."):
		      files.extend(filenames)
		      
		  files
		  ```
	- ## Search String
	  collapsed:: true
		- ```python
		  if( ".pdf" == file[:-4] )
		  
		  if( "Python" in my_string )
		  
		  if( my_string.find("Python") )
		  ```
- # Multi
  collapsed:: true
	- ```python
	  import concurrent.futures as multi
	  ```
	- ## Multi-Threading
		- ```python
		  with multi.ThreadPoolExecutor() as executor:
		      executor.map(read_file, files) # (function, list)
		  ```
	- ## Multi-Processing
		- Doesn't work by default in [[Jupyter Notebook]]
		- ```python
		  with multi.ProcessPoolExecutor() as executor:
		      executor.map(read_file, files) # (function, list)
		  ```
- # IDK
	- ```python
	  for (i, file) in enumerate(files):
	    print(i, "is", file)
	  ```