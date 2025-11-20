---
hide:
  - navigation
---
- `plt.figure(figsize=(x,y))` - set the width, height of the chart
- `sns.lineplot(data=dataframe)`
- `plt.title("title")`
	- `sns.lineplot(data=df[col1], lable='content1')`
	- `sns.lineplot(data=df[col2], lable='content2')
		- Both of the above will be plotted on the same graph even if there are 2 different statements
- `plt.xlable("x axis label")`
- `sns.barplot(x=df[col] or df.index, y=df[col])` 
- `sns.heatmap(data=df, annot=True)`
**Scatter Plots**
- `sns.scatterplot(x=df[col], y=df[col])` 
- `sns.regplot(x=df[col], y=df[col])` 
	- Regression line, the line that best fits the data
- `sns.scatterplot(x=df[col], y=df[col], hue=df[col])` 
- `sns.lmplot(x="col1", y="col2", hue="col", data=df)`
- `sns.swarmplot(x=df[col], y=df[col])`

- `sns.histplot(df[col])`
	- `sns.histplot(data=df, x=df[col], hue='col')`
- `sns.kdeplot(df[col], shade=True)`
	- `sns.kdeplot(data=df, x=df[col], hue='col', shade=True)`
		- 2 KDE plots
- `sns.jointplot(x=df[col1], y=df[col2], kind='kde')`
	- 2D KDE plot

**Choosing the charts**
- <u>Trends</u> - change in pattern
    - `sns.lineplot` - best to show trend over time
- <u>Relationship</u> - relationships between variables
    - `sns.barplot` - comparing quantities corresponding to different groups.
    - `sns.heatmap` -color-coded patterns in tables of numbers.
    - `sns.scatterplot` - relationship between two continuous variables - if color-coded, also show relationship third categorical variable
    - `sns.regplot` - regression line in scatter plot - easier to see linear relationship
    - `sns.lmplot` - drawing multiple regression lines - contains multiple color coded lines
    - `sns.swarmplot` - relationship between continuous variable and categorical variable.
- <u>Distribution</u> - show the possible values that we can expect to see in a variable, along with how likely they are.
    - `sns.histplot` -  distribution of a single numerical variable.
    - `sns.kdeplot` - estimated, smooth distribution of a single numerical variable (or two numerical variables).
    - `sns.jointplot` -  simultaneously displaying a 2D KDE plot with corresponding KDE plots for each individual variable.

**Styling**
- `sns.set_style('style')` - available styles are 
	- darkgrid
	- whitegrid
	- dark
	- white
	- ticks

