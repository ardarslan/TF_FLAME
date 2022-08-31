### Go to the main folder of this repository. Create and activate its conda environment. Install mesh library.

```
cd TF_FLAME
conda env create -f environment.yml
conda activate tf-flame
git clone git@github.com:MPI-IS/mesh.git
cd mesh
BOOST_INCLUDE_DIRS=/path/to/boost/include make all
cd ..
```

### Prepare data for TF_FLAME:

First, download the texture data.
```
wget http://files.is.tue.mpg.de/tbolkart/FLAME/FLAME_texture_data.zip
unzip FLAME_texture_data.zip
mv texture_data_512.npy data/
mv texture_data_2048.npy data/
rm -rf texture_data_*
rm -rf FLAME_texture_data.zip
```

Second, download the FLAME model.
- Sign in https://flame.is.tue.mpg.de/login.php
- Go to https://flame.is.tue.mpg.de/download.php
- Download "FLAME 2020 (fixed mouth, improved expressions, more data)"
- Create a folder named "models" in the TF_FLAME folder.
- Copy "generic_model.pkl" into "models" folder.

### Fit FLAME on an input image.
Set the following environment variable.
```
export PROTOCOL_BUFFERS_PYTHON_IMPLEMENTATION=python
```

If you will run the optimization in image space:
```
python3 fit_2D_landmarks.py --texture_data_path ./data/texture_data_512.npy --input_img_path /path/to/input/image
```

If you will run the optimization in texture space:
```
python3 fit_2D_landmarks.py --texture_data_path ./data/texture_data_2048.npy --input_img_path /path/to/input/image
```