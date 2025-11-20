---
hide:
  - navigation
---
### Handy Stuff
- `df.col.idxmax()` - index of the first occurrence of max value in col
- `df[col].str.lower().str.count(word)` return the occurrence of the word in the values of col - almost instant
- chaining commands - wanna apply condition in mid chain - use lambda

### Creation
- `pd.DataFrame(dict)` - keys will be column headings
	- `index=[]` - custom row labels, other than 0,1,2...
- `pd.Series([])` - single column data structure
- `pd.read_csv(path, index_col='col to set as index')` - csv to DataFrame
	- `index_col=0` - column to use as row labels/index in csv
- `df.shape` - (rows, columns) of DataFrame
- `df.head()` - first five rows
### Retrieval
- `df[column_name]` or `df.column_name` - get the column
	- `df[col_name][row_num]`
- `df.iloc[index]` - data selection based on index/row
	- `df.loc[label]` - data selection based on label
	- both are row-first, column-second
- `df.iloc[:,0]` - first column, all rows(range can be given 1 : 4)
	- `df.iloc[[list_of_rows], cols/list_of_cols]`
- `df.iloc[-5:]` - last five rows
- iloc is exclusive and loc is inclusive
	- `[0:10]` in iloc will give `0, 1, 2, ..., 9`
	- `[0:10]` in loc will give `0, 1, 2, ..., 10`
- `df.set_index(col_name)` - use col as index
- `df.loc[(df.col == 'col_value') & (condition 2) | (condition 3)]` - filtering the data
	- `&` is and, `|` is or
	- `df.loc[(row filteration  or col on condition), [list of cols want to select]]` - multi cols on the basis of a condition or single col without square bracket
- `df.loc[df.col.isin([list_of_values])]` - something like "if x in y"
- `df.loc[df.col.isnull()]` or `df.loc[df.col.notnull()]`
- `df[col] = val` - all rows of col will be val, range can be given in place of val
### Summarization and Representation
- `df.col.describe()` - High-Level Statistical report of the col
	- type-aware - output changes based on data/col
- `df.col.mean()`
- `df.col.unique()` - list of unique vals in col
- `df.col.value_counts()` - unique values and their frequency

- `df.col.map(function)` - a new dataframe - with vals of col - modified by the func
- `df.apply(function, axis=0 or 1)` - equivalent to above but transform the whole dataframe
	- axis = 0 - row
	- axis = 1 - column
- Both above return new df, do not change the original data
- operators like `+ - == < >` are faster than map() and apply() but the later are more flexible and used for more advanced things

### Grouping and Sorting
- `df.groupby(col for grouping)[col_for_operation].summary_method()`
	- `df.groupby[].apply()` - gives a slice of dataframe - accessible via apply()
- `df.groupby(['col_1', 'col_2'])` - combination of both/all cols
	- every group has same col_1 and col_2 values
- `df.groupby(col).col.agg([len, min, max, etc])` - lets you execute multiple methods on the same dataset
	- len is used to count rows
	- `count()` only counts the non-NaN
	- `len()` counts all rows
- groupby with multi cols gives Multi-index - the most common method used - `reset_index()` - convert back to regular index
- `df.sort_values(by='col', ascending=True/False)`
	- `df.sort_index()` - same arguments, just sorting basis is different
- `df.sort_values(by=['col_1', 'col_2'])` - first sort as col_1 then col_2
- `df.groupby(col).size()` - count the number of rows in each group

### Data Types and Missing Values
- `df.col.dtype` - data type of the col
	- `df.dtypes` - of all cols
- string cols falls under dtype Object
- type conversion - `df.col.astype('type')`

- Missing -> NaN -> always float64
- `df[col].isnull()` or `df[col].notnull()` - grab or not grab the NaN
	- `df[col].isnull().sum()` - count total number of NaN
- `df.col.fillna('val')` - replace all NaN with val
	- `df.col.fillna(method='bffill', inplace=True/False)` - backfill strategy
	- inplace - True - make changes in original df
- `df.col.replace('val_1', 'val_2')` - in col, replace val_1 with val_2

### Renaming and Combining
- `df.rename(columns={'old_col':'new_col'}, inplace=True/False)`
	- `df['new_col'] = df.pop('old_col')`
	- `df.rename(index={0:'first', 1:'second'})`
- `df.rename_axis('new_row_name', axis='rows').rename_axis('new_col_name', axis='columns')`

- Complexity - `concat()` < `join()` < `merge()`
- `pd.concat([df1, df2])`
- `join()` - combine diff dataframe objects with common index 
- `left.join(right, lsuffix='_from_left', rsuffix='_from_right')`
	- `left` and `right` is df names
	- lsuffix and rsuffix helps - same col names - no overlapping
- `df1.set_index("col").join(df2.set_index("col"))`
	- join for combining - two same cols in dfs
	- merge is better to join when joining on the basis of non-index