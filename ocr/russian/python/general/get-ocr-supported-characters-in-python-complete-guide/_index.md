---
category: general
date: 2026-06-25
description: Быстро получайте поддерживаемые OCR‑символы с помощью библиотеки aocr.
  Узнайте, как вывести список OCR‑символов, установить языки и отладить ваш OCR‑движок
  в Python.
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: ru
og_description: Получите поддерживаемые OCR‑символы с помощью aocr. Это руководство
  покажет, как перечислить символы OCR, выбрать языки и обработать крайние случаи
  в Python.
og_title: Получите поддерживаемые OCR‑символы в Python — Полный учебник
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Получить поддерживаемые OCR‑символы в Python — Полное руководство
url: /ru/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Получить поддерживаемые OCR символы в Python – Полное руководство

Когда‑то задумывались, как **получить поддерживаемые OCR символы** для конкретного языка, играя с OCR‑движком? Вы не одиноки. Будь то сканер чеков или многоязычный парсер документов, знание того, какие глифы ваш движок может распознать, спасает жизнь. В этом руководстве мы пройдём весь процесс — установку библиотеки, настройку языка и, наконец, вывод этих символов — чтобы вы могли отлаживать и тонко настраивать ваш OCR‑конвейер за считанные минуты.

Мы будем использовать библиотеку **aocr**, лёгкий Python‑OCR‑движок, который упрощает запрос возможностей языка. К концу этого руководства вы сможете **вывести список OCR‑символов**, переключаться между **поддерживаемыми OCR‑языками** и даже обнаруживать пробелы в покрытии до того, как они станут проблемой в продакшене.

---

## Требования

Перед тем как начать, убедитесь, что у вас есть:

* Python 3.8 или новее (пакет aocr прекращает поддержку 3.7)
* Терминал или командная строка с доступом к интернету
* Базовое знакомство с написанием скриптов на Python (если вы уже использовали `print()`, то всё в порядке)

Нет тяжёлых внешних зависимостей — только pip‑пакет `aocr`.

---

## Установка библиотеки aocr (OCR Engine Python)

Первое, что вам нужно, — рабочая установка **OCR engine Python**. Пакет aocr размещён на PyPI, поэтому достаточно одной команды pip:

```bash
pip install aocr
```

Если вы используете виртуальное окружение (настоятельно рекомендуется), сначала активируйте его:

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **Совет:** Зафиксируйте версию (`pip install aocr==1.2.4`), чтобы избежать неожиданных изменений API в дальнейшем.

---

## Выбор языка (Поддерживаемые OCR языки)

aocr поставляется с небольшим набором встроенных языковых пакетов. Каждый пакет определяет набор Unicode‑кодовых точек, которые движок может распознавать. Чтобы запросить эти пакеты, вам нужно установить атрибут `language` у экземпляра движка.

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

Вы можете заменить `aocr.Language.ENGLISH` на любое другое значение перечисления (`FRENCH`, `GERMAN` и т.д.). Если попытаться задать язык, который не включён в пакет, aocr выбросит `ValueError`. Поэтому рекомендуется сначала проверить список **поддерживаемых OCR языков**:

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## Получение набора символов (Get OCR Supported Characters)

Теперь переходим к сути руководства: действительно **получить поддерживаемые OCR символы**. Движок предоставляет удобный метод `get_supported_characters()`, который возвращает список строк‑символов длиной один символ.

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

Внутри aocr читает JSON‑файл, включённый в языковой пакет, и преобразует каждую Unicode‑кодовую точку в строку Python. Результат детерминирован, то есть вы получите один и тот же список каждый раз при запуске скрипта для одной и той же версии языка.

---

## Показать количество поддерживаемых символов

Знание количества помогает быстро оценить охват. Для английского обычно отображается несколько тысяч символов (включая пунктуацию и цифры).

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

Вызов `len()` имеет сложность O(1), потому что Python хранит длину списка внутри, поэтому даже для больших алфавитов нет штрафа по производительности.

---

## Предпросмотр первых 100 поддерживаемых символов

Быстрая визуальная проверка может показать, включены ли нужные вам символы (например, знак евро или «умные» кавычки). Выведем первые сто символов:

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

Операция `join` объединяет срез в одну строку, что читается лучше, чем печать списка Python.

---

## Полный скрипт – все шаги в одном месте

Ниже приведён полностью готовый пример, который связывает все шаги вместе. Сохраните его как `list_supported_chars.py` и запустите `python list_supported_chars.py` из терминала.

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**Ожидаемый вывод (усечённый для краткости):**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

Точная цифра может немного отличаться в зависимости от версии aocr, но вы всегда увидите длинный алфавит плюс обычную пунктуацию.

---

## Обработка граничных случаев

### Что делать, если пакет языка отсутствует?

Если запросить язык, который не включён в пакет, `aocr.Language` не будет содержать соответствующее перечисление, и возникнет `AttributeError`. Защититесь от этого простой проверкой:

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### Пустой список символов

Некоторые редкие языки могут вернуть пустой список, если исходные обучающие данные неполные. В таком случае можно переключиться на язык по умолчанию (например, английский) или выдать предупреждение:

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Нормализация Unicode

Список может содержать составные символы (например, «é» как `e` + острый акцент). Если последующая обработка ожидает предкомпозированные глифы, выполните шаг нормализации:

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## Профессиональные советы для реальных проектов

* **Cache the character list** – Если вы обрабатываете тысячи изображений, вызов `get_supported_characters()` на каждой итерации добавляет лишние затраты. Сохраните список в переменной уровня модуля или сериализуйте его в JSON для последующего повторного использования.
* **Cross‑language validation** – Когда в одном приложении поддерживается несколько языков, найдите пересечение наборов символов, чтобы определить общий подмножество. Это поможет создавать UI‑элементы, одинаково выглядящие во всех локалях.
* **Debugging OCR failures** – Если движок ошибочно классифицирует глиф, сравните проблемный символ с выводом `list_supported_chars`. Если его нет, вы обнаружили пробел в покрытии, который может потребовать пользовательского обучения.
* **Combine with custom fonts** – aocr учитывает диапазон Unicode, но качество рендеринга может различаться в зависимости от шрифта. Протестируйте поддерживаемые символы с тем шрифтом, который будет использоваться в продакшене, чтобы избежать сюрпризов.

---

## Часто задаваемые вопросы

**Q: Работает ли это с версией aocr 2.x?**  
A: Да, метод `get_supported_characters()` стабилен в версиях 1.x и 2.x. Единственное изменение — перечисления языков перенесены в `aocr.languages`.

**Q: Можно ли получить Unicode‑кодовую точку для каждого символа?**  
A: Конечно. Используйте `ord(ch)` внутри list comprehension:

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**Q: Что насчёт скриптов справа налево, например арабского?**  
A: aocr включает перечисление `ARABIC`. Список символов будет содержать арабские глифы, но может потребоваться включить RTL‑рендеринг в вашем UI.

---

## Заключение

Теперь вы знаете, **как получить поддерживаемые OCR символы** с помощью библиотеки aocr в Python, как переключаться между **поддерживаемыми OCR языками** и почему **вывод списка OCR‑символов** важен для надёжных конвейеров распознавания текста. Имея полный скрипт и приведённые выше советы, вы сможете быстро проверять покрытие языков, отлаживать недостающие глифы и создавать более умные OCR‑приложения.

Готовы к следующему шагу? Попробуйте сочетать этот список символов с пользовательским фильтром словаря или поэкспериментировать с другим OCR‑движком (Tesseract, EasyOCR) и сравнить результаты. Чем больше вы исследуете, тем лучше станут ваши OCR‑решения.

Счастливого кодинга, и пусть ваш набор символов всегда будет полным!

## Что изучать дальше?

- [Указать разрешённые символы OCR – используя Aspose.OCR для .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [Как выполнять OCR текста изображения с указанием языка, используя Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Постобработка OCR – Получить варианты символов](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}