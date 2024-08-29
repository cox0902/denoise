# DropMismatch: Removing Mismatched UI Elements for Better Pixel to Code Generation

This repository contains the code and resources for the paper **"DropMismatch: Removing Mismatched UI Elements for Better Pixel to Code Generation."** The paper introduces a novel framework to enhance the accuracy of deep learning models in UI code generation by identifying and removing mismatches between UI images and their corresponding layout code.

## Abstract

Under review.

## How to Run

### Train Mismatched Nodes Detection Model

Download dataset from [here](https://www.kaggle.com/datasets/meaner/rico240516/).

```
pip install torcheval open_clip_torch
git clone https://github.com/cox0902/dt.git
cp ./dt/run.py ./run.py
```

```
python ./run.py \
--seed 3407 \
--model resnext \
--load-weight \
--copy-weight \
--opt adamw \
--data-path /path/to/rico240516/ \
--fold 0 \
--use-ta \
--resample neg \
--k 2 \
--ema \
--amp
```

model can be one of 

```
resnet
resnext
```

### Train UI Code Generation Models

```
pip install torcheval
git clone https://github.com/cox0902/pytorch_pix2code.git
```

```
python ./pytorch_pix2code/train.py \
--seed 3407 \
--model imagecaption \
--metric auc \
--early-stop \
--image-path /path/to/rico240516/images.hdf5 \
--split-path /path/to/end-pix2code-true/split_fold_0.npz \
--code-path /path/to/end-pix2code-true/codes_true.hdf5 \
--test-path /path/to/end-pix2code-true/codes_true.hdf5 \
-b 64 \
--epochs 1000 \
--lr 4e-5 \
--grad-clip \
--ema \
--amp \
--no-comma
```

model can be one of

```
pix2code
imagecaption
```

split-path is the split of 5-fold-cv, can be one of:

```
/path/to/end-pix2code-true/split_fold_0.npz
/path/to/end-pix2code-true/split_fold_1.npz
/path/to/end-pix2code-true/split_fold_2.npz
/path/to/end-pix2code-true/split_fold_3.npz
/path/to/end-pix2code-true/split_fold_4.npz
```

code-path can be one of

```
/path/to/end-pix2code-clay/codes_rico.hdf5
/path/to/end-pix2code-clay/codes_clay.hdf5
/path/to/end-pix2code-true/codes_ours.hdf5
/path/to/end-pix2code-true/codes_true.hdf5
```

## Citation

If you use this code in your research, please cite our paper:

```
Under review.
```

## License

This repository is licensed under the MIT License. See the `LICENSE` file for more details.
