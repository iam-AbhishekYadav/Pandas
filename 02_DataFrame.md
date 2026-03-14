# # Data Structures / Objects in Pandas

# (2.) Pandas DataFrame

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


### (x) isnull()

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

### (xii) rename()

- Rename columns or index labels.
- **Syntax** : `DataFrame.rename(columns={'old_name': 'new_name'}, inplace=True)`
  - inplace --> Change   original DataFrame and create a new cpoy

> Change in Column

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


> Change in Index

``` py
movies.set_index('title_x',inplace=True)                   # Set 'title_x' as index

movies.rename(index={'Uri: The Surgical Strike':'Uri',
                    'Battalion 609':'Battalion'})            # Rename index name
```

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
movies = pd.read_csv('movies.csv')
movies

ipl = pd.read_csv('pl-matches.csv')
ipl

batsman = pd.read_csv('batsman_runs_ipl.csv')
batsman

students = pd.DataFrame(
    {
        'name':['nitish','ankit','rupesh',np.nan,'mrityunjay',np.nan,'rishabh',np.nan,'aditya',np.nan],
        'college':['bit','iit','vit',np.nan,np.nan,'vlsi','ssit',np.nan,np.nan,'git'],
        'branch':['eee','it','cse',np.nan,'me','ce','civ','cse','bio',np.nan],
        'cgpa':[6.66,8.25,6.41,np.nan,5.6,9.0,7.4,10,7.4,np.nan],
        'package':[4,5,6,np.nan,6,7,8,9,np.nan,np.nan]
    }
)
students
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


### (iii) sort_value()

- Sort a DataFrame in ascending or descending orderby one or more columns.
- **Syntax** - `DataFrame.sort_values()`
- **Parametrs**: 0 or index, inplace, ascending (bool or list of bools, default True)
  - inplace - Update the original DataFrame permanently

``` py
movies.sort_values('title_x',ascending=False)          # Output : It sort movie dataframe by Z to A on basis of column title_x
```

#### Some Important Cases

``` py
students = pd.DataFrame(
    {
        'name':['nitish','ankit','rupesh',np.nan,'mrityunjay',np.nan,'rishabh',np.nan,'aditya',np.nan],
        'college':['bit','iit','vit',np.nan,np.nan,'vlsi','ssit',np.nan,np.nan,'git'],
        'branch':['eee','it','cse',np.nan,'me','ce','civ','cse','bio',np.nan],
        'cgpa':[6.66,8.25,6.41,np.nan,5.6,9.0,7.4,10,7.4,np.nan],
        'package':[4,5,6,np.nan,6,7,8,9,np.nan,np.nan]

    }
)
students
```
| index | name        | college | branch | cgpa  | package |
|-------|------------|---------|--------|-------|---------|
| 0     | nitish     | bit     | eee    | 6.66  | 4.0     |
| 1     | ankit      | iit     | it     | 8.25  | 5.0     |
| 2     | rupesh     | vit     | cse    | 6.41  | 6.0     |
| 3     | NaN        | NaN     | NaN    | NaN   | NaN     |
| 4     | mrityunjay | NaN     | me     | 5.60  | 6.0     |
| 5     | NaN        | vlsi    | ce     | 9.00  | 7.0     |
| 6     | rishabh    | ssit    | civ    | 7.40  | 8.0     |
| 7     | NaN        | NaN     | cse    | 10.00 | 9.0     |
| 8     | aditya     | NaN     | bio    | 7.40  | NaN     |
| 9     | NaN        | git     | NaN    | NaN   | NaN     |

> **Case - 1 : Position of NaN values** 
> - It automatically moves the NaN value to the last position. (Default Behaviour)
> - But we can change it by parameter na_position

``` py
students.sort_values('name',na_position='first',ascending=False)
students                                       # Output : First values are NaN nad other are sorted by A to Z
```

| index | name        | college | branch | cgpa  | package |
|-------|------------|---------|--------|-------|---------|
| 3     | NaN        | NaN     | NaN    | NaN   | NaN     |
| 5     | NaN        | vlsi    | ce     | 9.00  | 7.0     |
| 7     | NaN        | NaN     | cse    | 10.00 | 9.0     |
| 9     | NaN        | git     | NaN    | NaN   | NaN     |
| 2     | rupesh     | vit     | cse    | 6.41  | 6.0     |
| 6     | rishabh    | ssit    | civ    | 7.40  | 8.0     |
| 0     | nitish     | bit     | eee    | 6.66  | 4.0     |
| 4     | mrityunjay | NaN     | me     | 5.60  | 6.0     |
| 1     | ankit      | iit     | it     | 8.25  | 5.0     |
| 8     | aditya     | NaN     | bio    | 7.40  | NaN     |


> **Case - 2 : Sort by Multiple Columns**
> - The order of the columns in the list determines the sorting priority 
> - It sorts by the first column, then the second within groups of tied values in the first, and so on

``` py
students.sort_values(by=['cgpa', 'package'], ascending=[False, False])

# Output
# First sort by cgpa (descending)
# If cgpa is same → then sort by package (descending)
```

| index | name        | college | branch | cgpa  | package |
|-------|------------|---------|--------|-------|---------|
| 7     | NaN        | NaN     | cse    | 10.00 | 9.0     |
| 5     | NaN        | vlsi    | ce     | 9.00  | 7.0     |
| 1     | ankit      | iit     | it     | 8.25  | 5.0     |
| 6     | rishabh    | ssit    | civ    | 7.40  | 8.0     |
| 8     | aditya     | NaN     | bio    | 7.40  | NaN     |
| 0     | nitish     | bit     | eee    | 6.66  | 4.0     |
| 2     | rupesh     | vit     | cse    | 6.41  | 6.0     |
| 4     | mrityunjay | NaN     | me     | 5.60  | 6.0     |
| 3     | NaN        | NaN     | NaN    | NaN   | NaN     |
| 9     | NaN        | git     | NaN    | NaN   | NaN     |



### (iv) sort_index()

- Returns a new DataFrame sorted by label if inplace argument is False.
- It behaves same in both Series and DataFrame.
- **Syntax** - `DataFrame.sort_index()`
- **Parametrs** : 0 or index, inplace, ascending (bool or list-like of bools, default True)

``` py
movies.sort_index(ascending=False)           # Output : It sorted movies DataFrame in decending order
```

### (v) set_index()

- This method is used to set one or more columns of a DataFrame as the index.
- **Syntax** - `DataFrame.set_index()`

``` py
batsman.set_index('batter')               # Output : 'batter' cloumn is now index                                 
```

> Output 

| batter | batsman_run |
|-------|-------------|
| A Ashish Reddy | 280 |
| A Badoni | 161 |
| A Chandila | 4 |
| ... | ... |
| Yuvraj Singh | 2754 |
| Z Khan | 117 |


### (vi) reset_index()

- This method in Pandas is used to manage and reset the index of a DataFrame.
- It is useful after performing operations that modify the index such as filtering, grouping or setting a custom index.
- **Syntax** -   `DataFrame.reset_index()`

``` py
batsman.set_index('batter', inplace=True)
batsman                                           # Output : 'batter' cloumn is now index ---> Permanent Change

batsman.reset_index()                              # Output : reset the index
```

> Otput 

| index | batter | batsman_run |
|------|--------|-------------|
| 0 | A Ashish Reddy | 280 |
| 1 | A Badoni | 161 |
| 2 | A Chandila | 4 |
| ... | ... | ... |
| 603 | Yuvraj Singh | 2754 |
| 604 | Z Khan | 117 |


#### Series to DataFrame using reset_index()

``` py
marks = {
    'maths':67,
    'english':57,
    'science':89,
    'hindi':100
}

marks_series = pd.Series(marks)
marks_series


marks_series.reset_index()
```

> Output

| index_no | index | 0 |
|---------|-------|---|
| 0 | maths | 67 |
| 1 | english | 57 |
| 2 | science | 89 |
| 3 | hindi | 100 |


### (vii) unique() ---> Series

- Return an array of all the unique values within a Series, in the order of their appearance.
- **Syntax** - `Series.unique()`

``` py
temp = pd.Series([1,1,2,2,3,3,4,4,5,5,np.nan,np.nan])
print(temp)

temp.unique()                           # Output : array([ 1.,  2.,  3.,  4.,  5., nan])
len(temp.unique())                      # Output : 6
```

### (viii) nunique()

- Return the number of unique values for each column.
- It ignore NaN values.
- **Syntax** - `DataFrame.nunique()`

``` py
temp = pd.Series([1,1,2,2,3,3,4,4,5,5,np.nan,np.nan])
print(temp)

temp.nunique()                      # Output : 5
```


### (ix) isnull()

- It is used to detect missing (NaN) values in a Pandas Series.
- It returns a Boolean Series:
  - True → value is missing
  - False → value is not missing
- **Syntax** - `Series.isnull()`

``` py
students['name'][students['name'].isnull()]                    # Give NaN values in `name` column

# Output
3    NaN
5    NaN
7    NaN
9    NaN
Name: name, dtype: str


students.isnull()
```

> Ouput 

| index | name | college | branch | cgpa | package |
|------|------|---------|--------|------|---------|
| 0 | False | False | False | False | False |
| 1 | False | False | False | False | False |
| 2 | False | False | False | False | False |
| ... | ... | ... | ... | ... | ... |
| 8 | False | True | False | False | True |
| 9 | True | False | True | True | True |


### (x) notnull()

- It is oppsite of `isnull()`
-  It is used to detect existing (non-missing) values.
- It returns a Boolean Series:
  - True → value is not missing
  - False → value is missing
- **Syntax** - `Series.notnull()`

``` py
students['name'][students['name'].notnull()]              # Give non missing values in `name` column

# Output
0        nitish
1         ankit
2        rupesh
4    mrityunjay
6       rishabh
8        aditya
Name: name, dtype: str


students.notnull()
```

> Output

| index | name | college | branch | cgpa | package |
|------|------|---------|--------|------|---------|
| 0 | True | True | True | True | True |
| 1 | True | True | True | True | True |
| 2 | True | True | True | True | True |
| ... | ... | ... | ... | ... | ... |
| 8 | True | False | True | True | False |
| 9 | False | True | False | False | False |



### (xi) dropna()

- It is used to remove missing (NaN) values from a DataFrame.
- **Syntax** - `DataFrame.dropna()`
- **Parameters** :
  - **`axis`**
    - 0 to drop rows (default)
    - 1 to drop columns
    - Only a single axis is allowed.
  - **`how`** 
    - `‘any’` : Drop if any value is missing (default)
    - `‘all’` : Drop if all are missing
  - **`subset`** - Labels to consider for NA checks (subset of columns)
  - **`thresh`** - Minimum number of non-NA values required to keep the row/column
  - **`inplace`**
    - If True, modifies the original DataFrame
    - If False (default), returns a new one

``` py
students['name'].dropna()                               # Drop NaN from 'name' series
students.dropna(how='any')                              # Drop NaN if any NaN values are present in coulmn/row
students.dropna(how='all')                              # Drop NaN if all NaN values are presentin coulmn/row
students.dropna(subset=['name','college'])              # Drop NaN if NaN is present in 'name' and 'college' column
students.dropna(thresh=3)                               # Drop NaN is NaN is more than 3 in coulmn/row
```

### (xii) fillna()

- It is used to replace missing (NaN) values in a Pandas DataFrame.
- It can be filled by Mean, Meadian, etc.
- Forward Fill (ffill) - Copies the previous value down.
  - `DataFrame.ffill()`
- Backward Fill (bfill) - Uses the next value.
  - `DataFrame.bfill()`

``` py
students['name'].fillna('unknown')                              # Fill NaN with 'unknown` from series 'name'
students['package'].fillna(students['package'].mean())          # Fill NaN with Mean of student package in package column 
students['name'].bfill()                                        # Fill NaN with backward values
```

### (xiii) drop_duplicates() 

- It removes repeated values from a DataFrame and keeps only unique ones (based on your settings).
- **Syntax** : `DataFrame.drop_duplicates(subset=None, keep='first', inplace=False)`
  - subset → column(s) to check duplicates
  - keep → which duplicate to keep ('first', 'last', False)
  - inplace → modify original data (True or False)

``` py
marks = pd.DataFrame([
    [100,80,10],
    [90,70,7],
    [120,100,14],
    [80,70,14],
    [80,70,14]
],columns=['iq','marks','package'])

marks

marks.drop_duplicates()
```

> **Output** : Removes 4th row of the table because it is duplicate of 3rd row

|   | iq  | marks | package |
|---|-----|-------|---------|
| 0 | 100 | 80    | 10      |
| 1 | 90  | 70    | 7       |
| 2 | 120 | 100   | 14      |
| 3 | 80  | 70    | 14      |


### Questions on drop_duplicates()

#### 1. Find the last match played by virat kohli in Delhi.

> Approach to solve this problem
>
> - First we Combine both team players to all players
> - Create a function that checks whether 'V Kohli' exists in the player list.
> - Create a new column indicating Kohli's presence
> - Filter matches played in Delhi
> - From Delhi matches, keep only those where Kohli participated.
> - Find the last match

``` py
# Step : 1
ipl['all_players'] = ipl['Team1Players'] + ipl['Team2Players']
ipl.head()

# Step : 2
def did_kohli_play(players_list):
    return 'V Kohli' in players_list

# Step : 3
ipl['did_kohli_play'] = ipl['all_players'].apply(did_kohli_play)

# Step : 4,5,6
ipl[(ipl['City'] == 'Delhi') & (ipl['did_kohli_play'] == True)].drop_duplicates(subset=['City','did_kohli_play'],keep='first')
```

> Output

| index | ID      | City  | Date       | Season | MatchNumber | Team1          | Team2                     | Venue               | TossWinner       | TossDecision | WonBy | Margin | method | Player_of_Match | Team1Players | Team2Players | Umpire1       | Umpire2                  | all_players | did_kohli_play |
|------|---------|-------|------------|--------|-------------|---------------|---------------------------|--------------------|-----------------|-------------|-------|--------|--------|----------------|--------------|--------------|--------------|--------------------------|-------------|---------------|
| 208  | 1178421 | Delhi | 2019-04-28 | 2019   | 46          | Delhi Capitals | Royal Challengers Bangalore | Arun Jaitley Stadium | Delhi Capitals | bat         | Runs  | 16     | NaN    | S Dhawan       | ['PP Shaw', 'S Dhawan', 'SS Iyer', 'RR Pant', ...] | ['PA Patel', 'V Kohli', 'AB de Villiers', ...] | BNJ Oxenford | KN Ananthapadmanabhan | ['PP Shaw', 'S Dhawan', 'SS Iyer', ...] | True |

### (xiv) drop()

- It is used to remove specified labels from rows or columns in a DataFrame.
- **Syntax** - `DataFrame.drop()`

``` py
# Delete Column
students.drop(columns=['branch','cgpa'])            # Delete column 'branch' and 'cgpa'

# Delete Row
students.set_index('name',inplace=True)             # Set 'name' as index
students.drop(index=['nitish','aditya'])            # Delete row with index 'nitish' and 'aditya'
``` 
























































