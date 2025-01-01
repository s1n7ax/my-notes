# Saving the Model

## Summary

- Saving a model

  - `SavedModel` format

    ```python
    model.save('<path>')
    ```

    - `HDF5` format

    ```python
    model.save('<path>.h5')
    ```

- Loading a model

```python
tf.keras.models.load_model('<path>')
```

## Content

### Saving and restoring the models

```python
model.save("save1")
restored_model = tf.keras.models.load_model("save1")

y_predict = restored_model.predict(X_test)

import matplotlib.pyplot as plt

plt.scatter(X_test, y_test, c="g", label="Expected")
plt.scatter(X_test, y_predict, c="red", label="Actual")
```
