# Binary Classification with Food 101 Dataset - Building CNN

## Summary

-

## Content

### Pre-processing images to be loaded to the CNN

```python
import tensorflow as tf
from tensorflow.keras.utils import image_dataset_from_directory
import pathlib

tf.random.set_seed(42)

train_dir = pathlib.Path("pizza_steak/train")
test_dir = pathlib.Path("pizza_steak/test")

train_data = image_dataset_from_directory(
    directory=train_dir,
    batch_size=32,
    image_size=(224, 224),
    label_mode="binary",
    seed=42
)

valid_data = image_dataset_from_directory(
    directory=test_dir,
    batch_size=32,
    image_size=(224, 224),
    label_mode="binary",
    seed=42
)

model = tf.keras.models.Sequential([
    # there is Normalization layer but it's not meant to be used for auto normalization
    # meaning, it will figure out how to normalize based on mean and variance
    # So in the case of an image, where the value could be 0 min and 255 max, we could use
    # Rescale to normalize the input data instead
    # tf.keras.layers.Normalization(axis=-1),

    # rescale layer will multiply the vector by the scale factor
    tf.keras.layers.Rescaling(scale=1/255)
    tf.keras.layers.Conv2D(filters=10,
                           kernel_size=3,
                           activation="relu",
                           input_shape=(224, 224, 3)),

    tf.keras.layers.Conv2D(10, 3, activation="relu"),
    tf.keras.layers.MaxPool2D(pool_size=2,
                              padding="valid"),
    tf.keras.layers.Conv2D(10, 3, activation="relu"),
    tf.keras.layers.Conv2D(10, 3, activation="relu"),
    tf.keras.layers.MaxPool2D(2),
    tf.keras.layers.Flatten(),
    tf.keras.layers.Dense(1, activation="sigmoid"),
])

model.compile(
    loss=tf.keras.losses.BinaryCrossentropy(),
    optimizer=tf.keras.optimizers.Adam(),
    metrics=['accuracy']
)

model.fit(train_data,
          epochs=5,
          steps_per_epoch=len(train_data),
          validation_data=valid_data,
          validation_steps=len(valid_data))
```
