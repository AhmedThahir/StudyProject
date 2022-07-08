- # Median
  collapsed:: true
	- There is no inbuilt median function
	- ## Approach 1 - General SQL
	  collapsed:: true
		- collapsed:: true
		  ```mysql
		  SELECT AVG(x)
		  FROM (
		    SELECT x,
		    ROW_NUMBER() OVER(ORDER BY x ASC) AS up,
		    ROW_NUMBER() OVER(ORDER BY x DESC) AS dn
		    FROM  your_table_name
		  ) AS X(x, up, dn)
		  WHERE up IN (dn, dn+1, dn-1);
		  ```
			- This is easier to see with a number line:
			  collapsed:: true
				- 1 2 3 4 5 6 8 9 = up
				  9 8 6 5 4 3 2 1 = dn
			- the middle subset is {4,5} and the average is 4.5 or the median.
	- ## Approach 2 - `mySQL` specific
	  collapsed:: true
		- ```mysql
		  select
		          (
		              substring_index(                          -- left median: max value in lower half:
		                  substring_index(
		                      group_concat(                     --   list all values in ascending order
		                          f.replacement_cost
		                          order by f.replacement_cost
		                      )
		                  ,   ','
		                  ,   ceiling(count(*)/2)               --   left half of the list 
		                  )
		              ,   ','
		              ,   -1                                    --   keep only the last value in list
		              )
		          +   substring_index(                          -- right median: min value in upper half:
		                  substring_index(
		                      group_concat(                     --   list all values in ascending order
		                          f.replacement_cost
		                          order by f.replacement_cost
		                      )
		                  ,   ','
		                  ,   -ceiling(count(*)/2)              --   right half of the list 
		                  )
		              ,   ','
		              ,   1                                     --   keep only the first value in list
		              )
		          ) / 2                                         -- average of left and right medians
		          as median
		  from    sakila.film f;
		  ```
- # Percentile
  collapsed:: true
	- `mySQL`
	  collapsed:: true
		- ```mysql
		  SELECT  SUBSTRING_INDEX(
		              SUBSTRING_INDEX(
		                  GROUP_CONCAT(                 -- 1) make a sorted list of values
		                      f.length
		                      ORDER BY f.length
		                      SEPARATOR ','
		                  )
		              ,   ','                           -- 2) cut at the comma
		              ,   90/100 * COUNT(*) + 1         --    at the position beyond the 90% portion
		              )
		          ,   ','                               -- 3) cut at the comma
		          ,   -1                                --    right after the desired list entry
		          )                 AS `90th Percentile`
		  FROM    sakila.film AS f
		  ```
	-