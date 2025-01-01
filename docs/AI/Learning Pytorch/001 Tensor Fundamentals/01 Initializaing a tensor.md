# Initializing a tensor

## Summary

- Tensor of shape of given
- Tensor from python array
- Tensor from numpy array
- Tensor from another tensor

## Content

### Tensor of shape of given

```python
shape = (2,3,4)
torch.ones(shape)
"""
tensor([[1., 1., 1.],
        [1., 1., 1.]])
"""

torch.zeros(shape)
"""
tensor([[0., 0., 0.],
        [0., 0., 0.]])
"""

torch.rand(shape)
"""
tensor([[0.7005, 0.1716, 0.9602],
        [0.8698, 0.1772, 0.7533]])
"""
```

### Tensor from python array

```python
data = [[1, 2], [3, 4]]
torch.tensor(data)
"""
tensor([[1, 2],
        [3, 4]])
"""
```

### Tensor from numpy array

```python
data = [[1, 2], [3, 4]]
np_array = np.array(data)
torch.from_numpy(np_array)

"""
tensor([[1, 2],
        [3, 4]])
"""
```

### Tensor from another tensor

```python
tensor = torch.tensor([[1, 2], [3, 4]])
torch.one_line(tensor)
"""
tensor([[1, 1],
        [1, 1]])
"""

torch.rand_like(tensor, dtype=torch.float)
#                       ^^ here the dtype is important because the rand is float
#                       but the inferred type from the list is int
"""
tensor([[0.2383, 0.7600],
        [0.1299, 0.0575]])
"""
```
