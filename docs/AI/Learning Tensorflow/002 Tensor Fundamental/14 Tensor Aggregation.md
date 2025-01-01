# Tensor Aggregation

## Summary

- Absolute of tensor `tf.abs()`
- Max value `tf.reduce_max()`
- Min `tf.reduce_min()`
- Mean `tf.reduce_mean()`
- Sum `tf.reduce_sum()`
- Variance `tf.math.reduce_variance(X)`
- Standard Deviation `tf.reduce_std()`

## Content

### Absolute of tensor

```python
X = tf.constant([-7, -10])
tf.abs(X)
"""
<tf.Tensor: shape=(2,), dtype=int32, numpy=array([ 7, 10], dtype=int32)>
"""
```

### Max of tensor

```python
X = tf.random.uniform(shape = (2,3), minval = 0, maxval = 100)
X, tf.reduce_max(X)
"""
(<tf.Tensor: shape=(2, 3), dtype=float32, numpy=
 array([[10.74779 ,  5.89422 , 64.03551 ],
        [82.08326 , 57.110287, 77.921165]], dtype=float32)>,
 <tf.Tensor: shape=(), dtype=float32, numpy=82.08326>)
"""
```

### Min of tensor

```python
X = tf.random.uniform(shape = (2,3), minval = 0, maxval = 100)
X, tf.reduce_min(X)
"""
(<tf.Tensor: shape=(2, 3), dtype=float32, numpy=
 array([[77.48363 , 31.440676, 66.64853 ],
        [46.323574,  6.213486, 99.50342 ]], dtype=float32)>,
 <tf.Tensor: shape=(), dtype=float32, numpy=6.213486>)
"""
```

### Mean of tensor

```python
X = tf.random.uniform(shape = (2,3), minval = 0, maxval = 100)
X, tf.reduce_mean(X)
"""
(<tf.Tensor: shape=(2, 3), dtype=float32, numpy=
 array([[80.673096, 26.919794, 35.174118],
        [20.695389, 12.291718, 23.293627]], dtype=float32)>,
 <tf.Tensor: shape=(), dtype=float32, numpy=33.174625>)
"""
```

### Sum of tensor

```python
X = tf.random.uniform(shape = (2,3), minval = 0, maxval = 100)
X, tf.reduce_sum(X)

"""
(<tf.Tensor: shape=(2, 3), dtype=float32, numpy=
 array([[30.714083, 42.53899 , 89.25537 ],
        [24.05014 , 35.643723, 81.90677 ]], dtype=float32)>,
 <tf.Tensor: shape=(), dtype=float32, numpy=304.10907>)
"""
```

### Variance

```python
X = tf.random.uniform(shape = (2,3), minval = 0, maxval = 100)
X, tf.math.reduce_variance(X)
"""
(<tf.Tensor: shape=(2, 3), dtype=float32, numpy=
 array([[32.329094, 88.4744  , 20.98316 ],
        [64.605545, 73.205414, 55.299423]], dtype=float32)>,
 <tf.Tensor: shape=(), dtype=float32, numpy=535.2413>)
"""
```

### Standard Deviation

```python
X = tf.random.uniform(shape = (2,3), minval = 0, maxval = 100)
X, tf.math.reduce_std(X)
"""
(<tf.Tensor: shape=(2, 3), dtype=float32, numpy=
 array([[ 0.9790182, 75.3329   , 39.303864 ],
        [ 3.744769 , 85.94814  , 92.115005 ]], dtype=float32)>,
 <tf.Tensor: shape=(), dtype=float32, numpy=37.33542>)
"""
```
