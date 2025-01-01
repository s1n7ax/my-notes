# Defining Models in Functional vs Sequential

## Summary

- Defining a model using functional pattern
- Defining a model using sequential pattern

## Content

Instead of using `Sequential` to create layers, functional approach can be used
to create the model. From the results, you can see, evaluation shows the
accuracy is similar in both models.

### Functional

```python
import tensorflow as tf

base_model = tf.keras.applications.EfficientNetB0(include_top=False)
base_model.trainable = False

inputs = tf.keras.layers.Input((256, 256, 3), name="input_layer")

x = base_model(inputs)
x = tf.keras.layers.GlobalAveragePooling2D(name="pooling_layer")(x)
outputs = tf.keras.layers.Dense(10, activation="softmax", name="output_layers")(x)

model_0 = tf.keras.Model(inputs, outputs)

model_0.compile(
    loss=tf.keras.losses.SparseCategoricalCrossentropy(),
    optimizer=tf.keras.optimizers.Adam(),
    metrics=["accuracy"],
)

model_0.fit(train_data, validation_data=test_data, epochs=4)
"""
loss: 1.8878 - accuracy : 0.3880 - val_loss: 1.3062 - val_accuracy: 0.7228
loss: 1.1279 - accuracy : 0.7467 - val_loss: 0.8900 - val_accuracy: 0.8208
loss: 0.8099 - accuracy : 0.8240 - val_loss: 0.7078 - val_accuracy: 0.8412
loss: 0.6601 - accuracy : 0.8467 - val_loss: 0.6165 - val_accuracy: 0.8564
"""
```

### Sequential

```python
import tensorflow as tf

base_model = tf.keras.applications.EfficientNetB0(include_top=False)
base_model.trainable = False

model = tf.keras.Sequential(
    [
        tf.keras.layers.Input((256, 256, 3)),
        base_model,
        tf.keras.layers.GlobalAveragePooling2D(),
        tf.keras.layers.Dense(10, activation="softmax"),
    ]
)

model.compile(
    loss=tf.keras.losses.SparseCategoricalCrossentropy(),
    optimizer=tf.keras.optimizers.Adam(),
    metrics=["accuracy"],
)

model.fit(train_data, validation_data=test_data, epochs=4)

"""
loss: 1.9393 - accuracy : 0.3893 - val_loss: 1.3565 - val_accuracy: 0.7188
loss: 1.1338 - accuracy : 0.7640 - val_loss: 0.8972 - val_accuracy: 0.8192
loss: 0.8184 - accuracy: 0.8213 - val_loss: 0.7134 - val_accuracy: 0.8416
loss: 0.6624 - accuracy: 0.8547 - val_loss: 0.6223 - val_accuracy: 0.8532
""""
```
