---
category: general
date: 2026-04-26
description: 'как использовать OCR в Python: научитесь извлекать текст из изображения
  и читать TIFF‑файлы в Python с помощью простого примера OCR. Быстрый, готовый к
  запуску код включён.'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: ru
og_description: 'как выполнить OCR в Python: пошаговое руководство, показывающее,
  как извлекать текст из изображения, читать TIFF‑файлы в Python и конвертировать
  текст сканированного изображения с помощью простого исполняемого скрипта.'
og_title: Как использовать OCR в Python – базовый пример OCR для извлечения текста
tags:
- OCR
- Python
- Image Processing
title: Как использовать OCR в Python – базовый пример OCR для извлечения текста
url: /ru/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to ocr python – Базовый пример OCR для извлечения текста

Когда‑то задавались вопросом **how to ocr python**, имея перед собой отсканированный TIFF? Вы не одиноки, глядя на кучу файлов изображений и задаваясь вопросом: «Как извлечь из этого слова?» Хорошая новость в том, что превратить картинку в обычный текст — проще простого, если использовать правильную библиотеку и следовать нескольким ясным шагам.

В этом руководстве мы пройдем через **basic OCR example**, который читает TIFF‑файл, извлекает текст и выводит его в консоль. К концу вы точно будете знать, как **extract text from image** файлов, как справляться с особенностями формата TIFF и что можно подправить, если нужно **convert scanned image text** в более полезный вид. Никакой скрытой магии — только прямой Python‑код, который можно скопировать‑вставить и запустить уже сегодня.

## What You’ll Need

Прежде чем углубиться, убедитесь, что у вас есть:

- Установленный Python 3.9+ (желательно последняя стабильная версия).
- Устанавливаемая через pip OCR‑библиотека. В этом руководстве мы будем использовать вымышленный пакет `aocr`, имитирующий популярные инструменты вроде Tesseract; позже его можно заменить на `pytesseract` или `easyocr`.
- TIFF‑изображение, которое нужно обработать — назовите его `input.tiff` и поместите в папку, путь к которой будет указан в коде.
- Базовые навыки работы с командной строкой (только для установки пакета).

И всё. Никаких тяжёлых зависимостей, без Docker‑контейнеров, всего несколько строк кода.

## Step 1 – Install and Import Dependencies (how to ocr python)

Сначала установим OCR‑пакет. Откройте терминал и выполните:

```bash
pip install aocr
```

Если хотите использовать реальную библиотеку, замените `aocr` на `pytesseract` и установите движок Tesseract отдельно.

Теперь импортируем необходимое. Класс `Path` из `pathlib` предоставляет удобный способ работы с путями к файлам независимо от ОС.

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*Почему `Path`?* Потому что он абстрагирует слеши (`/` vs `\`) и позволяет соединять каталоги без забот о конкретной системе. Эта небольшая деталь часто спасает от головной боли, когда скрипт переносится на CI‑сервер.

## Step 2 – Create the OCR Engine Instance (basic ocr example)

Далее создаём экземпляр OCR‑движка. Представьте `OcrEngine` как мозг, который будет «читать» картинку и выдавать символы.

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

Большинство OCR‑библиотек позволяют настроить язык, DPI или пороги уверенности здесь. Для этого **basic OCR example** мы оставим значения по умолчанию, но позже можно поиграть с `ocr_engine.config`, если понадобится поддержка нескольких языков.

## Step 3 – Load Your TIFF Image (read tiff file python)

Здесь вступает в действие часть **read tiff file python**. TIFF может быть многостраничным, но `Image.load` по умолчанию берёт первую страницу — идеально для одностраничного скана.

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

Замените `"YOUR_DIRECTORY"` на реальный каталог, где находится `input.tiff`. Если не уверены, где запускается скрипт, `Path.cwd()` выведет текущий рабочий каталог — удобно для отладки путей.

## Step 4 – Run the OCR Process (extract text from image)

Теперь происходит магия. Вызов `process()` пропускает изображение через OCR‑конвейер и возвращает объект результата.

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

За кулисами движок может конвертировать изображение в градации серого, применять пороговую обработку и подавать его в нейронную сеть. Вам не нужно управлять этими шагами; библиотека делает это за вас.

## Step 5 – Print the Recognized Text (convert scanned image text)

Наконец, выводим распознанный текст. В реальных проектах, скорее всего, вы запишете его в файл или базу данных, но печать сохраняет пример компактным.

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

При запуске скрипта вы должны увидеть что‑то вроде:

```
Hello, world!
This is a sample scanned document.
```

Если вывод выглядит «мусором», проверьте, что исходное изображение чёткое и что язык OCR совпадает с текстом.

## Full Working Script

Собираем всё вместе, вот полностью готовая к запуску программа:

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### Expected Output

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

Если нужно **convert scanned image text** в поисковый PDF, можно передать `ocr_result.text` в генератор PDF, например `reportlab` — но это уже отдельный урок.

## Common Pitfalls & Pro Tips

- **Низкое разрешение сканов**: OCR плохо работает ниже 150 DPI. Если ваш TIFF размытый, сначала увеличьте его с помощью Pillow (`Image.open(...).resize(...)`).
- **Несколько страниц**: Для многостраничных TIFF‑файлов перебирайте `Image.load_multi_page()` (если библиотека поддерживает) и конкатенируйте результаты.
- **Поддержка языков**: Многие движки по умолчанию используют английский. Установите `ocr_engine.language = "spa"` для испанского, например.
- **Обработка пробелов**: OCR часто добавляет лишние разрывы строк. Используйте `str.splitlines()` или регулярные выражения для очистки вывода.
- **Производительность**: При пакетной обработке переиспользуйте один экземпляр `OcrEngine` вместо создания нового для каждого файла.

## Extending the Example

Теперь, когда вы освоили **how to ocr python** для одного изображения, рассмотрите следующие шаги:

1. **Пакетная обработка** — пройдитесь по каталогу TIFF‑файлов и запишите каждый результат в файл `.txt`.
2. **Интеграция с Pandas** — храните извлечённый текст вместе с метаданными для быстрой аналитики.
3. **Гибридный подход** — комбинируйте OCR с NLP‑библиотеками, такими как `spaCy`, чтобы извлекать сущности (имена, даты, суммы) из отсканированных счетов.
4. **Альтернативные форматы файлов** — замените `Image.load` на `Image.from_bytes`, чтобы работать с изображениями, полученными из API или базы данных.

Все эти идеи опираются на базовую концепцию **extract text from image** и **convert scanned image text** в данные, понятные машинам.

## Conclusion

Мы прошли через чёткий, сквозной **basic OCR example**, который демонстрирует **how to ocr python**, **read tiff file python** и **extract text from image** файлы всего несколькими строками кода. Скрипт автономный, включает обработку ошибок и выводит результат напрямую, что делает его надёжной основой для любого проекта, требующего преобразования отсканированных документов в редактируемый текст.

Экспериментируйте — меняйте OCR‑бэкенд, подстраивайте предобработку или подключайте вывод к последующим этапам рабочего процесса. Возможности безграничны, когда вы надёжно **convert scanned image text** в поисковые, индексируемые данные.

Есть вопросы о граничных случаях, языковых пакетах или настройке производительности? Оставляйте комментарий ниже, и happy coding!

![how to ocr python example](/images/ocr-python-example.png "Screenshot of how to ocr python script output")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}