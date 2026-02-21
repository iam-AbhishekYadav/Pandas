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
subs.sum()                   # Output : 49510
```

**(iii) `product()`**

- Return the product  of the values over the requested axis.
- **Syntax** - `Series.product()`
- **Parametrs**: axis:{index (0)} 

``` py
subs.product ()                   # Output : 0  (There was a 0 in the middle of the data.)
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
print(subs.mean())           # Output : 135.64383561643837
print(vk.median())           # Output : 24.0
print(movies.mode())         # Output : 0    Akshay Kumar
```


**(iv) `std()`**

- **`Standard Deviation`** : It shows how spread out the numbers are from the mean (average).
  - **`Low standard deviation`** : values are close to the mean
  - **`High standard deviation`** : values are far from the mean
- **Syntax** - `Series.std()`

``` py
subs.std()           # Output : 62.6750230372527
```

**(v) `var()`**

- **`Variance`** : It measures how much the data values spread out from the mean.
  - **`Low standard deviation`** : values are close to the mean
  - **`High standard deviation`** : values are far from the mean
- **Syntax** - `Series.var()`
- **Parametrs**: axis:{index (0)} 

``` py
vk.var()           # Output : 688.0024777222343
```

**(vi) `min(), max()`**

- Return the minimum/maximum of the values over the requested axis.
- **Syntax** -
  - **Minimum** : `Series.min()`
  - **Maximum** : `Series.max()`

- **Parametrs**: axis:{index (0)} 

``` py
print(vk.min())         # Output : 0
print(vk.max())         # Output : 113
```

**(vii) `describe()`**

- Generate descriptive statistics.
- **Syntax** - `Series.describe()`

``` py
vk.describe()

# Output

count    215.000000
mean      30.855814
std       26.229801
min        0.000000
25%        9.000000
50%       24.000000
75%       48.000000
max      113.000000
Name: runs, dtype: float64
```

---


## Series Indexing

``` py
vk = pd.read_csv('kohli_ipl.csv', index_col='match_no').squeeze("columns")
vk

movies = pd.read_csv('bollywood.csv',index_col='movie').squeeze("columns")
movies

subs = pd.read_csv('Data/subs.csv').squeeze("columns")
subs
```

**(i) `Integer Indexing`**

**(ii) `Negative Indexing`**

**(iii) `Slicing`**

- Selecting a portion of values from a Series using index position or label.

> Index Position
``` py
vk[5:16]                         # How many runs VK scored in between 5 to 15 matches

# Output

match_no
6      9
7     34
8      0
9     21
10     3
11    10
12    38
13     3
14    11
15    50
16     2
Name: runs, dtype: int64
```

> Lalel
``` py
movies['Hum Tumhare Hain Sanam']                # Output : 'Shah Rukh Khan'
```

**(iv) `Negative Slicing`**

- It allowing you to select elements from the end of a Series.

``` py
vk[-5:]                         # How many runs VK scored in last 5 matches

# Output

match_no
211     0
212    20
213    73
214    25
215     7
Name: runs, dtype: int64
```

**(v) `Fancy Indexing`**

- Selecting multiple specific elements from a Series using a list of indices or labels.

``` py
vk[[1,3,5,7,9]]                         # How many runs VK scored in 1st, 3rd, 5th, 7th, 9th match

# Output

match_no
1     1
3    13
5     1
7    34
9    21
Name: runs, dtype: int64
```

---


## Series Indexing

``` py
marks = [67,57,89,100] 
subjects = ['maths','english','science','hindi'] 
marks_series = pd.Series(marks,index=subjects, name='Sachin ke marks')
marks_series

runs = [13,24,56,78,100]
runs_ser = pd.Series(runs)
runs_ser

movies = pd.read_csv('bollywood.csv',index_col='movie').squeeze("columns")
movies
```

**(i) `Using Indexing`**

``` py
marks_series.iloc[1] = 100 
marks_series

# Output

maths       67
english    100
science     89
hindi      100
Name: Sachin ke marks, dtype: int64
```

**(ii) `What if an index does not exist`**

``` py
marks_series['sst'] = 75
marks_series

# Output

maths       67
english    100
science     89
hindi      100
sst         75
Name: Sachin ke marks, dtype: int64
```

**(iii) `Slicing`**

``` py
runs_ser[2:4] = [100,100]
runs_ser

# Output

0     13
1     24
2    100
3    100
4    100
dtype: int64
```

**(iv) `Fancy Indexing`**

``` py
runs_ser[[0,3,4]] = [0,0,0]
runs_ser

# Output

0      0
1     24
2    100
3      0
4      0
dtype: int64
```

**(vi) `Using Index Label`**

``` py
movies['Aankhen (2002 film)'] = 'Alia Bhatt'
movies

# Output

movie
Uri: The Surgical Strike                   Vicky Kaushal
Battalion 609                                Vicky Ahuja
The Accidental Prime Minister (film)         Anupam Kher
Why Cheat India                            Emraan Hashmi
Evening Shadows                         Mona Ambegaonkar
                                              ...       
Hum Tumhare Hain Sanam                    Shah Rukh Khan
Aankhen (2002 film)                           Alia Bhatt                    ---> Amitabh Bachchan to Alia Bhatt
Saathiya (film)                             Vivek Oberoi
Company (film)                                Ajay Devgn
Awara Paagal Deewana                        Akshay Kumar
Name: lead, Length: 1500, dtype: str
```

---

## Series Python Functionalities


``` py
vk = pd.read_csv('kohli_ipl.csv', index_col='match_no').squeeze("columns")
vk

movies = pd.read_csv('bollywood.csv',index_col='movie').squeeze("columns")
movies

subs = pd.read_csv('Data/subs.csv').squeeze("columns")
subs

marks = [67,57,89,100] 
subjects = ['maths','english','science','hindi'] 
marks_series = pd.Series(marks,index=subjects, name='Sachin ke marks')
marks_series
```

**(i) `len()`** --> It returns the number of items (length) in an object.  
**(ii) `type()`** --> It returns the data type of a variable or object.  
**(iii) `dir()`** --> It returns a list of all attributes and methods of an object.  
**(iv) `sorted()`** --> It returns a new sorted list from any iterable (like list, tuple, string, dictionary).  
**(v) `max()`** --> It returns the largest value.  
**(vi) `min()`** --> It returns the smallest value.  

``` py
print(len(subs))                      # Output : 365
print(type(subs))                     # Output : <class 'pandas.Series'>
print(dir(subs))                      # Output : ['T', '_AXIS_LEN', '_AXIS_ORDERS', '_AXIS_TO_AXIS_NUMBER'....]
print(sorted(subs))                   # Output : [33, 33, 35, 37, 39, 40, ..... 290, 295, 301, 306, 312, 396]
print(min(subs))                      # Output : 33
print(max(subs))                      # Output : 396
```

**(vii) `type conversion`** 

- Type conversion means changing one data type into another.
- There are two types
  - Implicit Type Conversion (automatic)
  - Explicit Type Conversion (manual) 

``` py
list(marks_series)                       # Output : [67, 57, 89, 100]

dict(marks_series.index)                 # Output : ['maths', 'english', 'science', 'hindi']

dict(marks_series)                       # Output : {'maths': 67,
                                         #           'english': 57,
                                         #           'science': 89,
                                         #           'hindi': 100}
```


**(viii) `membership operator`**

- Membership Operator is `in` or `not in`
- It is used to check whether a value exists inside a Series.

``` py
'Hum Tumhare Hain Sanam' in movies            # Output : True 

'Shah Rukh Khan' in movies.values             # Output : True
```


**(ix) `looping`**

- It is used when we know how many times to repeat.

``` py
for i in movies:
  print(i)                             # Output : Print all movies form data

for j in movies.index:
  print(j)                             # Output : Print all actors name (index values) form data
```


**(x) `Arithmetic Operator`**

- It is used to perform mathematical calculations.

``` py
100 + marks_series

# Output

maths      167
english    157
science    189
hindi      200
Name: Sachin ke marks, dtype: int64
```

**(xi) `Relational Operators`**

- It is used to compare two values.
- It return a Boolean result: True or False.

``` py
vk >=50

# Output

match_no
1      False
2      False
3      False
       ...  
213     True
214    False
215    False
Name: runs, Length: 215, dtype: bool
```

---

## Boolean Indexing on Series

``` py
vk = pd.read_csv('kohli_ipl.csv', index_col='match_no').squeeze("columns")
vk

movies = pd.read_csv('bollywood.csv',index_col='movie').squeeze("columns")
movies

subs = pd.read_csv('subs.csv').squeeze("columns")
subs
```

**(i) `Find no. of 50's and 100's scored by Kholi`**

``` py
vk[vk >= 50]                   # Output : Gives list of 50's and 100's scored by Kholi
vk[vk >= 50].size              # Output : 50
```

**(ii) `Find the number of ducks`**

``` py
vk[vk == 0]                 # Output : Gives list of 0's scored by Kholi
vk[vk == 0].size            # Output : 9
```

**(iii) `Count number of days when I had more than 200 subscibers a day`**

``` py
subs[subs > 200].size       # Output : 59
```

**(iv) `Find actors who have done more than 20 movies`**

``` py
num_movies = movies.value_counts()
num_movies[num_movies > 20]

# Output

lead
Akshay Kumar        48
Amitabh Bachchan    45
Ajay Devgn          38
Salman Khan         31
Sanjay Dutt         26
Shah Rukh Khan      22
Emraan Hashmi       21
Name: count, dtype: int64
```

---

## Plotting Graphs on Series

**(i) `2D Chart`**

``` py
subs.plot()            # Output : Give a Graph
```

<img src="https://github.com/user-attachments/assets/3e768ea5-3d49-429e-88b9-7f5604f7a82e" width="550" height="400" />

**(ii) `Bar Chat`**

``` py
movies.value_counts().head(20).plot(kind='bar')         # Output : Gives a Bar chat of top 20 actors with most movies done
```

<img src="https://github.com/user-attachments/assets/4e6f0b3d-9c73-499f-a9a9-faca6e554709" width="550" height="400" />

**(iii) `Pie Chat`**

``` py
movies.value_counts().head(20).plot(kind='pie')         # Output : Gives a Pie chat of top 20 actors with most movies done
```

<img src="https://github.com/user-attachments/assets/66cb1a06-a6c0-4867-a637-673ee45e0217" width="550" height="400" />

---

# # Some Important Series Methods 

``` py
vk = pd.read_csv('kohli_ipl.csv', index_col='match_no').squeeze("columns")
vk

movies = pd.read_csv('bollywood.csv',index_col='movie').squeeze("columns")
movies

subs = pd.read_csv('subs.csv').squeeze("columns")
subs
```

**(i) `astype()`**

- It is is used to change the data type of a Pandas Series.
- It helps reduce memory usage
- It Ensures correct calculations.

``` py
import sys

sys.getsizeof(vk)                              # Output : 1884

vk.astype('int16')                             # Output : Change dtype to int16
sys.getsizeof(vk.astype('int16'))              # Output : 594
```

**(ii) `between()`**

- It is used to check whether values in a Series fall within a specified range.
- It returns a Boolean Series (True / False).
- **Syntax** : `Series.between(left, right, inclusive='both')`
  - **left** → lower limit
  - **right** → upper limit
  - **inclusive** → include boundaries or not

``` py
vk.between(50,99)

# Output
match_no
1      False
2      False
3      False
       ...  
214    False
215    False
Name: runs, Length: 215, dtype: bool

vk[vk.between(50,99)]

# Output
match_no
15     50
34     58
41     71
...
197    51
198    53
209    58
213    73
Name: runs, dtype: int64

vk[vk.between(50,99)].size        # Output : 45
```

**(iii) `clip()`**

- It is used to limit (cap) values within a specified range.
- If a value is:
  - Below the minimum → it becomes the minimum
  - Above the maximum → it becomes the maximum
- **Syntax** - `Series.clip(lower=None, upper=None)`


``` py
subs.clip(100,200)

# Output
0      100
1      100
2      100
3      100
4      100
      ... 
360    200
361    200
362    155
363    144
364    172
Name: Subscribers gained, Length: 365, dtype: int64
```

**(iv) `drop_duplicates()`**

- It removes repeated values from a Series and keeps only unique ones (based on your settings).
- **Syntax** : `Series.drop_duplicates(subset=None, keep='first', inplace=False)`
  - **subset** → column(s) to check duplicates
  - **keep** → which duplicate to keep ('first', 'last', False)
  - **inplace** → modify original data (True or False)

``` py
temp = pd.Series([1,1,2,2,3,3,4,4,5,5])
temp

# Output
0    1
1    1
2    2
3    2
4    3
5    3
6    4
7    4
8    5
9    5
dtype: int64

temp.drop_duplicates()

# Output
0    1
2    2
4    3
6    4
8    5
dtype: int64

temp.drop_duplicates(keep='last')

# Output
1    1
3    2
5    3
7    4
9    5
dtype: int64
```

**(v) `duplicated()`**

- It is used to detect duplicate values in a Series.
- It returns a Boolean Series:
  - **True** → duplicate
  - **False** → not duplicate


``` py
temp = pd.Series([1,1,2,2,3,3,4,4,5,5])
temp

temp.duplicated()

# Output
0    False
1     True
2    False
3     True
4    False
5     True
6    False
7     True
8    False
9     True
dtype: bool

temp.duplicated().sum()              # Output : 5
```

**(vi) `isnull()`**

- It is used to detect missing (NaN) values in a Pandas Series.
- It returns a Boolean Series:
  - **True** → value is missing
  - **False** → value is not missing

``` py
temp = pd.Series([1,2,3,np.nan,5,6,np.nan,8,np.nan,10])
temp

temp.isnull()

# Output
0    False
1    False
2    False
3     True
4    False
5    False
6     True
7    False
8     True
9    False
dtype: bool

temp.isnull().sum()           # Output : 3
```

**(vii) `dropna()`**

 - It is used to remove missing (NaN) values from a Series.

``` py
temp = pd.Series([1,2,3,np.nan,5,6,np.nan,8,np.nan,10])
temp

temp.dropna()

# Output
0     1.0
1     2.0
2     3.0
4     5.0
5     6.0
7     8.0
9    10.0
dtype: float64
```

**(viii) `fillna()`**

-  It is used to replace missing (NaN) values in a Pandas Series.
-  It can be filled by Mean, Meadian, etc.
-  **Forward Fill (ffill)** - Copies the previous value down.
   - `Series.ffill()`
- **Backward Fill (bfill)** - Uses the next value.
  - `Series.bfill()`

``` py
temp = pd.Series([1,np.nan,3,np.nan,5])
temp

temp.fillna(0)

# Output
0    1.0
1    0.0
2    3.0
3    0.0
4    5.0
dtype: float64

temp.fillna(temp.mean())

# Output
0    1.0
1    1.0
2    3.0
3    3.0
4    5.0
dtype: float64

temp.ffill()

# Output
0    1.0
1    3.0
2    3.0
3    3.0
4    5.0
dtype: float64
```

**(ix) `isin()`**

- It is used to check whether each value in a Series exists in a given list (or another Series).
- It returns a Boolean Series:
  - True → value is present
  - False → value is not present

``` py
vk.isin([49, 99])               # Output : Gives boolean result

vk[vk.isin([49, 99])]

# Output
match_no
82    99
86    49
Name: runs, dtype: int64
```

**(x) `apply()`**

- It is used to apply a function to each value of a Pandas Series.
- It works like a loop, but in a cleaner way.
- **Syntax** - `Series.apply(function)`

``` py
movies.apply(lambda x: x.split(' ')[0].upper())                  # Output : Gives first name of actor in capital letters

# Output
movie
Uri: The Surgical Strike                  VICKY
Battalion 609                             VICKY
The Accidental Prime Minister (film)     ANUPAM
Why Cheat India                          EMRAAN
Evening Shadows                            MONA
                                         ...   
Hum Tumhare Hain Sanam                     SHAH
Aankhen (2002 film)                     AMITABH
Saathiya (film)                           VIVEK
Company (film)                             AJAY
Awara Paagal Deewana                     AKSHAY
Name: lead, Length: 1500, dtype: str
```

> The day you get more than average subscribers is a good day, otherwise it is a bad day.
``` py
subs.mean()                    # Output : 135.64383561643837

subs.apply(lambda x:'Good Day' if x>subs.mean() else 'Bad Day')

# Output
0       Bad Day
1       Bad Day
2       Bad Day
3       Bad Day
4       Bad Day
         ...   
360    Good Day
361    Good Day
362    Good Day
363    Good Day
364    Good Day
Name: Subscribers gained, Length: 365, dtype: str
```

**(xi) `copy()`**

- It is used to create a separate (independent) copy of a Series.
- This prevents changes in one variable from affecting the original data.
- Without copy(), two variables may refer to the same data in memory. 

> Without copy() (Problem)
``` py
s1 = pd.Series([10, 20, 30])
s2 = s1   # No copy

s2[0] = 100

print(s1)

# Output : Original s1 changed too!
0    100
1     20
2     30
dtype: int64
```

> With copy() (Correct Way)
``` py
s1 = pd.Series([10, 20, 30])
s2 = s1.copy()

s2[0] = 100

print(s1)

# Output : Now s1 remains unchanged.
0    10
1    20
2    30
dtype: int64
```


