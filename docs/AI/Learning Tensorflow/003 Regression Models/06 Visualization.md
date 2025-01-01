# Visualization

## Summary

Visualization of

- Data
- Model
- Training of a model
- Predictions of a model

## Content

### Visualizing Data

```python
import matplotlib.pyplot as plt

X = tf.range(-100, 100, 3)
y = X + 10

len70p = int(len(X) / 100 * 80)

X_train = X[:len70p]
y_train = y[:len70p]

X_test = X[len70p:]
y_test = y[len70p:]

plt.scatter(X_train, y_train, c="b", label="training data")
plt.scatter(X_test, y_test, c="r", label="testing data")
plt.legend()
```

![[Pasted image 20231020220634.png]]

### Visualizing Model

**Method !:**:

```python
model = tf.keras.Sequential([
    tf.keras.layers.Input(1),
    tf.keras.layers.Dense(100),
    tf.keras.layers.Dense(100),
    tf.keras.layers.Dense(1)
])

model.summary()

"""
Model: "sequential"
_________________________________________________________________
 Layer (type)                Output Shape              Param #
=================================================================
 dense (Dense)               (None, 100)               200

 dense_1 (Dense)             (None, 100)               10100

 dense_2 (Dense)             (None, 1)                 101

=================================================================
Total params: 10,401
Trainable params: 10,401
Non-trainable params: 0
_________________________________________________________________
"""
```

**Method 2:**

```python
model = tf.keras.Sequential([
    tf.keras.layers.Input(1),
    tf.keras.layers.Dense(100),
    tf.keras.layers.Dense(100),
    tf.keras.layers.Dense(1)
])

tf.keras.utils.plot_model(
    model=model,
    show_shapes=True,
    show_dtype=True,
    show_trainable=True
)
```

![[Pasted image 20231020221539.png]]

### Visualizing the training of a model

### Visualizing the predictions of a model

```python
y_predict = model.predict(X_test)

import matplotlib.pyplot as plt

plt.scatter(X_test, y_test, c="g", label="Expected")
plt.scatter(X_test, y_predict, c="red", label="Actual")
```

![[Pasted image 20231024182807.png]]
