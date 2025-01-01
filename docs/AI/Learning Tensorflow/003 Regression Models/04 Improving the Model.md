# Improving the Model

## Summary

- When creating the model
  - By increasing the number of layers
  - By increasing the number of units per layer
- When compiling the model
  - By changing the optimization function
- When fitting the model
  - By changing the epochs
  - By increasing the number of training data

## Content

```python
# number of layers and units per layers has increased
model = tf.keras.Sequential([
    tf.keras.layers.Input(1),
    tf.keras.layers.Dense(100),
    tf.keras.layers.Dense(100),
    tf.keras.layers.Dense(1)
])

# using a better optimizer for the job
model.compile(
    loss=tf.keras.losses.mae,
    optimizer=tf.keras.optimizers.Adam(learning_rate=0.0001),
    metrics=[ tf.keras.losses.mae ]
)

# increase the number of iterations
model.fit(X, y, epochs=100)

model.predict([7])
# array([[15.082852]], dtype=float32)
# pretty close hah?
```
