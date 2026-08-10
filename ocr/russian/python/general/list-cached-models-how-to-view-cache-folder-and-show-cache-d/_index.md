---
category: general
date: 2026-02-22
description: Узнайте, как вывести список кэшированных моделей и быстро отобразить
  каталог кэша на вашем компьютере. Включает шаги по просмотру папки кэша и управлению
  локальным хранилищем моделей ИИ.
draft: false
keywords:
- list cached models
- show cache directory
- how to view cache folder
- AI model cache
- local model storage
language: ru
og_description: Узнайте, как вывести список кэшированных моделей, показать каталог
  кэша и просмотреть папку кэша в несколько простых шагов. Включён полный пример на
  Python.
og_title: список кэшированных моделей – краткое руководство по просмотру каталога
  кэша
tags:
- AI
- caching
- Python
- development
title: список кэшированных моделей – как просмотреть папку кэша и показать каталог
  кэша
url: /ru/python/general/list-cached-models-how-to-view-cache-folder-and-show-cache-d/
---

.

Now produce final output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# список кэшированных моделей – быстрое руководство по просмотру каталога кэша

Когда‑то задавались вопросом, как **просмотреть список кэшированных моделей** на своей рабочей станции, не копаясь в непонятных папках? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда нужно проверить, какие AI‑модели уже сохранены локально, особенно если место на диске ограничено. Хорошая новость: всего в нескольких строках кода вы можете как **просмотреть список кэшированных моделей**, так и **показать каталог кэша**, получив полную видимость своей папки кэша.

В этом руководстве мы пройдёмся по автономному Python‑скрипту, который делает именно это. К концу вы будете знать, как увидеть папку кэша, где она находится в разных ОС, и как получить аккуратно отформатированный список каждой загруженной модели. Никакой внешней документации, никаких догадок — только чистый код и объяснения, которые вы можете скопировать‑вставить прямо сейчас.

## Что вы узнаете

- Как инициализировать AI‑клиент (или заглушку), предоставляющий утилиты кэширования.  
- Точные команды для **просмотра списка кэшированных моделей** и **показа каталога кэша**.  
- Где находится кэш в Windows, macOS и Linux, чтобы при желании перейти к нему вручную.  
- Советы по обработке крайних случаев, таких как пустой кэш или пользовательский путь к кэшу.  

**Предварительные требования** — нужен Python 3.8+ и pip‑устанавливаемый AI‑клиент, реализующий `list_local()`, `get_local_path()` и, опционально, `clear_local()`. Если у вас ещё нет такого клиента, в примере используется мок‑класс `YourAIClient`, который вы можете заменить реальным SDK (например, `openai`, `huggingface_hub` и т.д.).  

Готовы? Поехали.

## Шаг 1: Настройка AI‑клиента (или мока)

Если у вас уже есть объект клиента, пропустите этот блок. В противном случае создайте небольшую заглушку, имитирующую интерфейс кэширования. Это позволяет скрипту работать даже без реального SDK.

```python
# step_1_client_setup.py
import os
from pathlib import Path

class YourAIClient:
    """
    Minimal mock of an AI client that stores downloaded models in a
    directory called `.ai_cache` inside the user's home folder.
    """
    def __init__(self, cache_dir: Path | None = None):
        # Use a custom path if supplied, otherwise default to ~/.ai_cache
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        """Return a list of model folder names that exist in the cache."""
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        """Absolute path to the cache directory."""
        return str(self.cache_dir.resolve())

    # Optional helper for demonstration purposes
    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# Initialize the client (replace with real client if you have one)
ai = YourAIClient()
# Populate with dummy data the first time you run the script
if not ai.list_local():
    ai._populate_dummy_models()
```

> **Pro tip:** Если у вас уже есть реальный клиент (например, `from huggingface_hub import HfApi`), просто замените вызов `YourAIClient()` на `HfApi()` и убедитесь, что методы `list_local` и `get_local_path` существуют или обёрнуты соответствующим образом.

## Шаг 2: **list cached models** – получить и отобразить их

Теперь, когда клиент готов, мы можем попросить его перечислить всё, что он знает о локальном хранилище. Это ядро нашей операции **list cached models**.

```python
# step_2_list_models.py
print("Cached models:")
for model_name in ai.list_local():
    print(" -", model_name)
```

**Ожидаемый вывод** (с фиктивными данными из шага 1):

```
Cached models:
 - model_1
 - model_2
 - model_3
```

Если кэш пуст, вы увидите просто:

```
Cached models:
```

Эта пустая строка говорит о том, что ничего ещё не сохранено — удобно при написании скриптов очистки.

## Шаг 3: **show cache directory** – где находится кэш?

Знание пути часто составляет половину задачи. Разные ОС размещают кэши в разных местах по умолчанию, а некоторые SDK позволяют переопределять его через переменные окружения. Следующий фрагмент выводит абсолютный путь, чтобы вы могли `cd` в него или открыть в проводнике.

```python
# step_3_show_path.py
print("\nCache directory:", ai.get_local_path())
```

**Типичный вывод** в Unix‑подобной системе:

```
Cache directory: /home/youruser/.ai_cache
```

В Windows вы можете увидеть что‑то вроде:

```
Cache directory: C:\Users\YourUser\.ai_cache
```

Теперь вы точно знаете, **как просмотреть папку кэша** на любой платформе.

## Шаг 4: Соберите всё вместе — один исполняемый скрипт

Ниже полностью готовая к запуску программа, объединяющая три шага. Сохраните её как `view_ai_cache.py` и выполните `python view_ai_cache.py`.

```python
# view_ai_cache.py
import os
from pathlib import Path

class YourAIClient:
    """Simple mock client exposing cache‑related utilities."""
    def __init__(self, cache_dir: Path | None = None):
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        return str(self.cache_dir.resolve())

    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    # Initialize (replace with real client if available)
    ai = YourAIClient()

    # Populate dummy data only on first run – remove this in production
    if not ai.list_local():
        ai._populate_dummy_models()

    # Step 1: list cached models
    print("Cached models:")
    for model_name in ai.list_local():
        print(" -", model_name)

    # Step 2: show cache directory
    print("\nCache directory:", ai.get_local_path())
```

Запустите её, и вы мгновенно увидите как список кэшированных моделей, **так и** расположение каталога кэша.

## Крайние случаи и варианты

| Ситуация | Что делать |
|-----------|------------|
| **Пустой кэш** | Скрипт выведет «Cached models:» без записей. Можно добавить условное предупреждение: `if not models: print("⚠️ No models cached yet.")` |
| **Пользовательский путь к кэшу** | Передайте путь при создании клиента: `YourAIClient(cache_dir=Path("/tmp/my_ai_cache"))`. Вызов `get_local_path()` отразит эту кастомную локацию. |
| **Ошибки доступа** | На ограниченных машинах клиент может бросить `PermissionError`. Оберните инициализацию в `try/except` и переключитесь на директорию, доступную пользователю. |
| **Использование реального SDK** | Замените `YourAIClient` на реальный класс клиента и убедитесь, что имена методов совпадают. Многие SDK предоставляют атрибут `cache_dir`, который можно прочитать напрямую. |

## Pro‑советы по управлению кэшем

- **Периодическая очистка:** Если вы часто скачиваете большие модели, запланируйте cron‑задачу, вызывающую `shutil.rmtree(ai.get_local_path())` после подтверждения, что они больше не нужны.  
- **Мониторинг использования диска:** Используйте `du -sh $(ai.get_local_path())` в Linux/macOS или `Get-ChildItem -Recurse | Measure-Object -Property Length -Sum` в PowerShell, чтобы следить за размером.  
- **Версионированные папки:** Некоторые клиенты создают подпапки для каждой версии модели. При **list cached models** вы увидите каждую версию как отдельный элемент — используйте это для удаления старых ревизий.  

## Визуальный обзор

![скриншот списка кэшированных моделей](https://example.com/images/list-cached-models.png "список кэшированных моделей – вывод консоли, показывающий модели и путь к кэшу")

*Alt text:* *список кэшированных моделей – вывод консоли, отображающий имена кэшированных моделей и путь к каталогу кэша.*

## Заключение

Мы рассмотрели всё, что нужно для **list cached models**, **show cache directory** и в целом **как просмотреть папку кэша** на любой системе. Краткий скрипт демонстрирует полное, готовое к запуску решение, объясняет **почему** каждый шаг важен и предлагает практические советы для реального применения.  

Далее вы можете исследовать **как программно очистить кэш**, либо интегрировать эти вызовы в более крупный конвейер развертывания, проверяющий доступность моделей перед запуском инференса. В любом случае у вас теперь есть фундамент для уверенного управления локальным хранилищем AI‑моделей.

Есть вопросы по конкретному AI‑SDK? Оставляйте комментарий ниже, и удачной кэш‑работы!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}