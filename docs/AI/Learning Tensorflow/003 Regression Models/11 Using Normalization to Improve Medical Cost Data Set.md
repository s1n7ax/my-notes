# Using normalization to Improve Medical Cost Data Set

```python
import tensorflow as tf
import pandas as pd
from matplotlib import pyplot as plt

data = pd.read_csv('https://raw.githubusercontent.com/stedy/Machine-Learning-with-R-datasets/master/insurance.csv')

from sklearn.compose import make_column_transformer
from sklearn.preprocessing import MinMaxScaler, OneHotEncoder
from sklearn.model_selection import train_test_split

ct = make_column_transformer(
    (OneHotEncoder(), ['sex', 'smoker', 'region']),
    (MinMaxScaler(), ['age', 'children', 'bmi'])
)

X = data.drop(columns=['charges'])
y = data['charges']

X_train, X_test, y_train, y_test = train_test_split(X, y, train_size=0.8)

ct.fit(X_train)

X_train_norm = ct.transform(X_train)
X_test_norm = ct.transform(X_test)

model = tf.keras.Sequential([
    tf.keras.layers.Input(11),
    tf.keras.layers.Dense(50),
    tf.keras.layers.Dense(50),
    tf.keras.layers.Dense(50),
    tf.keras.layers.Dense(1),
])

model.compile(
    loss = tf.keras.losses.mae,
    optimizer = tf.keras.optimizers.Adam(),
    metrics = ['mae']
)

training_data = model.fit(X_train_norm, y_train, epochs=100, verbose=False)
model.evaluate(X_test_norm, y_test)

pd.DataFrame(training_data.history).drop(columns=['mae']).plot()
plt.xlabel('iterations')
plt.ylabel('loss')
```
