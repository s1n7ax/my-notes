# Conv2D Layer

## Summary

- filter
- kernel size
- padding
- Strides

## Content

### Conv2D Layer Example

```python
tf.keras.layers.Conv2D(
    filters=10,
    kernel_size=3,
    padding="valid",
    strides=(1, 1),
    activation="relu",
    input_shape=(224, 224, 3),
)
```

### Filter

The number of convolutional filters in that layer. In the example above, there
are 10 filters. So, each filter will get a kernel weight of size `3 x 3` that's
unique to each convolutional filter.

### Kernel

Determines the shape of the filter matrix (sliding window)

### Padding

### Strides

Number of steps a filter takes across an image at a time
