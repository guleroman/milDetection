
# milDetection
Программный модуль оперативного обнаружения военных объектов по данным с беспилотных летательных аппаратов

## Описание
В настоящее время прослеживается тенденция постепенного отхода от ручного управления беспилотными летательными аппаратами (далее - БЛА). Полет может проходить в автоматическом режиме, путем предварительного задания координат точек изменения направления движения. Однако, всё это не исключает необходимости постоянного наблюдения оператора за передаваемым в режиме реального времени видеопотоком. Отсюда и существующее ограничение в возможном количестве единовременно используемых БЛА количеством операторов в расчете.

![img](/gui/img4.jpg)

Применение же разработанного программного модуля оперативного обнаружения объектов по данным с БЛА позволяет одному оператору запустить сразу несколько БЛА, управляемых в автоматическом режиме по заранее заданному маршруту, и ожидать поступления сигнала об обнаружении противника.

![img](/gui/img5.jpg)

## Подготовка
### Настройка каталога Tensorflow и виртуальной среды Anaconda
#### 1. Загрузка репозитория Tensorflow Object Detection API с github

   Создайте папку на диске D: и назовите ее "pythonOCR". Этот рабочий каталог будет содержать все файлы TensorFlow Object Detection, а также обучающие данные, обученную модель нейросети, файлы конфигурации и все остальное, что необходимо для обнаружения интересующих нас объектов.

Загрузите полный репозиторий TensorFlow Object Detection API, расположенный по адресу https://github.com/tensorflow/models в папку D:\pythonOCR.

#### 2. Загрузите Faster_RCNN_Resnet101_Kitti из TensorFlow's model zoo


[Faster_RCNN_Resnet101_Kitti](http://download.tensorflow.org/models/object_detection/faster_rcnn_resnet101_coco_2018_01_28.tar.gz)
Распакуйте из архива папку faster_rcnn_resnet101_kitti_2018_01_28 в директорию D:\pythonOCR\models\research\object_detection.

#### 3. Загрузите полный репозиторий, расположенный на этой странице. 
Прокрутите вверх и нажмите клонировать или загрузить и извлеките все содержимое непосредственно в D:\pythonOCR\models\research\object_detection.

#### 4. Загрузите архив с уже обученной нейросетью.
Если вы не собираетесь самостоятельно производить обучение нейросети загрузите [этот архив](https://yadi.sk/d/l-k20liGzFvsGw). Распакуйте его содержимое в каталог D:\pythonOCR\models\research\object_detection


#### 5. Настройка виртуальной среды Anaconda


```
D:\> conda create -n pythonOCR pip python=3.5
```


```
D:\> activate pythonOCR
```


```
(pythonOCR) D:\> conda install tensorflow-gpu
```


```
(pythonOCR) D:\> pip install tensorflow-gpu
```


```
(pythonOCR) D:\> conda install -c anaconda protobuf
(pythonOCR) D:\> pip install pillow
(pythonOCR) D:\> pip install lxml
(pythonOCR) D:\> pip install Cython
(pythonOCR) D:\> pip install jupyter
(pythonOCR) D:\> pip install matplotlib
(pythonOCR) D:\> pip install pandas
(pythonOCR) D:\> pip install opencv-python
(pythonOCR) D:\> pip install pyqt5
```

#### 6. Настройка переменных PYTHONPATH


```
(pythonOCR) D:\> set PYTHONPATH=D:\pythonOCR\models;D:\pythonOCR\models\research;D:\pythonOCR\models\research\slim
```

#### 7. Компиляция файлов Protobuf 

В командной строке Anaconda перейдите в каталог \models\research, скопируйте и вставьте в командную строку следующую команду и нажмите клавишу Ввод:


```
protoc --python_out=. .\object_detection\protos\anchor_generator.proto .\object_detection\protos\argmax_matcher.proto .\object_detection\protos\bipartite_matcher.proto .\object_detection\protos\box_coder.proto .\object_detection\protos\box_predictor.proto .\object_detection\protos\eval.proto .\object_detection\protos\faster_rcnn.proto .\object_detection\protos\faster_rcnn_box_coder.proto .\object_detection\protos\grid_anchor_generator.proto .\object_detection\protos\hyperparams.proto .\object_detection\protos\image_resizer.proto .\object_detection\protos\input_reader.proto .\object_detection\protos\losses.proto .\object_detection\protos\matcher.proto .\object_detection\protos\mean_stddev_box_coder.proto .\object_detection\protos\model.proto .\object_detection\protos\optimizer.proto .\object_detection\protos\pipeline.proto .\object_detection\protos\post_processing.proto .\object_detection\protos\preprocessor.proto .\object_detection\protos\region_similarity_calculator.proto .\object_detection\protos\square_box_coder.proto .\object_detection\protos\ssd.proto .\object_detection\protos\ssd_anchor_generator.proto .\object_detection\protos\string_int_label_map.proto .\object_detection\protos\train.proto .\object_detection\protos\keypoint_box_coder.proto .\object_detection\protos\multiscale_anchor_generator.proto .\object_detection\protos\graph_rewriter.proto
```

Наконец, выполните следующие команды из каталога D:\pythonOCR\models\research:


```
(pythonOCR) D:\pythonOCR\models\research> python setup.py build
(pythonOCR) D:\pythonOCR\models\research> python setup.py install
```

## Запуск 
![img](/gui/img6.jpg)

Вы можете использовать GUI, запустив файл window.py. 
В каталоге \object_detection введите следующую команду:

```
(pythonOCR) D:\pythonOCR\models\research\object_detection> python window.py
```
