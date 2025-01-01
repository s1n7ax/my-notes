# Fine Tuning Existing Model

## Summary

- Steps of fine tuning
- Fine Tuning

## Content

### Steps of Fine Tuning

- Usually before we fine-tune the existing model, we train the output layer
  after freezing the existing model.
- After that, we can activate some layers of the backbone and start training
- Usually, with the part of backbone is activated, we lower the learning rate of
  the model to avoid drastic changes

### Fine Tuning

- Training using freezed model

```python
import tensorflow as tf

train_data = tf.keras.utils.image_dataset_from_directory(train_dir)
test_data = tf.keras.utils.image_dataset_from_directory(test_dir)

base_model1 = tf.keras.applications.EfficientNetV2B0(include_top=False)
base_model1.trainable = False

data_augmentation1 = tf.keras.Sequential(
    [
        tf.keras.layers.RandomFlip("horizontal"),
        tf.keras.layers.RandomRotation(0.2),
        tf.keras.layers.RandomZoom(0.2),
        tf.keras.layers.RandomHeight(0.2),
        tf.keras.layers.RandomWidth(0.2),
    ]
)

model1 = tf.keras.Sequential(
    [
        tf.keras.layers.Resizing(224, 224),
        data_augmentation1,
        base_model1,
        tf.keras.layers.GlobalAveragePooling2D(),
        tf.keras.layers.Dense(10, activation="softmax"),
    ]
)

model1.compile(
    loss=tf.keras.losses.SparseCategoricalCrossentropy(),
    optimizer=tf.keras.optimizers.Adam(),
    metrics=["accuracy"],
)

model1.fit(
    train_data,
    epochs=4,
    validation_data=test_data,
    callbacks=[
        tf.keras.callbacks.ModelCheckpoint(
            "checkpoints/model1.ckpt",
            verbose=1,
            save_weights_only=True,
        ),
        tf.keras.callbacks.TensorBoard(log_dir="tensorboard/model1"),
    ],
)
```

- Unfreeze 10 layers and train for more

```python
model3 = tf.keras.models.clone_model(model1)

model3.compile(
    loss=tf.keras.losses.SparseCategoricalCrossentropy(),
    optimizer=tf.keras.optimizers.Adam(learning_rate=0.0001),
    metrics=["accuracy"],
)

base_model2 = tf.keras.applications.EfficientNetV2B0(include_top=False)
base_model2.trainable = False

for layer in base_model2.layers[-10:]:
    layer.trainable = True

model3.layers[2] = base_model2

model3.set_weights(model1.get_weights())

model3.fit(
    train_data,
    epochs=8,
    validation_data=test_data,
    initial_epoch=4,
    callbacks=[tf.keras.callbacks.TensorBoard(log_dir="tensorboard/model3")],
)
```
