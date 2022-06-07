tags:: #[[Data Type]]
alias:: Longitudinal

- Series of data for multiple people for multiple time periods
- # Types
  collapsed:: true
	- ## Balanced
	  |Year|Company|Revenue|
	  |--|--|--|
	  |2015|A|1K|
	  |2015|B|5K|
	  |2015|C|10K|
	  |2016|A|2K|
	  |2016|B|10K|
	  |2016|C|20K|
	  |2017|A|3K|
	  |2017|B|15K|
	  |2017|C|30K|
	- ## Unbalanced
	  | Year | Company | Revenue |
	  | ---- | ------- | ------- |
	  | 2015 | A       | 1K      |
	  | 2015 | C       | 10K     |
	  | 2016 | A       | 2K      |
	  | 2016 | B       | 10K     |
	  | 2016 | C       | 20K     |
	  | 2017 | B       | 15K     |
	  | 2017 | C       | 30K     |
- ``` python
  df = df.set_index([
    "Player Name",
    "Year"
  ])
  ```
	- Order matters
- ```python
  from linearmodels import PanelOLS
  from linearmodels import RandomEffects
  ```