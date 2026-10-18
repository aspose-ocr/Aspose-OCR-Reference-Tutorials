---
category: general
date: 2026-06-25
description: Выполните OCR PDF с помощью Python — узнайте, как загрузить PDF для OCR,
  извлечь текст со страниц PDF и эффективно просмотреть распознанный текст.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF pages
- load PDF for OCR
- how to OCR large PDF
- preview recognized text
language: ru
og_description: Выполните OCR PDF в Python. Это руководство показывает, как загрузить
  PDF для OCR, извлечь текст со страниц PDF и быстро просмотреть распознанный текст.
og_title: Выполните OCR PDF с помощью Python – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  headline: Perform OCR on PDF with Python – Complete Guide
  type: TechArticle
- description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  name: Perform OCR on PDF with Python – Complete Guide
  steps:
  - name: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
    text: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
  - name: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
    text: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
  - name: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
    text: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
  - name: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
    text: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Выполнить OCR в PDF с помощью Python – Полное руководство
url: /ru/python/general/perform-ocr-on-pdf-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнить OCR на PDF с помощью Python – Полное руководство

Когда‑нибудь нужно было **выполнить OCR на PDF**‑файлах, но вы не знали, с чего начать? Возможно, у вас горы отсканированных контрактов или один тяжёлый справочник, который отказывается работать с вашим обычным извлечением текста. Короче, вы хотите **загрузить PDF для OCR**, вытащить текст и получить быстрый предварительный просмотр — всё без того, чтобы перегрузить память вашего компьютера.

Вы попали в нужное место. В этом руководстве мы пройдёмся по полностью рабочему скрипту на Python, который **извлекает текст со страниц PDF**, показывает, как **просмотреть распознанный текст**, и даже решает классическую проблему **как выполнять OCR больших PDF**‑файлов эффективно.

К концу вы получите готовую к запуску программу, чёткое понимание каждой настройки и несколько советов, как избежать типичных ошибок, в которые попадают новички.

---

## Что вы узнаете

- Как **загрузить PDF для OCR** с помощью библиотеки `aocr`.
- Точные шаги для **выполнения OCR на PDF**‑страницах по одной.
- Способы **извлечения текста из PDF‑страниц**, контролируя использование памяти.
- Как **просмотреть распознанный текст** для проверки результатов.
- Стратегии обработки **больших PDF** без исчерпания ОЗУ.

> **Подсказка:** В этом руководстве предполагается, что у вас установлен Python 3.9+ и базовое знакомство с виртуальными окружениями. Если вы новичок в Python, сначала создайте virtualenv — поверьте, это спасёт от головной боли позже.

---

## Предварительные требования

| Требование | Почему это важно |
|------------|------------------|
| Пакет Python `aocr` (или любой совместимый OCR‑движок) | Предоставляет класс `OcrEngine`, используемый в скрипте. |
| `pip` и виртуальное окружение | Позволяют изолировать зависимости от системного Python. |
| Достаточно места на диске для временных изображений | Некоторые OCR‑движки записывают изображения страниц на диск перед обработкой. |
| Необязательно: `tqdm` для индикаторов прогресса | Улучшает UX при работе с **как выполнять OCR больших PDF** задачами. |

Установите необходимые пакеты:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate
pip install aocr tqdm
```

Если ваш PDF защищён паролем, позже понадобится передать пароль — см. раздел «Особые случаи».

---

## Шаг 1: Выполнить OCR на PDF — Создание движка

Прежде всего нам нужен экземпляр OCR‑движка. Представьте его как мозг, который будет читать изображение каждой страницы и выдавать обычный текст.

```python
import aocr                     # The OCR library
from tqdm import tqdm           # Optional, for a nice progress bar

def create_engine():
    """
    Initialise the OcrEngine with sensible defaults.
    Returns the configured engine ready for processing.
    """
    engine = aocr.OcrEngine()
    # Limit memory usage – crucial when tackling how to OCR large PDF files
    engine.max_memory_mb = 200               # 200 MB cap, adjust if needed
    # Choose a recognition mode that matches your source material
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine
```

> **Зачем задавать `max_memory_mb`?**  
> OCR‑движки часто кэшируют изображения страниц в ОЗУ. Ограничивая память, вы предотвращаете падение скрипта на 500‑страничном контракте.

---

## Шаг 2: Загрузить PDF для OCR и настроить параметры

Теперь мы действительно **загружаем PDF для OCR**. Путь может быть абсолютным или относительным; просто убедитесь, что файл существует.

```python
def load_pdf(engine, pdf_path):
    """
    Loads the PDF into the OCR engine.
    Raises FileNotFoundError if the file does not exist.
    """
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages ready.")
    except Exception as e:
        raise RuntimeError(f"Failed to load PDF: {e}")
```

Если PDF зашифрован, `engine.load_pdf` обычно бросит исключение. В этом случае можно вызвать `engine.load_pdf(pdf_path, password="secret")` — подробнее ниже.

---

## Шаг 3: Извлечь текст из PDF‑страниц — Основной цикл

Здесь мы **выполняем OCR на PDF** постранично. Мы также **просматриваем распознанный текст** для первых нескольких сотен символов, чтобы вы могли убедиться, что всё работает.

```python
def ocr_pages(engine, preview_len=200):
    """
    Iterates over each page, runs OCR, and yields the recognized text.
    Also prints a short preview for each page.
    """
    for page_index in tqdm(range(engine.page_count), desc="Processing pages"):
        # Select the current page – essential for multi‑page PDFs
        engine.select_page(page_index)

        # Perform the actual OCR
        page_text = engine.recognize()

        # Preview the first `preview_len` characters (helps with debugging)
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))

        yield page_text
```

> **Профессиональный совет:** Индикатор прогресса `tqdm` даёт визуальную подсказку, особенно полезную при работе с **как выполнять OCR больших PDF** документами, обработка которых занимает минуты.

---

## Шаг 4: Собираем всё вместе — Готовый к запуску скрипт

Ниже полный, готовый к исполнению пример. Сохраните его как `pdf_ocr.py` и запустите командой `python pdf_ocr.py path/to/your/file.pdf`.

```python
#!/usr/bin/env python3
"""
Complete script to perform OCR on PDF, extract text from PDF pages,
and preview recognized text. Works for both small and large PDFs.
"""

import sys
import aocr
from tqdm import tqdm

def create_engine():
    engine = aocr.OcrEngine()
    engine.max_memory_mb = 200
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine

def load_pdf(engine, pdf_path):
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages.")
    except Exception as exc:
        raise RuntimeError(f"Unable to load PDF: {exc}")

def ocr_pages(engine, preview_len=200):
    for page_index in tqdm(range(engine.page_count), desc="OCR progress"):
        engine.select_page(page_index)
        page_text = engine.recognize()
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))
        yield page_text

def main(pdf_path):
    engine = create_engine()
    load_pdf(engine, pdf_path)

    all_text = []
    for txt in ocr_pages(engine):
        all_text.append(txt)

    # Optional: write the combined output to a .txt file
    out_path = pdf_path.rsplit(".", 1)[0] + "_ocr.txt"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write("\n\n".join(all_text))
    print(f"\n✅ OCR complete. Full text saved to: {out_path}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python pdf_ocr.py <path_to_pdf>")
        sys.exit(1)
    pdf_file = sys.argv[1]
    main(pdf_file)
```

### Ожидаемый вывод (фрагмент)

```
✅ Loaded 'large_contract.pdf' – 342 pages.

--- Page 1 Preview ---
Contract Agreement between Party A and Party B ... 

--- Page 2 Preview ---
Recitals: Whereas, the parties desire to ...

...
✅ OCR complete. Full text saved to: large_contract_ocr.txt
```

Вы увидите короткий предварительный просмотр для каждой страницы, а затем окончательное подтверждение, что объединённый текстовый файл был записан.

---

## Особые случаи и практические советы

| Ситуация | Что делать |
|----------|------------|
| **Зашифрованный PDF** | Передайте пароль: `engine.load_pdf(pdf_path, password="mySecret")`. |
| **Очень большой PDF (> 1000 страниц)** | Осторожно увеличьте `max_memory_mb` или обрабатывайте порциями (например, по 200 страниц за раз). |
| **Смешанный контент (печатный + рукописный)** | Переключите `engine.recognition_mode` на `aocr.RecognitionMode.MIXED`, если библиотека это поддерживает. |
| **Отсутствие шрифтов или плохое качество сканирования** | Предобработайте страницы с помощью библиотеки улучшения изображений (например, Pillow) перед вызовом `recognize()`. |
| **Сбои из‑за нехватки памяти** | Уменьшите `preview_len` или сразу записывайте текст каждой страницы на диск, вместо того чтобы хранить всё в списке. |

---

## Как эффективно выполнять OCR больших PDF — Продвинутые стратегии

При решении задачи **как выполнять OCR больших PDF** скорость и стабильность становятся критичными. Вот несколько приёмов, которые можно добавить в скрипт:

1. **Параллелизация по страницам** — используйте `concurrent.futures.ThreadPoolExecutor`, если OCR‑движок потокобезопасен.  
2. **Кешировать промежуточные изображения** — некоторые движки позволяют сохранять растровые страницы на SSD, что резко снижает нагрузку на CPU при повторных запусках.  
3. **Пакетная запись результата** — вместо добавления в список Python откройте файл вывода один раз и записывайте текст каждой страницы сразу после его получения.  
4. **Регулировать DPI** — понижение DPI при растеризации уменьшает потребление памяти, но может повлиять на точность; найдите оптимальный баланс (обычно 200‑300 DPI).

Ниже быстрый фрагмент, показывающий, как можно параллелизовать шаг OCR (опционально, раскомментируйте для использования):

```python
# from concurrent.futures import ThreadPoolExecutor

# def ocr_page(engine, idx):
#     engine.select_page(idx)
#     return engine.recognize()

# with ThreadPoolExecutor(max_workers=4) as executor:
#     results = list(tqdm(executor.map(lambda i: ocr_page(engine, i),
#                                    range(engine.page_count)),
#                     total=engine.page_count,
#                     desc="Parallel OCR"))
```

Помните: параллелизм может увеличить нагрузку на CPU, поэтому следите за температурой системы при длительных запусках.

---

## Часто задаваемые вопросы

**В: Можно ли использовать этот скрипт с другими OCR‑библиотеками, например Tesseract?**  
О: Конечно. Замените вызовы `aocr` на `pytesseract.image_to...

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Как выполнить OCR PDF в .NET с помощью Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Как извлечь текст из изображения из потока с помощью Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Как извлечь текст из изображения по URL с помощью Aspose.OCR для Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}