# Dimensions

## Summary

- Get dimensions
- Add dimensions

## Content

### Get the number of dimensions of a tensor

```python
scalar = tf.constant(7)
scalar.ndim
# 0
```

```python
vec = tf.constant([1, 2, 3])
vec.ndim
# 1
```

```python
matrix1 = tf.constant([
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9],
])
matrix1.ndim
# 2

matrix2 = tf.constant([
    [[1, 2, 3]],
    [[4, 5, 6]],
    [[7, 8, 9]],
])
matrix2.ndim
# 3
```

### Add new dimension to existing tensor

```python
tensor = tf.constant([[1,2,3], [4,5,6], [7,8,9]])
tensor.ndim
# 2

new_tensor1 = tensor[..., tf.newaxis]
new_tensor1
'''
<tf.Tensor: shape=(3, 3, 1), dtype=int32, numpy=
array([[[1],
        [2],
        [3]],

       [[4],
        [5],
        [6]],

       [[7],
        [8],
        [9]]], dtype=int32)>
'''

new_tensor1.ndim
# 3
```

```python

tensor = tf.constant([[1,2,3], [4,5,6], [7,8,9]])
tensor.ndim
# 2

new_tensor2 = tensor[tf.newaxis, ...]
new_tensor2
'''
<tf.Tensor: shape=(1, 3, 3), dtype=int32, numpy=
array([[[1, 2, 3],
        [4, 5, 6],
        [7, 8, 9]]], dtype=int32)>
'''

new_tensor2.ndim
# 3
```
