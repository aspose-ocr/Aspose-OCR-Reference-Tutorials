---
category: general
date: 2026-07-05
description: Выполните OCR изображения с помощью Python. Узнайте, как преобразовать
  изображение в текст на Python, загрузить изображение для OCR и извлечь кириллический
  текст из изображения за несколько минут.
draft: false
keywords:
- perform OCR on image
- convert image to text python
- load image for OCR
- extract Cyrillic text from image
- recognize Cyrillic text
language: ru
og_description: Выполните OCR изображения в Python. Это руководство покажет, как преобразовать
  изображение в текст с помощью Python, загрузить изображение для OCR и быстро извлечь
  кириллический текст из изображения.
og_title: Выполнение OCR на изображении с помощью Python — Полный учебник
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Python. Learn how to convert image to text
    python, load image for OCR and extract Cyrillic text from image in minutes.
  headline: Perform OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Cyrillic
title: Распознавание текста на изображении с помощью Python — Полное пошаговое руководство
url: /ru/python/general/perform-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнить OCR на изображении с помощью Python – Полное пошаговое руководство

Когда‑нибудь задумывались, как **выполнять OCR на изображениях** без обращения к сторонним сервисам? Вы не одиноки. Во многих проектах — сканеры паспортов, цифровизаторы чеков или архивные инструменты — получение чистого текста из картинки является первой преградой.  

В этом руководстве мы пройдем практический пример, который **преобразует изображение в текст python**‑стиле, покажет, как **загрузить изображение для OCR**, и, наконец, **извлечь кириллический текст из изображения** с помощью открытой библиотеки `aocr`. К концу вы сможете **распознавать кириллический текст** на любой картинке, которую бросите в программу.

> **Что вы получите:** готовый к запуску скрипт, понятные объяснения каждого шага и советы по работе с типичными проблемами (размытие сканов, неожиданные шрифты). Без внешних API, только чистый Python.

---

## Требования

Прежде чем погрузиться в детали, убедитесь, что у вас есть:

- Python 3.8 или новее.
- Терминал или командная строка, с которыми вам удобно работать.
- Пакет `aocr` (устанавливается через `pip install aocr`).
- Файл изображения, содержащий кириллические символы (например, отсканированный российский паспорт).  

Если что‑то из этого звучит незнакомо, не паникуйте — каждый пункт будет кратко рассмотрен дальше.

---

## Шаг 1: Выполнить OCR на изображении – Настройка окружения

Первое, что нам нужно, — чистое Python‑окружение, где будет установлена OCR‑библиотека. Использование виртуального окружения изолирует зависимости и предотвращает конфликты версий.

```bash
# Create a virtual environment (optional but recommended)
python -m venv ocr-env
# Activate it (Windows)
ocr-env\Scripts\activate
# Activate it (macOS/Linux)
source ocr-env/bin/activate

# Install the aocr library
pip install aocr
```

**Зачем?**  
Отдельное окружение гарантирует, что пакет `aocr` и его нативные бинарники не будут мешать другим проектам. Это также упрощает воспроизводимость — кто‑то другой может клонировать ваш репозиторий и выполнить ту же команду `pip install -r requirements.txt`.

> **Pro tip:** Заморозьте зависимости с помощью `pip freeze > requirements.txt`, чтобы всегда знать, какие версии использовались.

---

## Шаг 2: Загрузить изображение для OCR – Импорт и подготовка файла

Теперь, когда библиотека готова, нам нужно **загрузить изображение для OCR**. Метод `aocr.Image.from_file` обрабатывает большинство распространённых форматов (PNG, JPEG, TIFF). Делается это так:

```python
import aocr

# Path to the Cyrillic image – replace with your actual file location
image_path = "YOUR_DIRECTORY/rus_passport.png"

# Load the image into an aocr.Image object
cyrillic_image = aocr.Image.from_file(image_path)
```

**Что происходит?**  
`aocr.Image.from_file` читает бинарные данные, декодирует их и сохраняет в объект, понятный OCR‑движку. Если файл не найден, Python выбросит `FileNotFoundError`, который можно перехватить позже для более мягкой обработки ошибок.

> **Edge case:** Некоторые сканеры выводят многостраничные TIFF‑файлы. В этом случае их нужно сначала разделить — `aocr` предоставляет `Image.from_tiff_pages()` для этой задачи.

---

## Шаг 3: Настроить OCR‑движок – Принудительное распознавание кириллицы

По умолчанию многие OCR‑движки пытаются угадать язык, что может привести к искажённому выводу для нелатинских скриптов. Чтобы **распознавать кириллический текст** надёжно, мы явно задаём язык «cyrillic».

```python
# Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Force the engine to use the Cyrillic recognizer
ocr_engine.language = "cyrillic"
```

**Зачем принудительно указывать язык?**  
Кириллические символы визуально похожи на латинские (например, «A» vs «А»). Указание движку ожидать кириллицу резко снижает количество ошибок, особенно на сканах низкого разрешения.

---

## Шаг 4: Выполнить OCR на изображении – Запуск распознавания

С загруженным изображением и настроенным движком мы, наконец, **выполняем OCR на изображении**. Метод `recognize` возвращает объект `OcrResult`, содержащий извлечённый текст и оценки уверенности.

```python
# Run the OCR process
ocr_result = ocr_engine.recognize(cyrillic_image)

# Print the raw text
print("Cyrillic text:")
print(ocr_result.text)
```

**Что даёт `ocr_result`?**  
- `text`: обычная строка распознанных символов.  
- `confidence`: число с плавающей точкой (0‑1), показывающее общую уверенность.  
- `lines`: список объектов строк, если нужен более детальный контроль.

> **Частый вопрос:** *Что делать, если текст перевёрнут?*  
> `aocr` умеет автоматически вращать изображения; просто установите `ocr_engine.auto_rotate = True` перед вызовом `recognize`.

---

## Шаг 5: Преобразовать изображение в текст python – Постобработка результата

Сырые строки могут содержать лишние пробелы или артефакты разрывов строк. Чтобы **преобразовать изображение в текст python**‑стиле, очистим их несколькими простыми шагами:

```python
import re

# Remove extra whitespace and normalize line breaks
clean_text = re.sub(r'\s+', ' ', ocr_result.text).strip()

print("\nCleaned Cyrillic text:")
print(clean_text)
```

**Зачем это нужно?**  
Очищенный вывод легче передавать в последующие конвейеры — будь то хранение в базе данных, отправка в API перевода или поиск регулярными выражениями номеров паспортов.

---

## Шаг 6: Извлечь кириллический текст из изображения – Собираем всё вместе

Соберём всё в одну переиспользуемую функцию. Это делает **извлечение кириллического текста из изображения** однострочным вызовом в ваших проектах.

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Loads an image, forces Cyrillic OCR, and returns cleaned text.
    """
    # Load image
    img = aocr.Image.from_file(image_path)

    # Configure OCR engine for Cyrillic
    engine = aocr.OcrEngine()
    engine.language = "cyrillic"

    # Recognize text
    result = engine.recognize(img)

    # Clean up the output
    cleaned = re.sub(r'\s+', ' ', result.text).strip()
    return cleaned

# Example usage
if __name__ == "__main__":
    path = "YOUR_DIRECTORY/rus_passport.png"
    print("Extracted text:", extract_cyrillic_text(path))
```

**Ожидаемый результат (пример):**

```
Extracted text: ПАСПОРТ РФ № 1234567890 ИМЯ ФАМИЛИЯ ДАТА РОЖДЕНИЯ 01.01.1990
```

Если изображение чёткое и шрифт соответствует модели OCR, вы получите почти идеальную транскрипцию.

---

## Устранение неполадок и советы

| Проблема | Возможная причина | Решение |
|----------|-------------------|---------|
| Искажённые символы | Неправильная настройка языка | Убедитесь, что `ocr_engine.language = "cyrillic"` |
| Пустой вывод | Слишком тёмное или низкокачественное изображение | Предобработайте с помощью `opencv`, увеличив контраст |
| Неправильная ориентация | Изображение повернуто на 90° | Установите `ocr_engine.auto_rotate = True` |
| Медленная работа | Большое изображение (>5 МП) | Перед распознаванием уменьшите размер через `aocr.Image.resize(width=1024)` |

---

![perform OCR on image example](ocr_example.png "perform OCR on image example")

*Alt text: “perform OCR on image example showing Python code extracting Cyrillic text from a passport scan.”*

---

## Заключение

Мы только что **выполнили OCR на изображениях** с помощью чистого Python, научились **загружать изображение для OCR**, принудительно заставили движок **распознавать кириллический текст** и, наконец, **извлекли кириллический текст из изображения** с помощью удобной вспомогательной функции. Весь конвейер — от установки `aocr` до очистки результата — умещается в несколько десятков строк кода и может быть внедрён в любой проект, которому нужно **преобразовать изображение в текст python**.

---

## Что дальше?

- **Пакетная обработка:** Перебирайте папку со сканами и сохраняйте результаты в SQLite.  
- **Определение языка:** Сочетайте `langdetect` с `aocr` для автоматического переключения между кириллицей и латиницей.  
- **Продвинутая предобработка:** Используйте `opencv` для исправления наклона, подавления шума или бинаризации изображений для повышения точности.  
- **Интеграция с FastAPI:** Откройте функцию `extract_cyrillic_text` как REST‑endpoint для веб‑приложений.

Экспериментируйте — поменяйте язык на «latin» для английских паспортов или попробуйте другой OCR‑бэкенд. Принципы остаются теми же, а код достаточно гибок, чтобы подстроиться.

Счастливого кодинга, и пусть ваши изображения всегда остаются читаемыми!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гиде. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Извлечь текст из изображения с помощью Aspose OCR – Пошаговое руководство](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Преобразовать изображение в текст – Выполнить OCR на изображении из URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Извлечение текста из изображения C# с выбором языка с помощью Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}