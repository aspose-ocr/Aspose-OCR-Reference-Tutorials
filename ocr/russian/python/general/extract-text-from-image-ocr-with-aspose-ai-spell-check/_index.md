---
category: general
date: 2026-05-03
description: Извлекать текст из изображения с помощью Aspose OCR и AI‑проверки орфографии.
  Узнайте, как выполнять OCR изображения, загружать изображение для OCR, распознавать
  текст из счета и освобождать ресурсы GPU.
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: ru
og_description: Извлекать текст из изображения с помощью Aspose OCR и AI‑проверки
  орфографии. Пошаговое руководство, охватывающее, как выполнять OCR изображения,
  загружать изображение для OCR и освобождать ресурсы GPU.
og_title: Извлечение текста из изображения – Полное руководство по OCR и проверке
  орфографии
tags:
- OCR
- Aspose
- AI
- Python
title: Извлечение текста из изображения — OCR с Aspose AI Spell‑Check
url: /ru/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# извлечение текста из изображения – Полное руководство по OCR и проверке орфографии

Когда‑то вам нужно было **извлечь текст из изображения**, но вы не знали, какая библиотека обеспечит и скорость, и точность? Вы не одиноки. Во многих реальных проектах — будь то обработка счетов, оцифровка чеков или сканирование контрактов — получение чистого, поискового текста с картинки является первой преградой.

Хорошая новость: Aspose OCR в паре с лёгкой моделью Aspose AI справится с этой задачей в несколько строк кода на Python. В этом руководстве мы пройдёмся по **как выполнить OCR изображения**, правильно загрузим картинку, запустим встроенный пост‑процессор проверки орфографии и, наконец, **освободим ресурсы GPU**, чтобы приложение оставалось экономным по памяти.

К концу этого руководства вы сможете **распознавать текст со счетов**, автоматически исправлять типичные ошибки OCR и поддерживать ваш GPU в чистоте для следующей партии.

---

## Что понадобится

- Python 3.9 или новее (код использует type hints, но работает и в более ранних версиях 3.x)
- пакеты `aspose-ocr` и `aspose-ai` (устанавливаются через `pip install aspose-ocr aspose-ai`)
- GPU с поддержкой CUDA — опционально; при отсутствии скрипт переключится на CPU.
- Пример изображения, например `sample_invoice.png`, размещённый в папке, к которой вы можете обратиться.

Никаких тяжёлых ML‑фреймворков, никаких массивных загрузок моделей — только небольшая Q4‑K‑M квантизированная модель, которая удобно помещается на большинстве GPU.

---

## Шаг 1: Инициализация OCR‑движка – extract text from image

Первое, что нужно сделать, — создать экземпляр `OcrEngine` и указать ожидаемый язык. Здесь мы выбираем английский и запрашиваем вывод в виде простого текста, что идеально подходит для последующей обработки.

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**Почему это важно:** Указание языка сужает набор символов, повышая точность. Режим простого текста удаляет информацию о макете, которая обычно не нужна, когда нужно просто извлечь текст из изображения.

---

## Шаг 2: Загрузка изображения для OCR – how to OCR image

Теперь передаём движку реальную картинку. Помощник `Image.load` понимает распространённые форматы (PNG, JPEG, TIFF) и абстрагирует особенности файлового ввода‑вывода.

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**Совет:** Если исходные изображения большие, подумайте о их масштабировании перед передачей в движок; меньшие размеры могут снизить потребление памяти GPU без потери качества распознавания.

---

## Шаг 3: Настройка модели Aspose AI – recognize text from invoice

Aspose AI поставляется с крошечной моделью GGUF, которую можно автоматически загрузить. В примере используется репозиторий `Qwen2.5‑3B‑Instruct‑GGUF`, квантизированный до `q4_k_m`. Мы также указываем runtime выделить 20 слоёв на GPU, что балансирует скорость и использование VRAM.

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**Что происходит за кулисами:** Квантизированная модель занимает примерно 1,5 ГБ на диске, что является лишь частью полной модели, но всё‑равно сохраняет достаточную языковую нюансировку для выявления типичных опечаток OCR.

---

## Шаг 4: Инициализация AsposeAI и подключение пост‑процессора проверки орфографии

Aspose AI включает готовый пост‑процессор проверки орфографии. Подключив его, каждый результат OCR будет автоматически очищен.

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**Зачем нужен пост‑процессор?** OCR‑движки часто читают «Invoice» как «Invo1ce» или «Total» как «T0tal». Проверка орфографии запускает лёгкую языковую модель над полученной строкой и исправляет такие ошибки без необходимости писать собственный словарь.

---

## Шаг 5: Запуск пост‑процессора проверки орфографии над результатом OCR

Когда всё соединено, один вызов выдаёт исправленный текст. Мы также выводим как оригинальную, так и очищенную версии, чтобы вы могли увидеть улучшение.

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

Типичный вывод для счета может выглядеть так:

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

Обратите внимание, как «Invo1ce» превратилось в правильное слово «Invoice». Это сила встроенной AI‑проверки орфографии.

---

## Шаг 6: Освобождение ресурсов GPU – release gpu resources safely

Если вы запускаете это в длительно работающем сервисе (например, веб‑API, обрабатывающем десятки счетов в минуту), необходимо освобождать контекст GPU после каждой партии. Иначе появятся утечки памяти и в конце концов ошибки «CUDA out of memory».

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**Профессиональный совет:** Вызывайте `free_resources()` внутри блока `finally` или контекстного менеджера, чтобы он всегда исполнялся, даже при возникновении исключения.

---

## Полный рабочий пример

Собрав все части вместе, вы получаете автономный скрипт, который можно вставить в любой проект.

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

Сохраните файл, поправьте путь к вашему изображению и запустите `python extract_text_from_image.py`. Вы должны увидеть очищенный текст счета, выведенный в консоль.

---

## Часто задаваемые вопросы (FAQ)

**Q: Работает ли это на машинах без GPU?**  
A: Абсолютно. Если GPU не обнаружен, Aspose AI переключается на выполнение на CPU, хотя будет работать медленнее. Вы можете принудительно задать CPU, установив `model_cfg.gpu_layers = 0`.

**Q: Что если мои счета на другом языке, не на английском?**  
A: Измените `ocr_engine.language` на соответствующее значение enum (например, `aocr.Language.Spanish`). Модель проверки орфографии многоязычная, но результаты могут быть лучше с языково‑специфичной моделью.

**Q: Можно ли обрабатывать несколько изображений в цикле?**  
A: Да. Просто перенесите шаги загрузки, распознавания и пост‑обработки внутрь цикла `for`. Не забудьте вызвать `ocr_ai.free_resources()` после цикла или после каждой партии, если переиспользуете один и тот же экземпляр AI.

**Q: Какой размер загрузки модели?**  
A: Около 1,5 ГБ для квантизированной версии `q4_k_m`. После первого запуска она кэшируется, так что последующие исполнения происходят мгновенно.

---

## Заключение

В этом руководстве мы продемонстрировали, как **извлечь текст из изображения** с помощью Aspose OCR, настроить крошечную AI‑модель, применить пост‑процессор проверки орфографии и безопасно **освободить ресурсы GPU**. Рабочий процесс охватывает всё — от загрузки картинки до очистки после себя, предоставляя надёжный конвейер для сценариев **распознавания текста со счетов**.

Следующий шаг? Попробуйте заменить проверку орфографии на пользовательскую модель извлечения сущностей.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}