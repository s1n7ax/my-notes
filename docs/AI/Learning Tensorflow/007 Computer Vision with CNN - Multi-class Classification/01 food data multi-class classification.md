# Food Data Multi-class Classification

## Summary

- Training a multi-class classification model

## Content

### Training a Multi-class Classification Model

```python
!wget https://storage.googleapis.com/ztm_tf_course/food_vision/10_food_classes_all_data.zip

import zipfile

with zipfile.ZipFile('10_food_classes_all_data.zip', 'r') as f:
    f.extractall()

from tensorflow.keras.utils import image_dataset_from_directory
import tensorflow as tf

train_dir = '10_food_classes_all_data/train'
test_dir = '10_food_classes_all_data/test'

train_data = image_dataset_from_directory(train_dir)
test_data =  image_dataset_from_directory(test_dir)
class_names = train_data.class_names

len(train_data), len(test_data), class_names

model = tf.keras.Sequential([
    tf.keras.layers.Resizing(180, 180),
    tf.keras.layers.Rescaling(1./255),
    tf.keras.layers.Conv2D(10, 3, activation='relu'),
    tf.keras.layers.Conv2D(10, 3, activation='relu'),
    tf.keras.layers.MaxPooling2D(),

    tf.keras.layers.Conv2D(10, 3, activation='relu'),
    tf.keras.layers.Conv2D(10, 3, activation='relu'),
    tf.keras.layers.MaxPooling2D(),

    tf.keras.layers.Flatten(),
    tf.keras.layers.Dense(len(class_names), activation='softmax')
])

model.compile(
    loss=tf.keras.losses.SparseCategoricalCrossentropy(),
    optimizer=tf.keras.optimizers.Adam(),
    metrics=['accuracy']
)

history = model.fit(train_data, epochs=4, validation_data=test_data)

"""
Accuracy is not that greate but at lease it performs better than randomly
guessing

Epoch 1/5
235/235 [==============================] - 25s 93ms/step - loss: 2.1862 - 
accuracy: 0.1849 - val_loss: 1.9902 - val_accuracy: 0.2952
Epoch 2/5
235/235 [==============================] - 25s 103ms/step - loss: 1.9091 - 
accuracy: 0.3392 - val_loss: 1.8910 - val_accuracy: 0.3476
Epoch 3/5
235/235 [==============================] - 22s 93ms/step - loss: 1.6766 - 
accuracy: 0.4292 - val_loss: 1.9594 - val_accuracy: 0.3304
Epoch 4/5
235/235 [==============================] - 23s 98ms/step - loss: 1.3300 - 
accuracy: 0.5552 - val_loss: 2.2000 - val_accuracy: 0.3280
"""
```
