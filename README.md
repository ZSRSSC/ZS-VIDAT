****ZS-ViDAT******


This repository contains the training code for the paper  "ZS-ViDAT: Visual descriptions using an Attribute-governed Transformer for zero-shot scene classification in remote sensing images". 

![](figs/zs-vidat2.jpg)

******Environment to run the ZS-ViDAT*****

The implementation of "ZS-ViDAT" is mainly based on Python 3.8.8 and [PyTorch](https://pytorch.org/) 1.8.0. To install all required dependencies:
```
$ pip install -r requirements.txt
```

Additionally, we use [Weights & Biases](https://wandb.ai/site) (W&B) to keep track and organize the results of experiments. You may need to follow the [online documentation](https://docs.wandb.ai/quickstart) of W&B to quickstart. To run these codes, [sign up](https://app.wandb.ai/login?signup=true) an online account to track experiments or create a [local wandb server](https://hub.docker.com/r/wandb/local) using docker (recommended).


******Downloading datasets********

We trained the model on 4 popular ZSL benchmarks: [UCM](http://weegee.vision.ucmerced.edu/datasets/landuse.html), [AID](https://captain-whu.github.io/AID/), NWPU, and WHU-RS19. Please download NWPU and RS19 datasets on your own way. Following, for the data splits use the code in ./data/xlsa17/code . In order to train the **ZSViDAT**, you should firstly download these datasets. Then decompress and organize them as follows: 
```
.
├── data
│   ├── UCM/UCMerced_LandUse/Images/...
│   ├── AID/...
│   ├── NWPU/...
│   └── RSD/...
└── ···
```

*****Extracting visual features********

In this step, you should run the following commands to extract the visual features of three datasets:

```
$ python preprocessing.py --dataset UCM --compression --device cuda:0
$ python preprocessing.py --dataset AID --compression --device cuda:0
$ python preprocessing.py --dataset NWPU --compression --device cuda:0
$ python preprocessing.py --dataset RSD --compression --device cuda:0
```

******ZS-ViDAT training*******

In `./wandb_config`, we provide our parameters setting of conventional ZSL (CZSL) and generalized ZSL (GZSL) tasks for UCM, AID, NWPU, and RSD. You can run the following commands to train the "ZS-ViDAT" from scratch:

```
$ python train_ucm.py   # UCM
$ python train_aid.py   # AID
$ python train_nwpu.py  # NWPU
$ python train_rsd.py  # RSD
```
Note: Please load the corresponding setting when aiming at the CZSL task.
