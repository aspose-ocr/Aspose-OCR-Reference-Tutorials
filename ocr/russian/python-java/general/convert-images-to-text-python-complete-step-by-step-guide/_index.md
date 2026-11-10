---
category: general
date: 2026-05-31
description: Узнайте, как конвертировать изображения в текст на Python с помощью скрипта
  массовой конвертации изображений в текст. Распознавайте текст со сканированных изображений
  с помощью Aspose.OCR за считанные минуты.
draft: false
keywords:
- convert images to text python
- bulk image to text conversion
- recognize text from scanned images
language: ru
og_description: Конвертировать изображения в текст на Python мгновенно. Это руководство
  показывает массовое преобразование изображений в текст и как распознавать текст
  со сканированных изображений с помощью Aspose.OCR.
og_title: Конвертация изображений в текст на Python – Полный учебник
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to convert images to text python with a bulk image to text
    conversion script. Recognize text from scanned images using Aspose.OCR in minutes.
  headline: Convert Images to Text Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to convert images to text python with a bulk image to text
    conversion script. Recognize text from scanned images using Aspose.OCR in minutes.
  name: Convert Images to Text Python – Complete Step‑by‑Step Guide
  steps:
  - name: Imports the OCR engine classes.
    text: Imports the OCR engine classes.
  - name: Instantiates a `BatchOcrEngine`.
    text: Instantiates a `BatchOcrEngine`.
  - name: Points the engine at an input folder of images.
    text: Points the engine at an input folder of images.
  - name: Directs the engine to write each extracted text file into an output folder.
    text: Directs the engine to write each extracted text file into an output folder.
  - name: Fires the `recognize()` method, which **recognize text from scanned images**
      one by one.
    text: Fires the `recognize()` method, which **recognize text from scanned images**
      one by one.
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Преобразование изображений в текст на Python – Полное пошаговое руководство
url: /ru/python-java/general/convert-images-to-text-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование изображений в текст Python – Полное пошаговое руководство

Когда‑то задумывались, как **convert images to text python** без бесконечного поиска библиотек? Вы не одиноки. Будь то оцифровка старых чеков, извлечение данных из отсканированных счетов‑фактур или создание поискового архива PDF‑файлов, преобразование картинок в обычный текст — ежедневная задача для многих разработчиков.

В этом руководстве мы пройдём через конвейер **bulk image to text conversion**, который распознаёт текст со сканированных изображений, сохраняет каждый результат в отдельный файл `.txt` и делает всё это всего несколькими строками кода на Python. Никаких скрытых API — Aspose.OCR делает всю тяжёлую работу, а мы покажем, как правильно его подключить.

## Что вы узнаете

- Как установить и настроить пакет Aspose.OCR for Python.  
- Точный код, необходимый для **convert images to text python** с использованием `BatchOcrEngine`.  
- Советы по работе с распространёнными проблемами, такими как неподдерживаемые форматы или повреждённые файлы.  
- Способы проверить, что шаг **recognize text from scanned images** действительно завершился успешно.  

К концу этого руководства у вас будет готовый к запуску скрипт, способный обработать тысячи изображений за один проход — идеальное решение для любого сценария пакетной обработки.

## Предварительные требования

- Python 3.8+ установленный на вашем компьютере.  
- Папка с изображениями (PNG, JPEG, TIFF и т.д.), которые вы хотите превратить в текст.  
- Активный аккаунт Aspose Cloud или бесплатная пробная лицензия (бесплатный уровень достаточен для тестов).  

Если всё это у вас есть, приступим.

---

## Шаг 1 – Настройте окружение Python

Прежде чем писать любой код OCR, убедитесь, что работаете в чистом виртуальном окружении. Это изолирует зависимости и предотвращает конфликты версий.

```bash
# Create a new virtual environment named venv
python -m venv venv

# Activate the environment (Windows)
venv\Scripts\activate

# Activate the environment (macOS / Linux)
source venv/bin/activate
```

> **Pro tip:** Держите каталог проекта аккуратным — создайте подпапку `ocr_project` и разместите скрипт там. Это упростит работу с путями позже.

## Шаг 2 – Установите Aspose.OCR for Python

Aspose.OCR — коммерческая библиотека, но она поставляется с бесплатным wheel‑пакетом в стиле NuGet, который можно установить из PyPI. Выполните следующую команду в активированном виртуальном окружении:

```bash
pip install aspose-ocr
```

Если возникла ошибка доступа, добавьте флаг `--user` или запустите команду с `sudo` (только Linux/macOS). После установки вы должны увидеть что‑то вроде:

```
Successfully installed aspose-ocr-23.9.0
```

> **Почему Aspose?** В отличие от многих открытых OCR‑инструментов, Aspose.OCR поддерживает **bulk image to text conversion** «из коробки» и работает с широким спектром форматов изображений без дополнительной настройки. Кроме того, он предоставляет класс `BatchOcrEngine`, который делает задачу **convert images to text python** одно‑строчным вызовом.

## Шаг 3 – Convert Images to Text Python с помощью Batch OCR

Теперь к сердцу руководства. Ниже полностью рабочий скрипт, который:

1. Импортирует классы OCR‑движка.  
2. Создаёт экземпляр `BatchOcrEngine`.  
3. Указывает движку входную папку с изображениями.  
4. Задаёт папку вывода, куда будут записаны текстовые файлы.  
5. Вызывает метод `recognize()`, который **recognize text from scanned images** по одному.

Сохраните следующее как `batch_ocr.py` в папке проекта:

```python
# batch_ocr.py
# -------------------------------------------------
# Bulk Image to Text Conversion using Aspose.OCR
# -------------------------------------------------

# Step 1: Import the OCR engine classes
from asposeocr import BatchOcrEngine, OcrEngine

# Step 2: Create a batch OCR engine instance
batch_engine = BatchOcrEngine()

# Step 3: Set the folder that contains the images to be processed
# Replace 'YOUR_DIRECTORY' with the absolute path to your images folder
batch_engine.input_folder = "YOUR_DIRECTORY/input_images"

# Step 4: Set the folder where the extracted text files will be saved
# Make sure this folder exists or Aspose will raise an error
batch_engine.output_folder = "YOUR_DIRECTORY/output_texts"

# Optional: Adjust OCR settings if you need higher accuracy
# For example, enable language detection for multilingual documents
# batch_engine.ocr_engine.language = "eng+spa"  # English + Spanish

# Step 5: Run the batch recognition – each supported image in the input folder is processed
batch_engine.recognize()

# Step 6: Notify that the batch operation has finished
print("Batch processing complete. Text files saved to YOUR_DIRECTORY/output_texts.")
```

### Как это работает

- **`BatchOcrEngine`** оборачивает обычный `OcrEngine`, добавляя оркестрацию на уровне папок — именно то, что нужно для **convert images to text python** в массовом режиме.  
- Свойство `input_folder` указывает движку, где искать исходные изображения. Он автоматически сканирует каталог и ставит в очередь каждый поддерживаемый тип файла.  
- Свойство `output_folder` определяет, куда сохранять каждый файл `.txt`. Движок сохраняет оригинальное имя файла, так что `receipt1.png` станет `receipt1.txt`.  
- Вызов `recognize()` запускает внутренний цикл, который загружает каждое изображение, выполняет OCR и записывает результат. Метод блокирует выполнение, пока не обработаются все файлы, что упрощает последующие действия (например, архивирование выходной папки).

#### Ожидаемый вывод

При запуске скрипта:

```bash
python batch_ocr.py
```

Вы увидите:

```
Batch processing complete. Text files saved to YOUR_DIRECTORY/output_texts.
```

В папке `output_texts` появится обычный текстовый файл для каждого изображения. Откройте любой из них в текстовом редакторе — вы увидите «сырой» результат OCR, обычно близкий к оригинальному печатному тексту.

## Шаг 4 – Проверка результатов и обработка ошибок

Даже лучший OCR‑движок может «споткнуться» на низкокачественных сканах или сильно искажённых страницах. Ниже простой способ проверить вывод и записать любые сбои.

```python
import os

def verify_output(output_dir):
    txt_files = [f for f in os.listdir(output_dir) if f.lower().endswith('.txt')]
    empty_files = [f for f in txt_files if os.path.getsize(os.path.join(output_dir, f)) == 0]

    if empty_files:
        print("Warning: The following files are empty – OCR may have failed:")
        for f in empty_files:
            print(f"  • {f}")
    else:
        print("All text files contain data. OCR succeeded for every image.")

# Run verification after batch processing
verify_output(batch_engine.output_folder)
```

**Зачем это нужно?**  
- Выявляет случаи, когда движок молча возвращает пустую строку (часто происходит с нечитаемыми изображениями).  
- Даёт список проблемных файлов, чтобы вы могли вручную проверить их или пере‑запустить с другими настройками (например, увеличить параметры `OcrEngine.preprocess`).  

### Пограничные случаи и настройки

| Ситуация | Предлагаемое решение |
|-----------|----------------------|
| Изображения повернуты на 90° | Установите `batch_engine.ocr_engine.rotation_correction = True`. |
| Несколько языков (английский + французский) | Перед `recognize()` задайте `batch_engine.ocr_engine.language = "eng+fra"`. |
| Большие PDF‑файлы, сначала преобразованные в изображения | Разбейте PDF на одностраничные изображения, затем передайте папку в batch‑engine. |
| Ошибки памяти при очень больших пакетах | Обрабатывайте меньшие подпапки последовательно или увеличьте `batch_engine.max_memory_usage`. |

## Шаг 5 – Автоматизация всего процесса (по желанию)

Если требуется выполнять конвертацию каждую ночь, оберните скрипт в простой shell‑скрипт или Windows‑batch файл и запланируйте его через `cron` (Linux/macOS) или Планировщик задач (Windows). Ниже минимальный `run_ocr.sh` для Unix‑подобных систем:

```bash
#!/usr/bin/env bash
# run_ocr.sh – Automate bulk image to text conversion

# Activate virtual environment
source /path/to/venv/bin/activate

# Execute the OCR script
python /path/to/ocr_project/batch_ocr.py

# Deactivate after completion
deactivate
```

Сделайте его исполняемым (`chmod +x run_ocr.sh`) и добавьте запись в cron:

```cron
0 2 * * * /path/to/run_ocr.sh >> /var/log/ocr_batch.log 2>&1
```

Это будет запускать конвертацию каждый день в 2 AM и сохранять любой вывод в лог для последующего анализа.

---

## Заключение

Теперь у вас есть проверенный, готовый к продакшну способ **convert images to text python** с использованием `BatchOcrEngine` из Aspose.OCR. Скрипт осуществляет **bulk image to text conversion**, аккуратно сохраняет каждый результат в отдельный файл и включает шаги проверки, чтобы убедиться, что вы действительно **recognize text from scanned images** корректно.

Дальше вы можете:

- Поэкспериментировать с различными настройками OCR (языковые пакеты, исправление наклона, подавление шума).  
- Передать сгенерированный текст в поисковый индекс, например Elasticsearch, для мгновенного полнотекстового поиска.  
- Скомбинировать этот конвейер с инструментами конвертации PDF, чтобы обрабатывать отсканированные PDF‑файлы за один проход.  

Есть вопросы или столкнулись с проблемой конкретного типа файла? Оставьте комментарий ниже, и мы разберёмся вместе. Приятного кодинга, и пусть ваши OCR‑запуски будут быстрыми и безошибочными!

## Что изучать дальше?

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}