---
category: general
date: 2026-06-25
description: Подготовьте изображение для OCR и распознайте текст из отсканированного
  документа с помощью Python. Пошаговое руководство с полным кодом.
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: ru
og_description: Подготовьте изображение для OCR и распознайте текст из отсканированного
  документа с помощью Python. Следуйте этому подробному, готовому к запуску руководству.
og_title: Предобработка изображения для OCR в Python – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Предобработка изображения для OCR в Python – Полное руководство
url: /ru/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Предобработка изображения для OCR в Python – Полное руководство

Когда‑нибудь задумывались, как **preprocess image for OCR** так, чтобы текст получался чистым и надёжным? Вы не одиноки — большинство разработчиков сталкиваются с той же проблемой, когда отсканированная страница наклонена или контраст сильно варьируется. Хорошая новость в том, что несколько строк кода на Python могут выпрямить этот беспорядок, бинаризовать изображение и вернуть вам чёткий, индексируемый текст.

В этом руководстве мы пройдём точные шаги, чтобы **preprocess image for OCR** *and* **recognize text from scanned document** файлы, используя популярную OCR‑библиотеку. К концу вы получите готовый к запуску скрипт, поймёте, почему каждый параметр важен, и узнаете, как настроить его для сложных граничных случаев.

## Что понадобится

- Python 3.8 или новее (код также работает на 3.10+)
- OCR‑пакет, предоставляющий классы `OcrEngine`, `ImagePreProcessingOptions` и `Image` (например, вымышленный модуль `ocr`, используемый в примере)
- Отсканированный или сфотографированный документ, слегка наклонённый или с низким контрастом
- Ваш любимый IDE или простой терминал — без тяжёлого GUI

Вот и всё. Никаких дополнительных бинарных файлов, без Docker‑трюков. Погрузимся.

## Предобработка изображения для OCR – Пошагово

Ниже представлен основной рабочий процесс, разбитый на пять чётких этапов. Каждый этап включает **why** мы это делаем, точный **code**, и короткое **explanation** того, что происходит под капотом.

### Шаг 1: Создать экземпляр OCR Engine

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Почему это важно:*  
`OcrEngine` объект — мозг операции. Он хранит конфигурацию, такую как языковые пакеты, пороги уверенности и — самое главное для нас — флаги предобработки изображения. Создание его в начале даёт нам чистый лист для включения последующих приёмов.

### Шаг 2: Включить автоматическое выравнивание и бинаризацию

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*Почему это важно:*  
- **Deskewing** вращает изображение так, чтобы строки текста стали горизонтальными. OCR‑движки сталкиваются с трудностями, когда базовая линия наклонена более чем на несколько градусов.  
- **Binarization** преобразует изображение в чисто чёрно‑белое, удаляя фоновой шум, который может сбивать с толку классификаторы символов.  
- Оба опции *automatic* во многих современных библиотеках, но их всё равно нужно включать — отсюда явное присваивание.

> **Pro tip:** Если ваши исходные изображения уже идеально выровнены, вы можете установить `auto_deskew=False`, чтобы сэкономить миллисекунду времени обработки.

### Шаг 3: Загрузить наклонённое изображение, которое нужно обработать

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*Почему это важно:*  
`Image.load` метод читает файл в память и оборачивает его в объект, понятный OCR‑движку. Он также извлекает метаданные, такие как DPI, которые могут влиять на коэффициент масштабирования по умолчанию для выравнивания.

> **Edge case:** Если изображение — многостраничный TIFF, вам придётся перебрать каждую страницу или использовать вспомогательный метод вроде `ocr.MultiPageImage.load`. Те же настройки предобработки применяются к каждой странице.

### Шаг 4: Выполнить OCR на предобработанном изображении

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*Почему это важно:*  
На этом этапе движок применяет шаги выравнивания и бинаризации, которые мы включили ранее, затем запускает свою нейронную сеть (или классический конвейер в стиле Tesseract) на очищенном битмапе. Возвращаемый объект `result` обычно содержит простой текст, оценки уверенности и иногда позиционные данные для каждого слова.

> **What if the text is still garbled?**  
Проверьте разрешение изображения: OCR работает лучше всего при 300 dpi или выше. Если ваш источник ниже, рассмотрите возможность увеличения масштаба перед загрузкой или запросите оригинальное сканирование у источника документа.

### Шаг 5: Вывести распознанный текст

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*Почему это важно:*  
`result.text` — это строковое представление всего, что движок смог прочитать. Вывод его на печать удобен для быстрой отладки; в реальном приложении вы, вероятно, запишете его в файл `.txt`, базу данных или передадите в последующий NLP‑конвейер.

---

## Распознавание текста из отсканированного документа – Выход за пределы базового

Теперь, когда базовый конвейер работает, давайте рассмотрим несколько распространённых вариантов, с которыми вы можете столкнуться, пытаясь **recognize text from scanned document** изображения в реальных условиях.

### 1. Обработка нескольких языков

Если ваш документ содержит как английский, так и французский, настройте движок перед шагом 1:

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

Большинство OCR‑движков принимают коды ISO‑639‑2; загрузка дополнительных языковых пакетов добавляет небольшие накладные расходы, но значительно повышает точность на многоязычных страницах.

### 2. Точная настройка порогов бинаризации

Автоматическая бинаризация работает в большинстве случаев, но некоторые старые ксерокопии требуют пользовательского порога:

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

Экспериментируйте со значениями от 120 до 220, пока фон не исчезнет, не стирая слабые символы.

### 3. Извлечение информации о макете

Иногда требуется больше, чем простой текст — вы хотите знать, где каждый абзац расположен на странице. Многие движки предоставляют коллекцию `result.blocks`:

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

Это бесценно для восстановления таблиц или сохранения порядка колонок.

### 4. Обработка пакета файлов

Если у вас есть папка, полная отсканированных PDF, преобразованных в JPEG, оберните весь процесс в цикл:

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

Цикл повторно использует один и тот же экземпляр `engine`, что эффективнее, чем создавать его заново для каждого файла.

### 5. Работа с низкоразрешёнными сканами

Низкоразрешённые изображения (< 150 dpi) часто дают размытые символы. Быстрое решение — увеличить масштаб с помощью высококачественного алгоритма перед передачей изображения OCR‑движку:

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

Увеличение масштаба не создаст детали волшебным образом, но шаг бинаризации может работать с более чёткими краями, обеспечивая небольшое улучшение.

---

## Ожидаемый вывод

Запуск оригинального пятишагового скрипта на умеренно наклонённом скане 300 dpi должен вывести что‑то вроде:

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

Если вы видите искажённые символы, дважды проверьте флаги предобработки, разрешение изображения и конфигурацию языка.

---

## Заключение

Мы рассмотрели всё, что вам нужно для **preprocess image for OCR** и **recognize text from scanned document** файлов с помощью Python. Начиная с нового экземпляра движка, мы включили автоматическое выравнивание и бинаризацию, загрузили наклонённое изображение, запустили распознавание и вывели чистый текст. По пути мы изучили поддержку нескольких языков, ручную настройку порогов, извлечение макета, пакетную обработку и обходные пути для низкого разрешения.

Попробуйте скрипт на своих сканах — возможно, стопку чеков, рукописную форму или старый газетный вырезка. Как только вы освоитесь, попробуйте добавить генерацию PDF или передать результат в поисковый индекс. Возможности безграничны.

**Ready for the next challenge?** Ознакомьтесь с нашими руководствами по *«Extract Tables from Scanned PDFs with Python»* и *«Train Custom OCR Models with TensorFlow»*, чтобы продолжать расширять ваш набор инструментов для автоматизации документов.

Счастливого кодинга, и пусть ваш OCR всегда будет чётким!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}