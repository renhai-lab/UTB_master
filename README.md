# The Urban Tree Canopy Cover in Brazil - Nationwide Perspectives from High-Resolution Remote Sensing Images



Urban tree canopy maps are essential for providing urban ecosystem services. The relationship between urban
trees and urban climate change, air pollution, urban noise, biodiversity, urban crime, health, poverty, 
and social inequality provides important information for better understanding and management of cities. To better service Brazil’s
urban ecosystem, we developed a semi-supervised deep learning method, which is able to learn semantic segmentation 
knowledge from both labeled and unlabeled images, to segment urban trees from high spatial resolution remote
sensing images. Using this approach, we created 0.5 m fine-scale tree canopy products for 472 cities in Brazil and
made them freely available to the community. Results showed that the urban tree canopy coverage in Brazil is between
5% and 35%, and the average urban tree canopy cover is approximately 18.68%. The statistical results of these tree
canopy maps quantify the nationwide urban tree canopy inequality problem in Brazil. Urban tree canopy coverage
from 130 cities that can accommodate approximately 27.22% of the total population is greater than 20%, whereas 342
cities that can accommodate approximately 42% of the total population have tree canopy cover less than 20%. 
Moreover, we found that many small-area cities with low tree canopy coverage require great attention from the Brazilian
government. We expect that urban tree canopy maps will encourage research on Brazilian urban ecosystem services
to support urban development and improve inhabitants’ quality of life to achieve the goals of the Agenda for Sustainable Development. 
In addition, it can serve as a benchmark dataset for other high-resolution and mid/low-resolution
remote sensing images urban tree canopy mapping results assessments.

This Pytorch repository contains the code for our work [Semi-supervised Semantic Segmentation with High- and Low-level Consistency](https://arxiv.org/pdf/1908.05724.pdf). The approach uses two network branches that link semi-supervised classification with semi-supervised segmentation including self-training. The approach attains significant improvement over existing methods, especially when trained with very few labeled samples.

## Package pre-requisites
The code runs on Python 3 and Pytorch 0.4 The following packages are required. 

```
pip install scipy tqdm matplotlib numpy opencv-python
```

## Dataset preparation

Download ImageNet pretrained Resnet-101([Link](https://download.pytorch.org/models/resnet101-5d3b4d8f.pth)) and place it ```./pretrained_models/```


```
### Training semi-supervised (SSL)
```
python train.py   
``` 
### Validation 
```
python evaluate.py

## Instructions for setting-up Multi-Label Mean-Teacher branch
This work is based on the [Mean-Teacher](https://arxiv.org/abs/1703.01780) Semi-supervised Learning work. To use the MLMT branch, follow the instructions below. 
1. Fork the [mean-teacher](https://github.com/CuriousAI/mean-teacher) repo. 
2. Modify the fully connected layer, according to the number of classes and add Sigmoid activation for multi-label classification.
3. Use Binary Cross Entropy loss fucntion instead of multi-class Cross entropy. 
4. Load the pretrained ImageNet weights for ResNet-101 from ```./pretrained_models/```.
5. Use student/teacher predictions for Network output fusion with s4GAN branch. 
6. For lower labeled-ratio, early stopping might be required.  


## Acknowledgement

Parts of the code have been adapted from: 
[DeepLab-Resnet-Pytorch](https://github.com/speedinghzl/Pytorch-Deeplab), [AdvSemiSeg](https://github.com/hfslyc/AdvSemiSeg), [PyTorch-Encoding](https://github.com/zhanghang1989/PyTorch-Encoding)


## Citation

```
@article{1908.05724,
    Author = {Sudhanshu Mittal and Maxim Tatarchenko and Thomas Brox},
    Title = {Semi-Supervised Semantic Segmentation with High- and Low-level Consistency},
    journal = {arXiv preprint arXiv:1908.05724},
    Year = {2019},
}
```

