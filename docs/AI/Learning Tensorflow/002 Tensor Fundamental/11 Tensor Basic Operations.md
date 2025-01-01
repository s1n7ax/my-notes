# Tensor Basic Operations

## Summary

- `tf.math.add`
- `tf.math.subtract`
- `tf.math.multiply`
- `tf.math.divide`

## Content

```python
tensor = tf.constant([[1,2,3], [4,5,6]])

# add
# `tensor + 10` is also possible
tf.math.add(tensor, 10)
"""
<tf.Tensor: shape=(2, 3), dtype=int32, numpy=
array([[11, 12, 13],
       [14, 15, 16]], dtype=int32)>
"""

# subtract
# tensor - 10 is also possible
tf.math.subtract(tensor, 10)
"""
<tf.Tensor: shape=(2, 3), dtype=int32, numpy=
array([[-9, -8, -7],
       [-6, -5, -4]], dtype=int32)>
"""

# multiply
# tensor * 10 is also possible
tf.math.multiply(tensor, 10)
"""
<tf.Tensor: shape=(2, 3), dtype=int32, numpy=
array([[10, 20, 30],
       [40, 50, 60]], dtype=int32)>
"""

# divide
# tensor / 10 is also possible
tf.math.divide(tensor, 10)
"""
<tf.Tensor: shape=(2, 3), dtype=float64, numpy=
array([[0.1, 0.2, 0.3],
       [0.4, 0.5, 0.6]])>
"""
```
