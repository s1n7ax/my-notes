# Visualizing the Loss

## Summary

- Visualizing the loss curve AKA training curve

## Content

- `model.fit` returns a table of training data

```python

trianing_data = model.fit(X_train, y_train, epochs=100, verbose=0)
trianing_data.history
'''
 	loss 	mae
0 	13283.436523 	13283.436523
1 	13038.412109 	13038.412109
2 	12411.069336 	12411.069336
3 	11086.649414 	11086.649414
4 	9185.347656 	9185.347656
... 	... 	...
95 	3920.450439 	3920.450439
96 	3885.978516 	3885.978516
97 	3856.638672 	3856.638672
98 	3842.188477 	3842.188477
99 	3831.773682 	3831.773682

100 rows × 2 columns
'''

```

- To visualize the history in a graph,

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

trianing_data = model.fit(X_train, y_train, epochs=100, verbose=0)

pd.DataFrame(trianing_data.history).plot()
plt.ylabel("loss")
plt.xlabel("epochs")
```

![[Pasted image 20231220235618.png]]
