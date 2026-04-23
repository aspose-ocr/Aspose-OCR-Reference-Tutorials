---
category: general
date: 2026-01-07
description: Как выполнять OCR и извлекать текст из изображения для обработки счетов.
  Узнайте, как улучшить точность OCR, загрузить изображение для OCR и эффективно обрабатывать
  OCR счетов.
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: ru
og_description: Как пошагово выполнять OCR на счетах‑фактурах. Извлекать текст из
  изображения, повышать точность OCR и загружать изображение для OCR с помощью Aspose
  AI.
og_title: Как запустить OCR для счетов — Полное руководство по Python
tags:
- OCR
- Python
- Image Processing
title: Как выполнить OCR на счетах‑фактурах – извлечь текст из изображения с помощью
  Python
url: /ru/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнить OCR на счетах‑фактурах – извлечь текст из изображения с помощью Python

Когда‑нибудь задумывались **как выполнить OCR** на отсканированном счете‑фактуре и получить чистый, индексируемый текст? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда необработанный вывод OCR полон опечаток, разорванных переносов строк и отсутствующей пунктуации. В этом руководстве мы пройдем через полное решение, которое не только **извлекает текст из изображения**, но и **повышает точность OCR** с помощью пост‑обработки моделью Aspose AI.

Вы увидите, как **загрузить изображение для OCR**, запустить встроенный движок и затем применить лёгкую проверку орфографии, делая результат готовым для последующего анализа. К концу у вас будет переиспользуемый скрипт, который можно внедрить в любой конвейер обработки счетов‑фактур.

> **Что понадобится**  
> * Python 3.9 или новее  
> * Пакеты `aspose-ocr` и `aspose-ai` (устанавливаются через `pip`)  
> * Изображение счёта‑фактуры (PNG, JPEG или TIFF) – в примере будем использовать `sample_invoice.png`  
> * Необязательно: GPU с минимум 4 ГБ VRAM для ускорения вывода модели (скрипт работает и на CPU)

---

## Шаг 1: Установить необходимые пакеты и подготовить окружение

Прежде чем мы сможем **загрузить изображение для OCR**, необходимо убедиться, что требуемые библиотеки доступны. Движок Aspose OCR поставляется с простым обёрткой для Python, а AI‑пост‑процессор использует квантизированную модель Hugging Face.

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **Pro tip:** Если планируете использовать ускорение GPU, установите `torch` с поддержкой CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`).

---

## Шаг 2: Загрузить изображение счёта‑фактуры

Загрузка изображения проста, но стоит упомянуть, почему мы явно задаём путь как raw‑строку (`r"..."`). Это предотвращает случайные ошибки с escape‑символами в путях Windows.

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*Почему это важно:* Использование `ocr.Image.load` гарантирует, что изображение будет предварительно обработано (бинаризация, исправление наклона) согласно оптимальным настройкам Aspose, что уже **повышает точность OCR** до любой AI‑магии.

---

## Шаг 3: Запустить встроенный OCR‑движок

Теперь мы действительно **запускаем OCR** и получаем необработанный текст. Этот шаг показывает типичный вывод, который вы получаете от базового OCR‑запуска — часто это хаос переносов строк и случайные опечатки.

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**Типичный необработанный вывод** (усечён для краткости):

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Вы можете заметить, что слово «Invoice» появляется как «Invo1ce» или что пунктуация отсутствует. Здесь и вступает в действие AI‑пост‑процессор.

---

## Шаг 4: Настроить модель Aspose AI

Модель AI, которую мы будем использовать, — **Qwen2.5‑3B‑Instruct‑GGUF**, лёгкая LLM с инструктивной настройкой, комфортно работающая на средне‑мощном GPU. Ниже приведён конфиг, указывающий Aspose, где загрузить модель, сколько слоёв держать на GPU и размер контекста для обработки длинных абзацев.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **Почему такой конфиг?**  
> * `gpu_layers=30` балансирует скорость и память — большая часть вывода происходит на GPU, а оставшиеся слои остаются на CPU, чтобы избежать ошибок OOM.  
> * `context_size=4096` гарантирует, что модель видит весь счёт‑фактуру целиком, предотвращая усечение важных полей.

---

## Шаг 5: Создать простой пост‑процессор проверки орфографии

Мы обернём вызов AI в небольшую функцию `simple_spell_check`. Промпт преднамеренно лаконичен: «Correct spelling and punctuation:» (Исправьте орфографию и пунктуацию) — за которым следует необработанный OCR‑текст. Модель возвращает очищенную версию.

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**Как это работает:** `ai.run_prompt` отправляет промпт в локально загруженную LLM, которая затем возвращает одну **строку** с исправленной орфографией, правильной пунктуацией и более естественным расположением переносов строк.

---

## Шаг 6: Применить пост‑процессор к необработанному OCR‑тексту

Теперь происходит магия. Мы передаём необработанный вывод OCR в наш пост‑процессор и **печатаем** улучшенный результат.

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**Пример улучшенного вывода**:

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Обратите внимание на исправленное написание «Invoice», правильное использование двоеточий и согласованные переносы строк — именно то, что нужно для надёжного последующего парсинга.

---

## Шаг 7: Освободить ресурсы

И OCR‑движок, и AI‑модель выделяют нативные ресурсы. Хорошая практика — освободить их после завершения работы, особенно в длительно работающих сервисах.

```python
ai.free_resources()
engine.dispose()
```

---

## Полный скрипт — готов к использованию

Ниже представлен полностью готовый к запуску скрипт, объединяющий все шаги. Сохраните его как `invoice_ocr.py`, замените `YOUR_DIRECTORY` на папку с изображением счёта‑фактуры и запустите командой `python invoice_ocr.py`.

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

Запустите скрипт, и вы увидите как «шумный» необработанный вывод OCR, так и «полированный», **улучшенный по точности OCR**, вариант рядом.

---

## Часто задаваемые вопросы и особые случаи

### 1. Что если моё изображение счёта‑фактуры — многостраничный PDF?

Aspose OCR может напрямую загружать страницы PDF. Замените строку загрузки изображения на:

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

Итерируйте `page_index`, чтобы последовательно обрабатывать каждую страницу.

### 2. Мой GPU заканчивает память — могу ли я использовать только CPU?

Конечно. Установите `gpu_layers=0` в `AsposeAIModelConfig`. Модель будет работать полностью на CPU, что медленнее, но безопасно для слабого железа.

### 3. Как обрабатывать счета‑фактуры не на английском?

Подмените идентификатор репозитория модели на модель, специфичную для языка, например `"mistralai/Mistral-7B-Instruct-v0.2"` для многоязычной поддержки. Остальная часть конвейера остаётся без изменений.

### 4. Можно ли цепочкой применять несколько пост‑процессоров (например, форматировать даты, извлекать суммы)?

Да. `ai.set_post_processor` принимает список вызываемых объектов. Пример:

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

Сначала будет выполнена проверка орфографии, затем извлечение итоговых сумм.

---

## Советы по производительности и лучшие практики

| Совет | Почему это помогает |
|------|----------------------|
| **Обрабатывать несколько счетов пакетно** — загружайте их в список и проходите в цикле. | Снижает накладные расходы интерпретатора Python и держит модель «тёплой» в памяти. |
| **Кешировать модель** — избегайте повторного вызова `initialize` в веб‑сервисе. | Загрузка модели может занимать ~30 секунд; кеширование даёт мгновенный отклик. |
| **Изменять размер больших изображений** до ширины 1500 px перед OCR. | Меньшие изображения ускоряют как OCR, так и AI‑вывод без потери точности. |
| **Установить `allow_auto_download="false"` в продакшене** — поставляйте модель вместе с деплоем. | Гарантирует детерминированное время старта и избегает проблем с сетью. |

---

## Заключение

Мы рассмотрели **как выполнить OCR** на счетах‑фактурах, от загрузки изображения до полировки результата с помощью AI‑проверки орфографии. Следуя этим шагам, вы сможете надёжно **извлекать текст из изображения**, **повышать точность OCR** и без проблем **обрабатывать OCR‑счета** в любом Python‑ориентированном рабочем процессе.

Попробуйте скрипт на разных макетах счетов — может быть, на рукописных чеках или отсканированных контрактах. Тот же конвейер адаптируется с минимальными изменениями, доказывая, что хорошо построенный OCR + AI‑комбо — универсальный инструмент для любой задачи автоматизации документов.

Если руководство оказалось полезным, поделитесь им с коллегами или поставьте звёздочку репозиторию, где размещены пакеты Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}