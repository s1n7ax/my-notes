# Binary Classification with Food 101 Dataset - Visualizing Data

## Summary

- Download data and visualize data

## Content

### Download data and visualize data

```python
# get data
import zipfile

!wget https://storage.googleapis.com/ztm_tf_course/food_vision/pizza_steak.zip

# extract data
zip_ref = zipfile.ZipFile("pizza_steak.zip")
zip_ref.extractall()
zip_ref.close()

# show directory structure
!sudo apt install tree
!tree -d pizza_steak
"""
pizza_steak
├── test
│   ├── pizza
│   └── steak
└── train
    ├── pizza
    └── steak
"""

# data count
import os

print(len(os.listdir("pizza_steak/train/pizza")), len(os.listdir("pizza_steak/train/steak")))
print(len(os.listdir("pizza_steak/test/pizza")), len(os.listdir("pizza_steak/test/steak")))
"""
750 750
250 250
"""

# view random images from the data
from tensorflow.keras.utils import image_dataset_from_directory
import pathlib

tf.random.set_seed(42)

train_dir = pathlib.Path("pizza_steak/train")
test_dir = pathlib.Path("pizza_steak/test")

train_data = image_dataset_from_directory(
    directory=train_dir,
    batch_size=32,
    image_size=(224, 224),
    label_mode="binary",
    seed=42
)

valid_data = image_dataset_from_directory(
    directory=test_dir,
    batch_size=32,
    image_size=(224, 224),
    label_mode="binary",
    seed=42
)

import matplotlib.pyplot as plt


class_names = train_data.class_names

plt.figure(figsize=(10, 10))
for images, labels in train_data.take(1):
  for i in range(9):
    ax = plt.subplot(3, 3, i + 1)
    plt.imshow(images[i].numpy().astype("uint8"))
    plt.title(class_names[int(labels[i][0].numpy())])
    plt.axis("off")
```

<!-- ![output](assets/2024-01-03-23-47-30.png) -->
