# # Group By Object

- A GroupBy object is created when you use the .groupby() method on a DataFrame or Series.
- It is used to split data into groups, apply operations, and combine the results.
- This concept follows the **`Split → Apply → Combine`** pattern.

``` py
# Top 1000 movies listed on IMDB

movies = pd.read_csv('imdb-top-1000.csv')
movies
```

## Applying builtin aggregation fuctions on groupby objects

- **Aggregation fuctions** : count(), sum(), avg(), min(), max(), etc.

``` py
genres = movies.groupby('Genre')
genres.sum()

# Output :
# It will group the DataFrame by the Genre column and
# Calculate the sum of all numeric columns for each genre.
```


## Questions on Group By

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











