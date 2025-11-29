---
hide:
  - navigation
---
- columns - also known as attributes/properties
- table - also known as schema
## Select
```sql
SELECT col1, col2, col3, ..
FROM table_name

-- to select all
SELECT * 
FROM table_name

-- conditionals
SELECT col1, col2
FROM table_name
WHERE condition
AND condition
OR condition
BETWEEN x AND y
NOT BETWEEN a AND b
col IN ('e', 'f', 'g', 'h')
col NOT IN ('j', 'k', 'l', 'm')

-- specific conditionals 
SELECT * 
FROM table_name
WHERE col = 'something' -- case-sensitive equality
col != 'something' -- case-sensitive equality
col LIKE 'something' -- pattern matching or case-sensitive equality
-- ILIKE is used for case-insensitive where LIKE is case-sensitive
col NOT LIKE 'something' -- pattern matching inequality 
-- wildcards are % - means any num of character and _ means only one character
col LIKE '%some%' -- any word with some in between
-- handsomeness
col LIKE 'some%' -- start with some and end with anything
-- someplace
col LIKE 'an_' -- start with an and then a single character
-- and, ant
```
full text search ? - Apache Lucene or Sphinx - dedicated external for long full text search

### Filtering and Sorting
```sql
SELECT DISTINCT col -- discard rows that have duplicate values blindly
-- can use multiple cols as well like this -> DISTINCT col, col2, col3
-- DISTINCT will be used on all of them
-- can also be used within aggregates COUNT(DISTINCT col)
FROM table_name
-- grouping/GROUP BY is used for removing duplication on criteria

SELECT col, col2
FROM table_name
WHERE condition --not necessary
ORDER BY col ASC -- or DESC
LIMIT num -- reduce the number of rows to return
OFFSET num -- how many rows to skip - OPTIONAL
-- LIMIT and OFFSET are majorly used/written at the end of the statement/query



-- when comparing date and time with the timestamp or date data, this is a better way
WHERE timestamp_data > 'date' -- '2010-01-01'
```

#### CASE - if/then logic in SQL
```sql
SELECT col, col2, col3, -- this comma is important else SYNTAX ERROR
CASE 
  WHEN col = 'value' THEN 'value_2'
	WHEN col2 = 'value2' THEN 'val2' -- multiple conditions can be used as well
  ELSE NULL/'Value'
END AS column_name -- the column name where the THEN values will be displayed
FROM table_name
```
***<u>IRL example</u>***
```sql
SELECT player_name, year,
CASE 
	WHEN year = 'SR' THEN 'yes'
	ELSE NULL 
END AS is_a_senior
FROM benn.college_football_players

-- CAN also use multiple statements
SELECT player_name, weight,
CASE 
	WHEN weight > 250 THEN 'over 250'
	WHEN weight > 200 AND weight <= 250 THEN '201-250'
	WHEN weight > 175 AND weight <= 200 THEN '176-200'
	ELSE '175 or under' 
END AS weight_group
FROM benn.college_football_players
  
-- CAN also be used with aggregate functions
SELECT 
CASE 
	WHEN year = 'FR' THEN 'FR'
	WHEN year = 'SO' THEN 'SO'
	WHEN year = 'JR' THEN 'JR'
	WHEN year = 'SR' THEN 'SR'
	ELSE 'No Year Data' 
END AS year_group,
COUNT(1) AS count
FROM benn.college_football_players
GROUP BY year_group
```

### Multi Table Queries - JOINS
- primary key is needed - uniquely identifies the entity throughout the database
- JOIN - combines data - from two table - based on primary/unique key
#### Inner Join
matches rows of first table with second table - based on same key - result is big table with combined cols of both tables
```sql
SELECT col, col2, ...
FROM table_name
INNER JOIN another_table -- can also use only JOIN but this enchances the readability
ON table_name.id = another_table.matching_id
WHERE condition(s)
```

#### Outer Join
Asymmetric data - use LEFT, RIGHT or FULL JOIN, (OUTER can be omitted)

<u>Left Join:</u> returns all rows of left table A whether is match is found in right table B or not
- The table with more DISTINCT rows should be considered as A, hence used with FROM
- The table whose row you want to preserve should be considered as A or left table
```sql
SELECT col1, col2, col3, FROM table_1 LEFT JOIN table_2 
--                       table on left side    table on right side
ON table_1.col = table_2.col
--    left         right
```
<u>Right Join:</u> same as above but reversed, include rows of right table regardless of match found in left table

<u>Full Join:</u> rows for both tables are kept, regardless of matching row exist or not
```sql
SELECT col, col2
FROM table_name
LEFT/RIGHT/FULL JOIN another_table
ON table_name.id = another_table.matching_id
WHERE conditions(s)
```

#### UNIONs

#### NULL values
- good to reduce them as much as possible
- special attention as functions behave differently with NULL
- instead of NULL, use data-type appropriate value 
	- 0 for numerical data
	- "" for string
- NULL however can be used to store incomplete data
	- average of numerical data
```sql
SELECT col, col2
FROM table_name
WHERE col IS/IS NOT NULL
```

### Expressions
**Simple**
```sql
SELECT col/2 AS half_col
--  expression    description
FROM very_long_table_name AS short_name
INNER JOIN mini_table
ON short_name.id = mini_table.matching_id
WHERE condition(s)

-- every database has its own mathematical, string and data functions, present in their docs
```

**Aggregates**
```sql
SELECT agg_func(col) AS new_name FROM table_name
-- if new_name contains spaces, use "new name" - double quotes
-- this is the only place in sql where double quotes are used
GROUP BY col -- group the rows that have same value in the col specified
HAVING group_condition -- conditions that are applied on grouped data
-- HAVING is not needed if GROUP BY is not being used

/*
COUNT(*)   -- count all rows
COUNT(col) -- count non-NULL values in cols
-- can also use numbers as the position of the col in the select statement
MIN(col) -- will return smallest number, earlier date and string closest to 'A'
MAX()
AVG()
SUM()
*/

```

### Order of Execution
```sql
| FROM → JOIN -- to determine the total working set
| WHERE -- all rows and cols are passed to apply the conditions 
| GROUP BY -- to group on the basis of common data
| HAVING -- if group by exist
| SELECT -- select the part that is needed to be displayed
| DISTINCT -- among the chosen column, remove the duplicates
| ORDER BY -- rows are now sorted
| LIMIT → OFFSET -- how much to display and from where to display
↓
```

## Data Types
List of the all the [data types](https://www.w3schools.com/sql/sql_datatypes.asp) in SQL.
- Data should be stored as optimal data type from the beginning, but if it is not, you can change it via query.
- It is common for dates or numbers to be stored as strong which will be problematic when using some functions.
- You can use `CAST(col AS data_type)` or `col::data_type`

## Data Cleaning
```sql
LEFT(col, num) -- get the num amount of characters from the left side of the data of col
RIGHT(col, num) -- same as above but for the right
SUBSTR(col, start, steps) -- create a sub string like above but from middle
LENGTH(col) -- length of the strings in the col
TRIM('chars' FROM 'string') -- remove the chars from the beginning and end of the string
POSITION('char/substring' IN 'string') -- index of the first occurrence
-- OR
STRPOS('string', 'char/substring') -- both are case sensitive
CONCAT(col, 'string', col) -- nothing much to explain here
UPPER(col)
LOWER(col)
EXTRACT('val' FROM date_format) -- extracting from the parts of the date
DATE_TRUNC('va' FROM date_format) -- round off the date upto a specific val
/*
THE AVAILABLE vals are
year, month, day, hour, minute, second, decade, dow
-- dow means day of the week 
*/
COALESCE(col, 'string') -- replace the null values with string
```
### CTE (Common Table Expression)
CTE - temporary table returned within a query, helps in splitting queries into readable chunks
```sql
WITH temp_table_name AS
(
SELECT col, col2 FROM table_name
WHERE condition
)
SELECT col2 FROM temp_table_name
```

### Current Data/Time Methods
```sql
SELECT CURRENT_DATE AS date,
       CURRENT_TIME AS time,
       CURRENT_TIMESTAMP AS timestamp,
       LOCALTIME AS localtime,
       LOCALTIMESTAMP AS localtimestamp,
       NOW() AS now
   
-- FOR THE TIMEZONE STUFF
SELECT CURRENT_TIME AS time,
       CURRENT_TIME AT TIME ZONE 'PST' AS time_pst
```
[List of time zones](https://www.postgresql.org/docs/7.2/timezones.html)
## Inserting Rows
- Schema - description of each table and data type of each col of the table
```sql
INSERT INTO table_name
VALUES (val1, val2, val3) -- as the cols are not specified, you must include values of all cols


-- IF THE DATA IS NOT COMPLETE
INSERT INTO table_name (col_name, col2, col3, col4)
VALUES (val1, val2, val3, val4) -- this will be inserted in sequence to the above cols sequence
-- col that is not mentioned here will be filled with default value(if not set)
-- instead of values, you can also use expression to be inserted such as (2.4, 1000/500)
```

## Updating Rows
```sql
UPDATE table_name
SET col = value_or_expression, 
	col2 = val2,
	col3 = val3, etc
WHERE conditions

-- be extra careful setting the values
-- check the proper cols and conditional statement

:TIP
-- first check the conditional query using SELECT whether you are updating the correct rows or not and then proceed to updation
```

## Deleting Rows
```sql
DELETE FROM table_name
WHERE condition -- if this is omitted, all rows are removed however quick way to clear the table if wants to 

:TIP
-- run SELECT first to check the conditional
-- read DELETE statement twice 
```

## Creating Tables
```sql
CREATE TABLE IF NOT EXISTS table_name(
col1_name datatype TableConstraint DEFAULT default_value,
col2_name datatype TableConstraint DEFAULT defauly_vaue
)
-- TableConstraint is applied on the value inserted into the col
```

### Table Data Types

| Data Type                         | Description                                                                                                                                                                                                                           |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Integer                           | Whole integer values                                                                                                                                                                                                                  |
| Boolean                           | int value of just 0 and 1                                                                                                                                                                                                             |
| Float, Double, Real               | Store more precise numerical data;<br>Different types is used as per the precision required                                                                                                                                           |
| Char(Character),<br>Varchar, Text | text based data types; the difference lies into the efficiency of database when working with them<br>CHAR(n) - fixed size, less will be filled with padding<br>VARCHAR(n) - variable but max is n number of chars<br>TEXT - unlimited |
| DATE, DATETIME                    | no explanation needed                                                                                                                                                                                                                 |
| BLOB                              | Binary data, must store with right metadata for requery                                                                                                                                                                               |

### Table Constraints

| CONSTRAINTS                                                                                                                           | Description                                                 |
| ------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| PRIMARY KEY                                                                                                                           | unique and each row can be identified with                  |
| AUTOINCREMENT                                                                                                                         | automatically filled and incremented with each row integrat |
| UNIQUE                                                                                                                                | cannot have duplic                                          |
| NOT NULL                                                                                                                              | cannot be NULL or                                           |
| CHECK(exp)                                                                                                                            | check whether the value inserted is valid o                 |
| FOREIGN                                                                                                                               |  Consistency check means each value in the col ensures it corresponds to another value in another col in another table                                                            |

## Altering Tables
```sql
ALTER TABLE table_name
ADD col datatype constraints DEFAULT val -- to add a column
DROP col                                 -- the col to be deleted
RENAME TO new_table_name                 -- new table name
```

All databases support slightly different methods so use docs for it.

## Dropping Tables
```sql
DROP TABLE IF EXISTS table_name

-- if it has FOREIGN KEY, either update the depended tables or remove those tables as well
```

## END
The basics are covered above, if want to explore more, follow these:

1. [Window Functions](https://www.thoughtspot.com/sql-tutorial/sql-window-functions)
2. [Performance Tuning](https://www.thoughtspot.com/sql-tutorial/sql-performance-tuning)
3. [Pivoting Data](https://www.thoughtspot.com/sql-tutorial/sql-pivot-table)
4. [Analytics](https://www.thoughtspot.com/sql-tutorial/sql-business-analytics-training)
