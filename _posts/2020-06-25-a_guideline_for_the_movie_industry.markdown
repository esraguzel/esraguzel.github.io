---
layout: post
title:      "A Guideline for the Movie Industry "
date:       2020-06-25 17:35:41 +0000
permalink:  a_guideline_for_the_movie_industry
---


 
 
The aim of this project is to provide insights which may help decision making process in terms of release timing, genre selection and give clear understanding about the interaction of production budget, domestic/worldwide gross, domestic/worldwide ROI ratio, popularity and vote average of the movies for the new companies/investors in the movie industry. 

Question 1: How many movies released every year, every month? Which month of the year is more profitable?


This question is asked to explore which time of the year is preferred for movie releases and which months are more profitable in return, as well as to see the overall distribution of movies over the years. 'tmdb_movies_gz' is chosen to search for movie distribution by months and years, the first part of the question, since it contains highest number of movies and release dates compared to other dataframes available. First visual shows figures only in the last ten years since most of the movies are concentrated in this period. 


<img src="https://github.com/esraguzel/dsc-mod-1-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-02-16%20at%2018.45.53.png?raw=true" width="100%">



<img src="https://github.com/esraguzel/dsc-mod-1-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-02-16%20at%2018.46.20.png?raw=true" width="100%">


For the second part of the question  'tn_movie_budgets_gz' dataframe is used since it already has release dates and production budget, domestic gross, worldwide gross. Worldwide and Domestic ROI ratio calculated to show each movie's profitability by months. 

<img src="https://github.com/esraguzel/dsc-mod-1-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-02-16%20at%2018.47.04.png?raw=true" width="100%">

Distribution of domestic ROI ratio, production budget, domestic gross and worldwide gross by months are also explored to gain more insights about the data.  



- 2013, 2014 and 2015 has the highest number of movies between 2009 and 2019,
- January, October, April and March are the top months movies releases happen,
- June, July and August are the months with highest average both worldwide and domestic ROI,
- top 4 months with highest average production budget are May, June, July and November,
- July is the month which least number of movies released.



Question 2: Is there any relation/correlation between production budget, domestic gross, worldwide gross, domestic ROI, worldwide ROI, vote average and popularity?

The two datasets used at the first question are merged to explore the second question. The first heatmap below analyze the correlation between production budget, domestic gross, worldwide gross, domestic ROI, worldwide ROI, vote average and popularity. 

During exploration some movies with 0 domestic and worldwide gross are noticed and treated as outliers. The second heatmap excludes those data aiming to observe a change in correlation values. 


<img src="https://github.com/esraguzel/dsc-mod-2-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-03-22%20at%2023.19.10.png?raw=true" width="100%">

<img src="https://github.com/esraguzel/dsc-mod-2-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-03-22%20at%2014.17.13.png?raw=true" width="100%">

<img src="https://github.com/esraguzel/dsc-mod-2-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-03-22%20at%2023.18.27.png?raw=true" width="100%">

<img src="https://github.com/esraguzel/dsc-mod-2-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-03-22%20at%2014.18.19.png?raw=true" width="100%">



There is positive and significant correlation between:

 - popularity and production budget, domestic gross and worldwide gross,  
 - ROI worldwide and ROI domestic.
 
There is weak linear relation between popularity and vote average.


Question 3: Is there any relation between ROI and genre? Which genre returns more ROI? What are the top genres in return?


To start with 'imdb_title_basics_gz' is chosen to work on since it contains high number of movies and the genres together. Then, it merged with 'tn_movie_budgets_gz' to unify all the necessary values in one dataframe. Also, the top genres are explored to gain insight about whether the genres returning more profit and popular genres are consistent with each other.

<img src="https://github.com/esraguzel/dsc-mod-1-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-02-16%20at%2019.01.36.png?raw=true" width="100%">

<img src="https://github.com/esraguzel/dsc-mod-1-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-02-16%20at%2019.02.24.png?raw=true" width="100%">



- Top 3 genres in terms of Worldwide ROI ratio are mystery, horror and thriller while on average reality-tv genre returns loss,
- Top 3 genres in terms of Domestic ROI ratio are mystery, horror and sport while reality-TV, news, western and war returns loss,
- Top genres produced are drama, comedy, action and thriller

- For worldwide movies mystery, horror and thriller genres should be preferred to reach higher worldwide ROI rates,
- For domestic movies mystery, horror and sport genres should be preferred to reach higher domestic ROI rates,
- For worldwide movies Reality-TV, for domestic movies reality-TV, news, western and war shouldn't be preferred.



