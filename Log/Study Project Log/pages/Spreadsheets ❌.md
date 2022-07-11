alias:: Sheet, Excel, Google Sheets, GSheets
tags:: [[Dashboards]]

- # Not Recommended
  collapsed:: true
  Programmatic Analysis is preferred, as
	- Faster
	- data and analysis are separate
	- automate analysis
	- reproducibility
	- Python is open-source, hence the analysis is open-source
	  collapsed:: true
		- Instead of paying for excel, you could use the money elsewhere
- # Formatting
  collapsed:: true
	- Conditional Formatting for Empty
	- Alternating Colors for Rows
	  collapsed:: true
		- Enhances legibility
- # Formulae
  collapsed:: true
	- Try to use fixed ranges, to improve performance
	- ## Value in $n^{th}$ row
	  collapsed:: true
		- ```c
		  =INDEX(Payable!A2:A100, 5)
		  ```
		- ### Value in Last Row
		  collapsed:: true
			- ```c
			  =INDEX(Payable!A2:A, COUNTA(Payable!A2:A))
			  ```
	- ## Automatic Numbering
	  collapsed:: true
		- ```c
		  =ARRAYFORMULA( if( ISBLANK(B2:B100), , row(B2:B100)-1 ) )
		  
		  =ARRAYFORMULA( if( ISBLANK(B4:B100), , row(B4:B100)-3 ) )
		  ```
	- ## Autofill Particular Word
	  collapsed:: true
		- ```c
		  =ARRAYFORMULA( if(ISBLANK(C2:C100), "-", "Al Quoz") )
		  ```
	- ## Natural Join
	  collapsed:: true
		- Uses  `VLOOKUP`
		  collapsed:: true
			- ```mysql
			  VLOOKUP(look_for_range, look_in_range, columns, sorted_always_FALSE)
			  ```
		- ## Single Column
		  collapsed:: true
			- ```mysql
			  =ARRAYFORMULA(if( ISBLANK(C2:C100), "-",
			  	VLOOKUP(C2:C100,'Student Details'!$A$2:$B100, 2, FALSE)
			  ))
			  ```
		- ### Multiple Columns
		  collapsed:: true
			- Make sure that the look_in_range is correct size
			- ```mysql
			  =ARRAYFORMULA(if( ISBLANK(C2:C100), "-",
			  	VLOOKUP(C2:C100,'Student Details'!$A$2:$D100, {2, 3, 4}, FALSE)
			  ))
			  ```
	- ## Count number of capital/small letters
	  collapsed:: true
		- ### Capital
		  collapsed:: true
			- ```mysql
			  =SUMPRODUCT(LEN(E3)-LEN(SUBSTITUTE(E3,CHAR(ROW(INDIRECT("65:90"))),"")))
			  ```
		- Small
		  collapsed:: true
			- ```mysql
			  =SUMPRODUCT(LEN(E3)-LEN(SUBSTITUTE(E3,CHAR(ROW(INDIRECT("97:122"))),"")))
			  ```
	- ## Import Data from another sheet
		- ```mysql
		  =ImportRange("1WsMosP6WaifrDsTaMuZUlEP8MSYP1nfTyKh9x7q4ads","Student_Details!B2:B200")
		  ```
- # Functionality
  collapsed:: true
	- Dropdown
	  collapsed:: true
		- Data Validation > List
	- ## Automatic Checkboxes
	  collapsed:: true
		- Data Validation > Checkboxes
- # Query
  collapsed:: true
	- Quite similar to mySQL
	- Tips
	  collapsed:: true
		- Put `where col is not null` whenever possible
		  collapsed:: true
			- to prevent crashes (due to too many blank values)
		- Use only required columns in the input_range
		- Use fixed ranges
	- ## Basic
	  collapsed:: true
		- ```mysql
		  QUERY(People!A2:Z, "select B where B is not null")
		  ```
	- ## Labels
	  collapsed:: true
		- ```mysql
		  QUERY(People!A2:Z, "select B where B is not null label B 'Roles'")
		  ```
	- ## Distinct
	  collapsed:: true
		- ```mysql
		  unique(QUERY(People!A2:Z, "select B where B is not null"))
		  ```
	- ## Sorting
	  collapsed:: true
		- ```mysql
		  =QUERY(Teams!A2:Z, "select B, count(B) where B is not null group by B order by count(B) desc label B 'Country', count(B) 'Count'")
		  ```
	- ## Double Grouping
	  collapsed:: true
		- ```mysql
		  =QUERY(Teams!A2:Z, "select C, B, count(B) where C is not null and B is not null group by C, B order by count(B) desc label C 'Continent', B 'Country', count(B) 'Count'")
		  ```
	- ## Rounding
	  collapsed:: true
		- ```mysql
		  =query(
		    D2:E,
		    "select 10/3 format 10/3 '#.#' "
		    )
		  ```
	- ## Calculating %
	  collapsed:: true
		- This query will automatically multiply with 100
		- ```mysql
		  =query(
		    D2:E,
		    "select 10/3 format '#.# %' "
		    )
		  ```
	- ## Using Cell as value
	  collapsed:: true
		- ### Number
		  collapsed:: true
			- ```mysql
			  =query(
			  	D2:E,
			  	"select 10/"&E2&""
			    )
			  ```
		- ## Text
		  collapsed:: true
			- Has `'` around the `"`
			- ```mysql
			  =query(
			  	D2:E,
			  	"select '"&E2&"'
			    )
			  ```
	- ## Subquery
	  collapsed:: true
		- ```mysql
		  =QUERY(
		    QUERY(
		    	People!B2:D,
		    	"select B, count(B) where B is not null group by D, B label B 'Important Divisions', count(B) 'Size'"
		    ),
		    "select Col1, avg(Col2), count(Col1) where Col1 is not null group by Col1 order by avg(Col2) desc label count(Col1) 'No of Teams', avg(Col2) 'Average Size'"
		   )
		  ```
		- ```mysql
		  =QUERY(
		  	QUERY(People!B2:D,
		            "select B, count(B) where B is not null group by D, B label B 'Important Division', count(B) 'Size'"
		           ),
		  	"select Col1, count(Col2), avg(Col2), avg(Col2)/"&E2&", min(Col2) where Col1 is not null group by Col1 order by count(Col2) desc, avg(Col2)/"&E2&" desc label min(Col2) 'Min Size', avg(Col2) 'Avg Size', avg(Col2)/"&E2&" 'Avg Size %', count(Col2) 'Teams having' format avg(Col2)/"&E2&" '#.# %' "
		  )
		  ```
- # Administrative Permission
  collapsed:: true
	- ## Read (Viewers)
	  collapsed:: true
		- Set sharing settings of the entire gsheet as view only
	- ## Read
	  collapsed:: true
		- Protect Sheet
		- Description - Summary
	- ## Read/Write/Update (Lock Schema)
	  collapsed:: true
		- Protect header row
		- Description - Header
	- ## Read/Update (not create/modify/delete)
	  collapsed:: true
		- Create a blank column
		- Protect the column from editing
		  collapsed:: true
			- Description - Update Only
		- Hide the column
- # Dashboards
  collapsed:: true
	- Even Google Sheets can create dashboard
	  collapsed:: true
	  id:: 62c96cec-9ad1-40d0-99cb-9ad67478a28b
		- File > Share > Publish to Web
		- Select what to include