# Normalizing Fashion Mnist Data

## Summary

- Normalize the data and train the model using the same configuration

## Content

### Normalize the data

```python
train_data_norm = train_data / 255
test_data_norm = test_data / 255
```

### Re-train the model

```python
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

history = model.fit(train_data_norm, train_labels, epochs=4, verbose=0)
model.evaluate(test_data_norm, test_labels)

"""
BEFORE:
313/313 [==============================] - 1s 2ms/step - loss: 1.0432 - accuracy: 0.5858

AFTER:
313/313 [==============================] - 1s 3ms/step - loss: 0.4513 - accuracy: 0.8402
"""
```
