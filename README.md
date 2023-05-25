# ChatInformationTheory2023
## Laboratory №1
**Дата:** 23/05/2023

**Выполнил:** Liao Xin, M4150 

**Название:** Сжатие изображений при помощи нейронных сестей


**Описание структуры каталогов:**
```
./
│   readme.md
│      
├───src
│   └───main
│       ├───java
│       │   └───lab3
│       └───resourse
└───target
    ├───classes
    │   └───lab3
    └───test-classes
```


**Требования к алгоритму:**
- Написать кодер и декодер ,которые работают как отдельные программы.
- На вход кодера подается изображение в raw формате(png,bmp, и т.д.),а также режим сжатия (слабее-сильнее).На выходе кодер генерирует файл со сжатым изображением.
- На вход декодера подается сжатый файл,на выходе декодер гинерирует изображение в raw формате.
- Алгоритм сжатия должен включать в себя вычисление признаков,квантование признаков,сжатие квантованных признаков без потерь.


**Реализация кодера**
image

**Реализация декодера**
image

## Качественные метрики
### Peak Signal-to-Noise Ratio (PSNR)

According to [wikipedia](https://en.wikipedia.org/wiki/Peak_signal-to-noise_ratio):
>Peak signal-to-noise ratio, often abbreviated PSNR, is an engineering term for the ratio between the maximum possible power of a signal and the power of corrupting noise that affects the fidelity of its representation. Because many signals have a very wide dynamic range, PSNR is usually expressed in terms of the logarithmic decibel scale.

### Peak Signal-to-Noise Ratio (PSNR)

According to [wikipedia](https://en.wikipedia.org/wiki/Peak_signal-to-noise_ratio):
>Peak signal-to-noise ratio, often abbreviated PSNR, is an engineering term for the ratio between the maximum possible power of a signal and the power of corrupting noise that affects the fidelity of its representation. Because many signals have a very wide dynamic range, PSNR is usually expressed in terms of the logarithmic decibel scale.


## Эксперименты: 
| Проблема | Размер | Параметры popsize и gens | Длина маршрута | Количество итераций до сходимости |Оптимальный маршрут|
| ------- |------| ------| ------| ------|------|
| XQF131 | 131 |	10,10 | 694.891 | 0 | 564 |
| XQF131 | 131 | 100,10000 | 662.821 | 3209 |  564 |
| XQG237 | 237 |	10,10 | 1241.59 | 0 | 1019|
| XQG237 | 237 | 100,10000 | 1206.756 | 7372 | 1019|
| PMA343 | 343 |	10,10 | 1655.441 | 0 | 1368 |
| PMA343 | 343 | 100,10000 | 1621.804 | 6452 | 1368 |
| PKA379 | 379 |	10,10 | 1634.006 | 0 | 1332 |
| PKA379 | 379 | 100,10000 | 1592.456 | 3221 | 1332 |
| BCL380 | 380 |	10,10 | 1912.537 | 0 | 1621 |
| BCL380 | 380 | 100,10000 | 1855.152 | 1324 | 1621 |

