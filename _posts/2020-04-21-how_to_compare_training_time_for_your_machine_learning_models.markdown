---
layout: post
title:      "How to compare training time for your machine learning models "
date:       2020-04-21 23:21:05 +0000
permalink:  how_to_compare_training_time_for_your_machine_learning_models
---

Most of the time applying and comparing machine learning models to our datasets  takes plenty of time.  To simplify this process and avoid confusion, the data scientists show the results in small dataframes.

In my last project I wanted to compare a few machine learning models in terms of accucary, f1and recall scores as well as training time.  

As I earlier stored my model results in 'best_model_params'  file, first I called my results for each model. I also stored the names and the classifiers in a dictionary called 'classifiers'.  

Rest of the code is quite simple that each model is fitted and scores calculated with the help of a for loop. 

During this process training time can easily calculated by applying `time.clock() `just before and after fitting the models. 

After appending your results in an empty dictionary, you can easily compare you models!

```
import os

if os.path.isfile('best_model_params.json'):
    with open('best_model_params.json', 'r') as file:
        model_params = json.load(file)
        
else:
    pass

classifiers = {
    "Logistic Regression": LogisticRegression(),
    "Decision Tree": DecisionTreeClassifier(),
    "Random Forest": RandomForestClassifier(),
    "XGBoost Classifier": xgb.XGBClassifier(),
    "Naive Bayes": GaussianNB(),
}

import time

results = {}
for model_title, model  in classifiers.items():
    
    model.set_params(**model_params.get(model_title))
    t_start = time.clock()
    model.fit(X_train, y_train)
    t_end = time.clock()
    t_diff = t_end - t_start
    
    training_preds = model.predict(X_train)
    y_pred = model.predict(X_test)
    training_accuracy = accuracy_score(y_train, training_preds)
    val_accuracy = accuracy_score(y_test, y_pred)
    f1 = f1_score(y_test, y_pred)
    recall = recall_score(y_test, y_pred)

    results[model_title] = {
        'Training time': t_diff,
        'Training score': training_accuracy,
        'Test score': val_accuracy,
        'f1 Score': f1,
        'Recall Score' : recall
    }

pd.DataFrame(results).T
```

<img src="https://github.com/esraguzel/dsc-mod-3-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-04-21%20at%2022.29.34.png?raw=true" width="100%">
