# Clothes Detection

## Dataset

Во-первых был подобран датасет: DeepFashion2 (https://github.com/switchablenorms/DeepFashion2). Объёмный, свежий, с хорошей разметкой - идеально для нашей задачи (за исключением малости категорий, всего 13). Статистика датасета:

![image](https://github.com/switchablenorms/DeepFashion2/blob/master/images/statistics_all.jpg)

Плюсом к датасету была статья (https://arxiv.org/pdf/1901.07973.pdf) содержащая много полезного: предлагаласть метрика + opensourse код для неё, также описывалось решение нашей задачи архитектурой Mask R-CNN и получение данных результатов:

<p align='center'>Table 1: Clothes detection trained with released DeepFashion2 Dataset evaluated on validation set.</p>

| AP | AP50 | AP75 | 
|---:|---:|---:|
|0.638|0.789|0.745|

<p align='center'>Table 2: Clothes detection on different validation subsets, including scale, occlusion, zoom-in, and viewpoint.</p>

|||<sub>Scale|||<sub>Occlusion|||<sub>Zoom_in|||<sub>Viewpoint||<sub>Overall|
|:----:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
||<sub>small|<sub>moderate|<sub>large|<sub>slight|<sub>medium|<sub>heavy|<sub>no|<sub>medium|<sub>large|<sub>no wear|<sub>frontal|<sub>side or back||
|<sub>AP|<sub>0.604|<sub>0.700|<sub>0.660|<sub>0.712|<sub>0.654|<sub>0.372|<sub>0.695|<sub>0.629|<sub>0.466|<sub>0.624|<sub>0.681|<sub>0.641|<sub>0.667|
|<sub>AP50|<sub>0.780|<sub>0.851|<sub>0.768|<sub>0.844|<sub>0.810|<sub>0.531|<sub>0.848|<sub>0.755|<sub>0.563|<sub>0.713|<sub>0.832|<sub>0.796|<sub>0.814|
|<sub>AP75|<sub>0.717|<sub>0.809|<sub>0.744|<sub>0.812|<sub>0.768|<sub>0.433|<sub>0.806|<sub>0.718|<sub>0.525|<sub>0.688|<sub>0.791|<sub>0.744|<sub>0.773

## Solution

Конечно, можно просто пойти по стопам составителей датасета, но мы всё-таки используем инновационные технологии) Воспользуемcя архитектурой YOLO и мы получим более быстрое и точное решение.
Преобразовав датасет в COCO Data, модифицировав cfg для COCO (config можно найти в https://github.com/AlberetOZ/WondeRobe_Clothes_test/yolo/df2cfg), переходим к обучению с помощью фреймворка Darknet:
./darknet detector train cfg/coco.data cfg/yolov3.cfg darknet53.conv.74

Полученные веса (checkpoints) лежат в папке https://github.com/AlberetOZ/WondeRobe_Clothes_test/yolo/weights/

## Result

Мы получили неплохую демо версию Детектрона атрибута одежды (Примеры работы можно найти в https://github.com/AlberetOZ/WondeRobe_Clothes_test/output/). В перспективе этот проект можно оптимизировать (тем более если потребуется работа с видеопотоком), расширить количество категорий одежды, модифицировать сетку и многое другое, + определять также цвет/стиль и др. По времени было затрачено ~20 часов. 

# That's all
![image](https://github.com/AlberetOZ/WondeRobe_Clothes_test/output/1+1_yolo.jpg)
