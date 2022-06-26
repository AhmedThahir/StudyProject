tags:: [[Pandas]] [[Python]]

- #+BEGIN_WARNING
  Use only for huge huge datasets
  #+END_WARNING
- ```python
  # import pandas as pd
  
  import modin.pandas as pd
  from distributed import Client
  client = Client()
  ```