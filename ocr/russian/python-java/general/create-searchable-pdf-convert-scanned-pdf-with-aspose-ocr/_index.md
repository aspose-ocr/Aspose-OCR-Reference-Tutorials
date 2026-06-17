---
category: general
date: 2026-03-18
description: Создайте PDF с возможностью поиска из ваших отсканированных файлов с
  помощью Aspose OCR. Узнайте, как конвертировать отсканированный PDF, извлекать текст
  из PDF и быстро распознавать текст в PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- extract text from pdf
- recognize text pdf
- convert image pdf
language: ru
og_description: Создайте поисковый PDF мгновенно. Следуйте этому руководству, чтобы
  преобразовать отсканированный PDF, извлечь текст из PDF и распознать текст в PDF
  с помощью Aspose OCR.
og_title: Создайте поисковый PDF – пошагово с Aspose OCR
tags:
- OCR
- PDF
- Aspose
- Python
title: Создать поисковый PDF – преобразовать отсканированный PDF с помощью Aspose
  OCR
url: /ru/python-java/general/create-searchable-pdf-convert-scanned-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF – пошаговое руководство  

Когда‑нибудь нужно было **создать поисковый PDF** из стопки отсканированных страниц, но вы не знали, с чего начать? Вы не одиноки — большинство разработчиков сталкиваются с этой проблемой, когда первая отсканированная копия попадает на их сервер.  

Хорошая новость: с Aspose OCR вы можете **конвертировать отсканированный pdf** всего в несколько строк кода, **извлекать текст из pdf** для проверки и даже **распознавать текст pdf** «на лету». В этом руководстве мы пройдем весь процесс, от установки библиотеки до сохранения полностью поискового документа, и добавим несколько советов по обработке граничных случаев **конвертировать image pdf**.

## Что вы получите  

К концу этого руководства вы сможете:

* Загрузить отсканированный PDF (или PDF, содержащий только изображения) в Aspose OCR.  
* Указать движку, какие страницы обрабатывать — удобно, когда нужен только подмножество.  
* Встроить результаты OCR обратно в оригинальный файл, чтобы получился настоящий **поисковый PDF**.  
* Проверить результат, распечатав количество страниц и, при желании, выведя извлечённый текст.  

Никаких внешних сервисов, никакой скрытой магии — только чистый Python и собственный API Aspose.

## Требования  

* Python 3.8 или новее.  
* Пакет `aspose-ocr` — установить с помощью `pip install aspose-ocr`.  
* Отсканированный PDF‑файл (или PDF, содержащий только изображения).  
* Базовое знакомство с написанием скриптов на Python.  

Если всё это уже есть, отлично — приступаем.

<img src="searchable-pdf-workflow.png" alt="Схема создания поискового PDF">  

*(Иллюстрация конвейера OCR — не требуется для кода, но помогает визуальным ученикам.)*

## Шаг 1 — Инициализация OCR‑движка  

Первое, что нужно: экземпляр `OcrEngine`. Считайте его мозгом, который будет читать каждый пиксель и превращать его в символы Unicode.

```python
# Step 1: Import the required classes and create the engine
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

# Initialize the OCR engine – this object holds all settings
ocr_engine = OcrEngine()
```

**Почему это важно:** Без движка вы не сможете задать параметры или запустить распознавание. Раннее создание экземпляра также даёт место для последующего подключения пользовательских словарей.

## Шаг 2 — Загрузка исходного PDF  

Aspose OCR умеет читать PDF напрямую, так что вам не придётся растеризовать каждую страницу вручную. Просто укажите движку путь к файлу.

```python
# Step 2: Load the scanned PDF (replace with your actual path)
input_path = "YOUR_DIRECTORY/input.pdf"
ocr_engine.setImageFromFile(input_path)
```

*Совет:* Если PDF огромный, рассмотрите возможность загрузки его из потока, чтобы избежать блокировки файла на диске.

## Шаг 3 — Настройка параметров распознавания PDF  

Здесь вторичные ключевые слова начинают проявлять свою силу. Вы можете указать движку **конвертировать отсканированный pdf** только на определённых страницах, внедрить распознанный текст или оставить оригинальные изображения нетронутыми.

```python
# Step 3: Create and configure PDF recognition options
pdf_options = PdfRecognitionOptions()
pdf_options.setEmbedRecognisedText(True)          # Makes the PDF searchable
pdf_options.setPageRange(1, 3)                    # Process only pages 1‑3 (optional)
pdf_options.setTextExtractionMode(True)          # Enables text extraction for verification
```

**Почему это важно:**  
* `setEmbedRecognisedText(True)` — ключ к превращению растрового PDF в **поисковый PDF**.  
* `setPageRange` помогает **конвертировать image pdf** выборочно — полезно для больших документов, когда нужен OCR лишь на нескольких страницах.  
* Включение извлечения текста позволяет позже **извлекать текст из pdf** без открытия просмотрщика.

## Шаг 4 — Привязка параметров к движку  

Теперь привяжите параметры к движку. Этот шаг легко упустить, но без него движок будет работать с настройками по умолчанию (без поискового текста).

```python
# Step 4: Attach the options to the OCR engine
ocr_engine.setPdfRecognitionOptions(pdf_options)
```

## Шаг 5 — Запуск OCR на выбранных страницах  

После того как всё соединено, фактическое распознавание происходит одной вызванной функцией.

```python
# Step 5: Perform OCR – this may take a few seconds per page
ocr_result = ocr_engine.recognize()
```

Если вы обрабатываете документ размером в несколько мегабайт, имеет смысл обернуть вызов в `try/except`, чтобы поймать `OcrException` и записать проблемную страницу в лог.

## Шаг 6 — Проверка результата  

Быстрая проверка — вывести количество страниц, которые движок считает обработанными. При необходимости можно также получить «сырой» текст, чтобы **извлекать текст из pdf** для дальнейшего анализа.

```python
# Step 6: Show how many pages were processed
print("Pages processed:", ocr_result.getPageCount())

# Optional: dump extracted text for the first page (helps debugging)
first_page_text = ocr_result.getPageText(0)   # 0‑based index
print("\n--- Extracted Text (Page 1) ---\n", first_page_text[:500])  # show first 500 chars
```

**Зачем это нужно:** Видя количество страниц, вы подтверждаете, что `setPageRange` сработал, а фрагмент извлечённого текста доказывает, что OCR действительно распознал символы.

## Шаг 7 — Сохранение поискового PDF  

Наконец, запишите результат на диск. Константа `ImageFormats.PDF` сообщает Aspose, что файл остаётся PDF, но теперь обогащён поисковым текстом.

```python
# Step 7: Save the searchable PDF
output_path = "YOUR_DIRECTORY/output.pdf"
ocr_engine.save(output_path, ImageFormats.PDF)

print(f"Searchable PDF saved to: {output_path}")
```

Откройте полученный файл в любом PDF‑просмотрщике и попробуйте поискать текст — вуаля, вы **создали поисковый pdf**!

## Обработка распространённых граничных случаев  

### Когда источник — *PDF, содержащий только изображения*  

Если ваш входной PDF состоит лишь из изображений (без текстового слоя), тот же код работает — просто убедитесь, что `setEmbedRecognisedText(True)` остаётся включённым. Возможно, стоит увеличить DPI для лучшей точности:

```python
pdf_options.setResolution(300)  # 300 DPI gives sharper OCR results
```

### Работа с несколькими языками  

Aspose OCR поддерживает языковые пакеты. Загрузите нужный язык перед вызовом `recognize()`:

```python
ocr_engine.setLanguage("spa")   # Spanish language pack
```

### Большие документы  

Обработка PDF из 500 страниц может потребовать значительных ресурсов памяти. Разделите работу:

1. Циклически задавайте диапазоны страниц (`setPageRange(start, end)`).  
2. Сохраняйте каждый фрагмент как временный поисковый PDF.  
3. Объединяйте фрагменты с помощью `PdfMerger` (другой компонент Aspose).

## Полный рабочий пример (все шаги вместе)

```python
# Full script – create searchable PDF from a scanned document
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

def create_searchable_pdf(input_file: str, output_file: str, start_page: int = 1, end_page: int = 0):
    """
    Convert a scanned or image‑only PDF into a searchable PDF.
    :param input_file: Path to the source PDF.
    :param output_file: Destination path for the searchable PDF.
    :param start_page: First page to process (1‑based). Default = 1.
    :param end_page: Last page to process. 0 means “till the end”.
    """
    # Initialize engine
    ocr_engine = OcrEngine()
    ocr_engine.setImageFromFile(input_file)

    # Set options
    pdf_opts = PdfRecognitionOptions()
    pdf_opts.setEmbedRecognisedText(True)          # embed searchable text
    pdf_opts.setTextExtractionMode(True)           # allow text extraction
    if end_page > 0:
        pdf_opts.setPageRange(start_page, end_page)  # selective processing
    else:
        pdf_opts.setPageRange(start_page, start_page)  # process from start_page onward

    # Attach options
    ocr_engine.setPdfRecognitionOptions(pdf_opts)

    # Run OCR
    result = ocr_engine.recognize()
    print("Pages processed:", result.getPageCount())

    # Optional verification
    print("\nSample extracted text (first page):")
    print(result.getPageText(0)[:300])

    # Save searchable PDF
    ocr_engine.save(output_file, ImageFormats.PDF)
    print(f"Searchable PDF saved to: {output_file}")

if __name__ == "__main__":
    create_searchable_pdf(
        input_file="YOUR_DIRECTORY/input.pdf",
        output_file="YOUR_DIRECTORY/output.pdf",
        start_page=1,
        end_page=3   # change or set to 0 to process the whole file
    )
```

Запуск этого скрипта даст вам **поисковый PDF**, который можно открыть в Adobe Reader, Chrome или любом другом просмотрщике и сразу искать нужные слова.

## Заключение  

Теперь у вас есть полное, сквозное решение для **создания поискового PDF** с помощью Aspose OCR. От загрузки источника, настройки параметров, которые **конвертируют отсканированный pdf**, извлечения и проверки текста, до финального сохранения поискового результата — каждый шаг покрыт.  

Далее вы можете исследовать сценарии **конвертировать image pdf**, когда источник представляет собой серию JPEG, упакованных в PDF, или углубиться в языко‑специфичный OCR для повышения точности в многоязычных документах. В любом случае шаблон остаётся тем же: задайте параметры, вызовите `recognize()`, сохраните.

Экспериментируйте — меняйте диапазон страниц, подгоняйте DPI или подключайте собственный словарь. Если возникнут проблемы, оставляйте комментарий ниже или смотрите официальную документацию Aspose для актуальных нюансов API. Приятного OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}