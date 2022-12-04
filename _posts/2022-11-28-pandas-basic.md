---
layout: post
title:  "Pandas 101"
date:   2022-28-28 22:00:00 +0700
categories: [datascience]
---

# What Pandas is
Pandas is python library for data analysis. Its name came from "panel data". We can import data from various source into datastructure so called "DataFrame" and do computation/manipulation operations on them as we wish.

# The basics
- DataFrame is the core class which consists Series(similiar to column)
- Series is column of DataFrame

# Read/Access operaions
## Useful method to display information
```python
df.head() 
# display first n rows (default 5)
df.tail() 
# display last n rows (default 5)
df.info() 
# display concise summary sucj as columns name, data type, memory usage
df.columns # this is not method
# display all columns label
```

## Read methods
Data access mental model is similar to how we access data on DB table. We can select row(s) or column(s), also apply filter condition.

The data example 
| first | last | email |
|-----|-------|-------|
| Klur | Vinci | kl@gmail.com |
| Dao | Vinci | dao@email.com |
| John | Cater | jc@email.com |
| Java | Scala | js@email.com |

```python
# select a column
df['first'] # or 
df.first
# select columns
df[['first', 'last']]

# select a row
index = 0 
df.loc[index] # or 
df.iloc[index] 
# select rows
df.loc[[0,1]] # or 
df.iloc[[0,1]]

# select portion of DataFrame
# df.loc[row(s), col(s)]
df.loc[0, ['first', 'last']] # or
df.iloc[0, [0, 1]]

df.loc[[0,1], ['first', 'email']] # or
df.iloc[[0,1], [0,2]]

# or with slice operator to do range select
df.loc[0:2, 'first':'email'] 
```

## loc vs iloc method
Both method usage are the same, are used to access portion of Dataframe by row(s) or column(s). The difference is the parameters. ```loc``` accessor parameters are label(s) whereas ```iloc``` accessor parameters are index based.

## Filtering row
We can pass Series of boolean to select rows as we want. To create boolean Series, we do as the following
```python
filter = df['last'] == 'Vinci'
df[filter] # select all column
df.loc[filter, ['first', 'last']]  # select only 2 columns
```

# Update
```python
# Update a single cell
df.at[0, 'first'] = 'Klur2' # or
df.loc[0, 'first'] = 'Klur2'

## Update schema
## Add/Drop column
df['middle'] = "init middle"
df.drop(columns=['middle'], inplace=True)
```

## The official cheat sheet from Pandas
https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf
