# One-hot Encode

## Summary

It basically converts,

This

```
[0, 1, 3, 0]
```

To this

```
-----------------
| 1 | 0 | 0 | 0 |
| 0 | 1 | 0 | 0 |
| 0 | 0 | 0 | 1 |
| 1 | 0 | 0 | 0 |
-----------------
```

- `tf.one_hot()`

## Content

```python
X = tf.constant([0, 1, 3, 0])
tf.one_hot(X, depth = 4)
"""
<tf.Tensor: shape=(4, 4), dtype=float32, numpy=
array([[1., 0., 0., 0.],
       [0., 1., 0., 0.],
       [0., 0., 0., 1.],
       [1., 0., 0., 0.]], dtype=float32)>
"""
```
