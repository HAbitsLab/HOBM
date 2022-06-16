# HOBM
This is the code repository for the paper [_Impacts of Image Obfuscation on Fine-grained Activity Recognition in Egocentric Video_](https://ieeexplore.ieee.org/abstract/document/9767447)
## Installation
```sh
git clone git@github.com:HAbitsLab/HOBM.git
cd HOBM
git submodule init
git submodule update
```
This repository uses SlowFast library by Meta but don't get confused. It supports I3D architecture which we used in this paper. Go ahead and follow the [guides](https://github.com/facebookresearch/SlowFast) to install SlowFast on your machine.

## Dataset Preparation
Download the dataset (make sure you set the right path for $DESTDIR in the bash file):
```sh
cd dataset_scripts/dataset_prep
. build.sh
```
This downloads the EGTEA Gaze+ dataset and extracts the frames from video clips. We also provided the hand+object masks for this dataset in numpy files. Then it generates the obfuscated jpg images using the numpy files. Depending on your internet connection speed, the download process might take some time. I'm planning to speed up the other steps by doing things in parallel. 

## Training
We provided config files that can be used to train the model both for raw and obfuscated images.
#### Raw
```sh
python 
```
#### HOBM
```sh
python 
```
