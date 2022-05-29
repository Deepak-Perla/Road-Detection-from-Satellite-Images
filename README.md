# Road-Detetction-from-Satellite-Images

## U-Net-Satellite

The aim of this project is road detection from satellite images using a variant of deep Convolutional Neural Networks which is known as U-Net. The output of the model is a segmentation mask which differentiates roads from other terrains.
 
 
 ## Overview
 
 ### Model

U-net is an encoder-decoder type network architecture for image segmentation. The name of the architecture comes from its unique shape, where the feature maps from convolution part in downsampling step are fed to the up-convolution part in up-sampling step. 
This model is a slight modification of original U-Net architecture. The details of the architecture can be clearly seen in the notebook as the output of the "model.summary()" cell.

![](https://miro.medium.com/proxy/1*lvXoKMHoPJMKpKK7keZMEA.png)

### Code

- Kaggle: https://www.kaggle.com/deepakperla/deepglobe-v3

### Data

This is a competition where they have given dataset to only participants so it is not officially released. Headover Acknowledgements
- The training data for Road Challenge contains 6226 satellite imagery in RGB, size 1024x1024.
- The imagery has 50cm pixel resolution, collected by DigitalGlobe's satellite.
- The dataset contains 1243 validation and 1101 test images (but no masks).

### Label
- Each satellite image is paired with a mask image for road labels. The mask is a grayscale image, with white standing for road pixel, and black standing for background.
- File names for satellite images and the corresponding mask image are id _sat.jpg and id _mask.png. id is a randomized integer.
- Please note:
  - The values of the mask image may not be pure 0 and 255. When converting to labels, please binarize them at threshold 128.
  - The labels are not perfect due to the cost for annotating segmentation mask, specially in rural regions. In addition, we intentionally didn't annotate small roads within farmlands.

### Training

The model was trained for 50 epochs and took about 4 hours on Kaggle GPU. After 50 epochs, the training Dice score and Jaccard index were 0.8918 and  0.9754. Corresponding validation metrics were 0.7533 and 0.9527.
The training vs validation loss is shown below :

- Val Accuracy
- ![](https://user-images.githubusercontent.com/71626642/170860729-f26a3420-6c7a-4628-b137-27649dc841db.png)

- Val Loss
- ![](https://www.kaggleusercontent.com/kf/94201908/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..1dqipK1gVmJzoGCucYi8pQ.dXhZC4muo9nQ6Csz2SNqvs1VYNKralnnhCujI11qkE5_CSTcnBZD5TlUujbDpkOnaSkrffQZwhaHC3AaiuB-TsN_tgH3GgxYavl-ihxkxSYeJHHJ6xjnXOc4J2fYS7tz3oWvDTquphM2NIzKeVuGbAsrahMd1HU7NthF8wS4LCHviVOge-PjNw-CSEdRC6FOv_kTbK4oHHHQc8jhHJ2_XmFKX_ChowYftMHF4km8_qOOd9Of-YbuEWUujFuIOxoMLtyNX5ql4Y5QcJanqoz7RhcRd5AkPbBN0E9dTaKb1UoWbY_1S6rbieiViwuJEXwiY2-8pUf30-lszLw-OEfRm5yCy2CM3BOEFDeOCDpcqxb7DVKGu2SWbhipjIlIVjyvBub2jLg2P-VkmXqtXjDr7-MXTCBxtgQzIK67se3FTM5afZO5yeOL3peGSNWzCjqR_uEbLpTPJOziN8b6RbFEL9Tqu4TaGSPm3Cv4gVVLwC-eM8xLM4zQ2gM6DX2DPBOZEpqabU9OGevz9F2E6ERtuJtV-EMWFv9SAUJI9jroqWrz3B0L48DjuuHW9C0YI_tv-uKiAnyuf6pQta0P2dzZXrsPbnKmW67XOivi5I0oI3BWhsRGa6kDd2aeWAep7bfcfl5LETr5sRxp4P7aFxEYiw.TtMDupggL4bu-yYAkFYQtg/__results___files/__results___27_0.png)

- IoU
- ![](https://www.kaggleusercontent.com/kf/94201908/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..1dqipK1gVmJzoGCucYi8pQ.dXhZC4muo9nQ6Csz2SNqvs1VYNKralnnhCujI11qkE5_CSTcnBZD5TlUujbDpkOnaSkrffQZwhaHC3AaiuB-TsN_tgH3GgxYavl-ihxkxSYeJHHJ6xjnXOc4J2fYS7tz3oWvDTquphM2NIzKeVuGbAsrahMd1HU7NthF8wS4LCHviVOge-PjNw-CSEdRC6FOv_kTbK4oHHHQc8jhHJ2_XmFKX_ChowYftMHF4km8_qOOd9Of-YbuEWUujFuIOxoMLtyNX5ql4Y5QcJanqoz7RhcRd5AkPbBN0E9dTaKb1UoWbY_1S6rbieiViwuJEXwiY2-8pUf30-lszLw-OEfRm5yCy2CM3BOEFDeOCDpcqxb7DVKGu2SWbhipjIlIVjyvBub2jLg2P-VkmXqtXjDr7-MXTCBxtgQzIK67se3FTM5afZO5yeOL3peGSNWzCjqR_uEbLpTPJOziN8b6RbFEL9Tqu4TaGSPm3Cv4gVVLwC-eM8xLM4zQ2gM6DX2DPBOZEpqabU9OGevz9F2E6ERtuJtV-EMWFv9SAUJI9jroqWrz3B0L48DjuuHW9C0YI_tv-uKiAnyuf6pQta0P2dzZXrsPbnKmW67XOivi5I0oI3BWhsRGa6kDd2aeWAep7bfcfl5LETr5sRxp4P7aFxEYiw.TtMDupggL4bu-yYAkFYQtg/__results___files/__results___28_0.png)
  
- Binary Accuracy
- ![](https://www.kaggleusercontent.com/kf/94201908/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..1dqipK1gVmJzoGCucYi8pQ.dXhZC4muo9nQ6Csz2SNqvs1VYNKralnnhCujI11qkE5_CSTcnBZD5TlUujbDpkOnaSkrffQZwhaHC3AaiuB-TsN_tgH3GgxYavl-ihxkxSYeJHHJ6xjnXOc4J2fYS7tz3oWvDTquphM2NIzKeVuGbAsrahMd1HU7NthF8wS4LCHviVOge-PjNw-CSEdRC6FOv_kTbK4oHHHQc8jhHJ2_XmFKX_ChowYftMHF4km8_qOOd9Of-YbuEWUujFuIOxoMLtyNX5ql4Y5QcJanqoz7RhcRd5AkPbBN0E9dTaKb1UoWbY_1S6rbieiViwuJEXwiY2-8pUf30-lszLw-OEfRm5yCy2CM3BOEFDeOCDpcqxb7DVKGu2SWbhipjIlIVjyvBub2jLg2P-VkmXqtXjDr7-MXTCBxtgQzIK67se3FTM5afZO5yeOL3peGSNWzCjqR_uEbLpTPJOziN8b6RbFEL9Tqu4TaGSPm3Cv4gVVLwC-eM8xLM4zQ2gM6DX2DPBOZEpqabU9OGevz9F2E6ERtuJtV-EMWFv9SAUJI9jroqWrz3B0L48DjuuHW9C0YI_tv-uKiAnyuf6pQta0P2dzZXrsPbnKmW67XOivi5I0oI3BWhsRGa6kDd2aeWAep7bfcfl5LETr5sRxp4P7aFxEYiw.TtMDupggL4bu-yYAkFYQtg/__results___files/__results___29_0.png)


## Results

The following images show the comparison of the ground truth, and it's corresponding prediction:

- ![](https://www.kaggleusercontent.com/kf/94201908/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..1dqipK1gVmJzoGCucYi8pQ.dXhZC4muo9nQ6Csz2SNqvs1VYNKralnnhCujI11qkE5_CSTcnBZD5TlUujbDpkOnaSkrffQZwhaHC3AaiuB-TsN_tgH3GgxYavl-ihxkxSYeJHHJ6xjnXOc4J2fYS7tz3oWvDTquphM2NIzKeVuGbAsrahMd1HU7NthF8wS4LCHviVOge-PjNw-CSEdRC6FOv_kTbK4oHHHQc8jhHJ2_XmFKX_ChowYftMHF4km8_qOOd9Of-YbuEWUujFuIOxoMLtyNX5ql4Y5QcJanqoz7RhcRd5AkPbBN0E9dTaKb1UoWbY_1S6rbieiViwuJEXwiY2-8pUf30-lszLw-OEfRm5yCy2CM3BOEFDeOCDpcqxb7DVKGu2SWbhipjIlIVjyvBub2jLg2P-VkmXqtXjDr7-MXTCBxtgQzIK67se3FTM5afZO5yeOL3peGSNWzCjqR_uEbLpTPJOziN8b6RbFEL9Tqu4TaGSPm3Cv4gVVLwC-eM8xLM4zQ2gM6DX2DPBOZEpqabU9OGevz9F2E6ERtuJtV-EMWFv9SAUJI9jroqWrz3B0L48DjuuHW9C0YI_tv-uKiAnyuf6pQta0P2dzZXrsPbnKmW67XOivi5I0oI3BWhsRGa6kDd2aeWAep7bfcfl5LETr5sRxp4P7aFxEYiw.TtMDupggL4bu-yYAkFYQtg/__results___files/__results___36_0.png)

## References

- Original Dataset:https://competitions.codalab.org/competitions/18467 (DATASET NOT RELEASED)
- Datasets used: https://www.kaggle.com/datasets/balraj98/deepglobe-road-extraction-dataset

## Acknowledgements
This dataset was obtained from Road Extraction Challenge Track in DeepGlobe Challenge . For more details on the dataset refer the related publication - DeepGlobe 2018: A Challenge to Parse the Earth through Satellite Images
