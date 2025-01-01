# Matrix Multiplication

## Summary

- `tf.linalg.matmul()`

## Content

```python
# 2 x 3 matrix
tensor1 = tf.constant([
    [1,2,3],
    [4,5,6]
])

# 3 x 2 matrix
tensor2 = tf.constant([
    [3,5],
    [1,6],
    [2,7]
])

# If the number of columns in the first matrix is
# equal to the number of rows of the second matrix,
# the matrices can be multiplied
tf.linalg.matmul(tensor1, tensor2)
"""
<tf.Tensor: shape=(2, 2), dtype=int32, numpy=
array([[11, 38],
       [29, 92]], dtype=int32)>
"""
```
