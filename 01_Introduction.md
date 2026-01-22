# # Whai is Pnadas ? 

- Pandas is a fast, powerful, flexible and easy to use open source data analysis and manipulation tool, built on top of the Python programming language.
- `Documentation` - https://pandas.pydata.org/about/index.html

## Importing Pandas

``` py
import numpy as np                # Recommended
import pandas as pd
```


# # Data Structures / Objects in Pandas

## (1.) Pandas Series

- A Pandas Series is like a column in a table. It is a 1-D array holding data of any type.
- Key Features of Pandas Series:
  - Supports integer-based and label-based indexing.
  - Stores heterogeneous data types.
  - Offers a variety of built-in methods for data manipulation and analysis.

---

## Accessing elements of Series

### (i) Position-based Indexing

- In order to access the series element refers to the index number.
- Use the index operator []to access an element in a series.
- The index must be an integer.

``` py
import pandas as pd
import numpy as np

data = np.array(['g','e','e','k','s','f', 'o','r','g','e','e','k','s'])
ser = pd.Series(data)

print(ser[:5])

# Output

0    g
1    e
2    e
3    k
4    s
dtype: object

```

### (ii) Label-based Indexing

- In order to access an element from series, we have to set values by index label.
- A Series is like a fixed-size dictionary in that we can get and set values by index label.

``` py
import pandas as pd
import numpy as np

data = np.array(['g','e','e','k','s','f', 'o','r','g','e','e','k','s'])
ser = pd.Series(data,index=[10,11,12,13,14,15,16,17,18,19,20,21,22])

print(ser[16])                                     # Output : o
```

---

## Series from lists

### (i) String Series

``` py
import numpy as np                # Recommended
import pandas as pd

country = ['India' , 'Pakistan' , 'USA' , 'Srilanka']
pd.Series(country)

# Output

0       India
1    Pakistan
2         USA
3    Srilanka
dtype: object
```

### (ii) Integer Series

``` py
runs = [13,24,56,78,100]
pd.Series(runs)

# Output

0     13
1     24
2     56
3     78
4    100
dtype: int64
```

### (iii) Custom Index Series

``` py
marks = [67,57,89,100]
subjects = ['maths','english','science','hindi']

pd.Series(marks,index=subjects)

# Output

maths       67
english     57
science     89
hindi      100
dtype: int64
```

### (iv) Setting a Name of Series

``` py
marks = [67,57,89,100]
subjects = ['maths','english','science','hindi']

pd.Series(marks,index=subjects, name='Nitish ke marks')

# Output

maths       67
english     57
science     89
hindi      100
Name: Nitish ke marks, dtype: int64
```

---

## Series from Dictionary

``` py
marks = {
    'maths':67,
    'english':57,
    'science':89,
    'hindi':100
}

marks_series = pd.Series(marks,name='nitish ke marks')
marks_series

# Output

maths       67
english     57
science     89
hindi      100
Name: nitish ke marks, dtype: int64
```

---

## Series Attributes

``` py
marks = {
    'maths':67,
    'english':57,
    'science':89,
    'hindi':100
}

marks_series = pd.Series(marks,name='nitish ke marks')
marks_series
```

**(i) `Size`** - Return the number of elements in the underlying data.
``` py
marks_series.size              # Output : 4
```
  

**(ii) `dtype`** - Return the dtype object of the underlying data.
``` py
marks_series.dtype             # Output : dtype('int64')
```

**(iii) `name`** - Return the name of the Series.
``` py
marks_series.name              # Output : nitish ke marks
```

**(iv) `is_unique`** - Return True if values in the object are unique.
``` py
marks_series.is_unique        # Output : True
```

**(v) `index`** - Generate Index values in a range
``` py
marks_series.index            # Output : Index(['maths', 'english', 'science', 'hindi'], dtype='object')
```

**(vi) `values`** - Return Series as ndarray or ndarray-like depending on the dtype.
``` py
marks_series.values           # Output : array([ 67,  57,  89, 100])
```

---

## Series using read_CSV

- Upload file CSV in Project folder.
- **`Squeeze`** -
  - **Syntax** - dataframe.squeeze(axis)
  - This method is most useful when you don’t know if your object is a Series or DataFrame, but you do know it has just a single column.
  - In that case you can safely call squeeze to ensure you have a Series.
  - **Parameter** - axis{0 or ‘index’, 1 or ‘columns’, None}, default None
  - **Returns** - DataFrame, Series, or scalar

``` py
pd.read_csv('filePath.csv').squeeze("columns")
```

### Example :-

> Upload CSV file of Virat Kholi Data in Project folder.  
> Data : How many runs has Virat kholi scored in each IPL match ?  
> **index_col** - It selects Index Coloumn  

``` py
vk = pd.read_csv('kohli_ipl.csv',index_col='match_no').squeeze('columns')
vk

# Output

match_no
1       1
2      23
3      13
4      12
5       1
       ..
211     0
212    20
213    73
214    25
215     7
Name: runs, Length: 215, dtype: int64
```

---

## Series Methods

















