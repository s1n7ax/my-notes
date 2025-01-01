# Attributes of tensor

## Summary

- Shape of the tensor
- Data type of the tensor
- Device the tensor is stored in

## Content

### Shape, dtype & device attributes

```python

tensor = torch.rand((2, 3))
tensor.shape
"""
torch.Size([2, 3])
"""

tensor.dtype
"""
torch.float32
"""

tensor.device
"""
device(type='cpu')
"""
```
