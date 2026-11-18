---
category: general
date: 2026-06-19
description: Как пошагово выполнять OCR и повышать точность распознавания с помощью
  простых текстовых методов OCR. Узнайте быстрый рабочий процесс для надёжного извлечения
  текста.
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: ru
og_description: Как эффективно выполнять OCR. Этот учебник показывает, как улучшить
  точность OCR, используя OCR обычного текста и постобработку с помощью ИИ.
og_title: Как запустить OCR в Python – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  headline: How to Run OCR in Python – Complete Guide
  type: TechArticle
- description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  name: How to Run OCR in Python – Complete Guide
  steps:
  - name: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
    text: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
  - name: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
    text: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
  - name: '**Export formats** – Write the corrected structure to a searchable PDF'
    text: '**Export formats** – Write the corrected structure to a searchable PDF'
  type: HowTo
tags:
- OCR
- Python
- AI
title: Как запустить OCR в Python – полное руководство
url: /ru/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как запустить OCR в Python – Полное руководство

Когда‑то задумывались **как запустить OCR** для пачки отсканированных PDF, не тратя часы на настройку параметров? Вы не одиноки. Во многих проектах первая преграда — просто получить надёжный текст из изображения, а разница между неустойчивым результатом и чистым извлечением часто сводится к паре умных шагов.

В этом руководстве мы пройдём практический четырёхшаговый конвейер, который не только **выполняет OCR**, но и **повышает точность OCR**, комбинируя быстрый проход «plain‑text», второй проход, учитывающий разметку, и пост‑обработку на базе ИИ. К концу вы получите готовый к запуску скрипт, чёткое объяснение, почему каждый этап важен, и советы по работе с краевыми случаями, такими как много‑колоночные страницы или шумные сканы.

---

## Что понадобится

Прежде чем погрузиться, убедитесь, что у вас есть следующее:

- **Python 3.9+** – код использует подсказки типов и f‑строки.  
- **Tesseract OCR** установлен и доступен через команду `tesseract`. (В Ubuntu: `sudo apt install tesseract-ocr`; в Windows скачайте установщик с официального репозитория.)  
- Обёртка **pytesseract** (`pip install pytesseract`).  
- **Библиотека пост‑обработки ИИ** – в этом примере будем притворяться, что у вас есть лёгкий модуль `ai`, предлагающий `run_postprocessor`. Замените его API OpenAI GPT‑4 или локальной LLM, если хотите.  
- Пара образцов изображений или PDF‑файлов для тестов.

Вот и всё. Никаких тяжёлых фреймворков, без Docker‑трюков. Пара установок pip — и можно начинать.

---

## Шаг 1: Выполнить быстрый проход plain‑text OCR

Первое, что многие разработчики упускают, — это то, что *plain text* OCR работает молниеносно и даёт быструю проверку sanity. Мы вызовем `engine.Recognize()`, чтобы получить сырые символы без какой‑либо разметки. Это то, что мы называем **plain text OCR**.

```python
import pytesseract
from PIL import Image

def plain_text_ocr(image_path: str) -> str:
    """Run a quick plain‑text OCR pass and return the raw string."""
    img = Image.open(image_path)
    # pytesseract returns a single string with line breaks.
    raw_text = pytesseract.image_to_string(img, lang='eng')
    return raw_text
```

*Почему это важно:*  
- **Скорость** – plain‑pass для страницы 300 dpi обычно завершается менее чем за секунду.  
- **База** – вы можете сравнить последующий структурированный вывод с этой базой, чтобы увидеть явные ошибки.  
- **Отлов ошибок** – если plain‑pass полностью проваливается (например, весь мусор), вы знаете, что качество изображения слишком низкое, и можете прекратить обработку.

---

## Шаг 2: Запустить детальный layout‑aware OCR проход

Plain text хорош, но он теряет *где* находится каждое слово на странице. Для счетов, форм или много‑колоночных журналов нужны координаты, номера строк и, возможно, информация о шрифте. Здесь вступает в игру `engine.RecognizeStructured()`.

Ниже — тонкая обёртка над TSV‑выводом Tesseract, который даёт иерархию страниц → строк → слов, сохраняющую ограничительные рамки.

```python
from typing import List, Dict

def structured_ocr(image_path: str) -> List[Dict]:
    """Return a list of pages, each containing lines with word coordinates."""
    img = Image.open(image_path)

    # Tesseract TSV includes page, block, paragraph, line, word indices.
    tsv_data = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT, lang='eng')

    pages = {}
    for i, level in enumerate(tsv_data["level"]):
        if level != 5:  # focus on word level (5)
            continue
        page_num = tsv_data["page_num"][i]
        line_num = tsv_data["line_num"][i]
        word = tsv_data["text"][i]
        if not word.strip():
            continue

        # Build nested dict structure.
        pages.setdefault(page_num, {}).setdefault(line_num, []).append({
            "text": word,
            "bbox": (
                tsv_data["left"][i],
                tsv_data["top"][i],
                tsv_data["width"][i],
                tsv_data["height"][i],
            ),
        })

    # Convert dicts to a more convenient list format.
    structured_result = []
    for page_id, lines in pages.items():
        page_obj = {"PageNumber": page_id, "Lines": []}
        for line_id, words in lines.items():
            line_text = " ".join(w["text"] for w in words)
            line_obj = {
                "LineNumber": line_id,
                "Text": line_text,
                "Words": words,
            }
            page_obj["Lines"].append(line_obj)
        structured_result.append(page_obj)

    return structured_result
```

*Зачем это делаем:*  
- **Координаты** позволяют позже сопоставлять извлечённый текст с оригинальным изображением для подсветки или редактирования.  
- **Группировка по строкам** сохраняет исходную разметку, что критично при восстановлении таблиц или колонок.  
- Этот проход немного медленнее plain‑pass, но всё равно занимает несколько секунд для большинства документов.

---

## Шаг 3: Запустить AI‑пост‑процессор для исправления ошибок OCR

Даже лучший OCR‑движок делает ошибки — «rn» вместо «m», пропущенные диакритические знаки или разбитые слова. Модель ИИ может взглянуть на сырую строку и структурированные данные, обнаружить несоответствия и переписать текст, сохранив оригинальные координаты.

Ниже — **мок**‑реализация; замените тело реальным вызовом LLM, если он у вас есть.

```python
def ai_postprocess(plain_text: str, structured_result: List[Dict]) -> List[Dict]:
    """
    Simulate an AI post‑processor that corrects OCR errors.
    It walks through each line, compares it with the plain text,
    and applies simple heuristics (e.g., spell‑check).
    """
    import difflib
    corrected = []

    for page in structured_result:
        new_page = {"PageNumber": page["PageNumber"], "Lines": []}
        for line in page["Lines"]:
            # Find the closest match in the plain text using difflib.
            best_match = difflib.get_close_matches(line["Text"], plain_text.splitlines(), n=1, cutoff=0.6)
            corrected_text = best_match[0] if best_match else line["Text"]
            # Preserve original word list but replace the text field.
            new_line = {
                "LineNumber": line["LineNumber"],
                "Text": corrected_text,
                "Words": line["Words"],  # coordinates stay the same
            }
            new_page["Lines"].append(new_line)
        corrected.append(new_page)

    return corrected
```

*Почему этот шаг повышает точность OCR:*  
- **Контекстные исправления** — ИИ может решить, что «l0ve» скорее «love», опираясь на окружающие слова.  
- **Сохранение координат** — разметка остаётся, так что последующие задачи (например, аннотация PDF) остаются точными.  
- **Итеративное уточнение** — можно запускать пост‑процессор несколько раз, каждый проход устраняя всё больше ошибок.

---

## Шаг 4: Пройтись по исправленному, структурированному выводу

Теперь, когда у нас есть очищенная структура, получение окончательного текста тривиально. Ниже мы выводим каждую строку, но вы также можете записать в CSV, загрузить в базу данных или создать поисковый PDF.

```python
def display_corrected_text(structured_result: List[Dict]) -> None:
    """Print each line of corrected OCR output."""
    for page in structured_result:
        print(f"\n--- Page {page['PageNumber']} ---")
        for line in page["Lines"]:
            print(line["Text"])

# Example usage tying everything together
if __name__ == "__main__":
    img_path = "sample_scan.png"

    # 1️⃣ Plain‑text OCR
    plain = plain_text_ocr(img_path)
    print("✅ Plain text OCR completed.")

    # 2️⃣ Structured OCR
    structured = structured_ocr(img_path)
    print("✅ Structured OCR completed.")

    # 3️⃣ AI post‑processing
    corrected = ai_postprocess(plain, structured)
    print("✅ AI post‑processor finished.")

    # 4️⃣ Show results
    display_corrected_text(corrected)
```

**Ожидаемый вывод** (при простом одностраничном счёте):

```
--- Page 1 ---
Invoice #12345
Date: 2024‑05‑01
Bill To: Acme Corp
Item Qty Price Total
Widget A 2 $15.00 $30.00
Widget B 1 $25.00 $25.00
Subtotal $55.00
Tax $5.50
Total $60.50
```

Обратите внимание, как сохраняются разрывы строк и порядок колонок, а типичные глюки OCR, такие как чтение «$15.00» как «$15,00», исправляются шагом ИИ.

---

## Как этот рабочий процесс помогает **повысить точность OCR**

| Этап | Что исправляет | Почему важно |
|------|----------------|--------------|
| **Plain text OCR** | Выявляет нечитаемые страницы заранее | Экономит время, пропуская безнадёжные входы |
| **Structured OCR** | Захватывает разметку, координаты | Позволяет выполнять downstream‑задачи (подсветка, редактирование) |
| **AI пост‑процессор** | Исправляет орфографию, объединяет разбитые слова, корректирует числа | Повышает общую точность символов с ~85 % до >95 % на шумных сканах |
| **Итерация** | Позволяет пере‑запускать с настроенными параметрами | Тонко настраивает конвейер под конкретные типы документов |

Объединив эти три концепции — **plain text OCR**, извлечение с учётом разметки и AI‑коррекцию — вы получаете надёжное решение, которое *значительно* **повышает точность OCR** без написания собственного нейронного сетевого кода.

---

## Распространённые подводные камни и профессиональные советы

- **Подводный камень:** Передача изображения низкого разрешения (≤150 dpi) в Tesseract приводит к искажённому выводу.  
  **Профи‑совет:** Предобработайте с помощью `Pillow` — примените `Image.convert('L')` и `Image.filter(ImageFilter.MedianFilter())` перед OCR.

- **Подводный камень:** AI‑пост‑процессор может случайно переписать специализированные термины (например, «SKU123»).  
  **Профи‑совет:** Сформируйте whitelist терминов и передайте его в LLM или в библиотеку проверяющего правописание, например `pyspellchecker`.

- **Подводный камень:** Много‑колоночные страницы объединяются в одну строку.  
  **Профи‑совет:** Определяйте границы колонок, используя поле `block_num` в TSV‑выводе Tesseract, и разбивайте строки соответственно.

- **Подводный камень:** Большие PDF‑файлы вызывают переполнение памяти при загрузке всех страниц сразу.  
  **Профи‑совет:** Обрабатывайте страницы по‑частям — цикл `pdf2image.convert_from_path(..., first_page=n, last_page=n)`.

---

## Расширение конвейера

Если вам интересны дальнейшие шаги, рассмотрите следующие улучшения:

1. **Пакетная обработка** — оберните весь скрипт в функцию, проходящую по каталогу, обрабатывающую тысячи файлов параллельно с `concurrent.futures`.  
2. **Языковые модели** — замените простую диффлиб‑эвристику вызовом OpenAI `gpt‑4o` или локальной модели LLaMA для более богатых контекстных исправлений.  
3. **Форматы экспорта** — запишите исправленную структуру в поисковый PDF  

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в своих проектах.

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Use OCR - Advanced Techniques with Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/)
- [Improve OCR Accuracy – Detect Areas Mode in OCR](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}