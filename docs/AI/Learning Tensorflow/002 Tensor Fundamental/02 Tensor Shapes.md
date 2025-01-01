# Tensor Shapes

## Summary

Mainly, we will talk about following data types

- Scalar
- Vector
- Multi-Dimensional (Matrix)

## Content

### Scalar

- Creating a scalar

```python
tf.constant(7)
# <tf.Tensor: shape=(), dtype=int32, numpy=7>
```

### Vector

- Creating a vector

```python
tf.constant([1, 2, 3])
# <tf.Tensor: shape=(3,), dtype=int32, numpy=array([1, 2, 3], dtype=int32)>
```

### Matrix

- Creating a matrix

```python
tf.constant([
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9],
])
''
<tf.Tensor: shape=(3, 3), dtype=int32, numpy=
array([[1, 2, 3],
       [4, 5, 6],
       [7, 8, 9]], dtype=int32)>
''
```
