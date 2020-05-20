---
layout: post
title:      "Observing Sensitivity and Specificity Throughout the Neural Network Models"
date:       2020-05-18 13:43:47 -0400
permalink:  observing_sensitivity_and_specificity_throughout_the_neural_network_models
---




In healthcare sector, it is believed that human-caused errors are the primary cause of negative experiences/events. To prevent medical human errors and improve patient safety many approaches and methods developed and combined with different fields such as computer science. 

Like in many fields, deep learning models becomes very useful in healthcare sector by reducing human caused errors, minimizing diagnosis time&costs, lowering medical legal risks and maximizing patient safety. 

One of the most common practices of deep learning in medical field is detecting the patients by classifying X-ray images.  Here, we will observe how accuracy, and recall scores will change as the neural network models gets deeper and more complicated. 

The data used for modelling 5860 training images of healthy persons and pneumonia patients, divided into 3-fold of train, validation and test. The data is also highly imbalanced that number of pneumonia images exceeds the number of normal images nearly 3 times.

Let's start with basic neural network model.

```
model = models.Sequential()
model.add(layers.Dense(10, activation='relu', input_shape=(12288,))) 
model.add(layers.Dense(5, activation='relu'))
model.add(layers.Dense(1, activation='sigmoid'))

optimizer = keras.optimizers.Adam(lr=0.00001,
    beta_1=0.9,
    beta_2=0.999,
    epsilon=1e-07,
    amsgrad=False)
		
model.compile(optimizer=optimizer,
              loss='binary_crossentropy',
              metrics=['accuracy'])
							
							
history = model.fit(train_img,
                    train_y,
                    epochs=60,
                    batch_size=32,
                    validation_data=(val_img, val_y))
```

Here is the accuracy report for this model:

```
		precision    recall  f1-score   support

 0       0.86      0.99        0.92            640
 1       0.96      0.56        0.70           236
 
accuracy                               0.87      876
macro avg          0.91      0.77      0.81       876
weighted avg       0.88      0.87      0.86       876
 
```



Here we can observe that accuracy is not enough for analysing our model's performance. Tough the accuracy score indicates 87% success, poor recall score for normal (Specificity) cases (56%) indicates that the model performed when detected pneumonia but performed poorly when detecting healthy X-ray images.


For the second model we will use a basic convolutional neural networks model:

```
model = models.Sequential()

model.add(layers.Conv2D(32, (3, 3), activation='relu', input_shape=(64, 64, 3)))
model.add(layers.MaxPooling2D((2, 2)))

model.add(layers.Conv2D(32, (4, 4), activation='relu'))
model.add(layers.MaxPooling2D((2, 2)))

model.add(layers.Conv2D(64, (3, 3), activation='relu'))
model.add(layers.MaxPooling2D((2, 2)))

model.add(layers.Flatten())
model.add(layers.Dense(64, activation='relu'))
model.add(layers.Dense(1, activation='sigmoid'))

model.compile(loss='binary_crossentropy',
              optimizer=optimizer,
              metrics=['acc'])

history = model.fit(train_images,
                    train_y,
                    epochs=30,
                    batch_size=32,
                    validation_data=(val_images, val_y))
									
```

Here is the classification report for the basic cnn model:
```

						precision    recall  f1-score      support

				 0       0.90      0.98      0.94            640
				 1       0.92      0.70      0.80           236

accuracy                                     0.90           876
macro avg          0.91      0.84     0.87                 876
weighted avg       0.90      0.90      0.90                 876
```


Here we can observe how a basic cnn model starts to differ local patterns of pneumonia and normal X-Ray images and our sensitivity rate increased to 70%. 
 
 The last model is a deeply connected cnn model.
 
```
model = Sequential()

model.add(Conv2D(16, (3, 3), input_shape=input_shape, kernel_initializer=glorot_uniform(seed=SEED)))
model.add(BatchNormalization())
model.add(Activation('relu'))
model.add(MaxPooling2D((2, 2)))

model.add(Conv2D(32, (3, 3), kernel_regularizer=l2(0.01), kernel_initializer=glorot_uniform(seed=SEED)))
model.add(BatchNormalization())
model.add(Activation('relu'))
model.add(MaxPooling2D((2, 2)))

model.add(Conv2D(64, (3, 3), kernel_regularizer=l2(0.01), kernel_initializer=glorot_uniform(seed=SEED)))
model.add(BatchNormalization())
model.add(Activation('relu'))
model.add(MaxPooling2D((2, 2)))
model.add(Dropout(rate=0.3, seed=SEED))

model.add(Flatten())
model.add(Dense(450, kernel_regularizer=l2(0.01), kernel_initializer=glorot_uniform(seed=SEED)))
model.add(BatchNormalization())
model.add(Activation('relu'))
model.add(Dense(1, activation='sigmoid', kernel_initializer=glorot_uniform(seed=SEED)))

model.compile(optimizer=SGD(lr=0.01, nesterov=True),
              loss=binary_crossentropy,
              metrics=['accuracy'])


model.summary()
```


And the classification report for the last cnn model:

      `precision    recall  f1-score         support`


```
0       0.88      0.78      0.83           236
1       0.92      0.96      0.94           640

accuracy                        0.91      876
macro avg     0.90      0.87    0.89      876
weighted avg 0.91      0.91      0.91    876
```

While the last model's accuracy score seems to increase slightly, by analysing the recall scores for each label it is observed that the model correctly predicted 96 % of the pneumonia 78 % of the normal people.

In conclusion, as the neural networks models got more complicated and deeper, it is observed that the overall accuracy of the model slightly increased, but the performance of the model for detecting both labels increased a lot. 

