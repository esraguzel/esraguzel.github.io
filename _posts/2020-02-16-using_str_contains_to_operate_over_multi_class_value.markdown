---
layout: post
title:      "Using `str.contains()`  to operate over multi class values"
date:       2020-02-16 15:26:45 -0500
permalink:  using_str_contains_to_operate_over_multi_class_value
---


Pandas Series.str.contains() function is generally used for to search whether a Series or Index contains a string pattern or a regular expression(regex). If the  Series or Index contains the searched pattern or regex, the function gives back a boolean Series or Index.

I wanted to explore the use of `str.contains()` function on pandas series, for instance a column which contains  multi class values.  Let's think that we have a dataframe df_genres which contains multi genre for each movie. 

```
df_genres.head()
```

<img src="https://github.com/esraguzel/dsc-mod-1-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-02-16%20at%2015.04.04.png?raw=True" width="100%">


First, we need to check the type of genres column. 

```
df_genres.['genre'].dtype
```
```
dtype('O')
```
Then, we need to change the datatype of genre column from object to string. By changing datatype to string we will be able to operate over the column with `str.contains()` function. 

```
df_genres['genres'] = df_genres['genres'].astype(str)
```

Now let's create a unique genres list with a for loop.  When we look at the genres column, we can see that each genre is separated with a coma from the other. The coma can be elimitated using the `split () `function. 

```
genres_list = []
for genres in df_genres['genres']:
    genres_list.extend(genres.split(','))
    
unique_genres = list(set(genres_list))
unique_genres
```

```
['Music',
 'Sport',
 'News',
 'Comedy',
 'Adventure',
 'Mystery',
 'Fantasy',
 'Drama',
 'War',
 'Family',
 'Sci-Fi',
 'Reality-TV',
 'Romance',
 'History',
 'Documentary',
 'Thriller',
 'Horror',
 'Musical',
 'Biography',
 'Crime',
 'Action',
 'nan',
 'Western',
 'Animation']
```


Now the `str.contains()` function can be used to iterate over the unique genres list to find genres for each movie.  Here the outcome is stored under a list called results. Later, results list is converted into a dataframe using unique genres list as an index. 




```
unique_genres = sorted(unique_genres)
results = []
for genre in unique_genres:
    result = df_genres[df_genres['genres'].str.contains(genre)]['id'].count()
    results.append(result)

output = pd.DataFrame({'Count': results}, index=unique_genres)


fig, ax = plt.subplots(figsize=(15,7))
output.plot.bar(ax=ax)

plt.show()
```

<img src="https://github.com/esraguzel/dsc-mod-1-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-02-16%20at%2019.08.19.png?raw=true" width="100%">


For many data scientist and programmers the `str.contains()` function is very practical and commonly used but  it may have some limitations.  For example if the unique values list contained two separate genres tv and reality tv, this function would  return true for both  tv and reality tv strings when operating over.

