# Clothes Detection

## Dataset

Во-первых был подобран датасет: DeepFashion2 (https://github.com/switchablenorms/DeepFashion2). Объёмный, свежий, с хорошей разметкой - идеально для нашей задачи (за исключением малости категорий, всего 13). Статистика датасета:

![image](https://github.com/switchablenorms/DeepFashion2/blob/master/images/statistics_all.jpg)

Плюсом к датасету была статья (https://arxiv.org/pdf/1901.07973.pdf) содержащая много полезного: предлагаласть метрика + opensourse код для неё, также описывалось решение нашей задачи архитектурой Mask R-CNN и получение данных результатов:

<p align='center'>Table 1: Clothes detection trained with released DeepFashion2 Dataset evaluated on validation set.</p>

| AP | AP50 | AP75 | 
|---:|---:|---:|/
|0.638|0.789|0.745|

<p align='center'>Table 2: Clothes detection on different validation subsets, including scale, occlusion, zoom-in, and viewpoint.</p>

|||<sub>Scale|||<sub>Occlusion|||<sub>Zoom_in|||<sub>Viewpoint||<sub>Overall|
|:----:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
||<sub>small|<sub>moderate|<sub>large|<sub>slight|<sub>medium|<sub>heavy|<sub>no|<sub>medium|<sub>large|<sub>no wear|<sub>frontal|<sub>side or back||
|<sub>AP|<sub>0.604|<sub>0.700|<sub>0.660|<sub>0.712|<sub>0.654|<sub>0.372|<sub>0.695|<sub>0.629|<sub>0.466|<sub>0.624|<sub>0.681|<sub>0.641|<sub>0.667|
|<sub>AP50|<sub>0.780|<sub>0.851|<sub>0.768|<sub>0.844|<sub>0.810|<sub>0.531|<sub>0.848|<sub>0.755|<sub>0.563|<sub>0.713|<sub>0.832|<sub>0.796|<sub>0.814|
|<sub>AP75|<sub>0.717|<sub>0.809|<sub>0.744|<sub>0.812|<sub>0.768|<sub>0.433|<sub>0.806|<sub>0.718|<sub>0.525|<sub>0.688|<sub>0.791|<sub>0.744|<sub>0.773

## Solution

Конечно, можно просто пойти по стопам составителей датасета, но с поры их решения данной задачи прошёл примерно год. Воспользуемcя более инновационной архитектурой: YOLOv3, мы получим более быстрое и точное решение.
