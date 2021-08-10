# CompactTransformers
My attempt at Re-Implementating Compact Transformer models from the paper '[Escaping the Big Data Paradigm with Compact Transformers](https://arxiv.org/abs/2104.05704)' by Ali Hassani et al.

## Model Architecture
![arch](https://user-images.githubusercontent.com/56354373/128810554-14f8ac36-4a3a-467c-b269-c8261a87010a.png)

## Paper Description
### Aim 
* Explore Vision Transformer based models using novel method that can be trained on less data
* The authors have proposed three architectures, each one an improvement on the previous one
* Namely, ViT-lite, Compact Vision Transformer, Compact Convolutional Transformer 
* CCT uses convolutions as the part of the tokenization steps which creates an inductive bias, so the patches preserves more spatial information 
* The authors also introduce a novel Sequence-Pooling layer which replaces the conventional class token design in Vision Transformer
* This paper claims to do better and more computationally efficient than the previous transformer based models and is comparable with CNN based models on classification tasks
## Methodology
![workflow](https://user-images.githubusercontent.com/56354373/128812050-dd6fd90e-1410-446c-a926-5012a6d0e32e.png)
![encoder](https://user-images.githubusercontent.com/56354373/128812086-cfd5b807-0429-40e6-892d-6fbfb1066616.png)

## Datasets
* [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html)

## Major Components Implemented
* **ViT-Lite** which includes the architecture of a Vision Transformer with lesser patch-size, transformer layers and MLP heads
* **Compact Vision Transformer** This used the same architecture if ViT-lite, here we replace the class tokens with a Sequence Pooling layer
* **Compact Convolutional Transformer** This is built on the of CVT, in the tokenization step, instead of sending the patches through the linear embedding layer, we send convolutions of the image as tokens

## Results
#### Hyperparameters
* Optimizer = AdamW 
* learning rate = 0.001 
* weight decay = 0.0001 
* batch size = 256 
* num epochs = 30
* image size = 32 
* patch size = 6 
* projection dim = 64 
* num heads = 4
* transformer layers = 8
* mlp head units = [2048, 1024]
* The training of ViT-Lite took about 120 minutes on Google Colaboratory's TPU and got an accuracy of 59.18 and validation accuracy of 60. 
CVT took 100 minutes to train with an accuracy of 61 and validation accuracy of 60 and a test accuracy of 59.29
The training of CCT took 200 minutes for training on Google and got an accuracy of 84.24 and validation accuracy of 77.64 and a test accuracy of 77.15.
#### Loss/ACC Vs Epochs for CCT
![image](https://user-images.githubusercontent.com/56354373/128816242-72421773-4e9d-4199-b9a6-1ff54b72bf03.png )
![image](https://user-images.githubusercontent.com/56354373/128816474-3fbc11f6-44a1-40ba-958f-8577bb4df881.png)
## Future Scope
* Further changes in the attention mechanism can be made to make the patches better represented such as using attention gradient rollout which ignores regions with low attention.
* It will be interesting to use involutions instead of convolutions in the tokenization step and see how the performance has changed.\newline \newline
* We can use different type of loss functions such as patch-wise contrastive loss, patch-wise mixing loss etc.

## Citation Of Original Paper
```
@article {hassani2021escaping, 
	title        = {Escaping the Big Data Paradigm with Compact Transformers},
	author       = {Ali Hassani and Steven Walton and Nikhil Shah and Abulikemu, Abuduweili and Jiachen Li and Humphrey Shi},
	year         = 2021,
	url          = {https://arxiv.org/abs/2104.05704},
	eprint       = {2104.05704},
	archiveprefix = {arXiv},
	primaryclass = {cs.CV}
}
```

