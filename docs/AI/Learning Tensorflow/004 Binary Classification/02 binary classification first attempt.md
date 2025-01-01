# Binary Classification First Attempt

## Summary

- Using a linear regression model to predict non linear predictions (doing this just for understanding)

## Content

```python
from sklearn.datasets import make_circles
from sklearn.model_selection import train_test_split
import tensorflow as tf
import matplotlib.pyplot as plt

# this creates points to create two circles X contains x and y coordinates while y shows whether the point is
# in the inner circle or not
X, y = make_circles(n_samples=1000, noise=0.03)
plt.scatter(X[:, 0], X[:, 1], c=y, cmap=plt.cm.RdYlBu)
```

![[Pasted image 20231226194100.png]]


```python
X_train, X_test, y_train, y_test = train_test_split(X, y, train_size=0.8)

model = tf.keras.Sequential([
    tf.keras.layers.Input(2),
    tf.keras.layers.Dense(100),
    tf.keras.layers.Dense(1)
])

model.compile(
    loss=tf.keras.losses.BinaryCrossentropy(),
    optimizer=tf.keras.optimizers.Adam(),
    metrics=['accuracy']
)

model.fit(X_train, y_train, epochs=100, verbose=0)
model.evaluate(X_test, y_test)

"""
Accuracy is less than 50% however this is expected because this is not sutable for non linear problem
7/7 [==============================] - 0s 3ms/step - loss: 0.6938 - accuracy: 0.4650

[0.6938250064849854, 0.4650000035762787]
"""
```
