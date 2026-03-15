# # Group By Object

- A GroupBy object is created when you use the .groupby() method on a DataFrame or Series.
- It is used to split data into groups, apply operations, and combine the results.
- This concept follows the **`Split → Apply → Combine`** pattern.

``` py
# Top 1000 movies listed on IMDB

movies = pd.read_csv('imdb-top-1000.csv')
movies
```

---

## # Applying builtin aggregation fuctions on GroupBy Objects

- **Aggregation fuctions** : count(), sum(), avg(), min(), max(), etc.

``` py
genres = movies.groupby('Genre')
genres.sum()

# Output :
# It will group the DataFrame by the Genre column and
# Calculate the sum of all numeric columns for each genre.
```

---

## # Questions on GroupBy

#### 1. Find the top 3 genres by total earning

> Approach to solve this problem
>
> - Take data set and group by on the basis of 'Genre'
> - Apply sum() on this group by
> - Sum applies on every column includingt 'Gross'
> - Then we extract top 3 gross earning from 'Gross' column 

``` py
# 1st Method
movies.groupby('Genre').sum()['Gross'].sort_values(ascending=False).head(3)

# 2nd Method ---> Fast
# Extract 'Gross' coulmn first then apply sum()
movies.groupby('Genre')['Gross'].sum().sort_values(ascending=False).head(3)

# Output

# Genre
# Drama     3.540997e+10
# Action    3.263226e+10
# Comedy    1.566387e+10
# Name: Gross, dtype: float64
```

#### 2. Find the genre with highest avg IMDB rating

> Same Approach as 1st question

``` py
movies.groupby('Genre')['IMDB_Rating'].mean().sort_values(ascending=False).head(3)

# Output

# Genre
# Western    8.350000
# Crime      8.016822
# Fantasy    8.000000
# Name: IMDB_Rating, dtype: float64
```

#### 3. Find director with most popularity (No_of_Votes)

> Same Approach as 1st question

``` py
movies.groupby('Director')['No_of_Votes'].mean().sort_values(ascending=False).head(3)

# Output

# Director
# Frank Darabont       1745452.000
# Lana Wachowski       1676426.000
# Christopher Nolan    1447293.125
# Name: No_of_Votes, dtype: float64
```

#### 4. Find number of movies done by each actor

> Same Approach as 1st question

``` py
# 1st Method
movies['Star1'].value_counts()

# 2nd Method
movies.groupby('Star1')['Series_Title'].count().sort_values(ascending=False)

# Output

# Star1
# Tom Hanks               12
# Robert De Niro          11
# Clint Eastwood          10
# Al Pacino               10
# Humphrey Bogart          9
#                         ..
# Zbigniew Zamachowski     1
# Zooey Deschanel          1
# Çetin Tekindor           1
# Éric Toledano            1
# Aaron Taylor-Johnson     1
# Name: Series_Title, Length: 660, dtype: int64
```

---

## # Attributes and Methods of GroupBy

``` py
movies = pd.read_csv('Lec-5/imdb-top-1000.csv')
movies
```

### (i) len()

-  Find the total number of GroupBy

``` py
len(movies.groupby('Genre'))        # Output : 14
```

### (ii) size()

- Find items in each group
- **Syntax** : `DataFrameGroupBy.size()`

``` py
movies.groupby('Genre').size()

# Output

# Genre
# Action       172
# Adventure     72
# Animation     82
# Biography     88
# Comedy       155
# Crime        107
# Drama        289
# Family         2
# Fantasy        2
# Film-Noir      3
# Horror        11
# Mystery       12
# Thriller       1
# Western        4
# dtype: int64
```

### (iii) first(), last() and nth()

- **`first()`** : Compute the first entry of each column within each group.
- **`last()`** : Compute the last entry of each column within each group.
- **`nth()`** : Compute the N-th entry of each column within each group.

``` py
genres = movies.groupby('Genre')
genres.first()                       # Output : Gives first movie of every genre
genres.last()                        # Output : Gives last movie of every genre
genres.nth(6)                        # Output : Gives 7th movie of every genre (7th because index starts from 0)
```

### (iv) get_group()

- This method retrieves all rows belonging to a specific group identified by the given name.
- Construct Series/DataFrame from group with provided name.
- **Syntax** :
  - Series --> `SeriesGroupBy.get_group(name)`
  - DataFrame --> `DataFrameGroupBy.get_group(name)`

``` py
genres = movies.groupby('Genre')

# 1st Method ---> Fast and more efficient
genres.get_group('Fantasy')            # It create DataFrame which movie genre is 'Fantasy'

# 2nd Method
movies[movies['Genre'] == 'Fantasy']
```

### (v) describe()

- Generate descriptive statistics.
- It gives count, mean, std, min, 25%, 50%, 75%, max
- **Syntax** :
  - Series --> `SeriesGroupBy.describe()`
  - DataFrame --> `DataFrameGroupBy.describe()`


``` py
genres = movies.groupby('Genre')
genres.describe()                    # It gives descriptive statistics of each genre
```

### (vi) sample()

- Return a random sample of items from each group.
- **Syntax** :
  - Series --> `SeriesGroupBy.sample()`
  - DataFrame --> `DataFrameGroupBy.sample()`
- **Parametrs(n)** : int, float, bool (default false)

``` py
genres = movies.groupby('Genre')
genres.sample()                    # It gives one random movie of each genre
```

### (vii) nunique()

- This method counts the number of unique values for each column within each group, optionally excluding NaN values.
- **Syntax** :
  - Series --> `SeriesGroupBy.nunique()`
  - DataFrame --> `DataFrameGroupBy.nunique()`

``` py
genres = movies.groupby('Genre')
genres.nunique()                    # It gives number of unique movies in each genre
```

---







