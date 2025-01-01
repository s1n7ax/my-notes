# Numpy Array to Tensor

## Summary

- Converting `numpy` data to tensor

## Content

`Numpy` arrays can easily be converted to Tensor

```python
import numpy as np

numpy_A = np.arange(1, 25, dtype=np.int32)
numpy_A

"""
array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16, 17,
       18, 19, 20, 21, 22, 23, 24], dtype=int32)
"""

tensor = tf.constant(numpy_A)
tensor
"""
<tf.Tensor: shape=(24,), dtype=int32, numpy=
array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16, 17,
       18, 19, 20, 21, 22, 23, 24], dtype=int32)>
"""
```
