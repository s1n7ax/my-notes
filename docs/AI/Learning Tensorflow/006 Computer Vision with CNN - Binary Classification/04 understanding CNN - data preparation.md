# CNN Data Preparation

## Summary

- Images into batches
- Data normalization

## Content

### Images into batches

#### Why make image batches

- There might not be enough memory to fit all the images into memory at the same
  time
- Trying to learn many images in one go could result in the model not being able
  to learn very well

#### How to make batches

```python
import tensorflow as tf
from tensorflow.keras.utils import image_dataset_from_directory
import pathlib

tf.random.set_seed(42)

train_dir = pathlib.Path("pizza_steak/train")

train_data = image_dataset_from_directory(
    directory=train_dir,
    batch_size=32,
    image_size=(224, 224),
    label_mode="binary",
    seed=42
)

obj_iter = iter(train_data.take(1))
i, l  = next(obj_iter)
print(i.shape)
```

### Data normalization

#### Why data normalization

- When the data is normalized, it tend to perform better

#### How to normalize data

```python
input = tf.constant([[2, 34, 255],
         [35, 231, 123],
         [52, 231, 111]])

# Rescaling layer will multiply the vector by the given scale factor
layer = tf.keras.layers.Rescaling(scale=1/255)
output = layer(input)

print(input)
print(output)

"""
tf.Tensor(
[[  2  34 255]
 [ 35 231 123]
 [ 52 231 111]], shape=(3, 3), dtype=int32)
tf.Tensor(
[[0.00784314 0.13333334 1.        ]
 [0.13725491 0.9058824  0.48235297]
 [0.20392159 0.9058824  0.43529415]], shape=(3, 3), dtype=float32)
"""
```
