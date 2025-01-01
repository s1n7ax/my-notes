# Classification of Fashion Mnist Data Set

## Summary

- classification of fashion mnist data set

## Content

```python
import tensorflow as tf
from tensorflow.keras.datasets import fashion_mnist
import matplotlib.pyplot as plt
import pandas as pd

(train_data, train_labels), (test_data, test_labels) = fashion_mnist.load_data()

# this is to visualize the image at `index`
index = 120

plt.imshow(train_data[index], cmap=plt.cm.binary)
plt.title(class_names[train_labels[index]])

tf.random.set_seed(42)

model = tf.keras.Sequential([
    tf.keras.layers.Flatten(),
    tf.keras.layers.Dense(10, activation="relu"),
    tf.keras.layers.Dense(10, activation="relu"),
    tf.keras.layers.Dense(10, activation="softmax")
])

model.compile(
    loss=tf.keras.losses.SparseCategoricalCrossentropy(),
    optimizer=tf.keras.optimizers.Adam(),
    metrics=['accuracy'],
)

history = model.fit(train_data, train_labels, epochs=4)
model.evaluate(test_data, test_labels)

"""
Accuracy is not that greate but it's ok!
We can improves this

313/313 [==============================] - 1s 2ms/step - loss: 1.0432 - accuracy: 0.5858

[1.0431597232818604, 0.5857999920845032]
"""
```
