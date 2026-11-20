---
category: general
date: 2026-11-20
description: Выполните OCR изображения с помощью Aspose OCR, а затем извлеките текст
  из изображения, используя встроенный AI‑постпроцессор. Изучите полный рабочий процесс
  Python за несколько минут.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from image
language: ru
lastmod: 2026-11-20
og_description: Выполните OCR изображения с помощью Aspose OCR, затем извлеките текст
  из изображения с помощью AI‑постобработки. Следуйте этому пошаговому руководству
  на Python.
og_image_alt: Diagram showing how to perform OCR on image and extract text from image
  using Aspose
og_title: Выполнить OCR изображения и извлечь текст из него с помощью Aspose
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Perform OCR on image with Aspose OCR and then extract text from image
    using the built‑in AI post‑processor. Learn a complete Python workflow in minutes.
  headline: Perform OCR on image and extract text from image with Aspose
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI post‑processing
title: Выполнить OCR на изображении и извлечь текст из изображения с помощью Aspose
url: /ru/python/general/perform-ocr-on-image-and-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнить OCR на изображении и извлечь текст из изображения с помощью Aspose

Если вам нужно **выполнить OCR на изображении** в Python, это руководство покажет полное решение от начала до конца. Используя Aspose OCR вместе с пост‑процессором Aspose AI, вы можете надёжно **извлекать текст из изображения** и улучшать исходный результат OCR с помощью лёгкой языковой модели.

В этом учебнике вы:

* Настроите движок Aspose OCR.
* Выполните OCR для **извлечения текста из изображения**.
* При желании сконфигурируете AI‑модель для пост‑обработки.
* Зарегистрируете пользовательскую функцию пост‑обработки.
* Получите улучшенный текст и освободите ресурсы.

Эти шаги работают с любым растровым изображением (PNG, JPEG, BMP) и требуют только пакета `aspose-ocr`.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

| Требование | Почему это важно |
|------------|-------------------|
| Python 3.8+ | Требуется SDK Aspose. |
| pip‑пакет `aspose-ocr` | Предоставляет `AsposeOCR`, `AsposeAI` и классы конфигурации модели. |
| Файл изображения (например, `sample_image.png`) | Источник, на котором вы **выполните OCR на изображении**. |
| Необязательно: поддержка GPU | Если планируете запускать большую модель на GPU, задайте `gpu_layers` соответственно. |

Установите SDK с помощью:

```bash
pip install aspose-ocr
```

## Шаг 1: Выполнить OCR на изображении

Первая операция — прочитать изображение и получить необработанный текст. Это основной шаг **выполнения OCR на изображении**.

```python
from aspose.ocr import AsposeOCR

# Initialise the OCR engine
ocr_engine = AsposeOCR()

# Path to the image you want to process
image_path = "YOUR_DIRECTORY/sample_image.png"

# Execute OCR – this returns the plain text extracted from the image
raw_text = ocr_engine.recognize_image(image_path)

print("Raw OCR result:")
print(raw_text)
```

**Почему это работает:** `AsposeOCR.recognize_image` использует предобученную модель оптического распознавания символов, оптимизированную по скорости и точности для обычных шрифтов. Метод возвращает обычную строку Unicode, которая служит базой для любой дальнейшей обработки.

> **Полезный совет:** Если изображение содержит несколько языков, установите `ocr_engine.language = "eng+spa"` (или любой поддерживаемый код ISO‑639‑2) перед вызовом `recognize_image`.

## Шаг 2: Инициализировать AI‑пост‑процессор

Aspose AI предоставляет лёгкий слой пост‑обработки, который может исправлять ошибки OCR, поправлять пунктуацию или применять пользовательскую бизнес‑логику.

```python
from aspose.ocr import AsposeAI

# Initialise the AI post‑processor with default logging
ai_processor = AsposeAI()
```

**Зачем это нужно:** Сырой OCR часто ошибается в распознавании символов (например, “0” vs “O”). Шаг AI уточняет вывод, делая результат **извлечения текста из изображения** более надёжным для последующих задач, таких как индексирование или аналитика.

## Шаг 3: (Опционально) Настроить AI‑модель

Вы можете указать процессору конкретную модель Hugging Face, включить автоматическую загрузку или принудительно выполнить на CPU. Этот шаг необязателен, но полезен, когда требуется детерминированное поведение.

```python
from aspose.ocr import AsposeAIModelConfig

# Create a configuration object
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"          # Download model if missing
model_config.hugging_face_repo_id = "openai/gpt2"   # Small, fast model
model_config.gpu_layers = 0                        # Use CPU; set >0 for GPU

# Apply the configuration to the AI processor
ai_processor.configure(model_config)
```

**Пояснение:**  
* `allow_auto_download` избавляет от ручного управления моделями.  
* `hugging_face_repo_id` выбирает модель; `gpt2` — хороший компромисс между размером и качеством для исправления коротких текстов.  
* `gpu_layers` определяет, сколько слоёв трансформера будет работать на GPU; `0` принудительно использует только CPU, что безопасно на всех машинах.

## Шаг 4: Зарегистрировать пользовательскую функцию пост‑обработки

Aspose AI позволяет подключить любую вызываемую функцию, получающую сырую строку OCR и возвращающую преобразованную версию. Ниже простой пример, который переводит всё в верхний регистр.

```python
def my_post_processor(text):
    """
    Custom post‑processor that transforms the OCR result.
    Replace this logic with your own business rules.
    """
    return text.upper()

# Register the function with the AI processor
ai_processor.set_post_processor(my_post_processor, custom_settings=None)
```

**Когда кастомизировать:** Используйте пользовательскую функцию, если нужен доменно‑специфичный очистка, например удаление конфиденциальных идентификаторов, нормализация дат или исправления на основе регулярных выражений. AI‑модель будет запускаться *после* этой функции, позволяя комбинировать детерминированные правила с вероятностными улучшениями.

## Шаг 5: Улучшить результат OCR с помощью AI‑пост‑процессора

Теперь запустите полный конвейер: сырый текст OCR сначала проходит через вашу пользовательскую функцию, затем через AI‑модель, и в конце вы получаете уточнённый вывод.

```python
# Run the AI post‑processor on the raw OCR text
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("\nOriginal OCR :")
print(raw_text)
print("\nAI‑enhanced   :")
print(enhanced_text)
```

**Что вы должны увидеть:**  
Если оригинальное изображение содержало “Hello world”, консоль может вывести:

```
Original OCR :
Hello world

AI‑enhanced   :
HELLO WORLD
```

В реальном сценарии AI‑модель исправит опечатки, добавит недостающую пунктуацию или переоформит разрывы строк, предоставив более чистый результат **извлечения текста из изображения**, готовый к хранению или анализу.

## Шаг 6: Освободить ресурсы после завершения

И OCR‑движок, и AI‑пост‑процессор выделяют нативные ресурсы. Явное их освобождение предотвращает утечки памяти, особенно в длительно работающих сервисах.

```python
# Clean up native resources
ai_processor.free_resources()
```

Если вы также создали `ocr_engine` с тяжёлым бекендом, можно вызвать `ocr_engine.dispose()` (если доступно) аналогичным образом.

## Распространённые варианты и граничные случаи

| Ситуация | Рекомендуемая настройка |
|----------|--------------------------|
| **Большие PDF‑файлы с множеством страниц** | Циклически обрабатывать каждую страницу, вызывая `recognize_image` для каждой растровой страницы, и агрегировать результаты. |
| **Среда с поддержкой GPU** | Установите `model_config.gpu_layers` в количество слоёв, которые хотите запустить на GPU (например, `4`). Убедитесь, что драйверы CUDA установлены. |
| **Текст не на английском** | Измените `ocr_engine.language` на соответствующий код языка и, при необходимости, выберите языко‑специфичную модель Hugging Face. |
| **Очень шумные сканы** | Предобработайте изображение с помощью OpenCV (удаление шума, пороговая обработка) перед вызовом `recognize_image`. |
| **Необходимо сохранить оригинальный регистр** | Замените функцию `my_post_processor` на бездействующую или более тонкую правило вместо `text.upper()`. |

## Полный рабочий пример

Объединив всё вместе, получаем единый скрипт, готовый к запуску (замените `YOUR_DIRECTORY/sample_image.png` на ваш реальный путь к файлу):

```python
from aspose.ocr import AsposeOCR, AsposeAI, AsposeAIModelConfig

# 1️⃣ Perform OCR on image
ocr_engine = AsposeOCR()
image_path = "YOUR_DIRECTORY/sample_image.png"
raw_text = ocr_engine.recognize_image(image_path)

# 2️⃣ Initialise the AI post‑processor
ai_processor = AsposeAI()

# 3️⃣ (Optional) Configure the AI model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "openai/gpt2"
model_config.gpu_layers = 0            # CPU execution
ai_processor.configure(model_config)

# 4️⃣ Register a custom post‑processor (example: uppercase)
def my_post_processor(text):
    return text.upper()

ai_processor.set_post_processor(my_post_processor, custom_settings=None)

# 5️⃣ Enhance the OCR result
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("Original OCR :", raw_text)
print("AI‑enhanced   :", enhanced_text)

# 6️⃣ Release resources
ai_processor.free_resources()
```

Запуск этого скрипта выводит как сырый результат OCR, так и версию, улучшенную AI, демонстрируя, как можно **выполнять OCR на изображении** и надёжно **извлекать текст из изображения** в едином воспроизводимом рабочем процессе.

## Заключение

Теперь вы знаете, как **выполнять OCR на изображении** с помощью Aspose OCR, а затем **извлекать текст из изображения** используя встроенный AI‑пост‑процессор. В руководстве рассмотрены:

* Инициализация OCR‑движка.
* Выполнение OCR для получения сырого текста.
* (Опционально) настройка лёгкой модели Hugging Face.
* Добавление 

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Извлечение текста из изображения с Aspose OCR & AI – Полное пошаговое руководство](/ocr/english/python/general/extract-text-image-with-aspose-ocr-ai-full-step-by-step-guid/)
- [Как исправлять ошибки OCR – Извлечение текста из изображения с Aspose OCR – Пошаговое руководство](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Извлечение текста из изображения на Python – Полное руководство по Aspose OCR](/ocr/english/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}