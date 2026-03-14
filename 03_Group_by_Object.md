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






























