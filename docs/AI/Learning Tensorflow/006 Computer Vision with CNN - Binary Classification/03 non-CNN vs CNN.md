# Non-CNN model vs CNN

## Summary

- Train a non-CNN model using the same dataset
- Compare the CNN results & non-CNN results

## Content

### Train a non-CNN model using the same dataset

```python
tf.random.set_seed(42)

model = tf.keras.Sequential([
    tf.keras.layers.Flatten(),
    tf.keras.layers.Dense(100, activation="relu"),
    tf.keras.layers.Dense(100, activation="relu"),
    tf.keras.layers.Dense(1, activation="sigmoid")
])


model.compile(
    loss = tf.keras.losses.BinaryCrossentropy(),
    optimizer = tf.keras.optimizers.Adam(),
    metrics = ['accuracy']
)


model.fit(train_data,
          epochs=4,
          steps_per_epoch=len(train_data),
          validation_data=valid_data,
          validation_steps=len(valid_data))
"""
Epoch 1/4
47/47 [==============================] - 6s 69ms/step - loss: 1401.8051 - accuracy: 0.6320 - val_loss: 283.8436 - val_accuracy: 0.7880
Epoch 2/4
47/47 [==============================] - 4s 79ms/step - loss: 450.6426 - accuracy: 0.6680 - val_loss: 753.7115 - val_accuracy: 0.5740
Epoch 3/4
47/47 [==============================] - 6s 117ms/step - loss: 350.1263 - accuracy: 0.7120 - val_loss: 138.8354 - val_accuracy: 0.7180
Epoch 4/4
47/47 [==============================] - 4s 77ms/step - loss: 145.2438 - accuracy: 0.7320 - val_loss: 344.5571 - val_accuracy: 0.5940
"""
```

### Compare the CNN results & non-CNN results

Even though non-CNN model contains 500x times more trainable parameters, it performs poorly compared to CNN

#### CNN model summary

```
_________________________________________________________________
 Layer (type)                Output Shape              Param #
=================================================================
 normalization_5 (Normaliza  (None, 224, 224, 3)       7
 tion)

 conv2d_24 (Conv2D)          (None, 222, 222, 10)      280

 conv2d_25 (Conv2D)          (None, 220, 220, 10)      910

 max_pooling2d_12 (MaxPooli  (None, 110, 110, 10)      0
 ng2D)

 conv2d_26 (Conv2D)          (None, 108, 108, 10)      910

 conv2d_27 (Conv2D)          (None, 106, 106, 10)      910

 max_pooling2d_13 (MaxPooli  (None, 53, 53, 10)        0
 ng2D)

 flatten_24 (Flatten)        (None, 28090)             0

 dense_57 (Dense)            (None, 1)                 28091

=================================================================
Total params: 31108 (121.52 KB)
Trainable params: 31101 (121.49 KB)
Non-trainable params: 7 (32.00 Byte)
```

#### Non-CNN model summary

```
_________________________________________________________________
 Layer (type)                Output Shape              Param #
=================================================================
 flatten_22 (Flatten)        (None, 150528)            0

 normalization_4 (Normaliza  (None, 150528)            301057
 tion)

 dense_53 (Dense)            (None, 100)               15052900

 dense_54 (Dense)            (None, 100)               10100

 dense_55 (Dense)            (None, 1)                 101

=================================================================
Total params: 15364158 (58.61 MB)
Trainable params: 15063101 (57.46 MB)
Non-trainable params: 301057 (1.15 MB)
```
