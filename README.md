# TensorFlow Object Detection API

| [TensorFlow 1.x](https://github.com/DmitryRyumin/tfObjDet/tree/master/tf1) | [TensorFlow 2.x](https://github.com/DmitryRyumin/tfObjDet/tree/master/tf2) |
| --- | --- |

<h4 align="center"><span style="color:#EC256F;">Полезные ресурсы</span></h4>

- [Тестовый блокнот с обнаружениями объектов](https://github.com/DmitryRyumin/tfObjDet/tree/master/useful_resources/object_detection_tutorial.ipynb)

<h4 align="center"><span style="color:#EC256F;">Установка (24.09.2020)</span></h4>

1. Установить `Cuda 10.1` с `cuDNN v7.6.5` (**Примечание!** Только для `Windows` + `GPU`)

2. Установить TensorFlow

    >  **Windows**
    >
    > CMD
    >
    > ```shell script
    > pip install tensorflow-gpu
    > ```

    >  **MacOS**
    >
    > CMD
    >
    > ```shell script
    > pip install tensorflow
    > ```

3. Установить `Git` (**Примечание!** Только для `Windows`)

    [Скачать и установить необходимый дистрибутив](https://git-scm.com/)

    >  **MacOS**
    >
    > CMD
    >
    > ```shell script
    > brew install git
    > ```

4. Клонировать основную ветку репозитория `Tensorflow Models`

    > CMD
    >
    > ```shell script
    > git clone https://github.com/tensorflow/models.git
    > ```

5. Удалить все из папки `models` кроме `research`

6. Скачать [Protocol Buffers](https://github.com/protocolbuffers/protobuf/tags)

7. Переместить файл `bin/protoc` в `models/research`

8. В папке `models/research` создать файл `use_protobuf.py`

    > Python code
    >
    > ```python
    > #!/usr/bin/env python
    > # -*- coding: utf-8 -*-
    > 
    > """
    > Конвертация proto файлов
    > """
    > 
    > # Импорт необходимых инструментов
    > import os  # Взаимодействие с файловой системой
    > import sys  # Доступ к некоторым переменным и функциям Python
    > 
    > args = sys.argv  # Список аргументов командной строки
    > 
    > directory = args[1]  # Директория с proto файлами
    > protoc_path = args[2]  # Полный путь к protoc файлу
    > 
    > # Проход по всем файлам в указанной деректории
    > for file in os.listdir(directory):
    >    # Файл с расширением proto
    >     if file.endswith('.proto'):
    >         # Конвертация proto файла
    >         os.system(protoc_path + ' ' + directory + '/' + file + ' --python_out=.')
    > ```

9. Перейти в директорию `models/research` и выполнить `use_protobuf.py` файл

    > CMD
    >
    > ```shell script
    > cd models/research
    > 
    > # models/research/object_detection/protos - путь к директории с proto файлами
    > # models/research/protoc - путь к protoc файлу
    > python use_protobuf.py object_detection/protos protoc
    > ```
    >
    > **Примечание!** В директории `models/research/object_detection/protos` должны быть созданы `*.py`

10. Скопировать установочный файл из `models/research/object_detection/packages/tf2` в `models/research`

11. Выполнить установку `Tensorflow Models`

    > CMD
    >
    > ```shell script
    > python -m pip install .
    > ```

12. Протестировать установку `Tensorflow Models`

    > CMD
    >
    > ```shell script
    > python object_detection/builders/model_builder_tf2_test.py
    >
    > # Результат:
    > #
    > # Ran 20 tests in 33.222s
    > # OK (skipped=1)
    > ```