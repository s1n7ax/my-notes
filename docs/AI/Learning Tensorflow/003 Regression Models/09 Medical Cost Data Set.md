# Medical Cost Data Set

## Summary

- Importing CSV
- One-hot encode data in Pandas
- Create training and testing data sets
- Train a model and evaluate

## Content

### Importing CSV

```python
import tensorflow as tf
import pandas as pd
import matplotlib.pyplot as plt


insurance = pd.read_csv('https://raw.githubusercontent.com/stedy/Machine-Learning-with-R-datasets/master/insurance.csv')
```

### One-hot encode

```python
i_one_hot = pd.get_dummies(insurance)

# head() shows the first 5 rows
i_one_hot.head()
```

### Training and testing data sets

```python
X = i_one_hot.drop("charges", axis=1)
y = i_one_hot["charges"]

from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

len(X), len(X_train), len(X_test)
```

### Training and evaluation

```python
model = tf.keras.Sequential([
    tf.keras.layers.Input(len(X.columns)),
    tf.keras.layers.Dense(50),
    tf.keras.layers.Dense(50),
    tf.keras.layers.Dense(50),
    tf.keras.layers.Dense(1),
])

model.compile(
    loss=tf.keras.losses.mae,
    optimizer=tf.keras.optimizers.Adam(learning_rate=0.0001),
    metrics=[tf.keras.losses.mae]
)

model.fit(X_train, y_train, epochs=5000, verbose=False)
model.evaluate(X_test, y_test)
"""
9/9 [==============================] - 0s 2ms/step - loss: 3161.2847 - mean_absolute_error: 3161.2847

[3161.28466796875, 3161.28466796875]

Results are way off but it's ok! We could improve that
"""

```
