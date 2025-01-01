# Indexing Tensors

## Summary

- Indexing

## Content

### Indexing

```python
tensor = torch.tensor([
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
])

print(f"tensor: {tensor}")
print(f"first column: {tensor[:, 0]}")
print(f"first two columns: {tensor[:, :2]}")
print(f"last column: {tensor[:, -1]}")

"""
tensor: tensor([[1, 2, 3],
        [4, 5, 6],
        [7, 8, 9]])
first column: tensor([1, 4, 7])
first two columns: tensor([[1, 2],
        [4, 5],
        [7, 8]])
last column: tensor([3, 6, 9])
"""
```
