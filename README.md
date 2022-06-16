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
#### Download and generate obfuscated frames
Download the dataset (make sure you set the right path for $DESTDIR in the bash file):
```sh
cd dataset_scripts/dataset_prep
. build.sh
```
This downloads the EGTEA Gaze+ dataset and extracts the frames from video clips. We also provided the hand+object masks for this dataset in numpy files. Then it generates the obfuscated jpg images using the numpy files. Depending on your internet connection speed, the download process might take some time. I'm planning to speed up the other steps by doing things in parallel. 
#### Interpolation
For those frames where the hand is not visible, the obfuscated image is basically a black frame. To account for this, we replaced these frames by interpolation. Refer to `interpolate.py` for more information.

#### splits
We removed some of the classes that didn't deal with objects in hand (e.g., fridge) and merged similar ones. Use the splits that we provided located at 'dataset_prep/splits'

## Training 
#### Download pre-trained weights:
We used pre-trained weights of I3D trained on kinetics400 to start training. The weights are provided by Meta and can be downloaded:
```sh
cd experiments/I3D/weights
. download.sh
```
We provided config files that can be used to train and test the model both for raw and obfuscated images. Change the config file paths accordingly and run:
#### Train
```sh
python tools/run_net.py --cfg ../experiments/I3D/configs/train/R50_raw_32x4.yaml NUM_GPUS 1
python tools/run_net.py --cfg ../experiments/I3D/configs/train/R50_hands_obj_32x4.yaml NUM_GPUS 1
```
#### Test
```sh
python tools/run_net.py --cfg ../experiments/I3D/configs/test/R50_raw_32x4.yaml NUM_GPUS 1
python tools/run_net.py --cfg ../experiments/I3D/configs/test/R50_hands_obj_32x4.yaml NUM_GPUS 1
```
