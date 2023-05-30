
# ChatInformationTheory2023
## Laboratory №1
**Дата:** 23/05/2023

**Выполнил:** Liao Xin, M4150 

**Название:** Сжатие изображений при помощи нейронных сестей


**Требования к алгоритму:**
- Написать кодер и декодер ,которые работают как отдельные программы.
- На вход кодера подается изображение в raw формате(png,bmp, и т.д.),а также режим сжатия (слабее-сильнее).На выходе кодер генерирует файл со сжатым изображением.
- На вход декодера подается сжатый файл,на выходе декодер гинерирует изображение в raw формате.
- Алгоритм сжатия должен включать в себя вычисление признаков,квантование признаков,сжатие квантованных признаков без потерь.


## Реализация
This repo is implementation for [Learned Image Compression with Discretized Gaussian Mixture Likelihoods and Attention Modules](https://github.com/LiuLei95/PyTorch-Learned-Image-Compression-with-GMM-and-Attention/tree/main) in pytorch.

**the Network architecture:**
![architecture](https://github.com/liaoxin-a/ChatInformationTheory2023/blob/main/image/architecture.JPG)



Cжатие изображения может быть сформулировано как:
| Формула | Определения |
| ------- |------|
| ![Gaussian Mixture Likelihoods model](https://github.com/liaoxin-a/ChatInformationTheory2023/blob/main/image/model.JPG) |где <br>$x$-необработанные изображения,<br>$\hat{x}$-реконструированные изображения,<br>$y$-скрытое представление перед квантованием,  <br>$\hat{y}$-сжатые коды,<br>$U\mid Q$-квантование и энтропийное кодирование |

### Реализация кодера
Во время тренировки квантование аппроксимируется однородным шумом U для генерации шумовых кодов $\widetilde{y}$
```python
    #!/usr/bin/env python3
    feature = self.Encoder(input_image)#Analysis_transform
    z = self.priorEncoder(feature)#Hyper_analysis
    if self.training:
        compressed_z = z + quant_noise_z
    else:
        compressed_z = torch.round(z)
```

### Реализация декодера
Во время вывода, $U\mid Q$ представляет реальное круговое квантование для генерации $\hat{y}$ и последующие энтропийные кодеры для генерации битового потока.
```python
    #!/usr/bin/env python3
    feature_renorm = feature # feature from Encoder
    if self.training:
        compressed_feature_renorm = feature_renorm + quant_noise_feature
    else:
        compressed_feature_renorm = torch.round(feature_renorm)
    recon_image = self.Decoder(compressed_feature_renorm) #Synthesis_transform
```

## Качественные метрики
### Peak Signal-to-Noise Ratio (PSNR)

According to [wikipedia](https://en.wikipedia.org/wiki/Peak_signal-to-noise_ratio):
>Peak signal-to-noise ratio, often abbreviated PSNR, is an engineering term for the ratio between the maximum possible power of a signal and the power of corrupting noise that affects the fidelity of its representation. Because many signals have a very wide dynamic range, PSNR is usually expressed in terms of the logarithmic decibel scale.

### Bits Per Pixel (BPP)

According to [wikipedia](https://en.wikipedia.org/wiki/Color_depth):
>Color depth or colour depth (see spelling differences), also known as bit depth, is either the number of bits used to indicate the color of a single pixel, or the number of bits used for each color component of a single pixel. When referring to a pixel, the concept can be defined as bits per pixel (bpp).

**Количество бит,затрачиваемое в среднем на один пиксель изображения для тестовых изображений.**

## Эксперименты: 
| Kартина | Результат |
| ------- |------|
| Lena | ![final_lena](https://github.com/liaoxin-a/ChatInformationTheory2023/blob/main/image/final_lena.png) |	
| Peppers | ![final_peppers](https://github.com/liaoxin-a/ChatInformationTheory2023/blob/main/image/final_peppers.png) | 
| Baboon | ![final_baboon](https://github.com/liaoxin-a/ChatInformationTheory2023/blob/main/image/final_baboon.png) |

## Графики сравнения алгоритма с JPEG
![result](https://github.com/liaoxin-a/ChatInformationTheory2023/blob/main/image/result.png)

## Использованные источники
[1]https://openaccess.thecvf.com/content_CVPR_2020/papers/Cheng_Learned_Image_Compression_With_Discretized_Gaussian_Mixture_Likelihoods_and_Attention_CVPR_2020_paper.pdf

[2] https://github.com/LiuLei95/PyTorch-Learned-Image-Compression-with-GMM-and-Attention/tree/main

