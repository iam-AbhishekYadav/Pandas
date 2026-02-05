# # What is Pnadas ? 

- Pandas is a fast, powerful, flexible and easy to use open source data analysis and manipulation tool, built on top of the Python programming language.
- `Documentation` - https://pandas.pydata.org/about/index.html

## Importing Pandas

``` py
import numpy as np                # Recommended
import pandas as pd
```

---

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
  - **Syntax** - `series.squeeze(axis)`
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

``` py
vk = pd.read_csv('kohli_ipl.csv', index_col='match_no').squeeze("columns")
vk

movies = pd.read_csv('bollywood.csv',index_col='movie').squeeze("columns")
movies
```

**(i) `head()`**  

- Return the first n rows.
- **Syntax** - `series.head(n)`
- **Parameters** (n): int, default 5

``` py
vk.head(3)

# Output

match_no
1     1
2    23
3    13
Name: runs, dtype: int64
```

**(ii) `tail()`**  

- Return the last n rows.
- **Syntax** - `series.tail(n)`
- **Parameters** (n): int, default 5

``` py
vk.tail(3)

match_no
213    73
214    25
215     7
Name: runs, dtype: int64
```

**(iii) `sample()`**

- Return a random sample of items from an axis of object.
- **Syntax** - `series.sample(n)`
- **Parametrs** (n): int, float, bool (default false)

``` py
vk.sample(5)    # Output : 5 Random items from data
```

**(iv) `value_count()`**

- Return a Series containing counts of unique values.
- **Syntax** - `series.value_counts()`
- **Parametrs**: bool (default false)

``` py
movies.value_counts()

# Output

lead
Akshay Kumar        48
Amitabh Bachchan    45
Ajay Devgn          38
Salman Khan         31
Sanjay Dutt         26
                    ..
Diganth              1
Parveen Kaur         1
Seema Azmi           1
Akanksha Puri        1
Edwin Fernandes      1
Name: count, Length: 566, dtype: int64
```

**(v) `sort_values()`**

- Sort a Series in ascending or descending order by some criterion.
- **Syntax** - `series.sort_values()`
- **Parametrs**: 0 or index, inplace, ascending (bool or list of bools, default True)
  - **inplace** - Update the original series permanently

``` py
vk.sort_values(ascending=False)           # Sort in Descending order

# Output

match_no
128    113
126    109
123    108
164    100
120    100
      ... 
93       0
211      0
130      0
8        0
135      0
Name: runs, Length: 215, dtype: int64
```

**(vi) `sort_index()`**

- Returns a new Series sorted by label if inplace argument is False.
- **Symtax** - `series.sort_index`
- **Parametrs**: 0 or index, inplace, ascending (bool or list-like of bools, default True)

``` py
movies.sort_index(ascending=True)                       # Sort Index column


# Output

movie
1920 (film)                   Rajniesh Duggall
1920: London                     Sharman Joshi
1920: The Evil Returns             Vicky Ahuja
1971 (2007 film)                Manoj Bajpayee
2 States (2014 film)              Arjun Kapoor
                                   ...        
Zindagi 50-50                      Veena Malik
Zindagi Na Milegi Dobara        Hrithik Roshan
Zindagi Tere Naam           Mithun Chakraborty
Zokkomon                       Darsheel Safary
Zor Lagaa Ke...Haiya!            Meghan Jadhav
Name: lead, Length: 1500, dtype: object
```
---

## Series Maths Method

``` py
vk = pd.read_csv('kohli_ipl.csv', index_col='match_no').squeeze("columns")
vk

movies = pd.read_csv('bollywood.csv',index_col='movie').squeeze("columns")
movies

subs = pd.read_csv('Data/subs.csv').squeeze("columns")
subs
```

**(i) `count()`**

- Return number of non-NA(Not Available/Not Applicable)/null observations in the Series.
- **Syntax** - `Series.count()`

``` py
vk.count()                    # Output : 215 (No. of matches played by VK)
```

**(ii) `sum()`**

- Return the sum of the values over the requested axis.
- **Syntax** - `Series.sum()`
- **Parametrs**: axis:{index (0)} 

``` py
subs.sum()                   # Outputr : 49510
```

**(iii) `product()`**

- Return the product  of the values over the requested axis.
- **Syntax** - `Series.product()`
- **Parametrs**: axis:{index (0)} 

``` py
subs.product ()                   # Outputr : 0  (There was a 0 in the middle of the data.)
```

**(iii) `mean(), median(), mode()`**

- They all Return the mean/median/mode of the values over the requested axis.
- **`Mean`** : The average of all numbers.
- **`Median`** : The middle value when numbers are arranged in order.
- **`Mode`** : The value that appears most frequently in the data.
- **Syntax** -
  - Mean : `Series.mean()`
  - Median : `Series.median()`
  - Mode : `Series.mode()`
- **Parametrs**: 
  - Mean : `axis:{index (0)}`
  - Median : `axis:{index (0)}`
  - Mode : `dropna: bool, default True`

``` py        
print(subs.mean())           # Outputr : 135.64383561643837
print(vk.median())           # Outputr : 24.0
print(movies.mode())         # Outputr : 0    Akshay Kumar
```



































