# Shuffle Tensor Elements

## Summary

- `randoom.shuffle()`

## Content

`tf.random.shuffle()` function can be used to shuffle tensors.

NOTE: `shuffle()` only shuffles the tensor along it's first dimension

```python
tensor = tf.constant([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
tensor
"""
<tf.Tensor: shape=(3, 3), dtype=int32, numpy=
array([[1, 2, 3],
       [4, 5, 6],
       [7, 8, 9]], dtype=int32)>
"""

tf.random.shuffle(tensor)
"""
<tf.Tensor: shape=(3, 3), dtype=int32, numpy=
array([[4, 5, 6],
       [1, 2, 3],
       [7, 8, 9]], dtype=int32)>
"""
```
