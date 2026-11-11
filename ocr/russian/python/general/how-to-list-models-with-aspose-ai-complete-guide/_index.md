---
category: general
date: 2026-07-05
description: Как вывести список моделей с помощью Aspose AI, включить автоматическую
  загрузку и скачать модель Hugging Face в Python. Следуйте этому пошаговому руководству,
  чтобы настроить кэш и начать использовать Aspose AI уже сегодня.
draft: false
keywords:
- how to list models
- enable auto download
- download hugging face model
- how to use aspose
- how to set cache
language: ru
og_description: Как вывести список моделей с помощью Aspose AI, включить автоматическую
  загрузку и скачать модель Hugging Face. Узнайте, как настроить кэш и использовать
  Aspose AI за несколько минут.
og_title: Как вывести список моделей с Aspose AI — Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  headline: How to list models with Aspose AI – Complete Guide
  type: TechArticle
- description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  name: How to list models with Aspose AI – Complete Guide
  steps:
  - name: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
    text: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
  - name: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
    text: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
  - name: Initialise the AI, then call `list_local()` to see exactly what’s cached.
    text: Initialise the AI, then call `list_local()` to see exactly what’s cached.
  - name: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
    text: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
  type: HowTo
tags:
- Aspose
- Python
- LLM
- Model Management
title: Как перечислить модели с помощью Aspose AI – Полное руководство
url: /ru/python/general/how-to-list-models-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как перечислить модели с Aspose AI – Полное руководство

Как перечислить модели с Aspose AI — это вопрос, который возникает, как только вы начинаете экспериментировать с большими языковыми моделями в Python. В этом руководстве мы пройдемся по включению **auto download**, настройке локального кеша и загрузке модели напрямую из Hugging Face — чтобы вы могли быстро приступить к работе без ручного поиска файлов.

Если вы когда‑нибудь задавались вопросом *«как использовать Aspose для OCR‑ориентированного ИИ?»* или *«какой самый простой способ настроить кеш для файлов моделей?»*, вы попали по адресу. К концу вы получите полностью рабочий скрипт, который перечислит все модели, хранящиеся локально, автоматически загрузит отсутствующие и покажет, где именно находятся файлы на диске.

---

## Что понадобится

- Python 3.9 или новее (библиотека использует подсказки типов, требующие современного интерпретатора)
- `pip` доступ для установки пакета **Aspose OCR** (`aocr`).  
  ```bash
  pip install aocr
  ```
- Подключение к интернету для первой загрузки из Hugging Face.
- Папка, в которой вы хотите хранить кеш моделей (например, `./model_cache`).

Вот и всё — без дополнительных Docker‑контейнеров, без тяжёлых виртуальных окружений, кроме чистой установки Python.

---

## ## Как перечислить модели с Aspose AI

Суть этого руководства — возможность **перечислять модели**, закешированные локально Aspose AI. После настройки кеша библиотека может перечислять всё, что она знает, что упрощает отладку и контроль версий.

```python
import aocr

# 1️⃣ Create an Aspose AI instance
ai = aocr.AsposeAI()

# 2️⃣ Configure the model cache and auto‑download behavior
cfg = aocr.AsposeAIModelConfig()
cfg.allow_auto_download = "true"                     # ← enable auto download
cfg.directory_model_path = r"./model_cache"          # ← how to set cache
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# 3️⃣ Initialise the AI with the config we just built
ai.initialize(cfg)

# 4️⃣ List the models that are already cached locally
print("🗂️ Models cached at:", ai.get_local_path())
print("📦 Available models:", ai.list_local())
```

**Почему это работает:**  
- `AsposeAI()` создает высокоуровневую точку входа, которая взаимодействует с движком вывода.  
- `AsposeAIModelConfig()` содержит все настройки; установка `allow_auto_download` в `"true"` сообщает библиотеке автоматически загружать недостающие файлы из указанного репозитория.  
- `directory_model_path` — это *директория кеша*, место, где находятся все загруженные бинарные файлы.  
- `initialize()` применяет конфигурацию, выполняя первую загрузку, если кеш пуст.  
- Наконец, `list_local()` сканирует папку кеша и возвращает список идентификаторов моделей в виде Python‑списка, который мы выводим.

### Ожидаемый вывод (первый запуск)

```
🗂️ Models cached at: ./model_cache
📦 Available models: ['Qwen2.5-3B-Instruct-GGUF']
```

Если вы запустите скрипт снова, библиотека пропустит загрузку и просто выведет уже присутствующую модель, доказывая, что **настройка кеша** действительно окупается при последующих запусках.

---

## ## Включить авто‑загрузку для отсутствующих моделей

Часто вам придётся работать с несколькими моделями в разных проектах. Ручная загрузка каждой из Hugging Face может быть утомительной. Включив авто‑загрузку, Aspose AI берёт на себя всю тяжёлую работу.

```python
cfg.allow_auto_download = "true"
```

> **Совет:** Оставляйте `allow_auto_download` установленным в `"true"` **только** в средах разработки или CI. В продакшене вы, возможно, захотите зафиксировать кеш, чтобы избежать неожиданного сетевого трафика.

Если позже решите отключить её, просто установите флаг в `"false"` перед повторным вызовом `initialize()`.

---

## ## Скачивание модели Hugging Face «на лету»

Строка

```python
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

сообщает Aspose AI, из какого удалённого репозитория выполнять загрузку. Библиотека поддерживает любую публичную модель на Hugging Face, предоставляющую файл GGUF. Хотите другую модель? Замените ID репозитория:

```python
cfg.hugging_face_repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
```

При запуске скрипта Aspose AI проверяет кеш:

- **Если модель существует**, она загружается мгновенно.  
- **Если её нет**, флаг авто‑загрузки инициирует загрузку, сохраняет файл в `directory_model_path` и затем регистрирует его для немедленного использования.

Такой подход устраняет двухшаговый процесс «скачать‑запустить», который многие руководства заставляют вас выполнять.

---

## ## Как использовать Aspose AI после того, как модель перечислена

Перечисление моделей — лишь половина истории. Как только вы убедились, что модель присутствует, можно приступать к инференсу:

```python
# Assume the model we just listed is the one we want to use
model_name = ai.list_local()[0]

# Create a simple prompt
prompt = "Explain the difference between supervised and unsupervised learning."

# Run inference
response = ai.run_inference(model_name, prompt)

print("🤖 Model response:", response)
```

**Почему это важно:**  
- `run_inference()` абстрагирует токенизацию, батчинг и работу с GPU.  
- Передавая *имя модели*, полученное из `list_local()`, вы гарантируете, что вызов инференса соответствует точному файлу на диске.

---

## ## Как задать расположение кеша для нескольких проектов

Если вы работаете с несколькими проектами, вам может потребоваться, чтобы каждый имел собственную папку кеша. Поле `directory_model_path` — просто строка, поэтому её можно формировать динамически:

```python
import os

project_name = "sentiment_analysis"
cache_root   = "./model_cache"
cfg.directory_model_path = os.path.join(cache_root, project_name)
```

Теперь каждый проект получает изолированную подпапку (`./model_cache/sentiment_analysis`), что предотвращает конфликты версий и упрощает очистку.

---

## ## Распространённые подводные камни и как их избежать

| Симптом | Вероятная причина | Решение |
|---------|-------------------|---------|
| **`PermissionError` при доступе к кешу** | Папка кеша принадлежит другому пользователю (часто на общих серверах) | Создайте папку вручную с правильными правами: `mkdir -p ./model_cache && chmod 775 ./model_cache` |
| **Модель никогда не появляется в `list_local()`** | `allow_auto_download` установлен в `"false"` и модель ещё не закеширована | Временно включите флаг, запустите один раз, затем при желании отключите |
| **Неожиданная версия модели** | Два разных репозитория имеют одинаковое имя, но разные файлы | Зафиксируйте точный ID репозитория (включая тег/коммит) или заблокируйте кеш, отключив авто‑загрузку после первой успешной загрузки |
| **Ошибки нехватки памяти** | Большие GGUF‑файлы на машине с недостаточным RAM/VRAM | Используйте меньшую модель (например, `Qwen2.5-1.5B`) или установите `cfg.device = "cpu"` для принудительного инференса на CPU |

---

## ## Полный скрипт, который можно скопировать и вставить

Ниже приведён полный готовый к запуску пример, включающий все описанные выше концепции. Сохраните его как `list_models_demo.py` и запустите командой `python list_models_demo.py`.

```python
# list_models_demo.py
import os
import aocr

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Create the Aspose AI instance
    # ------------------------------------------------------------------
    ai = aocr.AsposeAI()

    # ------------------------------------------------------------------
    # 2️⃣ Build configuration: enable auto download, set cache path,
    #    and point at a Hugging Face repo
    # ------------------------------------------------------------------
    cfg = aocr.AsposeAIModelConfig()
    cfg.allow_auto_download = "true"                               # enable auto download
    cfg.directory_model_path = os.path.abspath("./model_cache")   # how to set cache
    cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

    # ------------------------------------------------------------------
    # 3️⃣ Initialise the AI with the configuration
    # ------------------------------------------------------------------
    ai.initialize(cfg)

    # ------------------------------------------------------------------
    # 4️⃣ Verify cache location and list all locally available models
    # ------------------------------------------------------------------
    print("🗂️ Models cached at:", ai.get_local_path())
    print("📦 Available models:", ai.list_local())

    # ------------------------------------------------------------------
    # 5️⃣ (Optional) Run a quick inference using the first listed model
    # ------------------------------------------------------------------
    if ai.list_local():
        model_name = ai.list_local()[0]
        prompt = "Give a short summary of the Python GIL."
        response = ai.run_inference(model_name, prompt)
        print("\n🤖 Model response:", response)

if __name__ == "__main__":
    main()
```

**Запуск** выдаст вывод, похожий на предыдущий пример, а затем краткий ответ модели. Не стесняйтесь заменять запрос на любой другой — это самый быстрый способ проверить, что модель действительно пригодна после того, как вы **перечислили модели**.

---

## ## Итоги

Мы рассмотрели всё, что необходимо для **перечисления моделей** с помощью Aspose AI, от включения **auto download** до настройки постоянного **кеша** и загрузки **модели Hugging Face** по запросу. Основные выводы:

1. Создайте объект `AsposeAI` и `AsposeAIModelConfig`.  
2. Установите `allow_auto_download = "true"` и укажите `directory_model_path` в папку, которой вы управляете.  
3. Инициализируйте AI, затем вызовите `list_local()`, чтобы увидеть, что именно закешировано.  
4. Используйте полученное имя модели для инференса, и вы готовы создавать реальные приложения.

---

## Что дальше?

- **Экспериментировать с разными моделями** — замените `cfg.hugging_face_repo_id` на другой репозиторий и посмотрите, как изменится список.  
- **Тонкая настройка кеша**

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как пакетно обрабатывать изображения OCR со списком в Aspose.OCR для .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Как установить лицензию Aspose OCR и проверить её в Java](/ocr/english/java/ocr-basics/set-license/)
- [Как извлечь текст из изображения с помощью Aspose.OCR для .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}