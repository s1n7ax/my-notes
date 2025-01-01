# Tensor Data Types (dtype)

## Summary

- Auto data type
- Set data type on creation

## Content

### Auto dtype

Type will be determined based on the value being passed

```python
tf.contant(7)
# <tf.Tensor: shape=(), dtype=int32, numpy=7>
```

```python
tf.constant(7.)
# <tf.Tensor: shape=(), dtype=float32, numpy=1.0>
```

### Specify the type

`dtype` keyword argument can be used to specify the type of the parameter

```python
tf.constant([1, 2, 3])
# <tf.Tensor: shape=(3,), dtype=int32, numpy=array([1, 2, 3], dtype=int32)>
```

```python
tf.constant([1, 2, 3], dtype=tf.float32)
# <tf.Tensor: shape=(3,), dtype=float32, numpy=array([1., 2., 3.], dtype=float32)>
```
