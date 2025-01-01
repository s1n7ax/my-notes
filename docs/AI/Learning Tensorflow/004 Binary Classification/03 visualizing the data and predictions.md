# Visualizing the Data and Predictions

## Summary

- How to visualize data and predictions of the model

## Content

### How to visualize data and predictions

```python
"""
Takes in a trained model and X, y
X: [n, 2] - this contains x and y coordinates for the point
y: [n] - this contains binary prediction
"""
def plot_decision_boundary(model, X, y):
    # extract the x axis
    X0 = X[:, 0]
    # extract the y axis
    X1 = X[:, 1]

    # calculate the x and y axis in the graph with 0.1 margin
    x_min, x_max = X0.min() - 0.1, X0.max() + 0.1
    y_min, y_max = X1.min() - 0.1, X1.max() + 0.1

    '''
    mashgrid works as follows
    xx, yy = tf.meshgrid(
        [-2, -1, 0, 1, 2],
        [1, 2, 3, 4, 5]
    )

    xx, yy

    (<tf.Tensor: shape=(5, 5), dtype=int32, numpy=
    array([[-2, -1,  0,  1,  2],
            [-2, -1,  0,  1,  2],
            [-2, -1,  0,  1,  2],
            [-2, -1,  0,  1,  2],
            [-2, -1,  0,  1,  2]], dtype=int32)>,
    <tf.Tensor: shape=(5, 5), dtype=int32, numpy=
    array([[1, 1, 1, 1, 1],
            [2, 2, 2, 2, 2],
            [3, 3, 3, 3, 3],
            [4, 4, 4, 4, 4],
            [5, 5, 5, 5, 5]], dtype=int32)>)
    '''
    xx, yy = tf.meshgrid(
        # linespace returns a vector of 100 number sequence from x_min to x_max
        tf.linspace(x_min, x_max, 100),
        tf.linspace(y_min, y_max, 100)
    )

    # ravel is similar to flatmap but modifying the existing list instead of copy
    x_in = tf.stack([xx.numpy().ravel(), yy.numpy().ravel()], axis=1)
    y_pred = model.predict(x_in)

    # y_pred shape is [100000, 1] and to match this with the shape of the graph
    # this prediction has to be reshaped to [100, 100]
    # since this is binary classification, we round the predictions to either 0 or 1
    y_pred_graph = tf.reshape(tf.round(y_pred), xx.shape)

    plt.contourf(xx, yy, y_pred_graph, cmap=plt.cm.RdYlBu)
    plt.scatter(X[:, 0], X[:, 1], c=y, cmap=plt.cm.RdYlBu)
    plt.xlim(xx.numpy().min(), xx.numpy().max())
    plt.ylim(yy.numpy().min(), yy.numpy().max())
```

- When a linear model used in a non linear problem

![[Pasted image 20231227124758.png]]

- When a non linear model used in a non linear problem

![[Pasted image 20231227125114.png]]
