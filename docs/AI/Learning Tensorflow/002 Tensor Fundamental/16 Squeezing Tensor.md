# Squeezing Tensor

## Summary

Removes dimensions of size 1 from the shape of a sensor

- `tf.squeeze()`

## Content

```python
X = tf.random.uniform(shape=[1, 2, 1, 1, 5], minval = 1, maxval = 100)
squeezed = tf.squeeze(X)
X.shape, squeezed.shape, squeezed
"""
(TensorShape([1, 2, 1, 1, 5]),
 TensorShape([2, 5]),
 <tf.Tensor: shape=(2, 5), dtype=float32, numpy=
 array([[32.754486, 84.23745 , 21.90291 , 91.42302 , 36.214336],
        [58.26638 , 17.401817, 19.807457, 59.926483, 60.50828 ]],
       dtype=float32)>)
"""
```
