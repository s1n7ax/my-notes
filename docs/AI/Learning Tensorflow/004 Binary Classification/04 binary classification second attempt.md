# Binary Classification Second Attempt

## Summary

- Adjusting the linear model for non-linear problem

## Content

### Adjusting the linear model for non-linear problem

- In a binary classification problem, we can use `ReLU` for hidden layers, and `sigmoid` for output layers

```python
model = tf.keras.Sequential([
    tf.keras.layers.Input(2),
    tf.keras.layers.Dense(10, activation = 'relu'),
    tf.keras.layers.Dense(10, activation = 'relu'),
    tf.keras.layers.Dense(1, activation = 'sigmoid'),
])

model.compile(
    loss = tf.keras.losses.BinaryCrossentropy(),
    optimizer = tf.keras.optimizers.Adam(),
    metrics = ['accuracy']
)

model.fit(X_train, y_train, epochs = 200, verbose=0)
```

![[Pasted image 20231227131315.png]]