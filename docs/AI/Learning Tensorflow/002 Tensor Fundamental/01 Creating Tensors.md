# Creating Tensors

## Summary

- `tf.constant()`
- `tf.Variable()`

# Creating Tensors

1. `tf.constant()`
   - Once created, cannot be changed
2. `tf.Variable()`
   - Can be mutated

## Constant function

Once created, the value cannot be changed

```python
tf.constant([1, 2, 3])
# <tf.Tensor: shape=(3,), dtype=int32, numpy=array([1, 2, 3], dtype=int32)>
```

## Variable function

After created, the values can be changed using `tf.assign` or other operations

NOTE: New value should also be in the same shape and `dtype`

```python
vector = tf.Variable([1, 2, 3])
# <tf.Variable 'Variable:0' shape=(3,) dtype=int32, numpy=array([1, 2, 3], dtype=int32)>

vector.assign([4, 5, 6])
vector
# <tf.Variable 'Variable:0' shape=(3,) dtype=int32, numpy=array([4, 5, 6], dtype=int32)>

vector[0].assign(1)
vector
# <tf.Variable 'Variable:0' shape=(3,) dtype=int32, numpy=array([1, 5, 6], dtype=int32)>
```

## Variable vs Constant function

```python
readonly_vec = tf.constant([1, 2, 3])
vec = tf.Variable([1, 2, 3])

readonly_vec, vec

#(<tf.Tensor: shape=(3,), dtype=int32, numpy=array([1, 2, 3], dtype=int32)>,
# <tf.Variable 'Variable:0' shape=(3,) dtype=int32, numpy=array([1, 2, 3], dtype=int32)>)
```
