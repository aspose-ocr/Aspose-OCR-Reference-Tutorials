---
category: general
date: 2026-03-28
description: Узнайте, как выполнять OCR на изображении, автоматически загружать модель
  Hugging Face, очищать текст OCR и настраивать модель LLM в Python с использованием
  Aspose OCR Cloud.
draft: false
keywords:
- run OCR on image
- download hugging face model
- clean OCR text
- configure LLM model
language: ru
og_description: Запустите OCR на изображении и очистите вывод с помощью автоматически
  загруженной модели Hugging Face. Это руководство показывает, как настроить модель
  LLM в Python.
og_title: Запуск OCR на изображении – Полный учебник по Aspose OCR Cloud
tags:
- OCR
- Python
- LLM
- HuggingFace
title: Запуск OCR на изображении с помощью Aspose OCR Cloud – Полное пошаговое руководство
url: /ru/python/general/run-ocr-on-image-with-aspose-ocr-cloud-full-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Запуск OCR на изображении – Полный учебник Aspose OCR Cloud

Когда‑нибудь нужно было выполнить OCR на файлах изображений, но полученный результат выглядел как набор бессвязных символов? По моему опыту самая большая боль – не распознавание, а последующая очистка. К счастью, Aspose OCR Cloud позволяет подключить LLM‑постпроцессор, который может *автоматически очистить OCR‑текст*. В этом руководстве мы пройдем всё необходимое: от **загрузки модели с Hugging Face** до настройки LLM, запуска OCR‑движка и финальной полировки результата.

К концу этого руководства у вас будет готовый скрипт, который:

1. Загружает компактную модель Qwen 2.5 с Hugging Face (автоматически скачивается для вас).  
2. Настраивает модель так, чтобы часть сети работала на GPU, а остальное – на CPU.  
3. Выполняет OCR‑движок на изображении с рукописной заметкой.  
4. Использует LLM для очистки распознанного текста, получая человекочитаемый вывод.

> **Prerequisites** – Python 3.8+, пакет `asposeocrcloud`, GPU с минимум 4 ГБ видеопамяти (опционально, но рекомендуется) и интернет‑соединение для первой загрузки модели.

---

## Что вам понадобится

- **Aspose OCR Cloud SDK** – установить через `pip install asposeocrcloud`.  
- **Пример изображения** – например, `handwritten_note.jpg`, размещённый в локальной папке.  
- **Поддержка GPU** – если у вас есть CUDA‑совместимый GPU, скрипт выгрузит 30 слоёв; иначе он автоматически переключится на CPU.  
- **Разрешение на запись** – скрипт кэширует модель в `YOUR_DIRECTORY`; убедитесь, что папка существует.

---

## Шаг 1 – Настройка модели LLM (загрузка модели с Hugging Face)

Первое, что мы делаем, – сообщаем Aspose AI, откуда получать модель. Класс `AsposeAIModelConfig` отвечает за автоматическую загрузку, квантизацию и распределение слоёв по GPU.

```python
import asposeocrcloud as ocr
from asposeocrcloud.ai import AsposeAI, AsposeAIModelConfig

# ----------------------------------------------------------------------
# Step 1: Model configuration – this will download the model if it’s missing
# ----------------------------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                           # Enables auto‑download
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF", # Repo on Hugging Face
    hugging_face_quantization="int8",                     # Small footprint, fast inference
    gpu_layers=30,                                        # 30 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY"               # Cache folder (optional)
)
```

**Почему это важно** – квантизация до `int8` резко сокращает потребление памяти (≈ 4 ГБ против 12 ГБ). Разделение модели между GPU и CPU позволяет запускать LLM с 3‑миллиардами параметров даже на скромном RTX 3060. Если у вас нет GPU, задайте `gpu_layers=0`, и SDK оставит всё на CPU.

> **Tip:** При первом запуске будет скачано ~ 1,5 ГБ, поэтому выделите несколько минут и обеспечьте стабильное соединение.

---

## Шаг 2 – Инициализация AI‑движка с конфигурацией модели

Теперь мы поднимаем AI‑движок Aspose и передаём ему только что созданную конфигурацию.

```python
# ----------------------------------------------------------------------
# Step 2: Initialise the AI engine – pulls the model if needed
# ----------------------------------------------------------------------
ocr_ai = AsposeAI()
ocr_ai.initialize(model_config)  # This call blocks until the model is ready
```

**Что происходит за кулисами?** SDK проверяет `directory_model_path` на наличие уже загруженной модели. Если найдено соответствующее версии, она загружается мгновенно; иначе скачивается GGUF‑файл с Hugging Face, распаковывается и готовится конвейер вывода.

---

## Шаг 3 – Создание OCR‑движка и подключение AI‑постпроцессора

OCR‑движок выполняет тяжёлую работу по распознаванию символов. Подключив `ocr_ai.run_postprocessor`, мы автоматически включаем **очистку OCR‑текста** после распознавания.

```python
# ----------------------------------------------------------------------
# Step 3: Build the OCR engine and bind the LLM post‑processor
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=None)
```

**Зачем нужен пост‑процессор?** Сырой OCR часто содержит неверные разрывы строк, ошибочно распознанную пунктуацию или лишние символы. LLM может переписать вывод в правильные предложения, исправить орфографию и даже восстановить пропущенные слова – по сути превращая «мусор» в отшлифованный текст.

---

## Шаг 4 – Запуск OCR на файле изображения

Когда всё соединено, пришло время передать изображение в движок.

```python
# ----------------------------------------------------------------------
# Step 4: Load the image and run OCR
# ----------------------------------------------------------------------
input_image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")
raw_result = ocr_engine.recognize(input_image)   # Returns an OcrResult object
```

**Особый случай:** Если изображение большое (> 5 МП), имеет смысл сначала уменьшить его, чтобы ускорить обработку. SDK принимает объект Pillow `Image`, так что вы можете предварительно обработать его с помощью `PIL.Image.thumbnail()` при необходимости.

---

## Шаг 5 – Позвольте ИИ очистить распознанный текст и покажите обе версии

Наконец, вызываем ранее подключённый пост‑процессор. Этот шаг демонстрирует контраст между *до* и *после* очистки.

```python
# ----------------------------------------------------------------------
# Step 5: Clean the OCR output using the LLM and display both results
# ----------------------------------------------------------------------
cleaned_result = ocr_engine.run_postprocessor(raw_result)

print("=== Before AI ===")
print(raw_result.text)

print("\n=== After AI ===")
print(cleaned_result.text)
```

### Ожидаемый вывод

```
=== Before AI ===
Th1s 1s a h@ndwr1tt3n n0te.  It c0nta1ns m1st@k3s, l1n3 br3aks, & sp3c!@l ch@r@ct3rs.

=== After AI ===
This is a handwritten note. It contains mistakes, line breaks, and special characters.
```

Обратите внимание, как LLM:

- Исправил типичные ошибки OCR (`Th1s` → `This`).  
- Удалил лишние символы (`&` → `and`).  
- Привёл разрывы строк к корректным предложениям.

---

## 🎨 Визуальный обзор (рабочий процесс «Run OCR on image»)

![Запуск OCR на изображении workflow](run_ocr_on_image_workflow.png "Диаграмма, показывающая конвейер запуска OCR на изображении от загрузки модели до очищенного вывода")

Диаграмма выше суммирует весь конвейер: **загрузка модели с Hugging Face → настройка LLM → инициализация AI → OCR‑движок → AI‑постпроцессор → очистка OCR‑текста**.

---

## Часто задаваемые вопросы и профессиональные советы

### Что делать, если нет GPU?

Установите `gpu_layers=0` в `AsposeAIModelConfig`. Модель будет полностью работать на CPU, что медленнее, но всё равно функционально. Вы также можете переключиться на более маленькую модель (например, `Qwen/Qwen2.5-1.5B‑Instruct‑GGUF`), чтобы время вывода оставалось приемлемым.

### Как изменить модель позже?

Просто обновите `hugging_face_repo_id` и заново выполните `ocr_ai.initialize(model_config)`. SDK обнаружит изменение версии, скачает новую модель и заменит кэшированные файлы.

### Можно ли настроить подсказку (prompt) пост‑процессора?

Да. Передайте словарь в `custom_settings` с ключом `prompt_template`. Например:

```python
custom_prompt = {
    "prompt_template": "Correct the following OCR text and keep line breaks:\n{ocr_text}"
}
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=custom_prompt)
```

### Стоит ли сохранять очищенный текст в файл?

Определённо. После очистки вы можете записать результат в файл `.txt` или `.json` для дальнейшей обработки:

```python
with open("cleaned_note.txt", "w", encoding="utf-8") as f:
    f.write(cleaned_result.text)
```

---

## Заключение

Мы показали, как **запустить OCR на изображении** с помощью Aspose OCR Cloud, автоматически **скачать модель с Hugging Face**, профессионально **настроить параметры модели LLM** и, наконец, **очистить OCR‑текст** с помощью мощного LLM‑постпроцессора. Весь процесс укладывается в один простой Python‑скрипт и работает как на GPU‑окружениях, так и на машинах без видеокарты.

Если вам комфортно с этим конвейером, попробуйте поэкспериментировать с:

- **Различными LLM** – например, `meta-llama/Meta-Llama-3-8B‑Instruct‑GGUF` для более широкого контекстного окна.  
- **Пакетной обработкой** – пройдитесь по папке изображений и соберите очищенные результаты в CSV.  
- **Пользовательскими подсказками** – адаптируйте ИИ под вашу область (юридические документы, медицинские записи и т.д.).

Не бойтесь менять значение `gpu_layers`, заменять модель или подключать собственную подсказку. Возможности безграничны, а полученный код – это ваша стартовая площадка.

Счастливого кодинга, и пусть ваши OCR‑результаты всегда будут чистыми! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}