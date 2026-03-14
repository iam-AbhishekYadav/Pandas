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

### 1. Find the top 3 genres by total earning

> Approach to solve this problem
>
> - Take data set and group by on the basis of 'Genre'
> - Apply sum() on this group by
> - Sum applies on every column includingt 'Gross'
> - Then we extract top 3 gross earning from 'Gross' column 

``` py
# 1st Method
movies.groupby('Genre').sum()['Gross'].sort_values(ascending=False).head(3)

# 2nd Method
movies.groupby('Genre')['Gross'].sum().sort_values(ascending=False).head(3)

# Output

# Genre
# Drama     3.540997e+10
# Action    3.263226e+10
# Comedy    1.566387e+10
# Name: Gross, dtype: float64
```
























