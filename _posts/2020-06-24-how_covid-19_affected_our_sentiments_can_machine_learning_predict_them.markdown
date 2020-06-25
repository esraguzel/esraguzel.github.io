---
layout: post
title:      "How COVID-19 affected our sentiments? Can machine learning predict them?"
date:       2020-06-24 09:38:37 -0400
permalink:  how_covid-19_affected_our_sentiments_can_machine_learning_predict_them
---


For the last six months, all people around the world got affected by Covid-19 in many ways. Other than losing the beloved ones, people lost jobs, kids couldn't go to school, domestic violence increased incredibly, suicide rates escalated... How could experts can analyse public's mental health and improve it?

Among substantive amount of data on Coronavirus I have chosen to analyse UK Twitter  and UK coronavirus official data to build an NLP based application to identify how our sentiments changed during Coronavirus lock down, what affected the most and up to what degree the change in death rates are effecting our sentiments, in particular negative sentiment for my last project at Flatiron school. In other words, project aimed at evaluating Covid-19 lock down period in terms of change in sentiments and helping to identify patterns, trends and public awareness levels related public mental health. 

A total number of 22250 unique tweets between 15 March 2020 and 30 May 2020 that contains coronavirus and UK as keywords are imported for sentiment analysis. In order to conduct sentiment analysis, initially I worked with VADER sentiment analyser which is a sentiment analysis tool based on lexicons of sentiment-related words, especially attuned to sentiments expressed in social media.

Here are the top 50 bigrams through VADER Sentiment Analyser:

<img src="https://github.com/esraguzel/dsc-capstone-project-v2-onl01-dtsc-ft-012120/blob/master/images/bigram.png?raw=true" width="100%">

To further asses VADER's performance, I have plotted the polarity scores and hot topics on Twitter together. 

<img src="https://github.com/esraguzel/dsc-capstone-project-v2-onl01-dtsc-ft-012120/blob/master/images/vader.png?raw=true" width="100%">


To compare the VADER's result, I have also trained a sentiment classifier model on top of BERT. BERT is a pre-trained transformer language model which is developed by Google and trained on Wikipedia text. As the training set for classifier model 1400 tweets are labelled as positive, negative and neutral. I then plotted sentiment scores and change ratio in sentiment scores using this newly trained model with the same intentions. 

<img src="https://github.com/esraguzel/dsc-capstone-project-v2-onl01-dtsc-ft-012120/blob/master/images/sentiment.png?raw=true" width="100%">

<img src="https://github.com/esraguzel/dsc-capstone-project-v2-onl01-dtsc-ft-012120/blob/master/images/change_sentiment.png?raw=true" width="100%">

The graphs speak for itself and shows how the custom model outperforms VADER at analysing our sentiments. When I compared the accuracy results for both models the custom model achieved 84 % accuracy while VADER reached only 53 % accuracy on manually labelled data. 




As part of my project I also trained SARIMA model to predict the change in death rates. The tricky part of using SARIMA is finding the optimal p, d, q values with the lowest AIC value. In my case, I conducted a grid search to find optimal values.  During the prediction I used both one step ahead prediction and forecasting together to evaluate my model's performance. Here is my model’s performance:



<img src="https://github.com/esraguzel/dsc-capstone-project-v2-onl01-dtsc-ft-012120/blob/master/images/dynamicforecast.png?raw=true" width="100%">

<img src="https://github.com/esraguzel/dsc-capstone-project-v2-onl01-dtsc-ft-012120/blob/master/images/forecast.png?raw=true" width="100%">




At last part of my project I wanted to explore how the change in death rates affected our sentiments, in particular negative sentiments. I binned the negative sentiment into two groups and used DecisionTree, RandomForest and XGBoost Classifiers.

Before talking about accuracy scores, I want to mention that I had only 75 data points. In my case, It is important to note that the ML models doesn't have enough data to learn and results are biased. 

Besides death rates, I used day of the weeks, shifted death rates, shifted positive sentiment change and shifted negative sentiment as features to predict change in negative sentiment. 

Among the trained machine learning models,  DecisionTree classifier reached the with 76% accuracy, while Random Forest with further tuning reached 72%. 

<img src="https://github.com/esraguzel/dsc-capstone-project-v2-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-06-24%20at%2022.02.03.png?raw=true" width="100%">

Here it can be observed that out model used death rates and shifted detah rates as expected:

<img src="https://github.com/esraguzel/dsc-capstone-project-v2-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-06-24%20at%2022.04.22.png?raw=true" width="100%">

In short, It was very exciting to explore how the sentiment analysers, language classifier models are able to judge our sentiments and able to spot the events that caused sudden change in our feelings. It is intersting to see how machine learning classifiers used death rates for predicting our sentiments. I strongly believe that with more data and features it is possible to get better predictions with machine learning classifiers. 

If you would like to view the code for this project, feel free to view it at the following GitHub repository:

https://github.com/esraguzel/dsc-capstone-project-v2-onl01-dtsc-ft-012120

Thank you.



