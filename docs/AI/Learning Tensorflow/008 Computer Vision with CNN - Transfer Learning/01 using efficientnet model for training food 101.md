# Using EfficientNet Model for Food 101

## Summary

- What is transfer learning
- What is feature extraction
- How to use `efficientnet` model to train on food 101 dataset

## Content

### What is transfer learning

### What is feature extraction

### How to use `efficientnet` model to train on food 101 dataset

```python
import tensorflow as tf
import tensorflow_hub as hub
from tensorflow.keras import layers
import datetime


def create_tensorboard_callback(dirname, experiment_name):
    log_dir = (
        dirname
        + "/"
        + experiment_name
        + "/"
        + datetime.datetime.now().strftime("%Y%m%d-%H%M%S")
    )
    callback = tf.keras.callbacks.TensorBoard(log_dir=log_dir)
    print(f"saving tensorboard log files to: {log_dir}")
    return callback


IMG_SIZE = 180

feature_extractor_layer = hub.KerasLayer(
    efficient_net_url,
    trainable=False,
    name="feature_extraction_layer",
    input_shape=(IMG_SIZE, IMG_SIZE) + (3,),
)

model = tf.keras.Sequential(
    [
        tf.keras.layers.Resizing(IMG_SIZE, IMG_SIZE),
        tf.keras.layers.Rescaling(1 / 255),
        feature_extractor_layer,
        tf.keras.layers.Dense(10, activation="softmax"),
    ]
)

model.compile(
    loss=tf.keras.losses.SparseCategoricalCrossentropy(),
    optimizer=tf.keras.optimizers.Adam(),
    metrics=["accuracy"],
)

history = model.fit(
    train_data,
    validation_data=test_data,
    epochs=10,
    callbacks=[
        create_tensorboard_callback(
            dirname="tensorflow_hub", experiment_name="efficientnet_v2"
        )
    ],
)
```
