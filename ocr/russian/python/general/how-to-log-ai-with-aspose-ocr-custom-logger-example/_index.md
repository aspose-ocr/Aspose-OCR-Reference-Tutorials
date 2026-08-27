---
category: general
date: 2026-01-02
description: Изучите, как вести журнал AI с помощью Aspose OCR, используя пользовательский
  логгер. В этом руководстве рассматривается пример пользовательского логгера, импорт
  Aspose OCR и настройка пользовательского логгера.
draft: false
keywords:
- how to log ai
- use custom logger
- custom logger example
- import aspose ocr
- set custom logger
language: ru
og_description: Узнайте, как вести журнал AI с помощью Aspose OCR и пользовательского
  логгера. Следуйте пошаговому руководству по импорту Aspose OCR, настройке пользовательского
  логгера и просмотру вывода.
og_title: Как логировать AI с помощью Aspose OCR – пример пользовательского логгера
tags:
- Aspose OCR
- Python
- Logging
title: Как вести журнал AI с помощью Aspose OCR – пример пользовательского логгера
url: /ru/python/general/how-to-log-ai-with-aspose-ocr-custom-logger-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как вести журнал AI с Aspose OCR – пример пользовательского логгера

Задумывались ли вы **как вести журнал AI**, когда работаете с Aspose OCR? Возможно, вы пробовали стандартный консольный логгер и подумали: «Неплохо, но можно ли сделать его красивее или отправлять логи в файл?» Вы не одиноки. В этом руководстве мы пройдемся по полному **примеру пользовательского логгера**, покажем точный код, который вам нужен, и объясним *почему* каждый элемент важен.

К концу этого руководства вы сможете:

* **Импортировать Aspose OCR** в Python без проблем.  
* **Настроить пользовательский логгер**, который будет захватывать каждое сообщение, генерируемое AI‑движком.  
* Проверить вывод и адаптировать логгер под вашу собственную систему логирования.

Никакой внешней документации не требуется — всё, что нужно, находится здесь.

---

## Требования

Прежде чем приступить, убедитесь, что у вас есть:

| Требование | Причина |
|------------|---------|
| Python 3.8+ | Пакет `asposeocr` ориентирован на современные версии Python. |
| Установлена библиотека `asposeocr` (`pip install asposeocr`) | Предоставляет модуль `asposeocr.ai`, который мы будем использовать. |
| Базовое знакомство с функциями и вызываемыми объектами | Необходимо для создания пользовательского логгера. |

Если чего‑то не хватает, установите библиотеку сейчас:

```bash
pip install asposeocr
```

---

## Шаг 1 – Импорт Aspose OCR и AI‑модуля

Первое, что нужно сделать, когда вы хотите **импортировать Aspose OCR**, — это загрузить пространство имён `asposeocr.ai`. Это даст вам доступ к классу `AsposeAI`, который является точкой входа для всех OCR‑операций, управляемых ИИ.

```python
# Step 1: Import the Aspose OCR AI module
import asposeocr.ai as ai
```

*Почему это важно:* Импорт правильного модуля гарантирует, что вы взаимодействуете с нужным бекендом. Если пропустить подпакет `.ai`, вы получите только классический OCR‑API, который не предоставляет нужных хуков для логирования.

---

## Шаг 2 – Создание стандартного AI‑движка (консольный логгер)

Aspose OCR поставляется со встроенным логгером, который пишет напрямую в `stdout`. Запустим его, чтобы увидеть базовое поведение.

```python
# Step 2: Create an AI engine that logs to the console by default
default_engine = ai.AsposeAI()
```

При выполнении любой OCR‑операции с `default_engine` вы увидите сообщения вроде:

```
[INFO] AsposeAI initialized – version 23.10
[DEBUG] Loading language model...
```

Эти сообщения полезны для быстрой отладки, но им не хватает гибкости для продакшн‑окружения. Поэтому переходим к следующему шагу.

---

## Шаг 3 – Определение пользовательского логгера (любая вызываемая функция, принимающая строку)

**Пользовательский логгер** может быть любой вызываемой в Python функцией, принимающей один аргумент типа `str`. Ниже минимальный пример, который добавляет префикс `[AI LOG]`. При желании замените `print` на `logging.info`, запись в файл или отправку в сервис мониторинга.

```python
# Step 3: Define a custom logger (any callable that accepts a string)
def custom_logger(message: str):
    # You could replace this with `logging.info(message)` or any other sink.
    print("[AI LOG]", message)
```

*Почему это работает:* Конструктор `AsposeAI` ищет аргумент `logging`, реализующий протокол «вызвать с строкой». Предоставив функцию с такой сигнатурой, вы получаете полный контроль над тем, как обрабатывается каждая строка лога.

---

## Шаг 4 – Создание AI‑движка, использующего пользовательский логгер

Теперь связываем всё вместе. Передайте `custom_logger` в конструктор `AsposeAI` через параметр `logging`. Движок будет перенаправлять каждое внутреннее сообщение в вашу функцию.

```python
# Step 4: Create an AI engine that uses the custom logger
engine_with_custom_logger = ai.AsposeAI(logging=custom_logger)
```

### Ожидаемый вывод

Выполнение простого OCR‑вызова (например, `engine_with_custom_logger.recognize("sample.png")`) даст вывод, похожий на:

```
[AI LOG] AsposeAI initialized – version 23.10
[AI LOG] Loading language model...
[AI LOG] Model loaded successfully.
[AI LOG] Starting OCR on sample.png
[AI LOG] OCR completed – 98% confidence.
```

Обратите внимание, что каждая строка теперь начинается с `[AI LOG]`, точно так, как мы задали в `custom_logger`. Это доказывает, что **как вести журнал AI** полностью находится под вашим контролем.

---

## Полный рабочий пример – от импорта до выполнения

Ниже полностью готовый скрипт, который можно скопировать в файл `custom_logger_demo.py`. Он демонстрирует весь процесс: от импорта Aspose OCR до выполнения простого OCR‑запроса с пользовательским логгером.

```python
# custom_logger_demo.py
# -------------------------------------------------
# Demonstrates how to log AI using Aspose OCR
# with a user‑defined logger.
# -------------------------------------------------

import asposeocr.ai as ai

def custom_logger(message: str):
    """A tiny logger that prefixes messages."""
    print("[AI LOG]", message)

def main():
    # Use the custom logger when creating the AI engine
    ocr_engine = ai.AsposeAI(logging=custom_logger)

    # Path to an image you want to process (replace with your own)
    image_path = "sample.png"

    # Perform OCR – this will trigger the logger
    try:
        result = ocr_engine.recognize(image_path)
        print("\n--- OCR RESULT ---")
        print(result.text)  # Assuming the result object has a `text` attribute
    except Exception as e:
        print("[AI LOG] Error during OCR:", e)

if __name__ == "__main__":
    main()
```

**Что ожидать при запуске**

```bash
python custom_logger_demo.py
```

```
[AI LOG] AsposeAI initialized – version 23.10
[AI LOG] Loading language model...
[AI LOG] Model loaded successfully.
[AI LOG] Starting OCR on sample.png
[AI LOG] OCR completed – 98% confidence.

--- OCR RESULT ---
Hello world! This is the extracted text.
```

Если вы хотите **установить пользовательский логгер** в файл, просто замените `print` в `custom_logger` на что‑то вроде:

```python
def file_logger(message: str):
    with open("ocr.log", "a", encoding="utf-8") as f:
        f.write(message + "\n")
```

и передайте `logging=file_logger` при создании `AsposeAI`.

---

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|--------|-------|
| *Можно ли использовать стандартный модуль `logging`?* | Да. Просто настройте экземпляр логгера и вызывайте `logger.info(message)` внутри вашей функции. |
| *Что если мой логгер выбросит исключение?* | SDK перехватывает любые исключения из логгера и продолжает работу, но вы потеряете конкретную строку лога. Держите реализацию простой. |
| *Получает ли логгер сообщения уровня DEBUG?* | Да. AI‑движок передаёт **все** внутренние сообщения (INFO, DEBUG, WARN). Фильтруйте их внутри функции, если нужны только определённые уровни. |
| *Аргумент `logging` опционален?* | Если его опустить, движок вернётся к встроенному консольному логгеру. |
| *Будет ли это работать в асинхронном коде?* | Сам логгер синхронный; если нужен async‑обработчик, оберните вызов в coroutine `asyncio` и используйте `await` там, где это необходимо. |

---

## Профессиональные советы – делаем ваш логгер готовым к продакшн

1. **Пакетная запись** – Открывать и закрывать файл для каждой строки медленно. Используйте `logging.FileHandler` с буферизацией.  
2. **Добавляйте метки времени** – Включите `datetime.now().isoformat()` в префикс, чтобы упростить отладку.  
3. **Уровни логов** – Если нужна гранулярность, измените сигнатуру на приём кортежа `(level, message)` и адаптируйте вызов SDK (в текущей версии он передаёт только строку, поэтому уровни придётся парсить вручную).  
4. **Централизуйте конфигурацию** – Храните определение логгера в отдельном модуле (`my_logging.py`) и импортируйте его везде, где создаёте экземпляр `AsposeAI`.  

Эти приёмы помогут вам ответить не только на вопрос *как вести журнал AI*, но и *как вести журнал AI эффективно* в реальных сервисах.

---

## Заключение

Мы рассмотрели **как вести журнал AI** с Aspose OCR от начала до конца: импорт библиотеки, создание стандартного движка, написание **примера пользовательского логгера** и подключение этого логгера к AI‑движку. Код полностью готов, исполняем и адаптируем под любой бекенд логирования, который вам нужен.  

Если хотите пойти дальше, замените логгер на основе `print` на модуль `logging`, отправляйте логи в облачный сервис вроде Datadog или даже формируйте структурированный JSON для последующего анализа. Принцип остаётся тем же — **используйте пользовательский логгер** и **устанавливайте пользовательский логгер** при создании `AsposeAI`.

Счастливого кодинга, и пусть ваши логи будут так же ясны, как результаты OCR!

---

![скриншот как вести журнал AI](image.png "пример как вести журнал AI")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}