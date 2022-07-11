- Ensure Reproducibility
- Tips
	- Label sections using markdown
	- Sections
	  collapsed:: true
		- Import libraries
		- Import datasets
	- Functions for every operation
	  collapsed:: true
		- Use `pipe()` when working with datasets
		- collapsed:: true
		  ```python
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
- # Auto Export Config
	-
	- ```python
	  # Based off of
	  # https://github.com/jupyter/notebook/blob/master/docs/source/extending/savehooks.rst
	  # https://jupyter-notebook.readthedocs.io/en/stable/extending/savehooks.html
	  
	  # This could be a simple call to jupyter nbconvert --to script,
	  # but spawning the subprocess every time is quite slow.
	  
	  import io
	  import os
	  from notebook.utils import to_api_path
	  
	  from traitlets.config import Config
	  my_config = Config()
	  my_config.TemplateExporter.exclude_input = True
	  my_config.TemplateExporter.exclude_input_prompt = True
	  my_config.TemplateExporter.exclude_output_prompt = True
	  
	  from nbconvert.exporters.script import ScriptExporter
	  # from nbconvert.exporters.html import HTMLExporter
	  from nb_offline_convert import OfflineHTMLExporter #, OfflineWebPDFExporter
	  
	  # log = contents_manager.log
	  
	  _script_exporter = None
	  _html_exporter = None
	  
	  
	  def script_post_save(model, os_path, contents_manager, **kwargs):
	  		"""convert notebooks to Python script after save with nbconvert
	  		replaces `ipython notebook --script`
	  		"""
	  	
	  		if model['type'] != 'notebook':
	  				return
	  		
	  		base, ext = os.path.splitext(os_path)
	  
	  		# save html
	  		global _html_exporter
	  		if _html_exporter is None:
	  				_html_exporter = OfflineHTMLExporter( #HTMLExporter
	  					parent = contents_manager,
	  					config = my_config
	  				)
	  
	  		html, resources = _html_exporter.from_filename(os_path)
	  		html_fname = base + resources.get('output_extension', '.txt')
	  		# log.info("Saving html /%s", to_api_path(script_fname, contents_manager.root_dir))
	  
	  		# save .py file
	  		global _script_exporter
	  		if _script_exporter is None:
	  				_script_exporter = ScriptExporter(parent=contents_manager)
	  		
	  		script, resources = _script_exporter.from_filename(os_path)
	  		script_fname = base + resources.get('output_extension', '.txt')
	  		# log.info("Saving script /%s", to_api_path(script_fname, contents_manager.root_dir))
	  	
	  		with io.open(html_fname, 'w', encoding='utf-8') as f:
	  				f.write(html)
	  		with io.open(script_fname, 'w', encoding='utf-8') as f:
	  				f.write(script)
	  
	  
	  c.FileContentsManager.post_save_hook = script_post_save
	  ```