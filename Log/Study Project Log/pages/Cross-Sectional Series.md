tags:: #[[Data Type]]

- Series of data for multiple people for a single time period
- |Year|Company|Revenue|
  |--|--|--|
  |2015|A|1K|
  |2015|B|5K|
  |2015|C|10K|
- ```python
  df = df.set_index(
    "Player Name"
  )
  ```