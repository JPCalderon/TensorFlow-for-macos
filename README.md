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
System: /Users/juanpablo/miniconda3/envs/work3.10/bin/python
TensorFlow: 2.16.2
Num GPUs Available:  1


{
 "cells": [
  {
   "cell_type": "markdown",
   "source": [
    "Here is some Python code:"
   ]
  },
  {
   "cell_type": "code",
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Hello world!\n"
     ]
    }
   ],
   "source": [
    "print(\"Hello world!\")"
   ]
  }
  ...
  ]
}
