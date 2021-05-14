# IO

This library allows to read and write 3D images from different sources. It also has the SpatialImage class that extend numpy arrays so they also contain the voxel size information.

This library is an extension of the one proposed by [VirtualPlants](https://team.inria.fr/virtualplants/) and that can be found there: https://github.com/openalea/openalea-components (and specifically [there](https://github.com/openalea/openalea-components/tree/master/image/src/image))

The library can read and write 3D images from the following format: tiff, klb, hdf5 (only read, not write for the moment).
It can also read a stack of 2D images from a folder (useful when the stack is really big and hdf5/klb format are not available).

## Description of the repository
  - IO: folder containing the package
  - setup.py: Installation script
  - README.md: This file

## Basic usage
Once installed the library can be called the following way (as an example):
```python
from IO import imread, imsave, SpatialImage
```

## Dependencies
Some dependecies are requiered:
  - general python dependecies:
    - numpy, scipy
  - Image reading dependencies:
    - h5py (https://pypi.python.org/pypi/h5py)
    - pyklb (https://github.com/bhoeckendorf/pyklb)
    - tifffile (https://pypi.org/project/tifffile/)

If one wants to read and write klb file the pyklb (https://github.com/bhoeckendorf/pyklb) library is required. One can install it the following way (in `[]` are the optional commands, in `<>` are the place where the path has to be replace with the adequate one):
```shell
pip install cython [--user]
git clone https://github.com/bhoeckendorf/pyklb.git
cd pyklb
python setup.py bdist_wheel
pip install dist/<name_of_the_wheel>.whl [--user]
```

Then you need to manually link the pyklb libraries to your python environement:
```shell
path_lib='~/.local/lib' #This is an example that should work on linux
ln build/lib.<name-of-version>.<python-version>/pyklb.so $path_lib #links the two libraries to your libraries folder
ln build/lib/libklb.so $path_lib

echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:'$path_lib >> ~/.bashrc #replace .bashrc by .profile for macOs for example
echo 'export PYTHONPATH=$PYTHONPATH:'$path_lib >> ~/.bashrc #replace .bashrc by .profile for macOs for example
```

Then you can either open a new terminal or run the following command:
```shell
source ~/.bashrc
```

To check if pyklb is correctly installed, one should be able to run the following command in python:
```python
import pyklb
```
    
## Quick install
To quickly install the script so it can be call from the terminal and install too the common dependecies one can run from the IO folder:
```shell
pip install .
```
Still will be remaining to install pyklb package.
