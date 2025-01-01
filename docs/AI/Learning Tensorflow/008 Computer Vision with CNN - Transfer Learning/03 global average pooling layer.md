# Global Average Pooling Layer

## Summary

- `Flatten` vs `GlobalAveragePooling2D`
- What is `GlobalAveragePooling2D` layer

## Content

## Flatten vs GlobalAveragePooling2D

If we use Flatten instead of GlobalAveragePooling2D, accuracy of the end model
would be quite similar. However, `Flatten` and `GlobalAveragePooling2D` works
differently.

### Flatten

`Flatten` flatten the nd vector until the 1st axis

```python
a = tf.constant([[[[1, 2, 3], [2, 2, 3], [16, 2, 3]]]], dtype=tf.float32)

print(tf.keras.layers.Flatten()(a))
print(tf.keras.layers.GlobalAveragePooling2D()(a))
print(tf.reduce_mean(a, axis=[1, 2]))

"""
tf.Tensor([[ 1.  2.  3.  2.  2.  3. 16.  2.  3.]], shape=(1, 9), dtype=float32)
tf.Tensor([[6.3333335 2.        3.       ]], shape=(1, 3), dtype=float32)
tf.Tensor([[6.3333335 2.        3.       ]], shape=(1, 3), dtype=float32)
"""
```

## What is Average Pooling Layer

In previous example, we were using the `EfficientNetB0` to use derive the
existing features learnt by the base_model. When training the new model with the
base model, we keep the base model unchanged but get the feature vectors from
the base model using `GlobalAveragePooling2D` layer. Here
`GlobalAveragePooling2D` is used to extract the most important features from the
base model output.
