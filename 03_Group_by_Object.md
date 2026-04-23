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
movies = pd.read_csv('imdb-top-1000.csv')
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

## # Using Two or More Aggregation Methods

``` py
movies = pd.read_csv('imdb-top-1000.csv')
movies
```

### (i) Passing dict

``` py
genres.agg(
    {
        'Runtime':'mean',
        'IMDB_Rating':'mean',
        'No_of_Votes':'sum',
        'Gross':'sum',
        'Metascore':'min'
    }    
)
```

> Output

| Genre       | Runtime   | IMDB_Rating | No_of_Votes | Gross        | Metascore |
|------------|----------:|------------:|------------:|-------------:|----------:|
| Action     | 129.046512 | 7.949419    | 72282412    | 3.263226e+10 | 33.0      |
| Adventure  | 134.111111 | 7.937500    | 22576163    | 9.496922e+09 | 41.0      |
| Animation  | 99.585366  | 7.930488    | 21978630    | 1.463147e+10 | 61.0      |
| Biography  | 136.022727 | 7.938636    | 24006844    | 8.276358e+09 | 48.0      |


### (ii) Passing list







### (iii) Passing both dict and list

``` py
genres.agg(
    {
        'Runtime':['min','mean'],
        'IMDB_Rating':'mean',
        'No_of_Votes':['sum','max'],
        'Gross':'sum',
        'Metascore':'min'
    }
)
```

> Output


| Genre | Runtime |  | IMDB_Rating | No_of_Votes |  | Gross | Metascore |
|-------|--------|--------|-------------|-------------|-------------|-------|-----------|
|       | min    | mean   | mean        | sum         | max         | sum   | min       |
| Action    | 45  | 129.046512 | 7.949419 | 72282412 | 2303232 | 3.263226e+10 | 33.0 |
| Adventure | 88  | 134.111111 | 7.937500 | 22576163 | 1512360 | 9.496922e+09 | 41.0 |
| Animation | 71  | 99.585366  | 7.930488 | 21978630 | 999790  | 1.463147e+10 | 61.0 |
| Biography | 93  | 136.022727 | 7.938636 | 24006844 | 1213505 | 8.276358e+09 | 48.0 |

---

## # Split Apply Combine strategy

- `apply()` - It has builtin function


### Questions 

``` py
movies = pd.read_csv('imdb-top-1000.csv')
movies
```

#### 1. Find number of movies starting with A for each group

``` py
def foo(group):
  return group['Series_Title'].str.startswith('A').sum()

genres.apply(foo)


# Output

# Genre 
# Action       : 10
# Adventure    :  2
# Animation    :  2
# Biography    :  9
# Comedy       : 14
# Crime        :  4
# Drama        : 21
# Family       :  0
# Fantasy      :  0
# Film-Noir    :  0
# Horror       :  1
# Mystery      :  0
# Thriller     :  0
# Western      :  0
# dtype: int64
```


#### 2. Find ranking of each movie in the group according to IMDB score

``` py
def rank_movie(group):
  group['genre_rank'] = group['IMDB_Rating'].rank(ascending=False)
  return group

genres.apply(rank_movie)
```

> Output


| Index | Series_Title                  | Released_Year | Runtime | Genre  | IMDB_Rating | Director                | Star1              | No_of_Votes | Gross        | Metascore | genre_rank |
|------|------------------------------|--------------|---------|--------|-------------|-------------------------|--------------------|-------------|-------------|-----------|------------|
| 0    | The Shawshank Redemption     | 1994         | 142     | Drama  | 9.3         | Frank Darabont          | Tim Robbins        | 2343110     | 28341469.0  | 80.0      | 1.0        |
| 1    | The Godfather               | 1972         | 175     | Crime  | 9.2         | Francis Ford Coppola    | Marlon Brando      | 1620367     | 134966411.0 | 100.0     | 1.0        |
| 2    | The Dark Knight            | 2008         | 152     | Action | 9.0         | Christopher Nolan       | Christian Bale     | 2303232     | 534858444.0 | 84.0      | 1.0        |
| 3    | The Godfather: Part II     | 1974         | 202     | Crime  | 9.0         | Francis Ford Coppola    | Al Pacino          | 1129952     | 57300000.0  | 90.0      | 2.5        |
| 4    | 12 Angry Men               | 1957         | 96      | Crime  | 9.0         | Sidney Lumet            | Henry Fonda        | 689845      | 4360000.0   | 96.0      | 2.5        |



#### 3. Find normalized IMDB rating group wise

``` py
def normal(group):
  group['norm_rating'] = (group['IMDB_Rating'] - group['IMDB_Rating'].min())/(group['IMDB_Rating'].max() - group['IMDB_Rating'].min())
  return group

genres.apply(normal)
```

> Output

 Index | Series_Title                  | Released_Year | Runtime | Genre  | IMDB_Rating | Director                | Star1              | No_of_Votes | Gross        | Metascore | norm_rating |
|------|------------------------------|--------------|---------|--------|-------------|-------------------------|--------------------|-------------|-------------|-----------|-------------|
| 0    | The Shawshank Redemption     | 1994         | 142     | Drama  | 9.3         | Frank Darabont          | Tim Robbins        | 2343110     | 28341469.0  | 80.0      | 1.000       |
| 1    | The Godfather               | 1972         | 175     | Crime  | 9.2         | Francis Ford Coppola    | Marlon Brando      | 1620367     | 134966411.0 | 100.0     | 1.000       |
| 2    | The Dark Knight            | 2008         | 152     | Action | 9.0         | Christopher Nolan       | Christian Bale     | 2303232     | 534858444.0 | 84.0      | 1.000       |
| 3    | The Godfather: Part II     | 1974         | 202     | Crime  | 9.0         | Francis Ford Coppola    | Al Pacino          | 1129952     | 57300000.0  | 90.0      | 0.875       |
| 4    | 12 Angry Men               | 1957         | 96      | Crime  | 9.0         | Sidney Lumet            | Henry Fonda        | 689845      | 4360000.0   | 96.0      | 0.875       |

---

## # GroupBy on Multiple Columns

- To group by multiple columns, you simply pass a list of column names to the groupby() function.
- Example :

``` py
duo = movies.groupby(['Director','Star1'])
duo                                # Output : <pandas.api.typing.DataFrameGroupBy object at 0x00000220FA886F50>
```

- Size 

``` py
duo.size()

# Output

# Director             Star1         
# Aamir Khan           Amole Gupte       1
# Aaron Sorkin         Eddie Redmayne    1
# Abdellatif Kechiche  Léa Seydoux       1
# Abhishek Chaubey     Shahid Kapoor     1
# Abhishek Kapoor      Amit Sadh         1
# ...
# Zaza Urushadze       Lembit Ulfsak     1
# Zoya Akhtar          Hrithik Roshan    1
#                      Vijay Varma       1
# Çagan Irmak          Çetin Tekindor    1
# Ömer Faruk Sorak     Cem Yilmaz        1
# Length: 898, dtype: int64
```

- Get Group

``` py
duo.get_group(('Aamir Khan','Amole Gupte'))
```
> Output

| Index | Series_Title        | Released_Year | Runtime | Genre | IMDB_Rating | Director   | Star1        | No_of_Votes | Gross      | Metascore |
|------|--------------------|--------------|---------|-------|-------------|------------|--------------|-------------|------------|-----------|
| 65   | Taare Zameen Par   | 2007         | 165     | Drama | 8.4         | Aamir Khan | Amole Gupte  | 168895      | 1223869.0  | NaN       |


### Questions 

``` py
movies = pd.read_csv('imdb-top-1000.csv')
movies
```

#### 1. Find the most earning actor --> director combo

``` py
duo['Gross'].sum().sort_values(ascending=False).head(1)

# Output

# Director        Star1         
# Akira Kurosawa  Toshirô Mifune    2.999877e+09
# Name: Gross, dtype: float64
```

#### 2. Find the best(in-terms of metascore(avg)) actor --> genre combo

``` py
movies.groupby(['Star1','Genre'])['Metascore'].mean().reset_index().sort_values('Metascore',ascending=False).head(1)
```

> Output

| Index | Star1            | Genre | Metascore |
|------|------------------|-------|-----------|
| 230  | Ellar Coltrane   | Drama | 100.0     |


#### 3. Aggregate function on multiple groupby

``` py
duo = movies.groupby(['Director','Star1'])
duo

duo.agg(['min','max','mean'])
```
> Output

| Director | Star1 | Runtime |        |        | IMDB_Rating |        |        | No_of_Votes |        |        | Gross |        |        | Metascore |        |        |
|----------|-------|---------|--------|--------|-------------|--------|--------|-------------|--------|--------|-------|--------|--------|-----------|--------|--------|
|          |       | min     | max    | mean   | min         | max    | mean   | min         | max    | mean   | min   | max    | mean   | min       | max    | mean   |
| Aamir Khan | Amole Gupte | 165 | 165 | 165.0 | 8.4 | 8.4 | 8.4 | 168895 | 168895 | 168895.0 | 1223869.0 | 1223869.0 | 1223869.0 | NaN | NaN | NaN |
| Aaron Sorkin | Eddie Redmayne | 129 | 129 | 129.0 | 7.8 | 7.8 | 7.8 | 89896 | 89896 | 89896.0 | 853090410.0 | 853090410.0 | 853090410.0 | 77.0 | 77.0 | 77.0 |
| Abdellatif Kechiche | Léa Seydoux | 180 | 180 | 180.0 | 7.7 | 7.7 | 7.7 | 138741 | 138741 | 138741.0 | 2199675.0 | 2199675.0 | 2199675.0 | 89.0 | 89.0 | 89.0 |
| Abhishek Chaubey | Shahid Kapoor | 148 | 148 | 148.0 | 7.8 | 7.8 | 7.8 | 27175 | 27175 | 27175.0 | 218428303.0 | 218428303.0 | 218428303.0 | NaN | NaN | NaN |
| Abhishek Kapoor | Amit Sadh | 130 | 130 | 130.0 | 7.7 | 7.7 | 7.7 | 32628 | 32628 | 32628.0 | 1122527.0 | 1122527.0 | 1122527.0 | 40.0 | 40.0 | 40.0 |
















