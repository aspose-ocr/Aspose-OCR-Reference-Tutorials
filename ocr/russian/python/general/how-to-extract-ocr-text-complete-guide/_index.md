---
category: general
date: 2026-02-22
description: Узнайте, как извлекать текст из OCR и повышать точность OCR с помощью
  постобработки ИИ. Легко очищайте OCR‑текст в Python с пошаговым примером.
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: ru
og_description: Узнайте, как извлекать текст OCR, повышать точность OCR и очищать
  его, используя простой рабочий процесс на Python с постобработкой ИИ.
og_title: Как извлечь текст OCR – пошаговое руководство
tags:
- OCR
- AI
- Python
title: Как извлечь текст OCR – Полное руководство
url: /ru/python/general/how-to-extract-ocr-text-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как извлечь OCR‑текст – Полный программный учебник

Когда‑нибудь задавались вопросом **как извлечь OCR** из отсканированного документа, не получив кучу опечаток и разорванных строк? Вы не одиноки. Во многих реальных проектах необработанный вывод OCR‑движка выглядит как спутанный абзац, а его очистка ощущается как рутинная работа.  

Хорошая новость? Следуя этому руководству, вы увидите практический способ получить структурированные OCR‑данные, запустить AI‑постобработку и получить **чистый OCR‑текст**, готовый к дальнейшему анализу. Мы также коснёмся техник **повышения точности OCR**, чтобы результаты были надёжными с первого раза.

За несколько минут мы охватим всё необходимое: требуемые библиотеки, полностью рабочий скрипт и советы по избежанию типичных подводных камней. Никаких расплывчатых «см. документацию»‑шорткатов — только полное, автономное решение, которое можно скопировать, вставить и запустить.

## Что понадобится

- Python 3.9+ (код использует подсказки типов, но работает и на более старых версиях 3.x)
- OCR‑движок, способный возвращать **структурированный** результат (например, Tesseract через `pytesseract` с флагом `--psm 1`, либо коммерческий API, предоставляющий метаданные блоков/строк)
- AI‑модель пост‑обработки — в этом примере мы смоделируем её простой функцией, но вы можете заменить её на `gpt‑4o-mini` от OpenAI, Claude или любой LLM, принимающий текст и возвращающий очищенный вывод
- Пара образцов изображений (PNG/JPG) для тестирования

Если всё готово, приступим.

## Как извлечь OCR – начальное получение

Первый шаг — вызвать OCR‑движок и запросить **структурированное представление** вместо простой строки. Структурированные результаты сохраняют границы блоков, строк и слов, что значительно упрощает последующую очистку.

```python
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List

# Simple data classes mirroring a typical structured OCR response
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

def recognize_structured(image_path: str) -> StructuredResult:
    """
    Run Tesseract with the `--psm 1` layout mode to get block/line info.
    In a real engine you would get JSON directly; here we simulate it.
    """
    img = Image.open(image_path)

    # Tesseract's TSV output includes level, page_num, block_num, par_num, line_num, word_num, text…
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    current_block_idx = -1
    current_line_idx = -1

    for i, level in enumerate(tsv["level"]):
        if level == 3:  # block level
            result.blocks.append(Block())
            current_block_idx += 1
            current_line_idx = -1
        elif level == 4:  # line level
            result.blocks[current_block_idx].lines.append(Line(text=""))
            current_line_idx += 1

        # level 5 is word; concatenate words into the current line
        if level == 5:
            word = tsv["text"][i]
            if word.strip():
                line_obj = result.blocks[current_block_idx].lines[current_line_idx]
                line_obj.text += (word + " ")

    # Trim trailing spaces
    for block in result.blocks:
        for line in block.lines:
            line.text = line.text.strip()
    return result
```

> **Почему это важно:** Сохраняя блоки и строки, мы избегаем угадывания, где начинаются абзацы. Функция `recognize_structured` даёт чистую иерархию, которую позже можно передать AI‑модели.

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

Запуск фрагмента выводит первую строку точно так, как её увидел OCR‑движок, часто с ошибками вроде «0cr» вместо «OCR».

## Повышение точности OCR с помощью AI‑постобработки

Теперь, когда у нас есть необработанный структурированный вывод, передадим его AI‑постобработчику. Цель — **повысить точность OCR**, исправив типичные ошибки, нормализовав пунктуацию и, при необходимости, пере‑сегментировав строки.

```python
import openai  # Example: using OpenAI's API; replace with your provider

def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    """
    Sends each line to an LLM that returns a cleaned version.
    This simple loop can be parallelized for large documents.
    """
    api_key = "YOUR_OPENAI_API_KEY"
    openai.api_key = api_key

    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "You are an OCR cleanup assistant. Fix any spelling, spacing, "
                "or punctuation errors in the following line while preserving the original meaning:\n\n"
                f"\"{line.text}\""
            )
            response = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=200,
            )
            cleaned = response.choices[0].message.content.strip()
            line.text = cleaned
    return structured
```

> **Совет профессионала:** Если у вас нет подписки на LLM, замените вызов локальным трансформером (например, `sentence‑transformers` + дообученной моделью коррекции) или даже правил‑базированным подходом. Главное — AI видит каждую строку отдельно, чего обычно достаточно для **очистки OCR‑текста**.

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

Теперь вы должны увидеть гораздо более чистое предложение — опечатки исправлены, лишние пробелы удалены, пунктуация поправлена.

## Очистка OCR‑текста для лучших результатов

Даже после AI‑коррекции может потребоваться финальный шаг санитизации: удалить не‑ASCII символы, унифицировать разрывы строк и свернуть множественные пробелы. Этот дополнительный проход гарантирует, что вывод готов к дальнейшим задачам, таким как NLP или загрузка в базу данных.

```python
import re

def final_cleanup(structured: StructuredResult) -> str:
    """
    Flattens the hierarchy into a single string and performs
    additional regex‑based cleaning.
    """
    lines = []
    for block in structured.blocks:
        for line in block.lines:
            # Remove any lingering non‑printable characters
            cleaned = re.sub(r"[^\x20-\x7E]", "", line.text)
            # Collapse multiple spaces
            cleaned = re.sub(r"\s+", " ", cleaned).strip()
            lines.append(cleaned)
    # Join blocks with double newline to preserve paragraph breaks
    return "\n\n".join(lines)

clean_text = final_cleanup(structured_result)
print("\n=== Cleaned OCR Text ===\n")
print(clean_text)
```

Функция `final_cleanup` возвращает обычную строку, которую можно напрямую передать в поисковый индекс, языковую модель или экспортировать в CSV. Поскольку мы сохранили границы блоков, структура абзацев остаётся.

## Пограничные случаи и сценарии «что если»

- **Много‑колоночные макеты:** Если источник содержит колонки, OCR‑движок может перемешивать строки. Можно определить координаты колонок из TSV‑вывода и переупорядочить строки перед отправкой в AI.
- **Нелатинские скрипты:** Для языков вроде китайского или арабского переключите подсказку LLM на запрос коррекции, специфичной для языка, либо используйте модель, дообученную под этот скрипт.
- **Большие документы:** Отправка каждой строки отдельно может быть медленной. Пакетируйте строки (например, по 10 штук за запрос) и позвольте LLM вернуть список очищенных строк. Не забывайте о лимитах токенов.
- **Отсутствие блоков:** Некоторые OCR‑движки возвращают только плоский список слов. В этом случае можно восстановить строки, группируя слова с одинаковыми значениями `line_num`.

## Полный рабочий пример

Объединив всё вместе, получаем один файл, который можно запустить от начала до конца. Замените заполнители на свой API‑ключ и путь к изображению.

```python
# ocr_cleanup.py
import re
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List
import openai

# ---------- Data structures ----------
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

# ---------- Step 1: Extract OCR ----------
def recognize_structured(image_path: str) -> StructuredResult:
    img = Image.open(image_path)
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    cur_block = -1
    cur_line = -1

    for i, lvl in enumerate(tsv["level"]):
        if lvl == 3:                # block
            result.blocks.append(Block())
            cur_block += 1
            cur_line = -1
        elif lvl == 4:              # line
            result.blocks[cur_block].lines.append(Line(text=""))
            cur_line += 1
        elif lvl == 5:              # word
            word = tsv["text"][i]
            if word.strip():
                result.blocks[cur_block].lines[cur_line].text += word + " "

    # Trim spaces
    for blk in result.blocks:
        for ln in blk.lines:
            ln.text = ln.text.strip()
    return result

# ---------- Step 2: AI post‑processor ----------
def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    openai.api_key = "YOUR_OPENAI_API_KEY"
    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "Correct OCR errors (spelling, spacing, punctuation) in this line:\n"
                f"\"{line.text}\""
            )
            resp = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=150,
            )
            line.text = resp.choices[0].message.content.strip()
    return structured

# ---------- Step 3: Final cleanup ----------
def final_cleanup(structured: StructuredResult) -> str:
    out = []
    for block in structured.blocks:
        for line in block.lines:
            txt = re.sub(r"[^\x20-\x7E]", "", line.text)   # strip non‑ASCII
            txt = re.sub(r"\s+", " ", txt).strip

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}