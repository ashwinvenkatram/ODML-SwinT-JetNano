# ODML-SwinT-JetNano

# Getting started
Follow get_started.md from ./ODML-Swin-Transformer/get_started.md

[TODO] [Add env.yaml] Use env.yaml file to create repository with required dependencies

RESCIS45 dataset is too big to store on git.
Download from: https://1drv.ms/u/s!AmgKYzARBl5ca3HNaHIlzp_IXjs

Create top-level data storage folder as ./RESCIS45/ locally

# Data Loading for Swin Infrastrucutre
Refer: ODML-Swin-Transformer/get_started.md/L:100

- For standard folder dataset, move validation images to labeled sub-folders. The file structure should look like:
  ```bash
  $ tree data
  imagenet
  ├── train
  │   ├── class1
  │   │   ├── img1.jpeg
  │   │   ├── img2.jpeg
  │   │   └── ...
  │   ├── class2
  │   │   ├── img3.jpeg
  │   │   └── ...
  │   └── ...
  └── val
      ├── class1
      │   ├── img4.jpeg
      │   ├── img5.jpeg
      │   └── ...
      ├── class2
      │   ├── img6.jpeg
      │   └── ...
      └── ...
 
  ```
- To boost the slow speed when reading images from massive small files, we also support zipped ImageNet, which includes
  four files:
    - `train.zip`, `val.zip`: which store the zipped folder for train and validate splits.
    - `train_map.txt`, `val_map.txt`: which store the relative path in the corresponding zip file and ground truth
      label. Make sure the data folder looks like this:

  ```bash
  $ tree data
  data
  └── ImageNet-Zip
      ├── train_map.txt
      ├── train.zip
      ├── val_map.txt
      └── val.zip
  
  $ head -n 5 data/ImageNet-Zip/val_map.txt
  ILSVRC2012_val_00000001.JPEG	65
  ILSVRC2012_val_00000002.JPEG	970
  ILSVRC2012_val_00000003.JPEG	230
  ILSVRC2012_val_00000004.JPEG	809
  ILSVRC2012_val_00000005.JPEG	516
  
  $ head -n 5 data/ImageNet-Zip/train_map.txt
  n01440764/n01440764_10026.JPEG	0
  n01440764/n01440764_10027.JPEG	0
  n01440764/n01440764_10029.JPEG	0
  n01440764/n01440764_10040.JPEG	0
  n01440764/n01440764_10042.JPEG	0
  
# Fine-tuning Swin Transformer from Imagenet 1K on RESCIS45
Improving Classification of Remotely Sensed
Images with the Swin Transformer
https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9764016&tag=1

# Implementation Details
Starter model: Pre-trained Swin transformer trained on ImageNet-1k

Fine-tuning hyperparameters:
NUM_EPOCHS: 25
BATCHSIZE: 4
LEARNINGRATE: 1e-3
OPTIMIZER: SGD
LOSS: CrossEntropy Loss
SCHEDULER: Cosine AnnealingLR
PREPROCESSING: Images are resized into 224x224 (build.py:build_transform():L203)
