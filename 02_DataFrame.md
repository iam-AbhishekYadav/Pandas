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

## # Creating of DataFrame

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

|   | IQ  | Marks | Packages |
|---|-----|-------|----------|
| 0 | 100 | 80    | 10       |
| 1 | 90  | 70    | 7        |
| 2 | 120 | 100   | 14       |
| 3 | 80  | 50    | 2        |


### (iii) Using CSV

-  Reads a CSV file
- Converts it into a DataFrame
- It displays the DataFrame table

``` py
movies = pd.read_csv('movies.csv')
movies
```

---

## # DataFrame Attributes and Methods

``` py
movies = pd.read_csv('movies.csv')
movies

ipl = pd.read_csv('ipl-matches.csv')
ipl
```

### (i) shape

- Return a tuple representing the dimensionality of the DataFrame.
- **Syntax** : `DataFrame.shape`

``` py
movies.shape              # Output : (1629, 18)
ipl.shape                 # Output : (950, 20)
```

### (ii) dtype

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

### (iii) index

- The index of a DataFrame is a series of labels that identify each row.
- The labels can be integers, strings, or any other hashable type.
- **Syantax** : `DataFrame.index`

``` py
movies.index              # Output : RangeIndex(start=0, stop=1629, step=1)
ipl.index                 # Output : RangeIndex(start=0, stop=950, step=1)
```

### (iv) columns

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

### (v) values

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

### (vi) head() and tail()

- **head()** : Return the first n rows.
- **tail()** : Return the last n rows.
- Default n is 5 in both head and tail
- **Syntax** :
  - DataFrame.head(n=5)
  - DataFrame.tail(n=5)

``` py
movies.head()                  # Output : Gives first 5 rows
movies.tail()                  # Output : Gives last 5 rows
```

### (vii) sample()

- Return a random sample of items from an axis of object.
- **Syntax** - `DataFrame.sample(n)`
- **Parametrs** (n): int, float, bool (default false)

``` py
movies.sample(5)    # Output : 5 Random items from data
```

### (viii) info()

- This method prints information about a DataFrame including the index dtype and columns, non-NA values and memory usage.
- **Synhtax** : `DataFrame.info()`

``` py
movies.info()

# Output
<class 'pandas.DataFrame'>
RangeIndex: 1629 entries, 0 to 1628
Data columns (total 18 columns):
 #   Column            Non-Null Count  Dtype  
---  ------            --------------  -----  
 0   title_x           1629 non-null   str    
 1   imdb_id           1629 non-null   str    
 2   poster_path       1526 non-null   str    
 3   wiki_link         1629 non-null   str    
 4   title_y           1629 non-null   str    
 5   original_title    1629 non-null   str    
 6   is_adult          1629 non-null   int64  
 7   year_of_release   1629 non-null   int64  
 8   runtime           1629 non-null   str    
 9   genres            1629 non-null   str    
 10  imdb_rating       1629 non-null   float64
 11  imdb_votes        1629 non-null   int64  
 12  story             1609 non-null   str    
 13  summary           1629 non-null   str    
 14  tagline           557 non-null    str    
 15  actors            1624 non-null   str    
 16  wins_nominations  707 non-null    str    
 17  release_date      1522 non-null   str    
dtypes: float64(1), int64(3), str(14)
memory usage: 229.2 KB
```

### (ix) describe()

- Generate descriptive statistics.
- **Syntax** - `DataFrame.describe()`

``` py
movies.describe()
```

> Output

|        | is_adult | year_of_release | imdb_rating | imdb_votes |
|--------|----------|----------------|------------|------------|
| count  | 1629.0   | 1629.000000    | 1629.000000| 1629.000000|
| mean   | 0.0      | 2010.263966    | 5.557459   | 5384.263352|
| std    | 0.0      | 5.381542       | 1.567609   | 14552.103231|
| min    | 0.0      | 2001.000000    | 0.000000   | 0.000000   |
| 25%    | 0.0      | 2005.000000    | 4.400000   | 233.000000 |
| 50%    | 0.0      | 2011.000000    | 5.600000   | 1000.000000|
| 75%    | 0.0      | 2015.000000    | 6.800000   | 4287.000000|
| max    | 0.0      | 2019.000000    | 9.400000   | 310481.000000|


### (x) isnull

- Detect missing values.
- Return a boolean same-sized object indicating if the values are NA.
- It returns a Boolean Series:
  - **True** → value is missing
  - **False** → value is not missing
- **Syntax** : `DataFrame.isnull`

``` py
movies.isnull()                         # Output : Gives True/False values
movies.isnull().sum()

# Output
title_x                0
imdb_id                0
poster_path          103
wiki_link              0
title_y                0
original_title         0
is_adult               0
year_of_release        0
runtime                0
genres                 0
imdb_rating            0
imdb_votes             0
story                 20
summary                0
tagline             1072
actors                 5
wins_nominations     922
release_date         107
dtype: int64
```

### (xi) duplicated()

- It is used to detect duplicate values(rows) in a DataFrame.
- It returns a Boolean DataFrame:
  - **True** → duplicate
  - **False** → not duplicate
- **Syntax** : `DataFrame.duplicated()`

``` py
movies.duplicated()

# Output
0       False
1       False
2       False
3       False
4       False
        ...  
1624    False
1625    False
1626    False
1627    False
1628    False
Length: 1629, dtype: bool

movies.duplicated().sum()                # Output : 0
```

### (xii) rename

- Rename columns or index labels.
- **Syntax** : `DataFrame.rename(columns={'old_name': 'new_name'}, inplace=True)`
  - inplace --> Change   original DataFrame and create a new cpoy

``` py
student_dict = {'IQ': [100, 90, 120, 80],
                'Marks': [80, 70, 100, 50],
                'Packages': [10, 7, 14, 2]}

Students = pd.DataFrame(student_dict)
Students

Students.rename(columns={'Marks': 'Percentage', 'Packages': 'LPA'})                           # Does not change in original value
Students.rename(columns={'Marks': 'Percentage', 'Packages': 'LPA'}, inplace = True)           # Change in original value
```

> Output

|   | IQ  | Marks | Packages |
|---|-----|-------|----------|
| 0 | 100 | 80    | 10       |
| 1 | 90  | 70    | 7        |
| 2 | 120 | 100   | 14       |
| 3 | 80  | 50    | 2        |


---

## # DataFrame Maths Method

> Same as Series maths methods 

---

## # Selecting Column from a DataFrame

``` py
movies = pd.read_csv('movies.csv')
movies

ipl = pd.read_csv('ipl-matches.csv')
ipl
``` 

### (i) Single Column

-  It is Case Sensitive
-  Whenever we extract any single column from a dataframe then that will be a series.

``` py
ipl['Venue'] 

# Output

0                Narendra Modi Stadium, Ahmedabad
1                Narendra Modi Stadium, Ahmedabad
2                           Eden Gardens, Kolkata
3                           Eden Gardens, Kolkata
4                        Wankhede Stadium, Mumbai
                          ...                    
945                                  Eden Gardens
946                              Wankhede Stadium
947                              Feroz Shah Kotla
948    Punjab Cricket Association Stadium, Mohali
949                         M Chinnaswamy Stadium
Name: Venue, Length: 950, dtype: str
```


#### (ii) Multiple Columns

- Fancy indexing will do this. ---> `[[...]]`
- While receiving the data we determine/decide the order of the data.
- Whenever we extract any multiple column from a dataframe then that will be a series.

``` py
movies[['title_x', 'year_of_release', 'actors']]
```

> Output

| index | title_x                              | year_of_release | actors                                                                 |
|-------|--------------------------------------|-----------------|------------------------------------------------------------------------|
| 0     | Uri: The Surgical Strike             | 2019            | Vicky Kaushal \| Paresh Rawal \| Mohit Raina \| Yami Gautam ...       |
| 1     | Battalion 609                        | 2019            | Vicky Ahuja \| Shoaib Ibrahim \| Shrikant Kamat \| Elena ...          |
| 2     | The Accidental Prime Minister (film) | 2019            | Anupam Kher \| Akshaye Khanna \| Aahana Kumra \| Atul Srivastava ...  |
| ...   | ...                                  | ...             | ...                                                                    |
| 1626  | Sabse Bada Sukh                      | 2018            | Vijay Arora \| Asrani \| Rajni Bala \| Kumud Damle \| Utpal Dutt ...  |
| 1627  | Daaka                                | 2019            | Gippy Grewal \| Zareen Khan                                            |
| 1628  | Humsafar                             | 2011            | Fawad Khan                                                             |


**1629 rows × 3 columns**


## # Selecting Rows from a DataFrame

- **`iloc`** : Searches using index positions
- **`loc`** : Searches using index labels


``` py
movies = pd.read_csv('movies.csv')
movies

student_dict = {
                'Name' : ['Nitish', 'Ankit', 'Rupesh', 'Rishabh', 'Sagar', 'Raj'],
                'IQ': [100, 90, 120, 80, 110, 95],
                'Marks': [80, 70, 100, 50, 90, 75],
                'Packages': [10, 7, 14, 2, 12, 8]}

Students = pd.DataFrame(student_dict)
Students.set_index('Name', inplace=True)
Students
```

### (i) Single Row

-  It is Case Sensitive
-  Whenever we extract any single row from a dataframe then that will be a series.

``` py
movies.iloc[5]
type(movies.iloc[5])                        # Output : pandas.Series

# Output
# title_x                                                   Soni (film)
# imdb_id                                                     tt6078866
# poster_path         https://upload.wikimedia.org/wikipedia/en/thum...
# wiki_link                   https://en.wikipedia.org/wiki/Soni_(film)
# title_y                                                          Soni
# original_title                                                   Soni
# is_adult                                                            0
# year_of_release                                                  2018
# runtime                                                            97
# genres                                                          Drama
# imdb_rating                                                       7.2
# imdb_votes                                                       1595
# story               Soni  a young policewoman in Delhi  and her su...
# summary             While fighting crimes against women in Delhi  ...
# tagline                                                           NaN
# actors              Geetika Vidya Ohlyan|Saloni Batra|Vikas Shukla...
# wins_nominations                               3 wins & 5 nominations
# release_date                                    18 January 2019 (USA)
# Name: 5, dtype: object

Students.loc['Nitish']

# Output
# IQ          100
# Marks        80
# Packages     10
# Name: Nitish, dtype: int64

```


### (ii) Multiple Rows

- Whenever we extract any multiple row from a dataframe then that will be a series.

``` py
movies.iloc[0:5]             # Output : Gives the first 5 movies row (0,1,2,3,4)

Students.loc['Nitish':'Rishabh']
```

> Output of Student

| Name    | IQ  | Marks | Packages |
|---------|-----|-------|----------|
| Nitish  | 100 | 80    | 10       |
| Ankit   | 90  | 70    | 7        |
| Rupesh  | 120 | 100   | 14       |
| Rishabh | 80  | 50    | 2        |


### (iii) By using Fancy Indexing

- It is for random rows


``` py
movies.iloc[[0,4,5]]             # Output : Gives the row of 0th, 4th and 5th movies

Students.loc[['Rishabh', 'Sagar', 'Nitish']]
```

> Output of Student

| Name    | IQ  | Marks | Packages |
|---------|-----|-------|----------|
| Rishabh | 80  | 50    | 2        |
| Sagar   | 110 | 90    | 12       |
| Nitish  | 100 | 80    | 10       |


## # Selecting both Row and Columns

``` py
movies = pd.read_csv('movies.csv')
movies

movies.iloc[0:3,0:3]
movies.loc[0:2,'title_x':'poster_path']
```

> Output fr both loc and iloc

| index | title_x                              | imdb_id    | poster_path                                      |
|-------|--------------------------------------|------------|--------------------------------------------------|
| 0     | Uri: The Surgical Strike             | tt8291224  | https://upload.wikimedia.org/wikipedia/en/thum... |
| 1     | Battalion 609                        | tt9472208  | NaN                                              |
| 2     | The Accidental Prime Minister (film) | tt6986710  | https://upload.wikimedia.org/wikipedia/en/thum... |



---

## # Filtering DataFrame 

``` py
movies = pd.read_csv('Lec3/movies.csv')
movies

ipl = pd.read_csv('Lec3/ipl-matches.csv')
ipl
```

### (i) Find all the IPL final winners

``` py
# 1st Method
mask = ipl['MatchNumber'] == 'Final'
new_df = ipl[mask]
new_df[['Season','WinningTeam']]

# 2nd Method
ipl[ipl['MatchNumber'] == 'Final'][['Season','WinningTeam']]
```

> Output

| index | Season  | WinningTeam              |
|-------|---------|--------------------------|
| 0     | 2022    | Gujarat Titans           |
| 74    | 2021    | Chennai Super Kings      |
| 134   | 2020/21 | Mumbai Indians           |
| 194   | 2019    | Mumbai Indians           |
| 254   | 2018    | Chennai Super Kings      |
| 314   | 2017    | Mumbai Indians           |
| 373   | 2016    | Sunrisers Hyderabad      |
| 433   | 2015    | Mumbai Indians           |
| 492   | 2014    | Kolkata Knight Riders    |
| 552   | 2013    | Mumbai Indians           |
| 628   | 2012    | Kolkata Knight Riders    |
| 702   | 2011    | Chennai Super Kings      |
| 775   | 2009/10 | Chennai Super Kings      |
| 835   | 2009    | Deccan Chargers          |
| 892   | 2007/08 | Rajasthan Royals         |


### (ii) How many super over finishes have occured

``` py
ipl[ipl['SuperOver'] == 'Y'].shape[0]             # Output : 14
```

### (iii) How many matches has csk won in kolkata

``` py
ipl[(ipl['City'] == 'Kolkata') & (ipl['WinningTeam'] == 'Chennai Super Kings')].shape[0]           # Output : 5
```

### (iv) Toss winner is match winner in percentage

``` py
(ipl[ipl['TossWinner'] == ipl['WinningTeam']].shape[0]/ipl.shape[0])*100         # Output : 51.473684210526315
```

### (v) Movies with rating higher than 8 and votes > 10000

``` PY
movies[(movies['imdb_rating'] > 8.5) & (movies['imdb_votes'] > 10000)].shape[0]              # Output : 0
```

### (vi) Action movies with rating higher than 7.5

``` py
# 1st Method
mask1 = movies['genres'].str.split('|').apply(lambda x:'Action' in x)         # Output : Gives movie with rating higher than 7.5
mask2 = movies['imdb_rating'] > 7.5

# 2nd Method
mask1 = movies['genres'].str.contains('Action')
mask2 = movies['imdb_rating'] > 7.5

movies[mask1 & mask2]                  # oUTPUT : Gives movie with rating higher than 7.5
```

### (vii) Write a function that can return the track record of 2 teams against each other

---

## Creating New Columns

``` py
movies = pd.read_csv('Lec3/movies.csv')
movies

ipl = pd.read_csv('Lec3/ipl-matches.csv')
ipl
```

### (i) Completely New Column

``` py
movies = pd.read_csv('Lec3/movies.csv')
movies

ipl = pd.read_csv('Lec3/ipl-matches.csv')
ipl
```

``` py
movies['Country'] = 'India'
movies                              # Ouytput : Add a new 'Country' column with value for every movie 'India' 
```


### (ii) Create a Column from Existing Columns

``` py
movies.dropna(inplace=True)                         # Remove rows with any missing values

movies['lead actor'] = movies['actors'].str.split('|').apply(lambda x:x[0])              # Add a new 'Lead Actor' column (First actor is actors column is lead actor)
movies
```

---

## Important DataFrame Functions

``` py
movies = pd.read_csv('Lec3/movies.csv')
movies

ipl = pd.read_csv('Lec3/ipl-matches.csv')
ipl
```

### (i) astype()

- It is is used to change the data type of a Pandas DataFrame.
- It helps reduce memory usage
- It Ensures correct calculations.
- **Syntax** : `DataFrame.astype(dtype)`

``` py
# Before change in data type
ipl.info()                               # memory usage: 148.6 KB

ipl['ID']= ipl['ID'].astype('int32')     # Change the data type permanently

# After change in data type
ipl.info()                               # memory usage: 144.9 KB
```

### (ii) value_count()

- Return a Series containing the frequency of each distinct row in the DataFrame.
- It can be applied in both Series and DataFrame.
- **Syntax** - `DataFrame.value_count()`

``` py
marks = pd.DataFrame([
    [100,80,10],
    [90,70,7],
    [120,100,14],
    [80,70,14],
    [80,70,14]
],columns=['iq','marks','package'])

marks

marks.value_counts()

# Output
iq   marks  package
80   70     14         2
100  80     10         1
90   70     7          1
120  100    14         1
Name: count, dtype: int64
```

### Questions related to value_count()

##### 1. Find which player has won most potm -> in finals and qualifiers

> Approach to solve this problem
>
> - In Match Number column matches are number, qualifier, eliminator and final
> - We need to extract qualifier, eliminator and final only
> - Then we use value_count()

> [!NOTE]
> ~ is NOT Operator (logical negation)

``` py
potm = ipl[~ipl['MatchNumber'].str.isdigit()]['Player_of_Match'].value_counts()
potm.head()

# Output
Player_of_Match
F du Plessis    3
KA Pollard      3
SK Raina        3
JJ Bumrah       2
SR Watson       2
Name: count, dtype: int64
```

##### 2. Plot Toss decision

> Approach to solve this problem
>
> - First we extract TossDecision column from DataFrame
> - Then use value_count() and plot()

> [!NOTE]
> Autopct is used in pie chart to display percentage values on the chart.

``` py
ipl['TossDecision'].value_counts().plot(kind='pie', autopct='%1.1f%%')
```

<img src="https://github.com/user-attachments/assets/f8fe7f06-eee3-4fdb-89c1-b8eac7d11a46" width="500" height="500">


##### 3. How many matches each team has played

> Approach to solve this problem
>
> - It is possible that one team may be in Team-1 nad the same team maybe in Team-2 in another match
> - We apply value_count() on both Team-1 and Team-2

``` py
(ipl['Team2'].value_counts() + ipl['Team1'].value_counts()).sort_values(ascending=False)

# Output
Mumbai Indians                 231
Royal Challengers Bangalore    226
Kolkata Knight Riders          223
Chennai Super Kings            208
Rajasthan Royals               192
Kings XI Punjab                190
Delhi Daredevils               161
Sunrisers Hyderabad            152
Deccan Chargers                 75
Delhi Capitals                  63
Pune Warriors                   46
Gujarat Lions                   30
Punjab Kings                    28
Gujarat Titans                  16
Rising Pune Supergiant          16
Lucknow Super Giants            15
Kochi Tuskers Kerala            14
Rising Pune Supergiants         14
Name: count, dtype: int64
```



















