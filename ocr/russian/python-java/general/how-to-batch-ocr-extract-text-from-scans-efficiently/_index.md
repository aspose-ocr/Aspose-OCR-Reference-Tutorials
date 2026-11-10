---
category: general
date: 2026-04-26
description: Как пакетно выполнять OCR ваших документов и извлекать текст из сканов
  в Python. Узнайте пошаговую пакетную обработку с OcrEngine для вывода в формате
  JSON.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: ru
og_description: Как пакетно выполнять OCR ваших отсканированных файлов и извлекать
  текст из сканов в одном скрипте. Полный код, советы и обработка крайних случаев.
og_title: Как выполнять пакетное OCR – Быстрое руководство по Python
tags:
- OCR
- Python
- Automation
title: Как пакетно выполнять OCR – эффективно извлекать текст из сканов
url: /ru/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнить batch OCR – Извлечение текста из сканов эффективно

Когда‑нибудь задавались вопросом **how to batch OCR** гору отсканированных PDF‑файлов, не теряя рассудка? Вы не одиноки — разработчики постоянно спрашивают: *«Как можно extract text from scans за один раз?»* Хорошая новость в том, что несколько строк кода на Python могут превратить эту утомительную задачу в плавный, автоматизированный конвейер.

В этом руководстве мы пройдемся по полностью готовому к запуску решению, которое **extracts text from scans**, сохраняет результаты в формате JSON и предоставляет быструю проверку в конце. Никаких внешних сервисов, никакой магии — только чистый Python, класс `OcrEngine` и немного работы с папками.

## Что вы получите

- Полностью рабочий скрипт, который **batches OCR** любой папки с изображениями.
- Четкие объяснения *почему* каждая строка существует, а не только *что* она делает.
- Советы по работе с пустыми папками, не‑изображениями и большими пакетами.
- Способ проверить, что JSON‑вывод действительно содержит извлеченный текст.

### Предварительные требования (минимум)

| Требование | Почему это важно |
|-------------|----------------|
| Python 3.8+ | Современный синтаксис и подсказки типов |
| `OcrEngine` library (or a compatible wrapper) | Основная OCR‑функциональность |
| Каталог со сканированными изображениями (PNG, JPG, TIFF) | Входные данные |
| Права записи для папки вывода | Сохранение JSON‑результатов |

Если у вас уже всё есть, отлично — приступим.

![как выполнить batch OCR workflow](image-placeholder.png){alt="как выполнить batch OCR workflow"}

## Шаг 1 — Инициализация OCR‑движка (how to batch OCR)

Прежде чем мы сможем что‑либо обработать, нам нужен экземпляр OCR‑движка. Считайте его «мозгом», который будет читать каждое изображение и выдавать текст. Инициализировать его один раз и переиспользовать на протяжении всего пакета — самый эффективный подход.

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **Почему переиспользовать один и тот же экземпляр?**  
> Создание нового движка для каждого файла каждый раз загружало бы тяжёлые модели в память, резко замедляя пакетную обработку. Один экземпляр держит модель в ОЗУ и позволяет обрабатывать тысячи изображений без заметного замедления.

## Шаг 2 — Указать папку со сканами (extract text from scans)

Ваши сканы находятся где‑то на диске. Давайте укажем скрипту, где их искать. Использование абсолютных путей избавляет от неожиданностей «файл не найден», когда скрипт запускается из другой рабочей директории.

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **Совет:**  
> Если вы работаете в Windows, прямые слэши (`/`) работают без проблем с `os.path.abspath`, поэтому не нужно экранировать обратные слэши.

## Шаг 3 — Выбрать место для JSON‑результатов

Вероятно, вам понадобится аккуратная папка для OCR‑результатов. Хранение вывода отдельно от исходных данных упрощает последующую очистку или передачу JSON в другой конвейер.

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **Зачем создавать папку программно?**  
> Это гарантирует, что скрипт не упадёт, если директория отсутствует, а `exist_ok=True` делает операцию идемпотентной — скрипт можно запускать многократно без ошибок.

## Шаг 4 — Запуск пакетного процесса (how to batch OCR)

Теперь суть: указать `ocr_engine` пройтись по каждому файлу в `input_dir`, выполнить OCR и сохранить JSON в `output_dir`. Параметр `format="json"` сообщает движку сериализовать результат в структурированном виде, который любят последующие инструменты.

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### Что происходит под капотом?

1. **Поиск файлов** — Движок рекурсивно сканирует `input_folder`, игнорируя скрытые файлы.
2. **Проверка файлов** — На OCR‑модель подаются только поддерживаемые расширения изображений (`.png`, `.jpg`, `.tif` и т.д.).
3. **Выполнение OCR** — Каждое изображение отправляется в OCR‑движок; захватываются текст, оценки уверенности и данные о разметке.
4. **Сериализация в JSON** — Результат записывается в файл с тем же базовым именем, но с расширением `.json` в `output_folder`.

> **Обработка крайних случаев:**  
> - **Пустая папка:** Движок выводит в лог «No files found» и завершает работу без ошибок.  
> - **Повреждённое изображение:** Файл пропускается, ошибка записывается в `batch_errors.log`, и процесс продолжается.  
> - **Большой пакет (10k+ файлов):** Потребление памяти остаётся низким, поскольку каждое изображение обрабатывается независимо.

## Шаг 5 — Подтверждение завершения конвертации

Простое выражение `print` даёт мгновенную обратную связь в консоли. В продакшн‑конвейерах его можно заменить вызовом логгера или отправкой email‑уведомления.

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

Когда вы увидите эту строку, можно безопасно проверить папку `json_output`. Каждый JSON‑файл будет выглядеть примерно так:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

Теперь вы можете передать эти JSON‑файлы в базу данных, поисковый индекс или любой последующий аналитический инструмент.

## Часто задаваемые вопросы (и быстрые ответы)

**В: Что делать, если нужно обрабатывать PDF вместо изображений?**  
**О:** Сначала преобразуйте каждую страницу PDF в изображение (например, с помощью `pdf2image`) и поместите полученные PNG/JPG файлы в `input_dir`. Логика batch OCR остаётся без изменений.

**В: Можно ли изменить формат вывода на обычный текст?**  
**О:** Конечно. Замените `format="json"` на `format="txt"`, и движок запишет файл `.txt`, содержащий только извлечённый текст.

**В: Мои сканы находятся в нескольких подпапках — будет ли скрипт рекурсировать?**  
**О:** Да. `batch_process` по умолчанию проходит по дереву каталогов. Если нужен плоский вывод, установите `flatten=True` (если библиотека поддерживает) или пост‑обработайте имена JSON‑файлов.

**В: Как работать с нелатинскими скриптами?**  
**О:** Инициализируйте `OcrEngine` с параметром языка, например `OcrEngine(lang="spa+eng")`. Сам цикл batch не требует изменений.

## Профессиональные советы и распространённые подводные камни

- **Размер пакета имеет значение:** Если вы замечаете всплески нагрузки на CPU, ограничьте процесс простым `time.sleep(0.1)` между файлами.
- **Логирование:** Замените вызов `print` на модуль `logging` в Python, чтобы фиксировать метки времени и уровни ошибок.
- **Коллизии имён файлов:** Если два скана имеют одинаковое базовое имя, но находятся в разных подпапках, JSON‑файлы перезапишут друг друга. Добавьте хеш относительного пути к имени вывода, чтобы избежать этого.
- **Утечки памяти:** Некоторые OCR‑бэкенды удерживают нативные ресурсы. В конце скрипта вызовите `ocr_engine.close()`, если библиотека предоставляет метод очистки.

## Полный скрипт — готов к копированию и вставке

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**Ожидаемый вывод в консоль**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

Вы можете проверить JSON, открыв любой файл в `json_output` в текстовом редакторе или загрузив его в Python:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

Вы должны увидеть необработанный OCR‑извлечённый текст, напечатанный в консоли.

## Подведение итогов

Мы только что рассмотрели **how to batch OCR** целый каталог отсканированных изображений и **extract text from scans** в чистые, машинно‑читаемые JSON‑файлы. Подход преднамеренно прост: настроить движок один раз, указать папку и позволить библиотеке выполнить тяжёлую работу. Далее вы можете:

- Подключить JSON

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}