This is forked repogitory from [Attr2Font](https://github.com/hologerry/Attr2Font).

I made some modifications while using it to apply it to the Korean dataset.(korean language project is [here](https://github.com/withdongyeong/KDT_B4))

1. There is an issue where a zero is inserted in front of the file name intermittently. I don't know the cause, so I took temporary measure.
2. Fixed a typo in the Continue Learning function
3. Some dataset-related parameters are hard-coded. I will not modify them separately, but to use this model, you need to modify them according to the dataset.(in dataloader.py, lines 226-230)
4. I add inference function to web deploy(The attribute value is temporarily hard-coded and needs to be updated during web distribution later.)
   use `--phase inference` `--check_path check_path` `--infer_path infer_path`
6. Dataset download from original git has expired. A point to be aware of when building a custom dataset is that the character class, that is, the file name must start from 10.

   Ex) If you create a data set with the following 5 characters
   
   a b c d e

   The data set structure is as follows,
   
   - dataset_root_dir
      - explor_all (if you want change it, code fix is needed(options.py and dataloader.py line 226)
         - font_A
            - 10.png (a image)
            - 11.png (b image)
            - 12.png (c image)
            - 13.png (d image)
            - 14.png (e image)
         - font_B
            - 10.png (a image)
            - 11.png (b image)
            - 12.png (c image)
            - 13.png (d image)
            - 14.png (e image)

# Attr2Font
## Introduction

This is the official PyTorch implementation of the **Attribute2Font: Creating Fonts You Want From Attributes**.

![Teaser](img/teaser.png)

Paper: [arXiv](https://arxiv.org/abs/2005.07865) | [Research Gate](https://www.researchgate.net/publication/341423467_Attribute2Font_Creating_Fonts_You_Want_From_Attributes/comments)   
Supplementary Material: [link](paper/Siggraph2020_Attr2Font_Supplemental_Material.pdf)   
Video: [link](img/att2font_demo.mov)   
Code: [GitHub](https://github.com/hologerry/Attr2Font)   



## Abstract
Font design is now still considered as an exclusive privilege of professional designers, whose creativity is not possessed by existing software systems. Nevertheless, we also notice that most commercial font products are in fact manually designed by following specific requirements on some attributes of glyphs, such as italic, serif, cursive, width, angularity, etc. Inspired by this fact, we propose a novel model, Attribute2Font, to automatically create fonts by synthesizing visually pleasing glyph images according to user-specified attributes and their corresponding values. To the best of our knowledge, our model is the first one in the literature which is capable of generating glyph images in new font styles, instead of retrieving existing fonts, according to given values of specified font attributes. Specifically, Attribute2Font is trained to perform font style transfer between any two fonts conditioned on their attribute values. After training, our model can generate glyph images in accordance with an arbitrary set of font attribute values. Furthermore, a novel unit named Attribute Attention Module is designed to make those generated glyph images better embody the prominent font attributes. Considering that the annotations of font attribute values are extremely expensive to obtain, a semi-supervised learning scheme is also introduced to exploit a large number of unlabeled fonts. Experimental results demonstrate that our model achieves impressive performance on many tasks, such as creating glyph images in new font styles, editing existing fonts, interpolation among different fonts, etc.

## Model Architecture
![Architecture](img/att_arch.png)

## Demonstration
![Demo](img/att2font_demo.gif)

## Prerequisites

* Linux
* CPU or NVIDIA GPU + CUDA cuDNN
* Python 3
* PyTorch 1.0+

## Get Started

### Installation
1. Install PyTorch, torchvison and dependencies from [https://pytorch.org](https://pytorch.org)
2. Clone this repo:
   ```shell
   git clone https://github.com/hologerry/Attr2Font
   cd Attr2Font
   ```
3. Download the official pre-trained vgg19 model: [vgg19-dcbb9e9d.pth](https://download.pytorch.org/models/vgg19-dcbb9e9d.pth), and put it under this project root folder


### Datasets

Download the dataset from [PKU Disk](https://disk.pku.edu.cn:443/link/984852AA48580C84B1A63467390DAB69), [Google Drive](https://drive.google.com/open?id=1P2DbNbVw4Q__WcV1YdzE7zsDKilmd3pO) or [MEGA](https://mega.nz/file/zoYmyIxZ#1DqZjgu21AAJ1nenruYQPo2cS0Xjw4dINAjj3iTmfr8) and put it into the `data/`:
```
data/
    explor_all/
        image/
        attributes.txt/
```
| This dataset is constructed by O’Donovan et al. *Exploratory Font Selection Using Crowdsourced Attributes*. TOG 2014



### Model Training
```
python main.py --phase train
```

### Model Testing
```
python main.py --phase test
```


### Model Interpolation
```
python main.py --phase test_interp --test_epoch EPOCH
```


## Citation:

If you use this code or find our work is helpful, please consider citing our work:
```
@article{WangSIGGRAPH2020,
  author = {Yizhi Wang*, Yue Gao*, Zhouhui Lian},
  title = {Attribute2Font: Creating Fonts You Want From Attributes},
  journal = {ACM Trans. Graph.},
  year = {2020}
}
```
| * Denotes equal contribution


## Copyright

The code and dataset are only allowed for PERSONAL and ACADEMIC usage.
