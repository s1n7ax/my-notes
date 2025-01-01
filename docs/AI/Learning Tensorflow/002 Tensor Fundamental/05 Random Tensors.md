# Random Tensors

## Summary

- Creating random tensors
  - `random.normal`
  - `random.uniform`

## Content

There are many ways to create random tensors but following APIs will be considered

- `random.normal`
  More info in [[Normal Probability Distribution]]
- `random.uniform`
  More info in [[02 Uniform Probability Distribution]]

### Creating Random Tensors

```python
rand = tf.random.Generator.from_seed(2)
rand_tensor = rand.normal(shape=(2,3))
rand_tensor
"""
<tf.Tensor: shape=(2, 3), dtype=float32, numpy=
array([[-0.1012345 , -0.2744976 ,  1.4204658 ],
       [ 1.2609464 , -0.43640924, -1.9633987 ]], dtype=float32)>
"""
```
