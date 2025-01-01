# Prettier Confusion Matrix

## Summary

- Make confusion matrix easy to read

## Content

### Make confusion matrix easy to read

```python
import itertools
from sklearn.metrics import confusion_matrix
import numpy as np


def show_conf_matrix(test_labels, test_pred):
    conf_matrix = confusion_matrix(test_labels, tf.argmax(test_pred, axis=1))
    conf_matrix_norm = conf_matrix / conf_matrix.sum(axis=1)[..., tf.newaxis]
    n_classes = conf_matrix.shape[0]
    classes = tf.range(n_classes).numpy()


    fig, ax = plt.subplots(figsize=(20, 20))
    cax = ax.matshow(conf_matrix, cmap=plt.cm.Blues)
    fig.colorbar(cax)

    labels = tf.range(conf_matrix.shape[0])


    ax.set(
        title = "Confusion Matrix",
        xlabel = "Predicted Label",
        ylabel = "True Label",
        xticks = tf.range(n_classes).numpy(),
        yticks = tf.range(n_classes).numpy()
    )

    threashold = (conf_matrix.max() + conf_matrix.min()) / 2

    for i, j in itertools.product(classes, classes):
        plt.text(j, i, f"{conf_matrix[i, j]} ({conf_matrix_norm[i, j]*100:.1f}%)", horizontalalignment="center")

show_conf_matrix(test_labels, test_pred)
```

![[Pasted image 20240102120624.png]]
