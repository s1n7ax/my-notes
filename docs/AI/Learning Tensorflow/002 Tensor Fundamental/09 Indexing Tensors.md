# Indexing Tensors

## Summary

- Get the first two values from each dimension
- Get the first index from each dimension

## Content

### Get the first two values from each dimension

```python
tensor = tf.constant([[1,2,3], [4,5,6], [7,8,9]])

# following returns the first two elements of the first dimension
tensor[:2]
'''
<tf.Tensor: shape=(2, 3), dtype=int32, numpy=
array([[1, 2, 3],
       [4, 5, 6]], dtype=int32)>
'''

# following returns the first two elements of the first dimension
# after that, from the first result tensor, it will get first two dimension
# from the second dimension
tensor[:2, :2]
'''
<tf.Tensor: shape=(2, 2), dtype=int32, numpy=
array([[1, 2],
       [4, 5]], dtype=int32)>
'''
```

### Get the first two values from last dimension

```python
tensor = tf.constant([[1,2,3], [4,5,6], [7,8,9]])

# just : will return all
# :1 will return first element from the second dimension
tensor[:, :1]
'''
<tf.Tensor: shape=(3, 2), dtype=int32, numpy=
array([[1, 2],
       [4, 5],
       [7, 8]], dtype=int32)>
'''
```

### Get the last value from last dimension

```python
tensor = tf.constant([[1,2,3], [4,5,6], [7,8,9]])

# -1 returns the last element from the tensor just like lists in python
tensor[:, -1]

'''
<tf.Tensor: shape=(3,), dtype=int32, numpy=array([3, 6, 9], dtype=int32)>
'''
```
