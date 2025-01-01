# Data Casting

## Summary

- `tf.cast()`

## Content

- Casting `int32` to `float32`

```python
X = tf.constant([[1,2,3], [4,5,6]])
tf.cast(X, dtype=tf.float32)
"""
<tf.Tensor: shape=(2, 3), dtype=float32, numpy=
array([[1., 2., 3.],
       [4., 5., 6.]], dtype=float32)>
"""
```
