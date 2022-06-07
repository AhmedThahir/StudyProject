tags:: #[[Data Type]]

- Series of data for a single person for multiple time periods
- |Year|Company|Revenue|
  |--|--|--|
  |2015|A|1K|
  |2016|A|2K|
  |2017|A|3K|
- ```python
  df = df.set_index(
      "Year"
  )
  ```