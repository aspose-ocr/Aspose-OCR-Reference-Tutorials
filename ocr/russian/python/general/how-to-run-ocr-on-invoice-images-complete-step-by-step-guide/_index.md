---
category: general
date: 2026-01-12
description: Как выполнить OCR и извлечь текст из изображений счетов с помощью Aspose
  OCR и лёгкой модели Hugging Face. Узнайте, как скачать модель, исправить ошибки
  OCR и выполнить OCR на изображении.
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: ru
og_description: Как выполнять OCR на изображениях счетов, извлекать текст и исправлять
  ошибки с помощью LLM Hugging Face. Следуйте этому полному руководству для безупречных
  результатов.
og_title: Как выполнить OCR на изображениях счетов — полный учебник
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: Как выполнить OCR на изображениях счетов – полное пошаговое руководство
url: /ru/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнить OCR на изображениях счетов – Полное пошаговое руководство

Вы когда‑нибудь задумывались **how to run OCR** на отсканированном счете и получить чистый, индексируемый текст без траты часов на его очистку? Вы не одиноки. Во многих реальных проектах необработанный вывод OCR полон ошибок распознавания — например, “O” вместо “0”, “l” вместо “1”, или даже целые слова искажены. Хорошая новость? С несколькими строками кода на Python вы можете не только **perform OCR on image** файлы, но и автоматически **correct OCR errors**, используя лёгкую модель от Hugging Face.

В этом руководстве мы пройдем всё, что вам нужно знать: от загрузки изображения счета, извлечения необработанного текста, загрузки квантизированной модели, до полировки результата, чтобы получить идеальную транскрипцию, готовую к дальнейшей обработке. К концу вы сможете **extract text from invoice** PDF или PNG в едином, повторяемом скрипте.

## Требования и настройка

Before diving in, make sure you have:

| Требование | Зачем это нужно |
|-------------|----------------|
| Python 3.9+ | Современный синтаксис и подсказки типов |
| `aspose-ocr` package | Предоставляет `ocr.OcrEngine`, используемый в примере |
| `aspose-ai` package | Поставляет пост‑процессор `AsposeAI` |
| Access to a GPU (optional) | Ускоряет слои LLM; в противном случае CPU работает нормально |
| Internet connection (first run) | Необходима для автоматической **download Hugging Face model** |

Вы можете установить необходимые библиотеки с помощью:

```bash
pip install aspose-ocr aspose-ai
```

> **Pro tip:** Если вы планируете запускать LLM на GPU, установите `torch` с поддержкой CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

Теперь, когда окружение готово, давайте перейдём к коду.

---

## Шаг 1 – Инициализация OCR‑движка и загрузка изображения счета

Первое, что вам нужно сделать, — создать экземпляр OCR‑движка Aspose и указать ему файл, который вы хотите обработать. Этот шаг является основой **how to run OCR** на любом изображении.

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Why this matters:** `load_image` принимает PNG, JPEG, TIFF и даже страницы PDF, позволяя вам **perform OCR on image** данные независимо от формата.

---

## Шаг 2 – Выполнение базового OCR для получения необработанного текста

После загрузки изображения движок может создать необработанную транскрипцию. Этот вывод часто шумный, поэтому позже мы запустим шаг коррекции.

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

Типичный необработанный вывод может выглядеть так:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

Обратите внимание на нули (`0`) там, где должна быть буква “O”? Именно такие ошибки мы исправим позже.

---

## Шаг 3 – Настройка AI‑пост‑процессора с лёгкой LLM

Теперь мы подключаем **download Hugging Face model**, который достаточно мал для работы на скромном оборудовании, но достаточно мощный, чтобы понимать язык счетов. В примере используется модель Qwen 2.5 3B‑Instruct GGUF, квантизированная до `int8` для небольшого объёма памяти.

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **Why this model?** Квантизация `int8` уменьшает файл до ~1.2 GB, делая её пригодной для большинства ноутбуков. Слои GPU ускоряют инференс, но код плавно переходит на CPU, если GPU не найден.

---

## Шаг 4 – Запуск коррекции на основе LLM для необработанного результата OCR

Когда модель готова, мы передаём необработанный текст в пост‑процессор. LLM перепишет транскрипцию, исправляя распространённые ошибки OCR и нормализуя числа.

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

Ожидаемый очищенный вывод:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

Вы видите, что нули превратились обратно в букву “O”, а “Am0unt” теперь “Amount”. Это суть автоматической **correct OCR errors**.

---

## Шаг 5 – Освобождение ресурсов и очистка

Большие языковые модели могут удерживать память GPU, поэтому рекомендуется освобождать ресурсы после завершения.

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

Если вы планируете обрабатывать множество счетов пакетно, вы можете держать модель загруженной и освобождать её только в самом конце скрипта.

## Полный рабочий пример

Объединив всё вместе, вот единый скрипт, который вы можете поместить в файл `.py` и запустить:

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

Запуск скрипта должен вывести результат, похожий на блок «AI‑corrected», показанный ранее. Не стесняйтесь менять путь к изображению на любой другой счёт или чек, чтобы **extract text from invoice** файлы массово.

## Часто задаваемые вопросы и особые случаи

### Что если у меня нет GPU?

Параметр `gpu_layers` опционален. Установите его в `0` или опустите, и модель будет работать полностью на CPU. Ожидайте более медленного инференса — примерно 2–3 секунды на страницу на современном ноутбуке.

### Мои счета — многостраничные PDF. Как их обрабатывать?

Преобразуйте каждую страницу в отдельное изображение (например, с помощью `pdf2image`) и перебирайте страницы тем же скриптом. OCR‑движок может обрабатывать каждое изображение независимо, а LLM исправит каждый блок текста.

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### Загрузка модели не удаётся за файрволом?

Скачайте модель вручную с Hugging Face model hub, распакуйте её в локальную папку и укажите `hugging_face_repo_id` на локальный путь:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### Насколько точна коррекция?

Для типичных счетов на английском языке LLM исправляет >95 % распространённых ошибок OCR. Сложные рукописные заметки могут всё ещё требовать ручного просмотра.

## Советы и приёмы для продакшн‑использования

- **Batch processing:** Оберните шаги 2‑4 в функцию и передайте список путей к файлам. Переиспользуйте тот же экземпляр `AsposeAI`, чтобы избежать повторной загрузки модели.
- **Logging:** Замените `print` на модуль `logging` Python, чтобы фиксировать как необработанные, так и исправленные выводы для аудита.
- **Error handling:** Оберните вызов OCR в блоки `try/except`. Если изображение не удалось обработать, запишите имя файла в лог и продолжите.
- **Performance tuning:** Экспериментируйте с `gpu_layers`. Большее количество слоёв на GPU ускоряет инференс, но увеличивает использование VRAM.

## Заключение

Мы рассмотрели **how to run OCR** на изображениях счетов от начала до конца, показав, как **perform OCR on image**, **download Hugging Face model** и автоматически **correct OCR errors**. Полный скрипт демонстрирует практический рабочий процесс, который можно внедрить в любой Python‑основанный конвейер автоматизации.

Следующие шаги? Попробуйте расширить конвейер, чтобы **extract key fields** (номер счета, дата, итоговая сумма) с помощью регулярных выражений на исправленном тексте, или передать очищенный вывод в базу данных для поисковых записей. Вы также можете поэкспериментировать с другими лёгкими LLM от Hugging Face, если нужен другой язык или специфические доменные знания.

Удачной разработки, и пусть результаты вашего OCR всегда будут кристально чистыми!

![как выполнить OCR на изображении счета](ocr_invoice_example.png "как выполнить OCR на счете")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}