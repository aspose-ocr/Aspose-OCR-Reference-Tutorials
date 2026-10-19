---
category: general
date: 2026-04-29
description: Узнайте, как выполнять OCR на ваших сканах, автоматически использовать
  модель Hugging Face и распознавать текст со сканов с помощью Aspose OCR за считанные
  минуты.
draft: false
keywords:
- how to run OCR
- use hugging face model
- recognize text from scans
- download model automatically
language: ru
og_description: Как выполнять OCR на сканах с помощью Aspose OCR, автоматически загружать
  модель Hugging Face и получать чистый текст с пунктуацией.
og_title: Как запустить OCR с Aspose и Hugging Face – полное руководство
tags:
- OCR
- Aspose
- Hugging Face
- Python
title: Как запустить OCR с Aspose и Hugging Face — Полное руководство
url: /ru/python/general/how-to-run-ocr-with-aspose-hugging-face-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнить OCR с Aspose & Hugging Face – Полное руководство

Когда‑нибудь задавались вопросом **как выполнить OCR** на куче отсканированных документов, не тратя часы на настройку? Вы не одиноки. Во многих проектах разработчикам нужно **распознавать текст со сканов** быстро, но они сталкиваются с загрузкой моделей и пост‑обработкой.  

Хорошие новости: этот учебник показывает готовое к запуску решение, которое **использует модель Hugging Face**, автоматически загружает её и добавляет пунктуацию, чтобы вывод выглядел так, как будто его написал человек. К концу вы получите скрипт, который обрабатывает каждое изображение в папке и сохраняет чистый `.txt` файл рядом с каждым сканом.

## Что понадобится

- Python 3.8+ (код использует f‑строки, поэтому более старые версии не подойдут)
- `aspose-ocr` package (установите через `pip install aspose-ocr`)
- Доступ к Интернету для первой загрузки модели  
- Папка со сканами изображений (`.png`, `.jpg`, или `.tif`)

Вот и всё — никаких дополнительных бинарных файлов, никакой ручной настройки модели. Приступим.

![how to run OCR example](https://example.com/ocr-demo.png "how to run OCR example")

## Шаг 1: Импорт классов Aspose OCR и настройка окружения

Мы начинаем с импорта необходимых классов из библиотеки Aspose OCR. Импорт всего сразу делает скрипт аккуратным и упрощает поиск недостающих зависимостей.

```python
# Step 1: Import Aspose OCR classes
import os
from aspose.ocr import OcrEngine, AsposeAI, AsposeAIModelConfig
```

*Почему это важно*: `OcrEngine` выполняет основную работу, а `AsposeAI` позволяет подключить большую языковую модель для более умной пост‑обработки. Если пропустить импорт, остальная часть кода даже не скомпилируется — так что не забудьте его.

## Шаг 2: Настройка модели Hugging Face с поддержкой GPU  

Теперь мы указываем Aspose, откуда получать модель и сколько слоёв должно работать на GPU. Флаг `allow_auto_download="true"` отвечает за **автоматическую загрузку модели**.

```python
# Step 2: Configure a GPU‑aware AI model (replace with your own model folder)
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=40,                     # use GPU for faster inference
    directory_model_path=r"YOUR_DIRECTORY/models"
)
```

> **Совет**: Если у вас нет GPU, установите `gpu_layers=0`. Модель переключится на CPU, что медленнее, но всё равно будет работать.

### Почему выбирать модель Hugging Face?

Hugging Face предоставляет огромную коллекцию готовых к использованию LLM. Указывая `Qwen/Qwen2.5-3B-Instruct-GGUF`, вы получаете компактную модель, настроенную под инструкции, которая может добавлять пунктуацию, исправлять пробелы и даже устранять небольшие ошибки OCR. Это и есть суть **использования модели Hugging Face** на практике.

## Шаг 3: Инициализация AI‑движка и включение пост‑обработки пунктуации  

AI‑движок предназначен не только для продвинутого чата — здесь мы подключаем *добавление пунктуации*, которое очищает сырые результаты OCR.

```python
# Step 3: Initialise the AI engine and enable punctuation post‑processing
ai_engine = AsposeAI()
ai_engine.set_post_processor("punctuation_adder", {})
```

*Что происходит?* Вызов `set_post_processor` регистрирует встроенный пост‑процессор, который запускается после завершения работы OCR‑движка. Он берёт сырую строку и вставляет запятые, точки и заглавные буквы там, где это нужно, делая конечный текст гораздо более читаемым.

## Шаг 4: Создание OCR‑движка и привязка AI‑движка  

Подключение AI‑движка к OCR‑движку даёт нам один объект, который может как распознавать символы, так и улучшать результат.

```python
# Step 4: Create the OCR engine and attach the AI engine
ocr_engine = OcrEngine()
ocr_engine.set_ai_engine(ai_engine)
```

Если пропустить этот шаг, OCR всё равно будет работать, но вы потеряете улучшение пунктуации — поэтому вывод будет выглядеть как поток слов.

## Шаг 5: Обработка всех изображений в папке  

Это сердце учебника. Мы проходим по каждому изображению, запускаем OCR, применяем пост‑процессор и записываем очищенный текст в соседний файл `.txt`.

```python
# Step 5: Run OCR on each image in a folder, post‑process the result, and save the text
scans_folder = r"YOUR_DIRECTORY/scans"
for image_file in os.listdir(scans_folder):
    # Filter only supported image types
    if not image_file.lower().endswith(('.png', '.jpg', '.tif')):
        continue

    image_path = os.path.join(scans_folder, image_file)

    # Recognise text from the image
    ocr_result = ocr_engine.recognize(image_path)

    # Apply the punctuation post‑processor
    ocr_result = ocr_engine.run_postprocessor(ocr_result)

    # Show a brief confidence summary
    print(f"{image_file} – confidence {ocr_result.confidence:.2%}")

    # Save the cleaned text next to the source image
    txt_path = image_path + ".txt"
    with open(txt_path, "w", encoding="utf-8") as txt_file:
        txt_file.write(ocr_result.text)
```

### Что ожидать

Запуск скрипта выводит что‑то вроде:

```
invoice_001.png – confidence 96.73%
receipt_2024.tif – confidence 94.12%
```

Каждая строка показывает оценку уверенности (быстрая проверка состояния) и создаёт файлы `invoice_001.png.txt`, `receipt_2024.tif.txt` и т.д., содержащие пунктуацию и читаемый человеком текст.

### Особые случаи и варианты

- **Сканы не на английском**: Переключите `hugging_face_repo_id` на многоязычную модель (например, `microsoft/Multilingual-LLM-GGUF`).
- **Большие партии**: Оберните цикл в `concurrent.futures.ThreadPoolExecutor` для параллельной обработки, но учитывайте ограничения памяти GPU.
- **Пользовательская пост‑обработка**: Замените `"punctuation_adder"` своим скриптом, если нужна очистка, специфичная для домена (например, удаление номеров счетов).

## Шаг 6: Очистка ресурсов  

Когда задача завершается, освобождение ресурсов предотвращает утечки памяти, что особенно важно, если вы запускаете это в длительно работающем сервисе.

```python
# Step 6: Release resources
ai_engine.free_resources()
ocr_engine.dispose()
```

Пренебрежение этим шагом может оставить память GPU занятаой, что нарушит последующие запуски.

## Итоги: Как выполнить OCR от начала до конца  

Всего в нескольких строках мы продемонстрировали **как выполнить OCR** на папке со сканами, **использовать модель Hugging Face**, которая скачивается при первом запуске, и **распознавать текст со сканов** с автоматическим добавлением пунктуации. Полный скрипт готов к копированию, настройке ваших путей и запуску.

## Следующие шаги и связанные темы  

- **Пакетная пост‑обработка**: Изучите `ocr_engine.run_batch_postprocessor` для ещё более быстрой массовой обработки.  
- **Альтернативные модели**: Попробуйте семейство `openai/whisper`, если вам нужен speech‑to‑text вместе с OCR.  
- **Интеграция с базами данных**: Сохраняйте извлечённый текст в SQLite или Elasticsearch для поисковых архивов.  

Не стесняйтесь экспериментировать — меняйте модель, настраивайте `gpu_layers` или добавляйте свой пост‑процессор. Гибкость Aspose OCR в сочетании с модельным хабом Hugging Face делает это универсальной основой для любого проекта по оцифровке документов.

---

*Счастливого кодинга! Если возникнут проблемы, оставьте комментарий ниже или проверьте документацию Aspose OCR для более глубоких настроек.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}