---
hide:
  - navigation
---
[Docs](https://docs.cloud.google.com/bigquery/docs/)
#### Introduction
```python
from google.cloud import bigquery as bq

client = bq.Client() # centrol role in retrieving info from bigquery datasets
dataset_ref = client.dataset("hacker_news", project="bigquery-public-data") # arguments are dataset and the project where the data set is stored
dataset = client.get_dataset(dataset_ref) # fetching the database 
# this is only used for getting the info about the dataset and not the actual data in the dataset

tables = list(client.list_tables(dataset)) # getting all the tables
for table in tables:
	print(table.table_id) # getting the name of the tables

table_ref = dataset_ref.table("Table_name")
table = client.get_table(table_ref) # to get a table
table.schema # to get schema

client.list_rows(table, max_result = 5).to_dataframe() # get the top 5 rows
# bigquery library internally use pandas 

client.list_rows(table, 
	selected_fields=table.schema[:1], 
	max_results=5
).to_dataframe() # only first column
```


> !!! NOTE "Client"
> Go to server to run the query and get the data
>> !!! NOTE "Project"
>> Which holds the datasets
>>> !!! NOTE "Datasets"
>>> Which holds the tables
>>>> !!! NOTE "Tables"
>>>> Hold the actual data in rows and columns   

#### Running Queries
```python
from google.cloud import bigquery
client = bq.Client()

query = """
	SQL STATEMENT/QUERY GOES HERE
"""

# Date is the col name
"""
SELECT col, EXTRACT(DAY from Date) 
FROM table_name
"""
# to only get a part of the date


client.query(query)

# to estimate the size of query without running it
dry_run_config = bigquery.QueryJobConfig(dry_run=True)
dry_run_query_job = client.query(query, job_config=dry_run_config)
print("This query will process {} bytes.".format(dry_run_query_job.total_bytes_processed))

# to limit the data we can scan 
ONE_MB = 1000*1000
safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=ONE_MB)
safe_query_job = client.query(query, job_config=safe_config) # will only run if its is less than 1 MB
safe_query_job.to_dataframe()

```
[Date Docs](https://docs.cloud.google.com/bigquery/docs/reference/legacy-sql#datetimefunctions)
