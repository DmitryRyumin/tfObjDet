# TensorFlow Object Detection API

| [TensorFlow 1.x](https://github.com/DmitryRyumin/tfObjDet/tree/master/tf1) | [TensorFlow 2.x](https://github.com/DmitryRyumin/tfObjDet/tree/master/tf2) |
| --- | --- |

### Установка `24.09.2020`

**1. Установить `Cuda 10.1` с `cuDNN v7.6.5`**

> **Примечание!** Только для `Windows` + `GPU`

**2. Установить TensorFlow**

>  **Windows**

```shell script
pip install tensorflow-gpu
```

>  **MacOS**

```shell script
pip install tensorflow
```

**3. Установить `Git`**

>  **Windows**

[Скачать и установить необходимый дистрибутив](https://git-scm.com/)

>  **MacOS**

```shell script
brew install git
```

**4. Клонировать основную ветку репозитория `Tensorflow Models`**

```shell script
git clone https://github.com/tensorflow/models.git
```

**5. Удалить все из папки `models` кроме `research`**

**6. Скачать [Protocol Buffers](https://github.com/protocolbuffers/protobuf/tags)**

**7. Переместить файл `bin/protoc` в `research`**

**8. В папке `research` создать файл `use_protobuf.py`**

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

"""
Конвертация proto файлов
"""

# Импорт необходимых инструментов
import os  # Взаимодействие с файловой системой
import sys  # Доступ к некоторым переменным и функциям Python

args = sys.argv  # Список аргументов командной строки

directory = args[1]  # Директория с proto файлами
protoc_path = args[2]  # Полный путь к protoc файлу

# Проход по всем файлам в указанной деректории
for file in os.listdir(directory):
    # Файл с расширением proto
    if file.endswith('.proto'):
        # Конвертация proto файла
        os.system(protoc_path + ' ' + directory + '/' + file + ' --python_out=.')
```

**9. Перейти в директорию `models/research` и выполнить `use_protobuf.py` файл**

```shell script
cd models/research

# models/research/object_detection/protos - путь к директории с proto файлами
# models/research/protoc - путь к protoc файлу
python use_protobuf.py object_detection/protos protoc
```

> **Примечание!** В директории `models/research/object_detection/protos` должны быть созданы `*.py`

**10. Скопировать установочный файл из `models/research/object_detection/packages/tf2` в `models/research`**

**11. Выполнить установку `Tensorflow Models`**

```shell script
python -m pip install .
```

**12. Протестировать установку `Tensorflow Models`**

```shell script
python object_detection/builders/model_builder_tf2_test.py

# Результат:
#
# Ran 20 tests in 33.222s
# OK (skipped=1)
```