# TensorFlow-for-macos

## 1 Instalación Miniconda
```
mkdir -p ~/miniconda3
curl https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh -o ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm ~/miniconda3/miniconda.sh
source ~/miniconda3/bin/activate
conda init --all
conda config --set auto_activate_base false
```

## 2 Creacion entorno con TensorFlow
```
conda create -n work3.10 python=3.10.13 --yes
conda activate work3.10
conda install -c apple tensorflow-deps --yes
pip install tensorflow-macos
pip install tensorflow-metal
conda install -c conda-forge jupyterlab pandas matplotlib scikit-learn scipy plotly --yes
```

## 3 TensorFlow
```
import sys
import tensorflow as tf

print(f'System: {sys.executable}')
print(f'TensorFlow: {tf.__version__}')
print("Num GPUs Available: ", len(tf.config.list_physical_devices('GPU')))
```
> System: /Users/juanpablo/miniconda3/envs/work3.10/bin/python
> TensorFlow: 2.16.2
> Num GPUs Available:  1

### 3.1 GPU Test
```
%%time

import tensorflow as tf

import os
# When = 3, the messages (1 - informational(I), 2 - warnings(W) and 3- errors(E)) will not be logged during code execution.
os.environ['TF_CPP_MIN_LOG_LEVEL'] = '3'

# Ensure we see the GPU in device list.
print('Visible Devices: ', tf.config.get_visible_devices())

cifar = tf.keras.datasets.cifar100
(x_train, y_train), (x_test, y_test) = cifar.load_data()
model = tf.keras.applications.ResNet50(
    include_top=True,
    weights=None,
    input_shape=(32, 32, 3),
    classes=100,)

loss_fn = tf.keras.losses.SparseCategoricalCrossentropy(from_logits=False)
model.compile(optimizer="adam", loss=loss_fn, metrics=["accuracy"])
model.fit(x_train, y_train, epochs=1, batch_size=128)
```
> Visible Devices:  [PhysicalDevice(name='/physical_device:CPU:0', device_type='CPU'), PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]
> 391/391 ━━━━━━━━━━━━━━━━━━━━ 118s 243ms/step - accuracy: 0.0600 - loss: 4.8250
> CPU times: user 1min 56s, sys: 45.5 s, total: 2min 41s
> Wall time: 2min
> <keras.src.callbacks.history.History at 0x320623970>

### 3.2 CPU Testing
```
%%time

import tensorflow as tf
# Removes GPU from list, i.e. []
tf.config.set_visible_devices([], 'GPU')
print('Visible Devices: ', tf.config.get_visible_devices())

cifar = tf.keras.datasets.cifar100
(x_train, y_train), (x_test, y_test) = cifar.load_data()
model = tf.keras.applications.ResNet50(
    include_top=True,
    weights=None,
    input_shape=(32, 32, 3),
    classes=100,)

loss_fn = tf.keras.losses.SparseCategoricalCrossentropy(from_logits=False)
model.compile(optimizer="adam", loss=loss_fn, metrics=["accuracy"])
model.fit(x_train, y_train, epochs=1, batch_size=128)
```
> Visible Devices:  [PhysicalDevice(name='/physical_device:CPU:0', device_type='CPU')]
> 391/391 ━━━━━━━━━━━━━━━━━━━━ 493s 1s/step - accuracy: 0.0528 - loss: 4.9807
> CPU times: user 20min 53s, sys: 3min 23s, total: 24min 16s
> Wall time: 8min 14s
> <keras.src.callbacks.history.History at 0x17f61fac0>



