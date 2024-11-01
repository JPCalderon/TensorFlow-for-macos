# TensorFlow-for-macos

## 1 Instalación Miniconda
```mkdir -p ~/miniconda3```
```curl https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh -o ~/miniconda3/miniconda.sh```
```bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3```
```rm ~/miniconda3/miniconda.sh```
```source ~/miniconda3/bin/activate```
```conda init --all```

conda config --set auto_activate_base false

## 2 Creacion entorno con TensorFlow
conda create -n work3.10 python=3.10.13 --yes
conda activate work3.10
conda install -c apple tensorflow-deps --yes
pip install tensorflow-macos
pip install tensorflow-metal
conda install -c conda-forge jupyterlab pandas matplotlib scikit-learn scipy plotly --yes
