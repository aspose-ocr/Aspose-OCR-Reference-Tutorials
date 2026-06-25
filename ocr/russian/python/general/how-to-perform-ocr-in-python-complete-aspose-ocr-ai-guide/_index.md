---
category: general
date: 2026-06-25
description: Узнайте, как выполнять OCR в Python, откройте лучший способ загрузки
  изображения для OCR и затем повысите точность с помощью постобработки Aspose AI.
draft: false
keywords:
- how to perform OCR
- load image for OCR
- Aspose OCR Python
- AI post‑processor OCR
- OCR accuracy improvement
- Python image processing OCR
language: ru
og_description: Как выполнить OCR в Python? Следуйте этому руководству, чтобы загрузить
  изображение для OCR, выполнить базовое распознавание и улучшить результаты с помощью
  постобработки Aspose AI.
og_title: Как выполнить OCR в Python — Полный учебник по Aspose OCR и ИИ
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  headline: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  type: TechArticle
- description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  name: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  steps:
  - name: Expected Output
    text: '``` === Raw OCR === Inv0ice #12345 Date: 2023-08-15 Total: $1,23O'
  - name: What if I don’t have a GPU?
    text: Set `model_config.gpu_layers = 0` and optionally increase `model_config.context_size`
      to 2048 for better CPU performance. The model will run slower, but you still
      get the same quality of correction.
  - name: My image is rotated—will `load_image` handle it?
    text: 'Aspose OCR automatically detects orientation, but for extremely skewed
      scans you may want to pre‑rotate using Pillow:'
  - name: How do I process multiple files in a folder?
    text: Wrap the whole pipeline in a `for` loop and store each `enhanced_text` in
      a list or write directly to a CSV. Remember to call `ocr_ai.free_resources()`
      **once** after the loop, not after each file—re‑initialising the model repeatedly
      is wasteful.
  - name: Can I swap the language model?
    text: Absolutely. Just change `model_config.hugging_face_repo_id` to any GGUF‑compatible
      model on Hugging Face (e.g., `Meta/Llama-3.2-1B-Instruct-GGUF`). Keep the quantization
      setting consistent with your hardware.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: Как выполнить OCR в Python — Полное руководство по Aspose OCR и ИИ
url: /ru/python/general/how-to-perform-ocr-in-python-complete-aspose-ocr-ai-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR в Python – Полное руководство Aspose OCR & AI

Когда‑нибудь задавались вопросом **как выполнять OCR** в Python без борьбы с низкоуровневыми трюками с изображениями? Вы не одиноки. В этом руководстве мы пройдем процесс загрузки изображения для OCR, выполнения простого извлечения текста, а затем полировки результата с помощью AI‑постпроцессора Aspose. К концу вы получите готовый скрипт, который превращает шумные сканы в чистый, индексируемый текст — без дополнительных сервисов.

Мы охватим всё: от установки SDK до освобождения ресурсов в длительно работающих приложениях. Если вы когда‑либо пытались **load image for OCR** и получали непонятный набор символов, это руководство — ваш антивирус. Вы увидите, почему сочетание традиционного OCR с языковой моделью дает результаты, будто их набрал человек.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

- Python 3.9 или новее (в коде используются подсказки типов, которые старые интерпретаторы не поддерживают)
- Действующая лицензия Aspose OCR или бесплатный пробный период (community edition подходит для оценки)
- GPU с минимум 4 ГБ VRAM, если хотите ускорить работу AI‑модели (опционально, но удобно)
- Пример изображения, например `sample_invoice.png`, размещённый в доступном месте

Если что‑то из этого вам незнакомо, не паникуйте — установка SDK делается одной командой, а настройки GPU можно отключить позже.

## Шаг 1: Установить Aspose OCR и зависимости

Откройте терминал и выполните:

```bash
pip install aspose-ocr
pip install aspose-ocr-ai
```

Первый пакет предоставляет `aspose.ocr`, второй добавляет утилиты AI‑постпроцессора. Оба — чистые Python‑колёса, компилировать ничего не придётся.

## Шаг 2: Загрузить изображение для OCR и инициализировать движок

Теперь мы **load image for OCR** с помощью `OcrEngine` от Aspose. Представьте, что вы передаёте лист бумаги очень внимательному клерку, который читает каждый символ.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Initialise the basic OCR engine
ocr_engine = aocr.OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

# Perform a plain OCR scan – this returns a raw string
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)
```

> **Почему это важно:** Вызов `load_image` — это мост между вашей файловой системой и OCR‑движком. Если путь указан неверно, вы получите `FileNotFoundError` ещё до начала распознавания. Всегда проверяйте разделители каталогов, особенно в Windows против macOS/Linux.

## Шаг 3: Настроить AI‑постпроцессор Aspose

Aspose AI может скачать языковую модель с Hugging Face, кэшировать её локально и выполнять вывод на вашем GPU (или CPU). Ниже мы конфигурируем лёгкую модель в 3 млрд параметров, которая помещается на большинстве современных ноутбуков.

```python
# Initialise the AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()

# Allow the SDK to fetch the model automatically
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"

# Use half of the GPU layers – balances speed and VRAM usage
model_config.gpu_layers = 20
model_config.context_size = 1024

# Load (or download) the model now
ocr_ai.initialize(model_config)
```

> **Подсказка:** Если у вас машина только с CPU, установите `gpu_layers = 0`. Модель всё равно будет работать, просто немного медленнее. Квантование `int8` сохраняет небольшую память, при этом почти не теряя точности модели.

## Шаг 4: Зарегистрировать пользовательский пост‑процессор

AI‑модели нужен запрос‑подсказка, которая объясняет, что делать. Здесь мы просим её вести себя как корректировщик OCR: исправлять орфографические ошибки, соединять разорванные слова и удалять артефакты.

```python
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    # Temperature 0.0 makes the output deterministic
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

# Hook the custom processor into the AI pipeline
ocr_ai.set_post_processor(correction_processor, custom_settings=None)
```

> **Почему пользовательский процессор?** Стандартный пост‑процессор может добавить лишние объяснения или форматирование, которое вам не нужно. Предоставив свою функцию, мы получаем строго очищенный текст — идеально для последующей индексации или хранения в базе данных.

## Шаг 5: Запустить OCR‑конвейер с AI‑улучшением

Теперь мы передаём «сырой» результат OCR в слой AI. Движок вызовет наш `correction_processor`, который, в свою очередь, общается с языковой моделью.

```python
# Apply the AI post‑processor to the raw OCR result
enhanced_text = ocr_ai.run_postprocessor(raw_text)

print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)
```

Вы заметите явное улучшение: недостающие символы восстанавливаются, типичные ошибки OCR вроде «0» vs «O» исправляются, а разрывы строк становятся более логичными.

## Шаг 6: Очистка — освобождение ресурсов

Если планируете запускать это в веб‑службе или длительно работающем демоне, освобождение памяти GPU критично. Забвение вызова `free_resources` может привести к крашам «out‑of‑memory» после нескольких сотен запросов.

```python
ocr_ai.free_resources()
```

Вот и всё — ваш полный OCR‑конвейер теперь готов к продакшену.

## Полный скрипт

Ниже представлен полностью рабочий пример. Скопируйте его в файл `ocr_with_ai.py`, поправьте путь к изображению и запустите `python ocr_with_ai.py`.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Step 1: Load image for OCR and perform basic recognition
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)

# Step 2: Initialise the Aspose AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"
model_config.gpu_layers = 20          # half of GPU layers
model_config.context_size = 1024
ocr_ai.initialize(model_config)

# Step 3: Register custom correction processor
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

ocr_ai.set_post_processor(correction_processor, custom_settings=None)

# Step 4: Run AI post‑processor on raw OCR output
enhanced_text = ocr_ai.run_postprocessor(raw_text)
print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)

# Step 5: Release resources (important for long‑running apps)
ocr_ai.free_resources()
```

### Ожидаемый вывод

```
=== Raw OCR ===
Inv0ice #12345
Date: 2023-08-15
Total: $1,23O

=== AI‑enhanced OCR ===
Invoice #12345
Date: 2023-08-15
Total: $1,230
```

Обратите внимание, как «Inv0ice» превращается в «Invoice», а лишняя «O» после суммы исчезает. Это магия AI.

## Часто задаваемые вопросы и особые случаи

### Что если у меня нет GPU?

Установите `model_config.gpu_layers = 0` и при желании увеличьте `model_config.context_size` до 2048 для лучшей производительности на CPU. Модель будет работать медленнее, но качество коррекции останется тем же.

### Моё изображение повернуто — справится ли `load_image`?

Aspose OCR автоматически определяет ориентацию, но для сильно искривлённых сканов может потребоваться предварительное вращение с помощью Pillow:

```python
from PIL import Image
img = Image.open("sample.png")
rotated = img.rotate(90, expand=True)
rotated.save("rotated.png")
ocr_engine.load_image("rotated.png")
```

### Как обработать несколько файлов в папке?

Обёрните весь конвейер в цикл `for` и сохраняйте каждый `enhanced_text` в список или сразу записывайте в CSV. Не забудьте вызвать `ocr_ai.free_resources()` **один раз** после завершения цикла, а не после каждого файла — повторная инициализация модели тратит ресурсы.

```python
import os

for filename in os.listdir("invoices"):
    if filename.lower().endswith(".png"):
        ocr_engine.load_image(os.path.join("invoices", filename))
        raw = ocr_engine.recognize()
        clean = ocr_ai.run_postprocessor(raw)
        # Save or index `clean`
```

### Могу ли я заменить языковую модель?

Конечно. Просто измените `model_config.hugging_face_repo_id` на любую совместимую с GGUF модель на Hugging Face (например, `Meta/Llama-3.2-1B-Instruct-GGUF`). Сохраняйте согласованность настроек квантования с вашим оборудованием.

## Профессиональные советы и подводные камни

- **Совет:** Установите `temperature=0.0` для детерминированных исправлений. Более высокие температуры могут приводить к креативным, но неверным изменениям.
- **Остерегайтесь:** Очень длинных документов (> 5000 символов). Окно контекста модели в примере ограничено 1024 токенами; разбивайте текст на абзацы перед отправкой в AI.
- **Замечание по безопасности:** Если вы работаете в регулируемой среде, убедитесь, что URL загрузки модели включён в белый список. Флаг `allow_auto_download` можно отключить.

## Что изучать дальше?

Следующие руководства охватывают смежные темы, расширяющие техники, продемонстрированные в этом гайде. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы вы могли освоить дополнительные возможности API и исследовать альтернативные подходы в своих проектах.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}