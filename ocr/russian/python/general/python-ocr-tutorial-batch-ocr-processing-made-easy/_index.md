---
category: general
date: 2026-05-03
description: Учебник по OCR на Python, показывающий, как загружать PNG‑изображения,
  распознавать текст на изображении и использовать бесплатные AI‑ресурсы для пакетной
  обработки OCR.
draft: false
keywords:
- python ocr tutorial
- batch ocr processing
- free ai resources
- load png image
- recognize text from image
language: ru
og_description: Учебник по OCR на Python проведет вас через загрузку PNG‑изображений,
  распознавание текста на изображении и работу с бесплатными AI‑ресурсами для пакетной
  обработки OCR.
og_title: Учебник по OCR на Python – Быстрый пакетный OCR с бесплатными AI‑ресурсами
tags:
- OCR
- Python
- AI
title: Учебник по OCR на Python — Пакетная обработка OCR стала простой
url: /ru/python/general/python-ocr-tutorial-batch-ocr-processing-made-easy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Tutorial – Batch OCR Processing Made Easy

Когда‑то вам нужен **python ocr tutorial**, который действительно позволяет выполнять OCR для десятков PNG‑файлов, не теряя волосы? Вы не одиноки. В реальных проектах часто требуется **load png image** файлы, передать их движку и потом освободить AI‑ресурсы, когда работа завершена.  

В этом руководстве мы пройдем через полностью готовый к запуску пример, показывающий, как **recognize text from image** файлов, обрабатывать их пакетно и освобождать память AI. К концу вы получите автономный скрипт, который можно вставить в любой проект — без лишних деталей, только самое необходимое.

## What You’ll Need

- Python 3.10 или новее (используемый синтаксис опирается на f‑strings и type hints)  
- OCR‑библиотека, предоставляющая метод `engine.recognize` — для демонстрации будем считать, что существует вымышленный пакет `aocr`, но вы можете заменить его на Tesseract, EasyOCR и т.п.  
- Модуль‑помощник `ai`, показанный в кодовом фрагменте (он отвечает за инициализацию модели и очистку ресурсов)  
- Папка, заполненная PNG‑файлами, которые нужно обработать  

Если у вас нет `aocr` или `ai`, их можно имитировать с помощью заглушек — см. раздел «Optional Stubs» в конце.

## Step 1: Initialize the AI Engine (Free AI Resources)

Прежде чем подавать изображение в OCR‑конвейер, базовая модель должна быть готова. Инициализация один раз экономит память и ускоряет пакетные задания.

```python
# step_1_initialize.py
import ai                # hypothetical helper that wraps the AI model
import aocr               # OCR library

def init_engine(config_path: str = "config.yaml"):
    """
    Initialize the AI engine if it hasn't been set up yet.
    This uses free AI resources – the engine will be released later.
    """
    if not ai.is_initialized():
        ai.initialize(config_path)   # auto‑initialize with the provided configuration
    else:
        print("Engine already initialized.")
```

**Why this matters:**  
Вызов `ai.initialize` для каждого изображения заново будет выделять GPU‑память каждый раз, в итоге скрипт может упасть. Проверка `ai.is_initialized()` гарантирует единственное выделение — это и есть принцип «free AI resources».

## Step 2: Load PNG Image Files for Batch OCR Processing

Теперь собираем все PNG‑файлы, которые хотим пропустить через OCR. Использование `pathlib` делает код независимым от ОС.

```python
# step_2_load_images.py
from pathlib import Path
from typing import List

def collect_png_paths(directory: str) -> List[Path]:
    """
    Scan `directory` and return a list of Path objects pointing to PNG files.
    """
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files
```

**Edge case:**  
Если в папке есть файлы не‑PNG (например, JPEG), они будут проигнорированы, и `engine.recognize` не «запнётся» из‑за неподдерживаемого формата.

## Step 3: Run OCR on Each Image and Apply Post‑Processing

С готовым движком и списком файлов можно перебрать изображения, извлечь сырой текст и передать его пост‑процессору, который убирает типичные артефакты OCR (например, лишние разрывы строк).

```python
# step_3_ocr_batch.py
import aocr
import ai
from pathlib import Path
from typing import List

def ocr_batch(image_paths: List[Path]) -> List[str]:
    """
    Perform OCR on each PNG image and return a list of cleaned strings.
    """
    results = []
    for image_path in image_paths:
        # Load the image – aocr.Image.load abstracts away Pillow/OpenCV details
        img = aocr.Image.load(str(image_path))
        
        # Recognize raw text
        raw_text = engine.recognize(img)
        
        # Refine the raw OCR output using the AI post‑processor
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters extracted.")
    
    return results
```

**Why we separate loading from recognition:**  
`aocr.Image.load` может выполнять ленивое декодирование, что быстрее при больших партиях. Явный шаг загрузки также упрощает замену библиотеки изображений, если позже понадобится поддержка JPEG или TIFF.

## Step 4: Clean Up – Free AI Resources After the Batch

После завершения пакетной обработки необходимо освободить модель, чтобы избежать утечек памяти, особенно на машинах с GPU.

```python
# step_4_cleanup.py
import ai

def release_resources():
    """
    Free any allocated AI resources. Safe to call multiple times.
    """
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources have been released.")
    else:
        print("No AI resources were allocated.")
```

## Putting It All Together – The Complete Script

Ниже один файл, который соединяет четыре шага в единый рабочий процесс. Сохраните его как `batch_ocr.py` и запустите из командной строки.

```python
# batch_ocr.py
"""
Python OCR tutorial – end‑to‑end batch OCR processing.
Loads PNG images, runs OCR, post‑processes results, and frees AI resources.
"""

import sys
from pathlib import Path
import ai
import aocr

# ----------------------------------------------------------------------
# Helper functions (copied from the steps above)
# ----------------------------------------------------------------------
def init_engine(cfg: str = "config.yaml"):
    if not ai.is_initialized():
        ai.initialize(cfg)
    else:
        print("Engine already initialized.")

def collect_png_paths(directory: str):
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files

def ocr_batch(image_paths):
    results = []
    for image_path in image_paths:
        img = aocr.Image.load(str(image_path))
        raw_text = engine.recognize(img)
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters.")
    return results

def release_resources():
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources released.")
    else:
        print("No resources to release.")

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-png>")
        sys.exit(1)

    image_dir = sys.argv[1]

    try:
        init_engine()
        png_paths = collect_png_paths(image_dir)
        texts = ocr_batch(png_paths)

        # Optional: write results to a single text file
        output_file = Path("ocr_results.txt")
        with output_file.open("w", encoding="utf-8") as f:
            for path, txt in zip(png_paths, texts):
                f.write(f"--- {path.name} ---\n")
                f.write(txt + "\n\n")
        print(f"All results saved to {output_file.resolve()}")
    finally:
        release_resources()
```

### Expected Output

Запуск скрипта в папке с тремя PNG‑файлами может вывести:

```
Engine already initialized.
Found 3 PNG image(s) to process.
Processed invoice1.png: 452 characters.
Processed receipt2.png: 317 characters.
Processed flyer3.png: 689 characters.
All results saved to /home/user/ocr_results.txt
AI resources released.
```

Файл `ocr_results.txt` будет содержать чёткий разделитель для каждого изображения, за которым следует очищенный OCR‑текст.

## Optional Stubs for aocr & ai (If You Don’t Have Real Packages)

Если хотите проверить поток без тяжёлых OCR‑библиотек, можно создать минимальные mock‑модули:

```python
# aocr/__init__.py
class Image:
    @staticmethod
    def load(path):
        return f"ImageObject({path})"

def dummy_recognize(image):
    return "Raw OCR output for " + str(image)

engine = type("Engine", (), {"recognize": dummy_recognize})()
```

```python
# ai/__init__.py
_state = {"initialized": False}

def is_initialized():
    return _state["initialized"]

def initialize(cfg):
    print(f"Initializing AI engine with {cfg}")
    _state["initialized"] = True

def run_postprocessor(text):
    # Very naive cleanup: strip extra spaces
    return " ".join(text.split())

def free_resources():
    print("Freeing AI resources")
    _state["initialized"] = False
```

Поместите эти папки рядом с `batch_ocr.py`, и скрипт выполнится, выводя имитационные результаты.

## Pro Tips & Common Pitfalls

- **Memory spikes:** При обработке тысяч высокоразрешённых PNG‑файлов подумайте о их масштабировании перед OCR. `aocr.Image.load` часто принимает аргумент `max_size`.  
- **Unicode handling:** Всегда открывайте файл вывода с `encoding="utf-8"`; OCR‑движки могут генерировать символы вне ASCII.  
- **Parallelism:** Для CPU‑ограниченного OCR можно обернуть `ocr_batch` в `concurrent.futures.ThreadPoolExecutor`. Главное — сохранять один экземпляр `ai`; создание множества потоков, каждый из которых вызывает `ai.initialize`, разрушит цель «free AI resources».  
- **Error resilience:** Оберните цикл по изображениям в `try/except`, чтобы один повреждённый PNG не прерывал всю пакетную обработку.

## Conclusion

Теперь у вас есть **python ocr tutorial**, демонстрирующий, как **load png image** файлы, выполнять **batch OCR processing** и ответственно управлять **free AI resources**. Полный, готовый к запуску пример показывает, как **recognize text from image** объектов и как правильно освобождать ресурсы, так что вы можете скопировать‑вставить его в свои проекты без поиска недостающих частей.

Готовы к следующему шагу? Попробуйте заменить заглушки `aocr` и `ai` реальными библиотеками, например `pytesseract` и `torchvision`. Вы также можете расширить скрипт, чтобы выводить JSON, отправлять результаты в базу данных или интегрировать с облачным хранилищем. Возможности безграничны — приятного кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}