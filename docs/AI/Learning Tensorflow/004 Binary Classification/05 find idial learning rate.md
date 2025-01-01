# Find the Ideal Learning Rate

## Summary

- Dynamic learning rate update during training ( learning rate scheduler )
- Visualizing the learning rate to loss
- Find the ideal learning rate

## Content

### Learning Rate Scheduler

```python
model = tf.keras.Sequential([
    tf.keras.layers.Input(2),
    tf.keras.layers.Dense(10, activation="relu"),
    tf.keras.layers.Dense(10, activation="relu"),
    tf.keras.layers.Dense(1, activation="sigmoid"),
])

model.compile(
    loss=tf.keras.losses.BinaryCrossentropy(),
    optimizer=tf.keras.optimizers.Adam(),
    metrics=["accuracy"]
)

"""
Callback scheduler takes in a function. Function will receieve the current epoch. based on the current epoch,
we increase the learning rate

(epoch = 100) => 1e-4 * 10 ** ( 100 / 50 )

so the after 100th epoch, the learning rate becomes 1e-2 == 0.01
"""
lr_scheduler = tf.keras.callbacks.LearningRateScheduler(lambda epoch: 1e-4 * 10 ** (epoch/50))

history = model.fit(X_train, y_train, epochs=200, verbose=0, callbacks=[lr_scheduler])
model.evaluate(X_test, y_test)
```

### Visualizing the learning rate to loss

```python
# here we are creating a vector similar to the learning rate change
lrs = 1e-4 * ( 10 ** (tf.range(200) / 100) )
#                              ^^^ this should be the epoch

plt.figure()

# then we visualize it along side the loss curve
plt.semilogx(lrs, history.history['loss'])
```

![[Pasted image 20231228220955.png]]

### Find the Ideal Learning Rate

- Best to find the learning rate where the loss is just about to settle but still reducing

![[Pasted image 20231228221226.png]]
