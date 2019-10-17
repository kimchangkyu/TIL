## Start Python

## 1. Numpy

1. Packages that quickly compute linear algebra
2. import numpy as np
3. np.array(iterable) - create matrix
4. numpy random
    - seed : Random value
    - rand : Generate random values with uniform distribution
    - randn : Generate random values with normal distribution
    - randint : Randomly generate integer values with uniform distribution
    - shuffle : Shuffle the matrix data
    - choice : Select data with a certain probability
5. Join Matrix Data
    - np.concatenate((ndarray, ndarray))
    - np.c_[ndarray, ndarray]
    - np.r_[ndarray, ndarray]

## 2. Pandas

1. Easy to use, high performance open source for data analysis
2. import pandas as pd
3. Series
    - It has the same data type value.
    - pd.Series() - create Series
    - data type consisting of index and value
4. DataFrame
    - Composed of several series
    - pd.DataFrame() - create DataFrame
    - Value values in the same column have the same data type.
5. apply function
6. append function
    - Merging Data Frames
    - <DataFrame>.append(<DataFrame>)
    	- ignore_index = True : Reorder Index
    - reset_index : After append, Reorder Index - <DataFrame>.reset_index()
7. concat function
    - Used to combine data frames into rows or columns
    - pd.concat([DataFrame, DataFrame]).reset_index(drop=True)
    - pd.concat([DataFrame, DataFrame], axis = 1)
8. groupby function
    - How to combine duplicate data in a specific column to create a new dataframe
    - DataFrame.groupby(columnname)
    	- .size() - count
9. DF.describe()
    - Function summarizing data

## TODO

1. numpy and pandas study
2. math study
3. practice algorithm
