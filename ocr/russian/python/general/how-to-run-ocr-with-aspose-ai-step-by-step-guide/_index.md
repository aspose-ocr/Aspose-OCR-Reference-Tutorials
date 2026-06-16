---
category: general
date: 2026-02-09
description: как запустить OCR с использованием Aspose AI и модели Hugging Face —
  узнать, как скачать модель Hugging Face, исправить ошибки OCR и освободить память
  GPU.
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: ru
og_description: Как запустить OCR с Aspose AI объясняется в первом абзаце — узнайте,
  как скачать модель Hugging Face, исправить ошибки OCR и освободить память GPU.
og_title: Как запустить OCR с Aspose AI – Полное руководство
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: Как запустить OCR с Aspose AI – пошаговое руководство
url: /ru/python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# как запустить OCR с Aspose AI – Полное руководство

Когда‑нибудь задумывались **как запустить OCR** на отсканированном счете и получить идеально чистые цифры без часов, потраченных на исправление опечаток? Вы не одиноки. Во многих реальных проектах сырой текст, полученный от классического OCR‑движка, всё ещё содержит посторонние символы, сломанные знаки валют или искажённые цифры — особенно когда исходное изображение шумное.  

Хорошая новость в том, что вы можете подключить LLM к Aspose OCR, загрузить модель Hugging Face «на лету» и позволить ИИ отполировать результат за вас. В этом руководстве мы пройдём весь конвейер, от загрузки модели (да, мы покажем, как **download hugging face model** автоматически) до освобождения ресурсов GPU после завершения. К концу вы получите воспроизводимый скрипт, который **corrects OCR errors**, работает быстро на скромном GPU и сам очищает за собой, чтобы не тратить память.

## Что вы узнаете

- Как настроить Aspose AI для получения модели **Qwen2.5‑3B‑Instruct‑GGUF** из Hugging Face.  
- Как запустить стандартный движок Aspose OCR на файле изображения.  
- Как использовать пользовательский LLM‑prompt, сохраняющий цифры и знаки валют.  
- Как освободить память GPU с помощью встроенной процедуры **free gpu memory**.  
- Как подстроить рабочий процесс под особые случаи, такие как много‑страничные PDF или слабые GPU.

> **Prerequisites** – Python 3.9+, пакет `aspose-ocr`, доступ в интернет для первой загрузки модели и GPU с минимум 4 ГБ VRAM (опционально, но рекомендуется). Если у вас нет GPU, скрипт автоматически переключится на CPU для оставшихся слоёв.

---

## Как запустить OCR и улучшить результаты

Ниже представлен полностью готовый к запуску Python‑скрипт. Сохраните его как `ocr_with_ai.py` и замените заполнители путей на свои файлы.

```python
# ocr_with_ai.py
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Configure the AI engine (download hugging face model)
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # auto‑download if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # tiny memory footprint
    gpu_layers=20,                                  # 20 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY/Models"  # optional custom folder
)
ai = AsposeAI(ai_config)

# -------------------------------------------------
# Step 2 – Load an image and run the classic OCR engine
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()   # returns plain‑text string

# -------------------------------------------------
# Step 3 – Register a custom LLM prompt (correct OCR errors)
# -------------------------------------------------
def financial_prompt():
    # Bias the model toward financial terminology
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# -------------------------------------------------
# Step 4 – Let the LLM polish the output
# -------------------------------------------------
corrected_text = ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Enhanced :", corrected_text)

# -------------------------------------------------
# Step 5 – Release resources (free gpu memory)
# -------------------------------------------------
ai.free_resources()
```

> **Pro tip:** Параметр `gpu_layers` позволяет решить, сколько трансформерных слоёв останутся на GPU. Если вы получаете ошибки «out‑of‑memory», уменьшите это число, а остальные слои будут работать на CPU — вы всё равно сможете **free gpu memory** позже с помощью `ai.free_resources()`.

### Ожидаемый вывод

Запуск скрипта на примере счёта выдаёт примерно следующее:

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

Обратите внимание, как ИИ исправил «O» в `$1O0.00` на правильный ноль, сохранив знак доллара. Это и есть суть **correct OCR errors** для финансовых документов.

---

## Загрузка модели Hugging Face – Что происходит «под капотом»?

Когда вы задаёте `allow_auto_download="true"`, обёртка Aspose AI проверяет `directory_model_path`. Если файлов модели там нет, она обращается к Hugging Face Hub, вытягивает **int8‑quantized** версию `Qwen2.5‑3B‑Instruct‑GGUF` и сохраняет её локально. Эта одноразовая загрузка обычно занимает менее 2 ГБ, что делает её возможной даже на скромных SSD.

> **Почему int8?** Квантование до 8‑бит резко снижает потребление памяти — это критично, когда после обработки вы хотите **free gpu memory**. Потери в точности минимальны, а для пост‑обработки OCR‑текста они практически незаметны.

Если вы предпочитаете размещать модель у себя, просто поместите файлы `.gguf` в `YOUR_DIRECTORY/Models`, и Aspose подхватит их без повторных запросов в интернет.

---

## Как освободить GPU – Лучшие практики

GPU‑ресурсы часто являются общим ресурсом на рабочих станциях. Оставшиеся в памяти тензоры после завершения скрипта могут вызвать ошибки «CUDA out of memory» для последующих задач. Вызов `ai.free_resources()` делает три вещи:

1. **Уничтожает базовый трансформер** — все веса, находящиеся в памяти GPU, освобождаются.  
2. **Очищает кэш PyTorch** — внутри вызывается `torch.cuda.empty_cache()`.  
3. **Удаляет временные файлы** — все кэши на диске, созданные во время загрузки, удаляются.

При необходимости вы также можете вручную вызвать `torch.cuda.empty_cache()`, если комбинируете Aspose AI с другими задачами PyTorch, но встроенный метод обычно достаточен.

---

## Пошаговое руководство (H2 с дополнительными ключевыми словами)

### Автоматическая загрузка модели Hugging Face

Конструктор `AsposeAIModelConfig` скрывает сложность работы с API Hugging Face. Просто убедитесь, что у вас есть доступ в интернет при первом запуске скрипта. После этого модель будет храниться в `YOUR_DIRECTORY/Models`, а последующие запуски начнутся мгновенно.

### Освобождение памяти GPU после инференса

Если вы запускаете это в длительно работающем сервисе (например, Flask‑API), вызывайте `ai.free_resources()` после каждого запроса. Это предотвращает утечки памяти и гарантирует, что следующий запрос сможет без проблем использовать тот же GPU.

### Коррекция OCR‑ошибок с помощью пользовательского Prompt

Наша функция `financial_prompt` возвращает словарь с единственным ключом `prompt`. Вы можете адаптировать её под любую область:

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

Поменяйте название функции в `ai.set_post_processor(...)`, и у вас будет конвейер **correct OCR errors** для медицинских записей.

### Как запустить OCR на много‑страничных PDF

Aspose OCR умеет работать с PDF «из коробки»:

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

После получения сырой строки тот же LLM‑пост‑процессор очистит текст каждой страницы. Дополнительный код не требуется.

### Когда нет GPU – Как освободить GPU (даже без него)

Даже на машинах только с CPU вызов `ai.free_resources()` безопасен. Он просто очищает внутренние кэши, что может освободить RAM. Поэтому совет **how to free gpu** применим везде: всегда убирайте за собой ресурсы.

---

## Распространённые подводные камни и их решения

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Out‑of‑Memory на GPU** | `gpu_layers` установлен слишком высоко для вашей видеокарты | Уменьшите `gpu_layers` до 10 или 5, оставшиеся слои запустятся на CPU |
| **Модель не скачивается** | Корпоративный фаервол блокирует HTTPS к huggingface.co | Скачайте модель вручную с другой сети, затем укажите `directory_model_path` на локальную папку |
| **Цифры искажаются** | Prompt недостаточно явно указывает сохранять цифры | Добавьте в prompt фразу «preserve all numeric values and currency symbols exactly as they appear» |
| **`free_resources` бросает исключение** | Используется устаревшая версия Aspose OCR | Обновите пакет до последней версии (`pip install --upgrade aspose-ocr`) |

---

## Полный пример в обзоре

Вот скрипт ещё раз, теперь с встроенными комментариями, поясняющими каждую строку для будущего использования:

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Configure AI – will auto‑download the model if needed
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,                     # adjust based on your GPU size
    directory_model_path=r"YOUR_DIRECTORY/Models"
)
ai = AsposeAI(ai_config)               # initialise the engine

# 2️⃣ Run classic OCR on an image (or PDF)
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()      # plain‑text result

# 3️⃣ Define a prompt that tells the LLM to keep numbers intact
def financial_prompt():
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# 4️⃣ Let the LLM clean the text
corrected_text = ai.run_postprocessor(raw_text)

# 5️⃣ Show before/after
print("Original :", raw_text)
print("Enhanced :", corrected_text)

# 6️⃣ Clean up – this frees GPU memory for the next run
ai.free_resources()
```

---

## Заключение

Мы рассмотрели **how to run OCR** с Aspose, загрузку модели Hugging Face по требованию, создание prompt, который **corrects OCR errors**, и, наконец, **free gpu memory**, чтобы ваша рабочая станция оставалась отзывчивой. Весь процесс помещён в один автономный Python‑файл — без внешних скриптов, без ручного управления моделями и без оставшихся в памяти GPU‑выделений.

Дальнейшие шаги? Попробуйте заменить `financial_prompt` на

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}