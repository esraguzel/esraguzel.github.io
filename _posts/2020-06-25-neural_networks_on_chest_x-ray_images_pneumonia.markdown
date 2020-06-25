---
layout: post
title:      "Neural Networks on Chest X-Ray Images (Pneumonia)"
date:       2020-06-25 17:26:15 +0000
permalink:  neural_networks_on_chest_x-ray_images_pneumonia
---



In this project, the [Chest X-Ray Images (Pneumonia)] dataset on Kaggle is chosen to work on. The aim of this project is to predict whether the X-Ray images are belong to a healthy person or a pneumonia patient by applying neural network models.

The aim of to this project is to increase recall score for pneumonia images (Sensitivity) above 95% and target recall score for normal images (Specificity) above 90%.


The data obtained from [Kaggle](https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia) has 5860 training images, divided into 3 fold of train, validation and test. The data is also highly imbalanced that number of pneumonia images exceeds the number of normal images nearly 3 times.

After manual redistribution of the dataset into 3 folders, train set contains 70%, test and validation and test sets contains 15% of the data and balanced shares of normal and pneumonia images.

It is important to note that initial accuracy levels of the deep learning models visibly increased after balanced re-distibution of the images into train, validation and test folders. 


To observe accuracy and recall scores throughout the models, 7 models applied. 

- Basic neural network model with 2 layers
- Regulatized basic neural networks model with dropout
- Convolutional neural networks model
- Deep convolutional neural networks model
- Xception
- VGG16
- VGG19 

Recall, accuracy and f1 scores are used for evaluation metrics. As the data is highly imbalanced to increase performance of the last model data augmentation is also applied to the dataset.

As the models got complicated, it is observed accuracy, sensitivity and specificity scores increased throughout the models. Also, it is noticed that data augmentation lead to rise in both recall scores for each labels and increased model performance.

Among all trained models;


- CNN 2.0 performed the highest accuracy score,
- VGG19 achieved the highest specificity score,
- VGG16 achieved the highest sensitivity score,
- Baseline model has the lowest specificity and accuracy,
- VGG19 has the minimum sensitivity.



<img src="https://github.com/esraguzel/dsc-mod-4-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-05-20%20at%2020.58.36.png?raw=true" width="100%">

Among all the trained models, initially the best resulted obtained from the deeply connected CNN model. 


The model predicted;

- 19 False positives,
- 621 True positives,
- 175 True negatives,
- 61 False negatives.

<img src="https://github.com/esraguzel/dsc-mod-4-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-05-20%20at%2020.15.23.png?raw=true" width="100%">

The second cnn mmodel by performing 97% recall score for pneumonia (Sensitivity) partially achieved the set threshold. However, it is still underperforming in terms of Specificity threshold. 

<img src="https://github.com/esraguzel/dsc-mod-4-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-05-20%20at%2020.15.03.png?raw=true" width="100%">


This model should be used as a tool by medical experts and specialists which will support their diagnosis and treatment method. To reach higher levels of accuracy and recall score oversampling techniques should be used.Balancing the number of labels may also lead to higher accuracy and recall scores. 

 The Dataset can be enriched, and the target variables can be balanced by oversampling methods. Different pretrained models can be applied to observe accuracy , f1 and recall scores. The model can be trained over to detect the cause of pneumonia (bacteria or virus).


