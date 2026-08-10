---
category: general
date: 2026-05-31
description: Создайте PDF с возможностью поиска из отсканированных изображений с помощью
  OCR на Python. Узнайте, как конвертировать PDF из отсканированных изображений, преобразовать
  TIFF в PDF и добавить слой OCR‑текста за считанные минуты.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: ru
og_description: Создайте мгновенно PDF с возможностью поиска. Это руководство показывает,
  как выполнить OCR, преобразовать PDF со сканированным изображением и добавить слой
  текста OCR с помощью одного скрипта на Python.
og_title: Создайте поисковый PDF с помощью Python — Полный учебник
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: Создание PDF с возможностью поиска с помощью Python – пошаговое руководство
url: /ru/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF с помощью Python – пошаговое руководство

Задумывались ли вы когда‑нибудь, как **создать поисковый PDF** из отсканированной страницы без использования десятков инструментов? Вы не одиноки. Во многих офисных процессах отсканированный TIFF или JPEG попадает на общий диск, и следующий человек вынужден копировать‑вставлять текст вручную — болезненно, подвержено ошибкам и отнимает время.  

В этом руководстве мы пройдем чистое программное решение, которое позволяет **конвертировать PDF со сканированным изображением**, **конвертировать TIFF в PDF** и **добавить слой OCR‑текста** за один раз. К концу вы получите готовый к использованию скрипт, который запускает OCR, внедряет скрытый текст и выдаёт поисковый PDF, который можно индексировать, искать или делиться им с уверенностью.

## Что понадобится

- Python 3.9+ (любая современная версия подойдет)
- пакеты `aspose-ocr` и `aspose-pdf` (устанавливаются через `pip install aspose-ocr aspose-pdf`)
- отсканированный файл изображения (`.tif`, `.png`, `.jpg` или даже страница PDF, содержащая только изображение)
- умеренный объём ОЗУ (движок OCR лёгкий; даже ноутбук справится)

> **Совет:** Если вы используете Windows, самый простой способ получить пакеты — выполнить команду в окне PowerShell с повышенными правами.

```bash
pip install aspose-ocr aspose-pdf
```

Теперь, когда предварительные требования выполнены, давайте погрузимся в код.

## Шаг 1: Создать экземпляр OCR‑движка – *create searchable pdf*

Первое, что мы делаем, — запускаем OCR‑движок. Считайте его мозгом, который будет читать каждый пиксель и преобразовывать его в символы.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **Почему это важно:** Инициализация движка только один раз снижает использование памяти. Если вы будете вызывать `OcrEngine()` внутри цикла для каждой страницы, вы быстро исчерпаете ресурсы.

## Шаг 2: Загрузить отсканированное изображение – *convert tiff to pdf* & *convert scanned image pdf*

Далее указываем движку файл, который нужно обработать. API принимает любое растровое изображение, поэтому TIFF работает так же хорошо, как JPEG.

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

Если у вас есть PDF, содержащий только отсканированное изображение, вы всё равно можете использовать `load_image`, так как Aspose автоматически извлечёт первую страницу.

## Шаг 3: Подготовить параметры сохранения PDF – *add OCR text layer*

Здесь мы настраиваем, как будет выглядеть конечный PDF. Ключевой флаг — `create_searchable_pdf`; установка его в `True` сообщает библиотеке внедрить невидимый слой текста, который отражает визуальное содержимое.

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **Что делает слой текста:** Когда вы открываете полученный файл в Adobe Reader и пытаетесь выделить текст, вы видите скрытые символы. Поисковые системы также могут их индексировать — идеально для соответствия требованиям или архивирования.

## Шаг 4: Запустить OCR и сохранить – *how to run OCR* в одном вызове

Теперь происходит магия. Один вызов метода запускает движок распознавания и записывает поисковый PDF на диск.

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

Метод `recognize` возвращает объект статуса, который можно проверить на наличие ошибок, но для большинства простых сценариев достаточно приведённого выше простого вызова.

### Ожидаемый вывод

Running the script prints:

```
PDF saved as searchable PDF.
```

Если открыть `scanned_page_searchable.pdf`, вы заметите, что можно выделять текст, копировать‑вставлять его и даже выполнить поиск `Ctrl+F`. Это отличительная черта рабочего процесса **create searchable pdf**.

## Полный рабочий скрипт

Ниже представлен полный, готовый к запуску скрипт. Просто замените пути‑заполнители на фактические расположения ваших файлов.

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

Save this as `create_searchable_pdf.py` and execute:

```bash
python create_searchable_pdf.py
```

## Часто задаваемые вопросы и особые случаи

### 1️⃣ Можно ли обрабатывать многостраничные PDF?

Да. Используйте `ocr_engine.load_image("file.pdf")`, а затем в цикле обрабатывайте каждую страницу с помощью `ocr_engine.recognize(pdf_save_options, page_number)`. Библиотека автоматически создаст многостраничный поисковый PDF.

### 2️⃣ Что если мой исходный файл — высокоразрешающий TIFF (300 dpi+)?

Higher DPI yields better OCR accuracy but also larger memory usage. If you hit a `MemoryError`, downscale the image first:

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ Как изменить язык OCR?

Set the `language` property on the engine before loading the image:

```python
ocr_engine.language = "fra"   # French
```

Полный список поддерживаемых кодов языков находится в документации Aspose.

### 4️⃣ Что если нужно сохранить оригинальное качество изображения?

Класс `PdfSaveOptions` имеет свойство `compression`. Установите его в `PdfCompression.None`, чтобы сохранить растровые данные точно в оригинальном виде.

```python
pdf_save_options.compression = "None"
```

## Советы для продакшн‑готовых развертываний

- **Пакетная обработка:** Оберните основную логику в функцию, принимающую список путей к файлам. Записывайте каждый успех/неудачу в CSV для аудита.
- **Параллелизм:** Используйте `concurrent.futures.ThreadPoolExecutor` для запуска OCR на нескольких ядрах. Только помните, что каждый поток требует свой собственный экземпляр `OcrEngine`.
- **Безопасность:** Если вы работаете с конфиденциальными документами, запускайте скрипт в изолированной среде и сразу после обработки удаляйте временные файлы.

## Заключение

Теперь вы знаете, как **создавать поисковые PDF** файлы из отсканированных изображений с помощью лаконичного скрипта на Python. Инициализируя OCR‑движок, загружая TIFF (или любой растр), настраивая `PdfSaveOptions` для **добавления OCR‑слоя текста**, и, наконец, вызывая `recognize`, весь конвейер **convert scanned image pdf** и **convert TIFF to PDF** превращается в одну повторяемую команду.

Следующие шаги? Попробуйте связать этот скрипт с наблюдателем за файлами, чтобы любой новый скан, помещённый в папку, автоматически становился поисковым. Или поэкспериментируйте с различными языками OCR для поддержки многоязычных архивов. Возможности безграничны, когда вы комбинируете OCR с генерацией PDF.

Есть дополнительные вопросы о **how to run OCR** в других языках или фреймворках? Оставьте комментарий ниже, и удачной разработки! 

![Диаграмма, показывающая поток от отсканированного изображения → OCR‑движка → поискового PDF (create searchable pdf)](searchable-pdf-flow.png "Диаграмма потока создания поискового pdf")

## Что стоит изучить дальше?

- [Как выполнять OCR PDF в .NET с Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Конвертировать изображения в PDF C# – Сохранить многостраничный результат OCR](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Как выполнять OCR текста изображения с указанием языка с помощью Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}