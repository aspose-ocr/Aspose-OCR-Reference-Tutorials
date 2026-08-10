---
category: general
date: 2026-06-28
description: Как выполнять пакетное OCR в Python — извлекать текст из изображений
  и преобразовывать отсканированные страницы в текст с помощью пакетной обработки
  OCR.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: ru
og_description: Узнайте, как выполнять пакетное OCR в Python, извлекать текст из изображений
  и преобразовывать отсканированные страницы в текст с помощью эффективной пакетной
  обработки OCR.
og_title: Как выполнять пакетное OCR в Python — пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Как выполнять пакетное OCR в Python – Полное руководство по извлечению текста
  из изображений
url: /ru/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять пакетное OCR в Python – Полное руководство по извлечению текста из изображений

Если вы задаётесь вопросом **как выполнять пакетное OCR в Python**, вы попали в нужное место. В этом руководстве показан быстрый способ **извлечения текста из изображений** и **преобразования отсканированных страниц в текст** с использованием одного экземпляра OCR‑движка. Больше не нужно копировать‑вставлять файл за файлом — позвольте коду выполнить тяжёлую работу.

Мы пройдёмся по всему, что вам нужно: установке библиотеки, загрузке целой папки сканов, запуску пакетной обработки OCR и аккуратному обработке результатов. К концу у вас будет переиспользуемый скрипт, который за секунды превратит набор PNG или JPEG в поисковые текстовые файлы.

## Что понадобится

* Python 3.9+ установлен (код также работает на 3.8, но 3.9+ предоставляет новейшие возможности типизации).
* Современная OCR‑библиотека — здесь мы используем **Aspose.OCR for Python via .NET**, которая предоставляет класс `OcrEngine`, показанный в оригинальном фрагменте.  
  ```bash
  pip install aspose-ocr
  ```
* Папка со сканированными страницами (`page1.png`, `page2.png`, …). Всё, что может открыть Pillow, подойдёт, так что PDF, TIFF или BMP тоже подходят.
* Небольшая доля любопытства — если вы никогда не автоматизировали преобразование изображения в текст, вы скоро увидите, почему пакетный OCR меняет правила игры.

> **Совет:** Если вы предпочитаете чисто‑Python библиотеку, замените `OcrEngine` на `pytesseract.image_to_string`. Вокруглогика остаётся идентичной.

## Как выполнять пакетное OCR в Python – Пошаговое руководство

Ниже представлен полный, исполняемый скрипт. Каждая строка прокомментирована, чтобы вы видели *почему* каждый элемент важен, а не только *что* он делает.

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### Ожидаемый вывод

Запуск скрипта для папки с тремя PNG‑сканами выдаст примерно следующее:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

Предпросмотр показывает первые 200 символов каждой страницы, а полный текст сохраняется в директории `ocr_output`.

## Извлечение текста из изображений с использованием одного движка

Зачем мы создаём **один** `OcrEngine` и переиспользуем его? Создание экземпляра может быть дорогим, так как загружает языковые пакеты и нативные DLL. Делая один экземпляр доступным для всей партии, вы:

* **Экономите память** — только один набор ресурсов находится в ОЗУ.
* **Увеличиваете скорость** — движок остаётся «разогретым», избегая повторных инициализаций.
* **Поддерживаете согласованность** — одинаковые настройки распознавания применяются к каждой странице, что важно, когда вы хотите **извлекать текст из изображений**, имеющих одинаковую разметку.

Если необходимо подправить распознавание (например, включить проверку орфографии или сменить язык), сделайте это *до* вызова `recognize_batch`. Все последующие страницы автоматически унаследуют эти настройки.

## Эффективное преобразование отсканированных страниц в текст

Суть задачи — **преобразовать отсканированные страницы в текст** — решается с помощью `engine.recognize_batch(images)`. Под капотом библиотека обрабатывает каждое изображение в пуле фоновых потоков, обеспечивая почти линейное масштабирование на многопроцессорных машинах. Несколько моментов, которые стоит помнить:

* **Качество изображения имеет значение** — 300 dpi и выше дают наилучшие результаты. Если ваши сканы низкого разрешения, рассмотрите увеличение разрешения с помощью Pillow перед передачей их движку.
* **Цвет vs. градации серого** — OCR‑движки обычно работают быстрее с 8‑битными изображениями в градациях серого. Вы можете добавить шаг предобработки:  
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **Поддержка языков** — Aspose.OCR поддерживает более 40 языков. Установите `engine.language = "eng"` или `"fra"` перед вызовом пакетной обработки, если вы работаете не с английским.

## Лучшие практики пакетной обработки OCR

Хотя приведённый выше код уже лаконичен, OCR‑пакет в продакшене часто требует дополнительных мер предосторожности:

| Проблема | Рекомендуемый подход |
|----------|----------------------|
| **Большие партии ( > 500 файлов )** | Разделите на блоки по 100–200 изображений, чтобы держать потребление памяти в умеренных пределах. |
| **Повреждённые или неподдерживаемые файлы** | Вспомогательная функция `load_images` уже перехватывает исключения и записывает предупреждение; вы также можете добавить обработку, чтобы пропускать или перемещать плохие файлы. |
| **Мониторинг прогресса** | Оберните `recognize_batch` в цикл, который возвращает управление после каждой картинки, если библиотека предоставляет обратные вызовы для каждой картинки. |
| **Постобработка** | Запустите проверку орфографии или очистку с помощью regex на полученных строках, чтобы улучшить последующий поиск. |
| **Параллелизм** | Если у вас многокластерная конфигурация, распределите папки между воркерами и объедините `.txt` файлы в конце. |

Эти советы помогут вам масштабировать **пакетную обработку OCR** от нескольких страниц до тысяч без сбоев скрипта.

## Часто задаваемые вопросы

**Q:** Можно ли использовать это напрямую с PDF?  
A: Конечно. Сначала преобразуйте каждую страницу PDF в изображение (например, с помощью `pdf2image`) и передайте полученный список в `recognize_batch`. Остальная часть конвейера остаётся без изменений.

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [Извлечение текста из изображения с Aspose OCR – Пошаговое руководство](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Извлечение текста из изображений с использованием OCR‑операции по папкам](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Как извлечь текст из ZIP‑архивов с помощью Aspose.OCR для .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}