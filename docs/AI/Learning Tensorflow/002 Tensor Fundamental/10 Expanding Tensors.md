# Expanding Tensors

## Summary

- `tf.newaxis`
- `tf.expand_dims()`

## Content

```python
tensor = tf.constant([[1, 2, 3], [4, 5, 6]])

# [...] is equal to [:, :] in this case
tensor[..., tf.newaxis]
"""
<tf.Tensor: shape=(2, 3, 1), dtype=int32, numpy=
array([[[1],
        [2],
        [3]],

       [[4],
        [5],
        [6]]], dtype=int32)>
"""
```

# similar behaviour can be achieved using expand_dims

```python
tensor = tf.constant([[1, 2, 3], [4, 5, 6]])

tf.expand_dims(tensor, axis=-1)
"""
<tf.Tensor: shape=(2, 3, 1), dtype=int32, numpy=
array([[[1],
        [2],
        [3]],

       [[4],
        [5],
        [6]]], dtype=int32)>
"""
```
