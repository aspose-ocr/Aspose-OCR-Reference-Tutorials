---
category: general
date: 2026-06-22
description: Узнайте, как вывести список кэшированных AI‑моделей с помощью AI SDK
  на Python. Включает шаги по получению каталога кэша моделей и эффективному управлению
  локальными AI‑моделями.
draft: false
keywords:
- list cached ai models
- retrieve model cache directory
- list local ai models
- ai sdk python
- manage ai model cache
language: ru
og_description: Выведите список кэшированных AI‑моделей с помощью Python и AI SDK.
  Следуйте этому пошаговому руководству, чтобы получить каталог кэша моделей и работать
  с локальными AI‑моделями.
og_title: Список кэшированных AI‑моделей в Python – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  headline: List Cached AI Models in Python – Complete Guide
  type: TechArticle
- description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  name: List Cached AI Models in Python – Complete Guide
  steps:
  - name: Import the AI SDK
    text: '```python # Step 1: Import the AI SDK (replace with the actual package
      name if different) import ai ```'
  - name: List All Cached Models
    text: '```python # Step 2: List all models that are cached locally cached_models
      = ai.list_local() print("Cached models:", cached_models) ```'
  - name: Retrieve the Model Cache Directory
    text: '```python # Step 3: Retrieve the directory where the model files are stored
      cache_dir = ai.get_local_path() print("Model cache directory:", cache_dir) ```'
  - name: Empty Cache
    text: If `ai.list_local()` returns an empty list, you might wonder whether the
      SDK is misconfigured. Double‑check the environment variable `AI_CACHE_DIR` (or
      the SDK’s config file) to ensure it points to a writable location.
  - name: Permissions Issues
    text: When accessing `ai.get_local_path()`, a `PermissionError` can surface on
      restrictive systems. The fix is usually to run the script with appropriate user
      rights or to adjust the directory’s ACLs.
  - name: Version Mismatches
    text: 'Sometimes the cache contains an older version of a model while your code
      requests a newer one. The SDK will automatically download the newer version,
      but you can pre‑empt this by inspecting the version tag in the list:'
  - name: Cleaning Up Old Models
    text: 'If you need to free up space, you can delete a specific model folder directly:'
  type: HowTo
- questions:
  - answer: Yes. The SDK abstracts away OS‑specific paths, so `ai.get_local_path()`
      returns a valid string on Linux, macOS, and Windows.
    question: Does this work on all operating systems?
  - answer: The built‑in `list_local()` only reports locally stored artifacts. For
      remote registries you’d use `ai.list_remote()` (if your SDK version provides
      it).
    question: Can I list models from a remote cache?
  - answer: 'Replace the import line with the actual package name, e.g., `import myai
      as ai`. All subsequent calls stay the same because the API contract is consistent
      across implementations. --- ## Conclusion You now have a solid, production‑ready
      method to **list cached AI models** using the **AI SDK Python** '
    question: What if the SDK name isn’t `ai`?
  type: FAQPage
tags:
- python
- ai
- sdk
title: Список кэшированных моделей ИИ в Python – Полное руководство
url: /ru/python/general/list-cached-ai-models-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Список кэшированных AI‑моделей в Python – Полное руководство

Когда‑нибудь задумывались, как **перечислить кэшированные AI‑модели** на рабочей станции, не копаясь в скрытых папках? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда нужно проверить, какие модели уже сохранены локально, особенно при ограниченной пропускной способности или офлайн‑развёртываниях. В этом руководстве вы увидите быстрый, без лишних деталей способ запросить AI SDK, вывести содержимое кеша и точно узнать, где находятся эти файлы.

Мы также коснёмся связанных тем, таких как **получение каталога кеша моделей**, обработка пустых кешей и лучшие практики **управления кешем AI‑моделей** в производственных скриптах. К концу вы получите автономный фрагмент кода, который можно вставить в любой проект на Python.

## Предварительные требования

Прежде чем погрузиться в детали, убедитесь, что у вас есть:

- Python 3.8 или новее установлен.
- AI SDK (пакет `ai`) установлен через `pip install ai-sdk` или внутренний репозиторий вашей организации.
- Базовое знакомство с запуском скриптов из командной строки.

Дополнительные библиотеки не требуются, поэтому пример остаётся лёгким и переносимым.

---

## Список кэшированных AI‑моделей – Краткий обзор

Первое, что нужно сделать, — импортировать SDK и вызвать его вспомогательные функции. SDK предоставляет два удобных метода:

1. `ai.list_local()` — возвращает список идентификаторов моделей, уже находящихся в кеше.
2. `ai.get_local_path()` — возвращает абсолютный каталог, где хранятся файлы моделей.

Оба вызова синхронные и бросают понятный `AIError`, если что‑то пошло не так, что упрощает обработку ошибок.

> **Зачем использовать эти функции?**  
> Знание точного набора кэшированных моделей позволяет избежать лишних загрузок, отлаживать несоответствия версий и автоматически очищать старые артефакты. Это небольшая часть более крупного рабочего процесса **AI SDK Python**, но может сэкономить часы ручного поиска по файловой системе.

### Шаг 1: Импортировать AI SDK

```python
# Step 1: Import the AI SDK (replace with the actual package name if different)
import ai
```

*Почему это важно:* Импорт пакета регистрирует нижележащие C‑расширения и загружает файлы конфигурации (например, пути кеша) из вашей среды. Пропуск этого шага вызовет `ModuleNotFoundError` в момент вызова любой функции SDK.

### Шаг 2: Перечислить все кэшированные модели

```python
# Step 2: List all models that are cached locally
cached_models = ai.list_local()
print("Cached models:", cached_models)
```

**Что вы увидите:** Если у вас хранится три модели, вывод может выглядеть так:

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
```

Если кеш пуст, вы получите пустой список:

```
Cached models: []
```

> **Полезный совет:** Оберните вызов в блок `try/except`, если подозреваете, что SDK может быть некорректно инициализирован.

```python
try:
    cached_models = ai.list_local()
except ai.AIError as e:
    print("Failed to list cached models:", e)
    cached_models = []
```

### Шаг 3: Получить каталог кеша моделей

```python
# Step 3: Retrieve the directory where the model files are stored
cache_dir = ai.get_local_path()
print("Model cache directory:", cache_dir)
```

Типичный вывод в Unix‑подобной системе:

```
Model cache directory: /home/you/.cache/ai/models
```

В Windows вы можете увидеть что‑то вроде `C:\Users\you\AppData\Local\ai\models`. Знание этого пути необходимо, когда нужно **управлять кешем AI‑моделей** вручную — например, очистить старые версии или скопировать файлы на общий диск.

---

## Визуальное резюме

![Diagram showing how to list cached AI models, retrieve their names, and locate the cache directory](https://example.com/images/list-cached-ai-models.png)

*Alt text:* Диаграмма, иллюстрирующая процесс **перечисления кэшированных AI‑моделей** с помощью AI SDK в Python.

---

## Обработка граничных случаев и распространённых подводных камней

### Пустой кеш

Если `ai.list_local()` возвращает пустой список, вы можете задуматься, не ошибочно ли сконфигурирован SDK. Проверьте переменную окружения `AI_CACHE_DIR` (или файл конфигурации SDK), чтобы убедиться, что она указывает на записываемое место.

```python
if not cached_models:
    print("No models are cached. Consider downloading a model first.")
```

### Проблемы с правами доступа

При обращении к `ai.get_local_path()` может возникнуть `PermissionError` на системах с ограниченными правами. Обычно решение — запустить скрипт от имени пользователя с нужными правами или скорректировать ACL каталога.

### Несоответствие версий

Иногда в кеше находится более старая версия модели, а ваш код запрашивает более новую. SDK автоматически скачает новую версию, но вы можете предотвратить это, проверив тег версии в списке:

```python
for model in cached_models:
    if "v2" not in model:
        print(f"Model {model} may be outdated.")
```

### Очистка старых моделей

Если нужно освободить место, можно удалить конкретную папку модели напрямую:

```python
import shutil, os

def purge_model(model_name):
    path = os.path.join(cache_dir, model_name)
    if os.path.isdir(path):
        shutil.rmtree(path)
        print(f"Purged {model_name} from cache.")
    else:
        print(f"{model_name} not found in cache.")
```

Вызов `purge_model('bert-base-uncased')` удалит эту модель и освободит дисковое пространство.

---

## Полный скрипт, готовый к копированию

Ниже представлен готовый к запуску скрипт, объединяющий все шаги, добавляющий базовую обработку ошибок и выводящий удобное резюме.

```python
#!/usr/bin/env python3
"""
Complete example: list cached AI models and show cache directory.
"""

import ai
import os
import sys
import shutil

def main():
    try:
        # Retrieve cached model list
        cached = ai.list_local()
        print("Cached models:", cached)

        # Retrieve cache directory
        cache_dir = ai.get_local_path()
        print("Model cache directory:", cache_dir)

        # Summarize status
        if not cached:
            print("\n⚠️  No models are currently cached.")
        else:
            print("\n✅  Found {} model(s) in cache.".format(len(cached)))

        # Optional: ask user if they want to purge an old model
        if cached:
            to_purge = input("\nEnter a model name to purge (or press Enter to skip): ").strip()
            if to_purge:
                purge_path = os.path.join(cache_dir, to_purge)
                if os.path.isdir(purge_path):
                    shutil.rmtree(purge_path)
                    print(f"🗑️  Purged {to_purge} from cache.")
                else:
                    print(f"❌  Model {to_purge} not found in cache.")
    except ai.AIError as err:
        print("AI SDK error:", err, file=sys.stderr)
        sys.exit(1)
    except Exception as exc:
        print("Unexpected error:", exc, file=sys.stderr)
        sys.exit(1)

if __name__ == "__main__":
    main()
```

**Ожидаемый вывод (при заполненном кеше):**

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
Model cache directory: /home/you/.cache/ai/models

✅  Found 3 model(s) in cache.

Enter a model name to purge (or press Enter to skip):
```

Запустите скрипт командой `python list_models.py`, и вы мгновенно узнаете, что находится на диске.

---

## Часто задаваемые вопросы

**В: Работает ли это на всех операционных системах?**  
О: Да. SDK абстрагирует пути, специфичные для ОС, поэтому `ai.get_local_path()` возвращает корректную строку и на Linux, и на macOS, и на Windows.

**В: Можно ли перечислить модели из удалённого кеша?**  
О: Встроенный `list_local()` сообщает только о локально сохранённых артефактах. Для удалённых реестров используйте `ai.list_remote()` (если ваша версия SDK его поддерживает).

**В: Что если имя пакета SDK не `ai`?**  
О: Замените строку импорта на фактическое название пакета, например `import myai as ai`. Все последующие вызовы останутся теми же, поскольку контракт API одинаков для разных реализаций.

---

## Заключение

Теперь у вас есть надёжный, готовый к продакшну способ **перечислять кэшированные AI‑модели** с помощью библиотеки **AI SDK Python**, получать **каталог кеша моделей** и даже очищать старые файлы. Эти знания помогут поддерживать окружение в порядке, избегать лишних загрузок и легко отлаживать проблемы с версиями.

Готовы к следующему шагу? Попробуйте расширить скрипт автоматической загрузкой недостающих моделей или интегрировать его в CI‑конвейер, который проверяет состояние кеша перед каждой сборкой. Изучение стратегий **управления кешем AI‑моделей** сделает ваши AI‑приложения быстрее и надёжнее.

Счастливого кодинга, и пусть ваш кеш остаётся лёгким!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом пособии. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}