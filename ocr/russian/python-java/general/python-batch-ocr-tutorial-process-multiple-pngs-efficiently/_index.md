---
category: general
date: 2026-06-22
description: Учебник по пакетному OCR на Python, показывающий, как выполнить многопоточный
  OCR в папке с PNG‑изображениями с использованием Tesseract и pathlib. Узнайте, как
  быстро выполнять пакетный OCR изображений в Python.
draft: false
keywords:
- python batch ocr tutorial
- multithreaded OCR in Python
- tesseract OCR batch processing
- pathlib image handling
- OCR thread count optimization
language: ru
og_description: Python‑batch‑OCR‑урок проведёт вас через полностью готовый скрипт,
  который обрабатывает множество PNG‑файлов с помощью Tesseract, используя несколько
  потоков.
og_title: Python пакетный OCR‑урок – быстрый многопоточный OCR для PNG‑изображений
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  headline: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  type: TechArticle
- description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  name: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  steps:
  - name: '**Collects** every PNG with **pathlib image handling**.'
    text: '**Collects** every PNG with **pathlib image handling**.'
  - name: '**Spins up** a **multithreaded OCR in Python** worker pool.'
    text: '**Spins up** a **multithreaded OCR in Python** worker pool.'
  - name: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
    text: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
  - name: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
    text: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
  type: HowTo
tags:
- OCR
- Python
- Batch Processing
title: 'Учебник по пакетному OCR на Python: эффективная обработка нескольких PNG.'
url: /ru/python-java/general/python-batch-ocr-tutorial-process-multiple-pngs-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# python batch ocr tutorial – Быстрый многопоточный OCR для PNG‑изображений

Задумывались когда‑нибудь, как **python batch ocr tutorial** пройтись по сотням скриншотов PNG, не позволяя процессору перегреться? Вы не одиноки. Независимо от того, оцифровываете ли вы сканированные формы, извлекаете текст из чеков или создаёте поисковый архив, надёжный пакетный OCR‑конвейер экономит часы.

В этом руководстве мы создадим небольшой, но мощный скрипт, который собирает каждый `*.png` в папке, передаёт их Tesseract через многопоточный процессор и сохраняет результаты в виде простого текста в аккуратный каталог вывода. Никаких загадочных библиотек — только `pathlib`, `concurrent.futures` и проверенный `pytesseract`. К концу вы получите **python batch ocr tutorial**, который можно скопировать и вставить в любой проект.

## Что вы узнаете

- Как собирать файлы изображений с помощью **pathlib image handling**  
- Настройка пула воркеров **multithreaded OCR in Python**  
- Настройка **OCR thread count optimization** под ядра вашего процессора  
- Сохранение каждого результата с понятной схемой именования для последующего поиска  
- Запуск всего как единого, автономного скрипта  

## Предварительные требования (Что вам нужно сначала)

| Требование | Почему это важно |
|------------|-------------------|
| Python 3.9+ | Современный синтаксис (`pathlib`, f‑strings) |
| Tesseract 5.x установлен и доступен в `PATH` | OCR‑движок, используемый `pytesseract` |
| `pytesseract` (`pip install pytesseract`) | Обёртка Python для Tesseract |
| `Pillow` (`pip install pillow`) | Загрузка изображений для Tesseract |
| Папка с PNG‑файлами, которые нужно обработать | Цель нашего **tesseract OCR batch processing** |

> **Pro tip:** Если вы используете Windows, добавьте `C:\Program Files\Tesseract-OCR` в системный `PATH`, чтобы `pytesseract` мог автоматически находить исполняемый файл.

---

## Шаг 1 – Сбор всех PNG‑изображений (Using pathlib)

First things first: we need a list of every image we plan to run OCR on. `pathlib` makes this a one‑liner and keeps the code OS‑agnostic.

```python
import pathlib

# Adjust the path to point at your source folder
source_dir = pathlib.Path("YOUR_DIRECTORY/batch_images")
image_files = list(source_dir.glob("*.png"))

print(f"Found {len(image_files)} PNG files to process.")
```

*Why `pathlib`?* It abstracts away Windows backslashes vs. Unix slashes, letting the same script run everywhere. This is the cornerstone of **pathlib image handling** in our tutorial.

*Почему `pathlib`?* Он абстрагирует различия между обратными слешами Windows и слешами Unix, позволяя запускать один и тот же скрипт везде. Это фундамент **pathlib image handling** в нашем руководстве.

## Шаг 2 – Определение простого класса пакетного OCR‑процессора

Below is a lightweight wrapper that hides the threading boilerplate. It mirrors the pseudo‑code you saw earlier but is fully functional.

```python
import concurrent.futures
import pytesseract
from PIL import Image
import os

class BatchOcrProcessor:
    """Encapsulates multithreaded OCR logic."""

    def __init__(self):
        self.thread_count = os.cpu_count() or 4  # sensible default
        self.output_folder = pathlib.Path("ocr_results")
        self.output_folder.mkdir(parents=True, exist_ok=True)

    def set_thread_count(self, count: int):
        """Adjust the number of worker threads (OCR thread count optimization)."""
        if count < 1:
            raise ValueError("Thread count must be at least 1")
        self.thread_count = count
        print(f"Thread pool size set to {self.thread_count}")

    def set_output_folder(self, folder: str):
        """Where each OCR result will be saved (tesseract OCR batch processing)."""
        self.output_folder = pathlib.Path(folder)
        self.output_folder.mkdir(parents=True, exist_ok=True)
        print(f"Output folder set to {self.output_folder}")

    def _process_single(self, image_path: pathlib.Path):
        """Run OCR on a single image and write the text file."""
        try:
            img = Image.open(image_path)
            text = pytesseract.image_to_string(img)
            out_file = self.output_folder / f"{image_path.stem}.txt"
            out_file.write_text(text, encoding="utf-8")
            return f"✅ {image_path.name} → {out_file.name}"
        except Exception as exc:
            return f"❌ {image_path.name} failed: {exc}"

    def process(self, image_paths):
        """Run OCR on the entire batch using a thread pool."""
        print("🚀 Starting batch OCR...")
        with concurrent.futures.ThreadPoolExecutor(max_workers=self.thread_count) as executor:
            results = list(executor.map(self._process_single, image_paths))
        for line in results:
            print(line)
        print("🏁 Batch OCR completed.")
```

**Объяснение ключевых решений**

- **ThreadPoolExecutor** обеспечивает истинный многопоток для задач, ограниченных вводом‑выводом, таких как чтение файлов и вызов внешнего бинарного файла Tesseract.  
- Метод `set_thread_count` — место, где вы можете экспериментировать с **OCR thread count optimization**; больше потоков часто означает большую пропускную способность, пока ваши ядра процессора не будут полностью загружены.  
- Каждое изображение создаёт файл `.txt`, названный так же, как оригинальный PNG — идеально для последующего индексирования или поиска.  

## Шаг 3 – Связывание всех компонентов

Now we instantiate the processor, tweak the thread count, point it at our output folder, and finally hand it the list of images.

```python
if __name__ == "__main__":
    # 1️⃣ Gather PNGs (already done above)
    # 2️⃣ Create processor instance
    ocr_processor = BatchOcrProcessor()

    # 3️⃣ Configure thread pool – feel free to change 8 → your core count
    ocr_processor.set_thread_count(8)   # multithreaded OCR in Python

    # 4️⃣ Choose where results land
    ocr_processor.set_output_folder("YOUR_DIRECTORY/ocr_results")

    # 5️⃣ Run the batch – this call blocks until everything is done
    ocr_processor.process(image_files)

    # 6️⃣ All done – a friendly console message
    print("✅ All images processed. Check the ocr_results folder.")
```

Running the script will produce output similar to:

```
Found 42 PNG files to process.
Thread pool size set to 8
Output folder set to YOUR_DIRECTORY/ocr_results
🚀 Starting batch OCR...
✅ invoice_001.png → invoice_001.txt
✅ receipt_2023-04-15.png → receipt_2023-04-15.txt
...
🏁 Batch OCR completed.
✅ All images processed. Check the ocr_results folder.
```

Each `.txt` contains the raw OCR output. Open any file and you’ll see the extracted text ready for indexing, sentiment analysis, or whatever comes next.

Каждый `.txt` содержит необработанный вывод OCR. Откройте любой файл, и вы увидите извлечённый текст, готовый к индексации, анализу настроений или к любой дальнейшей обработке.

## Шаг 4 – Распространённые ошибки и как их избежать

| Симптом | Вероятная причина | Решение |
|---------|-------------------|----------|
| Пустые файлы `.txt` | Tesseract не находит языковые данные или изображение слишком тёмное | Установите языковые пакеты (`tesseract-ocr-eng`) и предобработайте изображения (увеличьте контраст). |
| `UnicodeDecodeError` при чтении результатов | Вывод содержит символы, не являющиеся UTF‑8 | Записывайте файлы с `encoding="utf-8"` (уже в коде) или используйте `errors="ignore"` как быстрый обходной путь. |
| Пики нагрузки CPU, но нет ускорения | Количество потоков превышает количество физических ядер | Уменьшите `set_thread_count` до `os.cpu_count()` или ниже. |
| `FileNotFoundError` при открытии изображения | Путь содержит не‑ASCII символы в Windows | Добавьте префикс `r` к строке или используйте объекты `pathlib` напрямую (как мы делаем). |

## Шаг 5 – Расширение руководства (Следующие шаги)

- **Add image preprocessing** с OpenCV (`cv2`) для повышения точности OCR (например, выравнивание, пороговая обработка).  
- **Parallelize across machines** используя `multiprocessing` или простую очередь задач вроде RabbitMQ для огромных объёмов работы.  
- **Integrate with a search engine** (Elasticsearch) чтобы сделать извлечённый текст доступным для поиска в реальном времени.  
- **Swap Tesseract for a cloud OCR API** (Google Vision, Azure Computer Vision), если нужна более высокая точность распознавания рукописного текста.  

Все эти идеи опираются на уже построенный фундамент: чистый, **python batch ocr tutorial**, который работает сразу из коробки.

## Заключение

Вы только что создали полноценный **python batch ocr tutorial**, который:

1. **Собирает** каждый PNG с помощью **pathlib image handling**.  
2. **Запускает** **multithreaded OCR in Python** пул воркеров.  
3. **Оптимизирует** количество потоков под ваше оборудование (**OCR thread count optimization**).  
4. **Записывает** каждый результат в отдельную папку (**tesseract OCR batch processing**).  

Скрипт готов к интеграции в любой конвейер, будь то обработка чеков, юридических документов или горы скриншотов. Поиграйте с количеством потоков, добавьте предобработку изображений или подключите вывод к базе данных — ваш выбор.

Есть вопросы? Оставляйте комментарии ниже, и счастливого кодинга!

![Workflow diagram of python batch ocr tutorial processing multiple PNG files in parallel](/images/python-batch-ocr-workflow.png){.center width=600 alt="Схема рабочего процесса python batch ocr tutorial по обработке нескольких PNG‑файлов параллельно"}

---

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Aspose OCR Tutorial – Оптическое распознавание символов](/ocr/english/)
- [Как пакетно распознавать изображения OCR со списком в Aspose.OCR для .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Извлечение текста из изображения C# с выбором языка с помощью Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}