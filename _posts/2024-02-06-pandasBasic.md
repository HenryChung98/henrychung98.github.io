---
layout: single
title: "Pandas Basic"
categories: note
tags: [python, numpy, pandas]
author_profile: false
search: true
---

### Introduction

Pandas is a open-source data manipulation and analysis library.
It provides data structures for efficiently storing and manipulating large datasets and tools for working with structured data.

```python
import pandas as pd
```

Here is simple example of creating a DataFrame using pandas

```python
data = {'Name': ['Alice', 'Bob', 'Charlie'],
        'Age': [25, 30, 35],
        'City': ['New York', 'San Francisco', 'Los Angeles']}

df = pd.DataFrame(data)

print(df)
#      Name  Age           City
# 0   Alice   25       New York
# 1     Bob   30  San Francisco
# 2  Charlie   35    Los Angeles

print(type(df)) # pandas.core.frame.DataFrame
print(df.columns) # [Name, Age, City]
```

It is quite easy to create data frames with pandas.

```python
import pandas as pd
two_dimensional_list = [["a", 50, 86], ["b", 89, 31], ["c", 68, 91], ["d", 88, 75]]
my_df = pd.DataFrame(two_dimensional_list)
print(my_df)
```

output

|       | **0** | **1** | **2** |
| ----- | ----- | ----- | ----- |
| **0** | a     | 50    | 86    |
| **1** | b     | 89    | 31    |
| **2** | c     | 68    | 91    |
| **3** | b     | 88    | 75    |

If you do not define the row, column names, it will be automatically generated 0, 1, 2, 3 ...

You can define the names like this

```python
import pandas as pd
two_dimensional_list = [["a", 50, 86], ["b", 89, 31], ["c", 68, 91], ["d", 88, 75]]
my_df = pd.DataFrame(two_dimensional_list, columns=["name", "english_score", "math_score"], index=["a", "b", "c", "d"])
print(my_df)
```

output

|       | **name** | **english_score** | **math_score** |
| ----- | -------- | ----------------- | -------------- |
| **a** | a        | 50                | 86             |
| **b** | b        | 89                | 31             |
| **c** | c        | 68                | 91             |
| **d** | b        | 88                | 75             |

If you want to check data types,

```python
print(my_df.dtypes)
# name             object
# english_score     int64
# math_score        int64
# dtype: object
```

### Data Frame

Data frame can contain a variety of data types, but within the same column, it should be of the same data type.

You can also create a frame using dictionary

```python
import numpy as np
import pandas as pd

names = ['a', 'b', 'c', 'd']
english_scores = [50, 89, 68, 88]
math_scores = [86, 31, 91, 75]

dict1 = {
    'name': names,
    'english_score': english_scores,
    'math_score': math_scores
}

dict2 = {
    'name': np.array(names),
    'english_score': np.array(english_scores),
    'math_score': np.array(math_scores)
}

dict3 = {
    'name': pd.Series(names),
    'english_score': pd.Series(english_scores),
    'math_score': pd.Series(math_scores)
}

# same outputs
df1 = pd.DataFrame(dict1)
df2 = pd.DataFrame(dict2)
df3 = pd.DataFrame(dict3)

print(df1)

```

output

|       | **name** | **english_score** | **math_score** |
| ----- | -------- | ----------------- | -------------- |
| **a** | a        | 50                | 86             |
| **b** | b        | 89                | 31             |
| **c** | c        | 68                | 91             |
| **d** | b        | 88                | 75             |

or

```python
import numpy as np
import pandas as pd

my_list = [
    {'name': 'dongwook', 'english_score': 50, 'math_score': 86},
    {'name': 'sineui', 'english_score': 89, 'math_score': 31},
    {'name': 'ikjoong', 'english_score': 68, 'math_score': 91},
    {'name': 'yoonsoo', 'english_score': 88, 'math_score': 75}
]

# if you do not specify the order of the column, it might be arranged it alphabetically.
df = pd.DataFrame(my_list, columns=["english_score", "math_score", "name"])
print(df)
```

output

|       | **english_score** | **math_score** | **name** |
| ----- | ----------------- | -------------- | -------- |
| **a** | 50                | 86             | a        |
| **b** | 89                | 31             | b        |
| **c** | 68                | 91             | c        |
| **d** | 88                | 75             | b        |

Several dtypes that can be contained in pandas.

| **dtype**  | **explain**   |
| ---------- | ------------- |
| int64      | int           |
| float64    | float         |
| object     | string        |
| bool       | boolean       |
| datetime64 | date and time |
| category   | category      |

### Read CSV File

Using pandas, you can quite easily read CSV files.

```csv
,released,display,memory,version,Face ID
iPhone 7,2016-09-16,4.7,2GB,iOS 10.0,No
iPhone 7 Plus,2016-09-16,5.5,3GB,iOS 10.0,No
iPhone 8,2017-09-22,4.7,2GB,iOS 11.0,No
iPhone 8 Plus,2017-09-22,5.5,3GB,iOS 11.0,No
iPhone X,2017-11-03,5.8,3GB,iOS 11.1,Yes
iPhone XS,2018-09-21,5.8,4GB,iOS 12.0,Yes
iPhone XS Max,2018-09-21,6.5,4GB,iOS 12.0,Yes
```

```python
import pandas as pd
iphone_df = pd.read_csv("data/csvfile.csv")
print(ipone_df)
```

output

|       | **Unnamed: 0** | **released** | **display** | **memory** | **version** | **Face ID** |
| ----- | -------------- | ------------ | ----------- | ---------- | ----------- | ----------- |
| **0** | iPhone 7       | 2016-09-16   | 4.7         | 2GB        | iOS 10.0    | No          |
| **1** | iPhone 7 Plus  | 2016-09-16   | 5.5         | 3GB        | iOS 10.0    | No          |
| **2** | iPhone 8       | 2017-09-22   | 4.7         | 2GB        | iOS 11.0    | No          |
| **3** | iPhone 8 Plus  | 2017-09-22   | 5.5         | 3GB        | iOS 11.0    | No          |
| **4** | iPhone X       | 2017-11-03   | 5.8         | 3GB        | iOS 11.0    | Yes         |
| **5** | iPhone XS      | 2018-09-21   | 5.8         | 4GB        | iOS 12.0    | Yes         |
| **6** | iPhone XS Max  | 2018-09-21   | 6.5         | 4GB        | iOS 12.0    | Yes         |

If you use rede_csv()functions, the first row will be considered as a header.
If the csv file has no header, you have to do like

```python
iphone_df = pd.read_csv("data/csvfile.csv", header=None)
```

and you may notice that there is Unnamed header. If you see the csv file, first column of the header is empty, so that is why you got Unnamed. I wanted to give the first column as index.

```python
iphone_df = pd.read_csv("data/csvfile.csv", index_col=0)
```

then you will get this frame

|                   | **released** | **display** | **memory** | **version** | **Face ID** |
| ----------------- | ------------ | ----------- | ---------- | ----------- | ----------- |
| **iPhone 7**      | 2016-09-16   | 4.7         | 2GB        | iOS 10.0    | No          |
| **iPhone 7 Plus** | 2016-09-16   | 5.5         | 3GB        | iOS 10.0    | No          |
| **iPhone 8**      | 2017-09-22   | 4.7         | 2GB        | iOS 11.0    | No          |
| **iPhone 8 Plus** | 2017-09-22   | 5.5         | 3GB        | iOS 11.0    | No          |
| **iPhone X**      | 2017-11-03   | 5.8         | 3GB        | iOS 11.0    | Yes         |
| **iPhone XS**     | 2018-09-21   | 5.8         | 4GB        | iOS 12.0    | Yes         |
| **iPhone XS Max** | 2018-09-21   | 6.5         | 4GB        | iOS 12.0    | Yes         |

### Indexing

You can access the data

Getting one data source

```python
iphone_df.loc["iPhone 7", "released"]
# 2016-09-16
```

Getting all chosen row

```python
iphone_df.loc["iPhone 7"]
# or
iphone_df.loc["iPhone 7", :]

# released        2016-09-16
# display             4.7
# memory               2GB
# version        iOS 10.0
# Face ID            No
# Name: iPhone 7, dtype: object
```

Getting all chosen column

```python
iphone_df["display"]
# or
iphone_df.loc[:, "display"]

# iPhone 7         4.7
# iPhone 7 Plus    5.5
# iPhone 8         4.7
# iPhone 8 Plus    5.5
# iPhone X         5.8
# iPhone XS        5.8
# iPhone XS Max    6.5
# Name: display, dtype: float64
```

Getting multiple rows

```python
iphone_df.loc[["iPhone 7", "iPhone 7 Plus"]]
```

output

|                   | **released** | **display** | **memory** | **version** | **Face ID** |
| ----------------- | ------------ | ----------- | ---------- | ----------- | ----------- |
| **iPhone 7**      | 2016-09-16   | 4.7         | 2GB        | iOS 10.0    | No          |
| **iPhone 7 Plus** | 2016-09-16   | 5.5         | 3GB        | iOS 10.0    | No          |

Getting multiple columns also same idea(without loc).

Getting multiple rows and columns using slicing

```python
iphone_df.loc["iPhone 7":"iPhone X", "released":"memory"]
```

output

|                   | **released** | **display** | **memory** |
| ----------------- | ------------ | ----------- | ---------- |
| **iPhone 7**      | 2016-09-16   | 4.7         | 2GB        |
| **iPhone 7 Plus** | 2016-09-16   | 5.5         | 3GB        |
| **iPhone 8**      | 2017-09-22   | 4.7         | 2GB        |
| **iPhone 8 Plus** | 2017-09-22   | 5.5         | 3GB        |
| **iPhone X**      | 2017-11-03   | 5.8         | 3GB        |

Getting data using boolean methods

```python
condition = (iphone_df["display"] > 5) & (iphone_df["Face ID"] == "YES")
# iPhone 7         False
# iPhone 7 Plus    False
# iPhone 8         False
# iPhone 8 Plus    False
# iPhone X         False
# iPhone XS        False
# iPhone XS Max    False
# dtype: bool

iphone_df.loc[condition]
```

output

|                   | **released** | **display** | **memory** | **version** | **Face ID** |
| ----------------- | ------------ | ----------- | ---------- | ----------- | ----------- |
| **iPhone X**      | 2017-11-03   | 5.8         | 3GB        | iOS 11.0    | Yes         |
| **iPhone XS**     | 2018-09-21   | 5.8         | 4GB        | iOS 12.0    | Yes         |
| **iPhone XS Max** | 2018-09-21   | 6.5         | 4GB        | iOS 12.0    | Yes         |

#### Indexing Table

Here is a table of indexing syntax

##### Indexing by Name

|                       | Basic Form                            | Shortcut Form                  |
| --------------------- | ------------------------------------- | ------------------------------ |
| Single row by name    | `df.loc["row4"]`                      |
| List of row names     | `df.loc[["row4", "row5", "row3"]]`    |
| Slicing row names     | `df.loc["row2":"row5"]`               | `df["row2":"row5"]`            |
| Single column by name | `df.loc[:, "col1"]`                   | `df["col1"]`                   |
| List of column names  | `df.loc[:, ["col4", "col6", "col3"]]` | `df[["col4", "col6", "col3"]]` |
| Slicing column names  | `df.loc[:, "col2":"col5"]`            |                                |

##### Indexing by Position

|                           | Basic Form              | Shortcut Form |
| ------------------------- | ----------------------- | ------------- |
| Single row by position    | `df.iloc[8]`            |               |
| List of row positions     | `df.iloc[[4, 5, 3]]`    |               |
| Slicing row positions     | `df.iloc[2:5]`          | `df[2:5]`     |
| Single column by position | `df.iloc[:, 3]`         |               |
| List of column positions  | `df.iloc[:, [3, 5, 6]]` |               |
| Slicing column positions  | `df.iloc[:, 3:7]`       |               |

### Handling DataFrame

#### Modify

```python
# modify one element
iphone_df.loc['iPhone 7', "memory"] = '2.5GB'

# modify one row
iphone_df.loc['iPhone 8'] = ['2015-09-22', '4.7', '2.5GB', 'ios 11.0', 'No']

# modify one column
iphone_df['display'] = ['4.5 in' '4.7 in'...]
ipohne_df['Face ID'] = 'Yes' # will be modified all rows to 'Yes'

# modify multiple rows
iphone_df.loc[['iphone 7', 'iphone 8']] = 'a'
iphone_df.loc['iphone 7' : 'iphone 8'] = 'a'
```

#### Add, Delete

##### Add

```python
# will be added end of the row
iphone_df.loc['iPhone XR'] = ['2017-11-03', '5.8', '3GB', 'iOS 11.0', 'Yes']

# will be added end of the column
iphone_df['Company'] = 'Apple'
```

##### Delete

```python
# delete selected row
iphone_df.drop('iPhone XR', axis='index', inplace=True)

# delete selected column
iphone_df.drop('Company', axis='columns', inplace=True)
```

if inplace=False, the original data frame will not be affected.

#### Rename index/column

```python
# this create new data frame
iphone_df.rename(columns={'released' : 'Released', 'display' : 'Display'...})

# this modify the original data frame
iphone_df.rename(columns={'released': 'Released', 'display' : 'Display'...}, inplace=True)

# naming index name
iphone_df.index.name = 'Model Name'
```

### Big DataFrame

#### Get Data From Top or Bottom

```python
iphone_df.head(3) # top 3
iphone_df.tail(3) # bottom 3
```

|       | Unnamed: 0    | released   | display | memory | version  | Face ID |
| ----- | ------------- | ---------- | ------- | ------ | -------- | ------- |
| **0** | iPhone 7      | 2016-09-16 | 4.7     | 2GB    | iOS 10.0 | No      |
| **1** | iPhone 7 Plus | 2016-09-16 | 5.5     | 3GB    | iOS 10.0 | No      |
| **2** | iPhone 8      | 2017-09-22 | 4.7     | 2GB    | iOS 11.0 | No      |

|       | Unnamed: 0    | released   | display | memory | version  | Face ID |
| ----- | ------------- | ---------- | ------- | ------ | -------- | ------- |
| **4** | iPhone X      | 2017-11-03 | 5.8     | 3GB    | iOS 11.0 | Yes     |
| **5** | iPhone XS     | 2018-09-21 | 5.8     | 4GB    | iOS 12.0 | Yes     |
| **6** | iPhone XS Max | 2018-09-21 | 6.5     | 4GB    | iOS 12.0 | Yes     |

```python
iphone_df.shape # (n rows, n columns)
```

#### Get Information of the DataFrame

```python
iphone_df.info()
```

```txt
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 7 entries, 0 to 6
Data columns (total 7 columns):
 #   Column       Non-Null Count  Dtype
---  ------       --------------  -----
 0   Unnamed: 0   7 non-null      object
 1   released     7 non-null      object
 2   display      7 non-null      float64
 3   memory       7 non-null      object
 4   version      7 non-null      object
 5   Face ID      7 non-null      object
dtypes: float64(1), object(6)
memory usage: 520.0+ bytes
```

```python
iphone_df.describe()
```

Returns columns that consisting only of numbers.

|       | display  |
| ----- | -------- |
| count | 7.000000 |
| mean  | 5.357143 |
| std   | 0.687871 |
| min   | 4.700000 |
| 25%   | 4.700000 |
| 50%   | 5.500000 |
| 75%   | 5.800000 |
| max   | 6.500000 |

#### Sort the DataFrame

```python
iphone_df.sort_values(by='memory', ascending=True, inplace=True)
```
