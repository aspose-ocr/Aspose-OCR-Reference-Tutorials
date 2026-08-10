---
category: general
date: 2026-06-19
description: Узнайте, как выполнять OCR изображения с помощью Aspose OCR и AI‑постпроцессора
  в Python. Включает автоматически загружаемую модель, проверку орфографии и ускорение
  на GPU.
draft: false
keywords:
- perform OCR on image
- Aspose OCR Python
- AI post‑processor
- auto‑downloaded model
- spellcheck post‑processor
- GPU acceleration
language: ru
og_description: выполнить OCR изображения с использованием Aspose OCR и AI‑постпроцессора.
  Пошаговое руководство с автоматически загружаемой моделью, проверкой орфографии
  и ускорением на GPU.
og_title: Выполнить OCR на изображении — Полный учебник по Python
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  headline: perform OCR on image with Aspose AI – Full Python Guide
  type: TechArticle
- description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  name: perform OCR on image with Aspose AI – Full Python Guide
  steps:
  - name: Initializes the Aspose OCR engine and loads a sample invoice image.
    text: Initializes the Aspose OCR engine and loads a sample invoice image.
  - name: Runs a basic OCR pass and prints the raw text.
    text: Runs a basic OCR pass and prints the raw text.
  - name: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
    text: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
  - name: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
    text: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
  - name: Releases all resources cleanly.
    text: Releases all resources cleanly.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: Выполнить OCR изображения с помощью Aspose AI – Полное руководство по Python
url: /ru/python/general/perform-ocr-on-image-with-aspose-ai-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# выполнить OCR на изображении – Полный учебник Python

Когда‑нибудь задумывались, как **выполнить OCR на изображении** без борьбы с десятками библиотек? По моему опыту основной болевой пункт — это управление «сырой» OCR‑движком, а затем попытки очистить шумный вывод. К счастью, Aspose OCR для Python в паре с AI‑постпроцессором делает весь конвейер простым.

В этом руководстве мы пройдем практический, сквозной пример, который покажет, как **выполнить OCR на изображении**, повысить точность с помощью автоматически загружаемой модели, включить проверку орфографии и даже воспользоваться ускорением GPU, если оно доступно. К концу вы получите переиспользуемый скрипт, который можно вставить в любой проект по сканированию счетов, чеков или оцифровке документов.

## Что вы построите

Мы создадим небольшую программу на Python, которая:

1. Инициализирует движок Aspose OCR и загружает пример изображения счета.  
2. Выполняет базовый проход OCR и выводит необработанный текст.  
3. Конфигурирует **Aspose AI** с **автоматически загружаемой моделью** с Hugging Face.  
4. Запускает **AI‑постпроцессор** (включая **постпроцессор проверки орфографии**) для очистки вывода OCR.  
5. Аккуратно освобождает все ресурсы.

Никаких внешних сервисов, никаких API‑ключей — только несколько строк кода Python и мощь Aspose.

> **Совет профессионала:** Если у вас есть машина с достойным GPU, установка `gpu_layers` может сэкономить секунды на этапе пост‑обработки.

## Необходимые условия

- Python 3.8 или новее (в коде используются подсказки типов, но они необязательны).  
- Пакеты `aspose-ocr` и `aspose-ai`, установленные через `pip`.  
  ```bash
  pip install aspose-ocr aspose-ai
  ```  
- Пример изображения (PNG, JPG или TIFF), размещённый там, где вы сможете сослаться, например, `sample_invoice.png`.  
- (Опционально) GPU с поддержкой CUDA и соответствующие драйверы, если вы хотите **ускорение GPU**.

Теперь, когда подготовка завершена, давайте погрузимся в код.

![пример выполнения OCR на изображении](image.png)

## выполнить OCR на изображении – Шаг 1: Инициализация OCR‑движка и загрузка изображения

Первое, что нам нужно, — это экземпляр OCR‑движка. Aspose OCR предлагает чистый, объектно‑ориентированный API, который абстрагирует низкоуровневую предобработку изображений.

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()
ocr_engine.Language = "en"                     # English; change as needed

# Load the image you want to analyse
ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")
```

**Почему это важно:**  
Установка языка заранее сообщает движку, какой набор символов ожидать, что может улучшить скорость распознавания и точность. Если вы работаете с многоязычными документами, просто замените `"en"` на `"fr"` или `"de"` по необходимости.

## Шаг 2: Выполнить базовый OCR и посмотреть необработанный текст

Теперь мы действительно запускаем распознавание. Объект результата содержит необработанный текст, оценки уверенности и даже ограничивающие рамки, если они вам понадобятся позже.

```python
# Run OCR
ocr_result = ocr_engine.Recognize()

# Show the unprocessed output
print("Raw OCR output:")
print(ocr_result.Text)
```

Типичный вывод может выглядеть так (обратите внимание на случайные ошибочные символы):

```
Raw OCR output:
Inv0ice N0: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00
```

Вы видите нули (`0`) там, где движок принял их за букву «O». Именно здесь проявляется сила **AI‑постпроцессора**.

## Настройка Aspose AI – автоматически загружаемая модель и проверка орфографии

Прежде чем передать необработанный результат OCR слою AI, нам нужно указать Aspose AI, какую модель использовать. Библиотека может автоматически загрузить модель с Hugging Face, так что вам не придётся вручную управлять большими `.bin`‑файлами.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

# Create a model configuration that auto‑downloads the Qwen2.5‑3B‑Instruct model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"   # reduces RAM usage
model_config.gpu_layers = 20                      # use GPU if available

# Initialise the AI engine with the config
ai_engine = AsposeAI(model_config)

# Enable the built‑in spellcheck post‑processor
ai_engine.set_post_processor("spellcheck", None)
```

**Пояснение настроек**

| Настройка | Что делает | Когда менять |
|-----------|------------|--------------|
| `allow_auto_download` | Позволяет Aspose автоматически загрузить модель при первом запуске. | Оставляйте `true`, если только не скачали модель заранее для офлайн‑использования. |
| `hugging_face_repo_id` | Идентификатор модели на Hugging Face. | Замените, если нужен доменно‑специфический вариант. |
| `hugging_face_quantization` | Выбирает уровень квантизации (`int8`, `float16` и т.д.). | Используйте `int8` в средах с ограниченной памятью; `float16` — для более высокой точности. |
| `gpu_layers` | Количество слоёв трансформера, исполняемых на GPU. | Установите `0` для работы только на CPU или значение до общего количества слоёв модели (20 для Qwen2.5‑3B). |

## Запуск AI‑постпроцессора над результатом OCR

Когда движок готов, мы просто передаём необработанный вывод OCR в AI‑конвейер. Встроенный **постпроцессор проверки орфографии** исправит очевидные опечатки, а языковая модель может переформулировать или дополнить недостающую информацию, если позже вы включите дополнительные процессоры.

```python
# Enhance the OCR result using the AI post‑processor
enhanced_result = ai_engine.run_postprocessor(ocr_result)

# Display the cleaned‑up text
print("\nAI‑enhanced OCR output:")
print(enhanced_result.Text)
```

Ожидаемый вывод после шага проверки орфографии:

```
AI‑enhanced OCR output:
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

Обратите внимание, как нули заменились на правильные буквы, а ошибочное «Am0unt» превратилось в «Amount». **AI‑постпроцессор** работает, отправляя необработанный текст через выбранную модель, которая возвращает уточнённую версию на основе своего обучения.

### Пограничные случаи и советы

- **Низкое разрешение изображений**: Если OCR‑движок справляется плохо, попробуйте сначала увеличить изображение (`Pillow` может помочь) или увеличить `ocr_engine.ImagePreprocessingOptions`.  
- **Нелатинские скрипты**: Измените `ocr_engine.Language` на соответствующий ISO‑код (`"zh"` для китайского, `"ar"` для арабского).  
- **GPU не обнаружен**: Настройка `gpu_layers` автоматически переходит на CPU, если совместимый GPU не найден, так что дополнительная обработка ошибок не требуется.  
- **Ограничения размера модели**: Модель Qwen2.5‑3B занимает ~4 ГБ в сжатом виде; убедитесь, что на диске достаточно места для автоматической загрузки.

## Освобождение ресурсов – чистое завершение

Объекты Aspose держат нативные дескрипторы, поэтому рекомендуется освобождать их после завершения работы. Это предотвращает утечки памяти, особенно в длительно работающих сервисах.

```python
# Free AI resources
ai_engine.free_resources()

# Dispose of the OCR engine
ocr_engine.Dispose()
```

Вы можете обернуть весь скрипт в блок `try…finally`, если предпочитаете явную очистку.

## Полный скрипт – готов к копированию

Ниже представлен весь код программы, готовый к запуску после замены `YOUR_DIRECTORY` на путь к вашему изображению.

```python
# -*- coding: utf-8 -*-
"""
Full example: perform OCR on image using Aspose OCR + AI post‑processor.
Author: Your Name
Date: 2026‑06‑19
"""

from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = OcrEngine()
    ocr_engine.Language = "en"
    ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Basic OCR
    ocr_result = ocr_engine.Recognize()
    print("Raw OCR output:")
    print(ocr_result.Text)

    # 3️⃣ Configure Aspose AI with auto‑downloaded model
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "int8"
    model_cfg.gpu_layers = 20   # GPU acceleration if available

    ai_engine = AsposeAI(model_cfg)
    ai_engine.set_post_processor("spellcheck", None)   # enable spellcheck

    # 4️⃣ AI post‑processing
    enhanced = ai_engine.run_postprocessor(ocr_result)
    print("\nAI‑enhanced OCR output:")
    print(enhanced.Text)

    # 5️⃣ Clean up
    ai_engine.free_resources()
    ocr_engine.Dispose()

if __name__ == "__main__":
    main()
```

Запустите его с помощью:

```bash
python perform_ocr_on_image.py
```

Вы должны увидеть необработанный и очищенный вывод, напечатанный в консоли.

## Заключение


## Что изучать дальше?


Следующие учебники охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Извлечение текста из изображения с Aspose OCR – Пошаговое руководство](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Извлечение текста из изображения C# с выбором языка с помощью Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Преобразование изображения в текст – Выполнение OCR на изображении по URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}