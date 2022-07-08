tags:: [[SQL]]

- Good schema
	- Having foreign key constraints enables faster joins
		- because query optimizer understands the relationships between tables
		- it knows that every value of the foreign key should exist in the primary table
- Use `varchar` instead of `char`
- Use numeric fields for numbers instead of `varchar`
- select only required fields, instead of `select *`
- Avoid `distinct` keyword
	- If really required, use `distinct (colname)` instead of `distinct *`
- Use `union all` instead of `union`
	- Union will eliminate duplicates, which adds complexity for searching
- `LIMIT 1` for searching
  id:: 62c01390-e80e-41e2-a69d-7d96c2b75ff0
  collapsed:: true
	- If we know that there is only result, `LIMIT 1` will stop once found
		- equivalent of break statement
	- ```mysql
	  select name
	  from student
	  where id = 198
	  limit 1;
	  
	  # faster than
	  select name
	  from student
	  where id = 198;
	  ```
- Use `EXISTS`, `NOT EXISTS` instead of than `IN`, `NOT IN`
  collapsed:: true
	- `EXISTS` stops processing after the first row is found
	- Basically the equivalent of adding ((62c01390-e80e-41e2-a69d-7d96c2b75ff0))
	- ```mysql
	  # display graduated students
	  SELECT name
	  FROM student
	  WHERE id EXISTS (
	      SELECT id
	      FROM graduated
	  );
	  # is better than
	  SELECT name
	  FROM student
	  WHERE id IN (
	      SELECT id
	      FROM graduated
	  );
	  ```
- Use materialized views to store views like tables