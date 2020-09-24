# TensorFlow Object Detection API

| [TensorFlow 1.x](https://github.com/DmitryRyumin/tfObjDet/tree/master/tf1) | [TensorFlow 2.x](https://github.com/DmitryRyumin/tfObjDet/tree/master/tf2) |
| --- | --- |

## Установка

**1. Установить `Git`**

>  **Windows**

[Скачать и установить необходимый дистрибутив](https://git-scm.com/)

>  **MacOS**

```shell script
brew install git
```

**2. Клонировать основную ветку репозитория `Tensorflow Models`**

```shell script
git clone https://github.com/tensorflow/models.git
```

**3. Удалить все из папки `models` кроме `research`**

**4. Скачать [Protocol Buffers](https://github.com/protocolbuffers/protobuf/tags)**

**5. Переместить файл `bin/protoc` в `research`**

**6. В папке `research` создать файл `use_protobuf.py`**

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

**7. Перейти в директорию `models/research` и выполнить `use_protobuf.py` файл**

```shell script
cd models/research

# models/research/object_detection/protos - путь к директории с proto файлами
# models/research/protoc - путь к protoc файлу
python use_protobuf.py object_detection/protos protoc
```

> **Примечание!** В директории `models/research/object_detection/protos` должны быть созданы `*.py` файлы
