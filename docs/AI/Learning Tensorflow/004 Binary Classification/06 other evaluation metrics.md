# Other Evaluation Metrics

## Summary

- Other useful evaluation metrics
  - Accuracy - Default metric for classification. Not the best for imbalanced classes
  - Precision - Higher precision leads to less false positives
  - Recall - Higher recall leads to less false negatives
  - F1-score - Combination of precision and recall usually a good overall metric for a classification model
  - Confusion matrix - When comparing prediction to truth labels to see where model gets confused

## Content

### Confusion Matrix

```python
from sklearn.metrics import confusion_matrix

y_pred = model.predict(X_test)
y_pred_binary = tf.round(y_pred)

conf_matrix = confusion_matrix(y_test, tf.round(y_pred_binary))

"""
Following are the results retured by the function
+----------------------------------+
|True negatives  | False positives |
+----------------------------------+
|False negatives | True positives  |
+----------------------------------+

array([[ 97,   0],
       [  0, 103]])
"""
```

### Pretty Confusion Matrix
