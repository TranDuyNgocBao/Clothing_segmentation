# Clothes Segmentation using U2NET

![Python 3.7](https://img.shields.io/badge/python-3.8-green.svg)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1EhEy3uQh-5oOSagUotVOJAf8m7Vqn0D6?usp=sharing)

This repo contains training code, inference code and pre-trained model for Cloths Parsing from human portrait.</br>
This model works well with any background and almost all poses. For more samples visit [samples.md](samples.md)

# Techinal details

-   **U2NET** : This project uses an amazing [U2NET](https://arxiv.org/abs/2005.09007) as a deep learning model. Only categorical cross-entropy loss is used for a given version of the checkpoint.

-   **Dataset** : U2net is trained on 45k images [iMaterialist (Fashion) 2019 at FGVC6](https://www.kaggle.com/c/imaterialist-fashion-2019-FGVC6/data) dataset. To reduce complexity, I have clubbed the original 46 categories from dataset labels into supperclass. All images are resized intosquare `¯\_(ツ)_/¯` 768 x 768 px for training. (This experiment was conducted with 768 px but around 384 px will work fine too if one is retraining on another dataset).

# Training

-   Để training project này cần:
<ul>
    <ul>
    <li>&nbsp; PyTorch > 1.3.0</li>
    <li>&nbsp; tensorboardX</li>
    <li>&nbsp; gdown</li>
    </ul>
</ul>

-   Tải dataset từ [link](https://www.kaggle.com/c/imaterialist-fashion-2019-FGVC6/data), giải nén.
-   Cài đặt path cho `train` folder bao gồm training images và `train.csv` ở trong `options/base_options.py`
-   To port original u2net of all layer except last layer please run `python setup_model_weights.py` and it will generate weights after model surgey in `prev_checkpoints` folder.
-   You can explore various options in `options/base_options.py` like checkpoint saving folder, logs folder etc.
-   For single gpu set `distributed = False` in `options/base_options.py`, for multi gpu set it to `True`.
-   For single gpu run `python train.py`
-   For multi gpu run <br>
    &nbsp;`python -m torch.distributed.launch --nnodes=1 --node_rank=0 --nproc_per_node=4 --use_env train.py` <br>
    Here command is for single node, 4 gpu. Tested only for single node.
-   You can watch loss graphs and samples in tensorboard by running tensorboard command in log folder.

# Testing/Inference

-   Download pretrained model from this [link](https://drive.google.com/file/d/1mhF3yqd7R-Uje092eypktNl-RoZNuiCJ/view?usp=sharing)(165 MB) in `trained_checkpoint` folder.
-   Put input images in `input_images` folder
-   Run `python infer.py` for inference.
-   Output will be saved in `output_images`

### OR

-   Inference in colab from here [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1EhEy3uQh-5oOSagUotVOJAf8m7Vqn0D6?usp=sharing)

# Acknowledgements

-   U2net model is from original [u2net repo](https://github.com/xuebinqin/U-2-Net). Thanks to Xuebin Qin for amazing repo.
-   Complete repo follows structure of [Pix2pixHD repo](https://github.com/NVIDIA/pix2pixHD)
