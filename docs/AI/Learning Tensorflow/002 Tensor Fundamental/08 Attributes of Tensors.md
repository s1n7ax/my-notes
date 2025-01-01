# Attributes of Tensor

## Summary

- Shape
- Rank
- Axis
- Data type

## Content

Following are the main attributes of a tensor

1. **Shape** - Length of the each dimension

```python
tf.tensor.shape()
```

2. **Rank** - Number of dimensions of the tensor

```python
tf.tensor.ndim()
```

3. **Axis|Dimension** - Particular dimension of a tensor

```python
tensor[n]
```

4. **Size** - Total number of items in the tensor

```python
tf.size()
```

5. **DType** - Data type of the stored values

```python
tensor.dtype
```

Ex:-

```python
rand = tf.random.Generator.from_seed(40)
tensor = rand.normal(shape=(2, 3, 5))

tensor.shape
# TensorShape([2, 3, 5])

tensor.ndim
# 3

tensor[0, 0]
"""
<tf.Tensor: shape=(5,), dtype=float32, numpy=
array([-1.2864609,  2.1502466, -0.6779422,  1.4553545, -0.8907286],
      dtype=float32)>
"""

tf.size(tensor)
# <tf.Tensor: shape=(), dtype=int32, numpy=30>

tensor.dtype
# tf.float32
```
