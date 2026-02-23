# # Data Structures / Objects in Pandas

# (2.) Pnadas DataFrame

- It is a two-dimensional table-like structure in Python where data is arranged in rows and columns.
- It can store different types of data such as numbers, text and dates across its columns.
- The main parts of a DataFrame are:
  - **Data** : Actual values in the table.
  - **Rows** : Labels that identify each row.
  - **Columns** : Labels that define each data category.


<img src="https://github.com/user-attachments/assets/d684b587-31a2-4fcd-9d66-3553c84b14fd" width="700" height="600">

---

## Creating of DataFrame

### (i) Using Lists

``` py
student_data = [[100,80,10],
                [90,70,7],
                [80,50,2],]

pd.DataFrame(student_data, columns=['IQ', 'Marks', 'Packages'])
```

### (ii) Using dict

``` py
student_dict = {'IQ': [100, 90, 120, 80],
                'Marks': [80, 70, 100, 50],
                'Packages': [10, 7, 14, 2]}

Students = pd.DataFrame(student_dict)
Students
```

> Output of (i) & (ii)

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>IQ</th>
      <th>Marks</th>
      <th>Packages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>100</td>
      <td>80</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>90</td>
      <td>70</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>120</td>
      <td>100</td>
      <td>14</td>
    </tr>
    <tr>
      <th>3</th>
      <td>80</td>
      <td>50</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>


### (iii) Using CSV

-  Reads a CSV file
- Converts it into a DataFrame
- It displays the DataFrame table

``` py
movies = pd.read_csv('movies.csv')
movies
```

## DataFrame Attributes and Methods

``` py
movies = pd.read_csv('movies.csv')
movies

ipl = pd.read_csv('ipl-matches.csv')
ipl
```

**(i) `shape`**

- Return a tuple representing the dimensionality of the DataFrame.
- **Syntax** : `DataFrame.shape`

``` py
movies.shape              # Output : (1629, 18)
ipl.shape                 # Output : (950, 20)
```

**(ii) `dtype`**

- Return the dtypes in the DataFrame.
- This returns a Series with the data type of each column.
- **Syntax** : `DataFrame.dtype`

``` py
movies.dtypes

# Output
title_x                 str
imdb_id                 str
poster_path             str
wiki_link               str
title_y                 str
original_title          str
is_adult              int64
year_of_release       int64
runtime                 str
genres                  str
imdb_rating         float64
imdb_votes            int64
story                   str
summary                 str
tagline                 str
actors                  str
wins_nominations        str
release_date            str
dtype: object
```

**(iii) `index`**

- The index of a DataFrame is a series of labels that identify each row.
- The labels can be integers, strings, or any other hashable type.
- **Syantax** : `DataFrame.index`

``` py
movies.index              # Output : RangeIndex(start=0, stop=1629, step=1)
ipl.index                 # Output : RangeIndex(start=0, stop=950, step=1)
```

**(iv) `columns`**

- This property holds the column names as a pandas Index object.
- It provides an immutable sequence of column labels that can be used for data selection, renaming, and alignment in DataFrame operations.
- **Syntax** : `DataFrame.columns`

``` py
movies.columns

# Output
Index(['title_x', 'imdb_id', 'poster_path', 'wiki_link', 'title_y',
       'original_title', 'is_adult', 'year_of_release', 'runtime', 'genres',
       'imdb_rating', 'imdb_votes', 'story', 'summary', 'tagline', 'actors',
       'wins_nominations', 'release_date'],
      dtype='str')
```

**(v) `values`**

- Returns 2D Numpy array
- **Syntax** : `DataFrame.values`

``` py
student_dict = {'IQ': [100, 90, 120, 80],
                'Marks': [80, 70, 100, 50],
                'Packages': [10, 7, 14, 2]}

Students = pd.DataFrame(student_dict)
Students.values

# Output
array([[100,  80,  10],
       [ 90,  70,   7],
       [120, 100,  14],
       [ 80,  50,   2]])
```

**(vi) `head and tail`**

- **head** : Return the first n rows.
- **tail** : Return the last n rows.
- Default n is 5 in both head and tail
- **Syntax** :
  - DataFrame.head(n=5)
  - DataFrame.tail(n=5)

``` py
movies.head()                  # Output : Gives first 5 rows
movies.tail()                  # Output : Gives last 5 rows
```















