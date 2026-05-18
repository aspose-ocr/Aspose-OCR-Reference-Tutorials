---
category: general
date: 2026-04-26
description: Быстро маскируйте номера кредитных карт с помощью постобработки OCR AsposeAI.
  Узнайте о соблюдении требований PCI, маскировании с помощью регулярных выражений
  и очистке данных в пошаговом руководстве.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: ru
og_description: Маскируйте номера кредитных карт в результатах OCR с помощью AsposeAI.
  В этом руководстве рассматриваются соответствие требованиям PCI, маскирование с
  помощью регулярных выражений и очистка данных.
og_title: Маскирование номеров кредитных карт – Полное руководство по постобработке
  OCR на Python
tags:
- OCR
- Python
- security
title: Маскирование номеров кредитных карт в выводе OCR – Полное руководство по Python
url: /ru/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Маскирование номеров кредитных карт – Полное руководство по Python

Когда‑нибудь вам нужно было **маскировать номера кредитных карт** в тексте, полученном напрямую от OCR‑движка? Вы не одиноки. В регулируемых отраслях раскрытие полного PAN (Primary Account Number) может привести к проблемам с аудиторами по PCI‑compliance. Хорошая новость? С помощью нескольких строк кода на Python и post‑processing‑hook от AsposeAI вы можете автоматически скрыть средние восемь цифр и оставаться в безопасности.

В этом руководстве мы пройдем реальный сценарий: запуск OCR на изображении чека, а затем применение пользовательской функции **OCR post‑processing**, которая очищает любые PCI‑данные. К концу вы получите переиспользуемый фрагмент, который можно вставить в любой workflow AsposeAI, а также несколько практических советов по обработке граничных случаев и масштабированию решения.

## Что вы узнаете

- Как зарегистрировать пользовательский post‑processor в **AsposeAI**.  
- Почему подход **regular expression masking** быстрый и надёжный.  
- Основы **PCI compliance**, связанные с очисткой данных.  
- Способы расширения шаблона для нескольких форматов карт или международных номеров.  
- Ожидаемый вывод и как проверить, что маскирование сработало.  

> **Prerequisites** – Вы должны иметь рабочую среду Python 3, установленный пакет Aspose.AI for OCR (`pip install aspose-ocr`) и пример изображения (например, `receipt.png`), содержащий номер кредитной карты. Другие внешние сервисы не требуются.  

---

## Шаг 1: Определите post‑processor, который маскирует номера кредитных карт

Сердце решения находится в небольшой функции, которая получает результат OCR, запускает **regular expression masking**‑процедуру и возвращает очищенный текст.

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**Почему это работает:**  
- Регулярное выражение `(\d{4})\d{8}(\d{4})` точно совпадает с 16 последовательными цифрами, типичным форматом для Visa, MasterCard и многих других.  
- Сохраняя первые и последние четыре цифры (`\1` и `\2`), мы оставляем достаточно информации для отладки, одновременно соблюдая правила **PCI compliance**, запрещающие хранить полный PAN.  
- Подстановка `\1****\2` скрывает чувствительные средние восемь цифр, превращая `1234567812345678` в `1234****5678`.  

> **Pro tip:** Если нужно поддерживать 15‑значные номера American Express, добавьте второй шаблон, например `r'(\d{4})\d{6}(\d{5})'`, и выполните оба замещения последовательно.  

---

## Шаг 2: Инициализируйте движок AsposeAI

Прежде чем привязать наш post‑processor, нам нужен экземпляр OCR‑движка. AsposeAI включает модель OCR и простой API для пользовательской обработки.

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**Почему инициализировать здесь?**  
Создание объекта `AsposeAI` один раз и его повторное использование для нескольких изображений уменьшает нагрузку. Движок также кэширует языковые модели, что ускоряет последующие вызовы — удобно при сканировании пакетов чеков.  

---

## Шаг 3: Зарегистрируйте пользовательскую функцию маскирования

AsposeAI предоставляет метод `set_post_processor`, позволяющий подключить любой вызываемый объект. Мы передаём нашу функцию `mask_pci` вместе с необязательным словарём настроек (пока пустым).

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**Что происходит за кулисами?**  
Когда позже вызывается `run_postprocessor`, AsposeAI передаёт необработанный результат OCR функции `mask_pci`. Функция получает лёгкий объект (`data`), содержащий распознанный текст, и возвращает новую строку. Такой дизайн оставляет ядро OCR нетронутым, позволяя централизованно применять политики **data sanitization**.  

---

## Шаг 4: Запустите OCR на изображении чека

Теперь, когда движок знает, как очистить вывод, мы передаём ему изображение. Для целей этого руководства предполагается, что у вас уже есть объект `engine`, сконфигурированный с нужными языком и настройками разрешения.

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**Tip:** Если у вас нет предварительно сконфигурированного объекта, его можно создать так:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

Вызов `recognize_image` возвращает объект, чей атрибут `text` содержит необработанную, немаскированную строку.  

---

## Шаг 5: Примените зарегистрированный post‑processor

Получив необработанные OCR‑данные, передаём их экземпляру AI. Движок автоматически запускает функцию `mask_pci`, которую мы зарегистрировали ранее.

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**Почему использовать `run_postprocessor`, а не вызывать функцию вручную?**  
Это сохраняет согласованность рабочего процесса, особенно когда задействовано несколько post‑processor‑ов (например, проверка орфографии, определение языка). AsposeAI ставит их в очередь в порядке регистрации, гарантируя детерминированный вывод.  

---

## Шаг 6: Проверьте очищенный вывод

Наконец, выведем очищенный текст и убедимся, что все номера кредитных карт правильно замаскированы.

```python
print(final_result.text)
```

**Ожидаемый вывод** (отрывок):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

Если в чеке не было номера карты, текст останется без изменений — нечего маскировать, нечего беспокоиться.  

---

## Обработка граничных случаев и распространённых вариаций

### Несколько номеров карт в одном документе
Если чек содержит более одного PAN (например, карта лояльности плюс платёжная карта), регулярное выражение работает глобально, автоматически маскируя все совпадения. Дополнительный код не требуется.  

### Нестандартное форматирование
Иногда OCR вставляет пробелы или дефисы (`1234 5678 1234 5678` или `1234-5678-1234-5678`). Расширьте шаблон, чтобы игнорировать эти символы:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

Добавление `[ -]?` допускает опциональные пробелы или дефисы между блоками цифр.  

### Международные карты
Для 19‑значных PAN, используемых в некоторых регионах, можно расширить шаблон:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

Просто помните, что **PCI compliance** всё равно требует маскировать средние цифры, независимо от длины.  

### Логирование замаскированных значений (опционально)
Если нужны аудиторские следы, передайте флаг через `custom_settings` и скорректируйте функцию:

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

Затем зарегистрируйте её так:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## Полный рабочий пример (готовый к копированию)

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

Запуск этого скрипта на чеке, содержащем `4111111111111111`, даст:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

Это весь конвейер — от необработанного OCR до **data sanitization** — упакованный в несколько чистых строк Python.  

---

## Заключение

Мы только что показали, как **маскировать номера кредитных карт** в результатах OCR, используя post‑processing‑hook AsposeAI, лаконичную регулярную маску и несколько рекомендаций по **PCI compliance**. Решение полностью автономно, работает с любым изображением, которое способен прочитать OCR‑движок, и может быть расширено для более сложных форматов карт или требований к логированию.  

Готовы к следующему шагу? Попробуйте связать эту маску с процедурой **вставки в базу данных**, сохраняющей только последние четыре цифры для справки, или интегрировать **пакетный процессор**, сканирующий всю папку чеков за ночь. Вы также можете исследовать другие задачи **OCR post‑processing**, такие как стандартизация адресов или определение языка — каждая следует той же схеме, что и здесь.  

Есть вопросы о граничных случаях, производительности или о том, как адаптировать код под другую OCR‑библиотеку? Оставьте комментарий ниже, и давайте продолжим обсуждение. Приятного кодинга и будьте в безопасности!  



![Diagram illustrating how mask credit card numbers works in an OCR pipeline](https://example.com/images/ocr-mask-flow.png "Diagram of OCR post‑processing masking flow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}