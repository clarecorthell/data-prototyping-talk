Follow me on twitter [@clarecorthell](https://twitter.com/clarecorthell)!

## Prototyping in the Data World - Data Scripting Skills // @ Hackbright Academy (Slides & Resources)

* Vimeo _**link coming**_
* [Slides](http://www.slideshare.net/ClareCorthell/hackbright-talk)

## Talk Notes

### Tools
* [numpy](http://www.sam.math.ethz.ch/~raoulb/teaching/PythonTutorial/intro_numpy.html) _multi-dimensional container of data_
* [pandas](http://nbviewer.ipython.org/urls/gist.github.com/fonnesbeck/5850375/raw/c18cfcd9580d382cb6d14e4708aab33a0916ff3e/1.+Introduction+to+Pandas.ipynb) _data structures analysis tools_
* [matplotlib](http://www.ast.uct.ac.za/~sarblyth/pythonGuide/PythonPlottingBeginnersGuide.pdf) _python plotting library_
* [iPython](http://www.reddit.com/r/Python/comments/1q9tq7/what_is_the_big_deal_about_ipython_notebooks/) _browser-based code notebook / IDE (run blocks of code, not the whole program)_

### Notes accompanying the talk ([slides](http://www.slideshare.net/ClareCorthell/hackbright-talk))

All python code for this talk was run in the browser-based iPython interpreter

#### Import tools

```
import numpy as np
import pandas as pd

# Render our plots inline
%matplotlib inline
import matplotlib.pyplot as plt
```

#### Get Data

turn a csv into a DataFrame (for example, an export from excel in csv form)

`mattermark_df = pd.read_csv('mattermark_data.csv')` => Mattermark data about funding rounds in New York City in the last five years

#### What's in here?

sample different parts of the data

`mattermark_df[:10]` sample the first ten rows of our DataFrame

`mattermark_df.iloc[0]` use .iloc to index into row location 0

`mattermark_df['cached_uniques']` sample the column

`mattermark_df['cached_uniques'].describe()` show some standard statistics about that column (for numeric data)

`mattermark_df.describe()` show some standard statistics about all numeric columns

`mattermark_df.sort('amount', ascending=False)` sort entire table (descending) by amount amount of funding

#### What's _not_ in here?

mattermark_df['amount'].isnull()` In the column, is the value at a given index null? (true or false)

`len(np.where(mattermark_df['amount'].isnull())[0])` Count the number of null values in the column

#### Ask a few Questions (which lead to other questions)

**What is the most common stage for funding?**

`mattermark_df['series'].value_counts()` count the values in each category

`mattermark_df['series'].value_counts().plot(kind='bar')` plot in a bar graph (grouped by series) to get a quick idea of relative scale

**Leads to Question: What is the typical funding amount by round?**

`by_series = mattermark_df.groupby('series')` group records by series column (stored in a variable)

`print by_series['amount'].mean().astype(int)` within each grouping, calculate the mean (and do some explicit type conversion)

**How many of these are mobile companies?**

`mobile_df = mattermark_df.dropna(subset=['cached_mobile_downloads'])` we do some brash inference that if a company doesn't have a monthly count of mobile downloads, it doesn't have a mobile application; using the .dropna function, we get rid of the rows that don't have a value for that column.

```
mattermark_df.shape
mobile_df.shape
```
compare the shape of the two DataTables to see how many companies (rows) have mobile app data to see a rough proportion

**For more context, see the [video (coming soon)]() & [slides](http://www.slideshare.net/ClareCorthell/hackbright-talk))**

### Great Resources for Getting Started

* [The Open Source Data Science Masters](http://datasciencemasters.org/) - A curated curriculum of open source resources to get you working with and understanding data
* [pandas cookbook](http://nbviewer.ipython.org/github/jvns/pandas-cookbook/blob/master/cookbook/Chapter%201%20-%20Reading%20from%20a%20CSV.ipynb) - great beginning resource from [Julia Evans](https://twitter.com/b0rk)
* [Python for Data Analysis / Book](http://amzn.to/Q2pI5I)
