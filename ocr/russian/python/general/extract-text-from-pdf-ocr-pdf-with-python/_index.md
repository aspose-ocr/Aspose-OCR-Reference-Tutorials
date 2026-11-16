---
category: general
date: 2026-04-29
description: Извлекать текст из PDF с помощью Aspose OCR в Python. Узнайте о пакетной
  обработке PDF с OCR, конвертации текста из отсканированных PDF и работе со страницами
  низкой уверенности.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: ru
og_description: Извлечение текста из PDF с помощью Aspose OCR в Python. Это руководство
  демонстрирует пакетную обработку PDF с OCR, преобразование текста отсканированных
  PDF и обработку результатов с низкой уверенностью.
og_title: Извлечение текста из PDF – OCR PDF с помощью Python
tags:
- OCR
- Python
- PDF processing
title: Извлечение текста из PDF — OCR PDF с помощью Python
url: /ru/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из PDF – OCR PDF с Python

Когда‑нибудь вам нужно было **извлечь текст из PDF**, но файл оказался просто отсканированным изображением? Вы не одиноки — многие разработчики сталкиваются с этой проблемой, пытаясь превратить PDF‑файлы в поисковые данные. Хорошая новость? С Aspose OCR для Python вы можете конвертировать текст из отсканированного PDF за несколько строк кода и даже выполнять **пакетную обработку OCR PDF**, когда у вас десятки файлов.

В этом руководстве мы пройдем весь процесс: настройку библиотеки, запуск OCR для одного PDF, масштабирование до пакетной обработки и работу со страницами с низкой уверенностью, чтобы знать, когда требуется ручная проверка. К концу вы получите готовый к запуску скрипт, извлекающий текст из любого отсканированного PDF, и поймете причины каждого шага.

## Что понадобится

Перед тем как начать, убедитесь, что у вас есть:

- Python 3.8 или новее (код использует f‑строки, поэтому работает с 3.6+, но рекомендуется 3.8+)
- Лицензия Aspose OCR для Python или бесплатный пробный ключ (можно получить на сайте Aspose)
- Папка с одним или несколькими отсканированными PDF, которые нужно обработать
- Умеренное количество места на диске для создаваемых отчетов *.txt*

Вот и всё — никаких тяжёлых внешних зависимостей, никаких трюков с OpenCV. Движок Aspose OCR делает всю тяжелую работу за вас.

## Настройка окружения

Сначала установите пакет Aspose OCR из PyPI:

```bash
pip install aspose-ocr
```

Если у вас есть файл лицензии (`Aspose.OCR.lic`), поместите его в корень проекта и активируйте следующим образом:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **Совет:** Держите файл лицензии вне системы контроля версий; добавьте его в `.gitignore`, чтобы избежать случайного раскрытия.

## Выполнение OCR для одного PDF

Теперь извлечём текст из одного отсканированного PDF. Основные шаги:

1. Создать экземпляр `OcrEngine`.
2. Указать ему PDF‑файл.
3. Получить `OcrResult` для каждой страницы.
4. Записать полученный обычный текст на диск.
5. Освободить движок, вызвав его уничтожение, чтобы освободить нативные ресурсы.

Вот полный, готовый к запуску скрипт:

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**Что вы увидите:** Для каждой страницы скрипт выводит что‑то вроде `Page 1: confidence 97.45%`. Если уверенность страницы ниже 80 %, появляется предупреждение, указывающее, что OCR мог пропустить символы.

### Почему это работает

- **`OcrEngine`** — это шлюз к нативной библиотеке Aspose OCR; он обрабатывает всё, от предварительной обработки изображений до распознавания символов.
- **`extract_from_pdf`** автоматически растеризует каждую страницу PDF, поэтому вам не нужно самостоятельно конвертировать PDF в изображения.
- **Оценки уверенности** позволяют автоматизировать проверку качества — это критично при обработке юридических или медицинских документов, где важна точность.

## Пакетная обработка OCR PDF с Python

Большинство реальных проектов работают с более чем одним файлом. Давайте расширим скрипт для одного файла до **пакетной обработки OCR PDF**, который проходит по каталогу, обрабатывает каждый PDF и сохраняет результаты в соответствующей подпапке.

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### Как это помогает

- **Масштабируемость:** Функция проходит по папке один раз, создавая отдельную подпапку вывода для каждого PDF. Это упрощает работу, когда у вас десятки документов.
- **Повторное использование:** `ocr_pdf_file` можно вызывать из других скриптов (например, веб‑службы), так как это чистая функция.
- **Обработка ошибок:** Скрипт выводит дружелюбное сообщение, если входная папка пуста, избавляя от тихих сбоев.

## Конвертация текста из отсканированного PDF — обработка крайних случаев

Хотя приведённый код работает для большинства PDF, вы можете столкнуться с некоторыми особенностями:

| Ситуация | Почему происходит | Как смягчить |
|-----------|----------------|-----------------|
| **Зашифрованные PDF** | PDF защищён паролем. | Передайте пароль в `extract_from_pdf(pdf_path, password="yourPwd")`. |
| **Документы на нескольких языках** | По умолчанию Aspose OCR использует английский. | Установите `ocr_engine.language = "spa"` для испанского или задайте список для смешанных языков. |
| **Очень большие PDF (>500 страниц)** | Потребление памяти резко возрастает, так как каждая страница загружается в ОЗУ. | Обрабатывайте PDF частями, используя `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` и цикл. |
| **Низкое качество сканирования** | Низкое DPI или сильный шум снижают уверенность. | Предобработайте PDF с `engine.image_preprocessing = True` или увеличьте DPI через `engine.dpi = 300`. |

> **Внимание:** Включение предобработки изображений может заметно увеличить время работы CPU. Если вы запускаете ночную пакетную обработку, запланируйте достаточное время или запустите отдельный воркер.

## Проверка вывода

После завершения скрипта вы увидите структуру папок, похожую на:

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

Откройте любой файл `.txt`; вы должны увидеть чистый текст в кодировке UTF‑8, соответствующий оригинальному отсканированному содержимому. Если заметите искажённые символы, проверьте настройки языка PDF и убедитесь, что на машине установлены необходимые пакеты шрифтов.

## Очистка ресурсов

Aspose OCR использует нативные DLL, поэтому важно вызвать `engine.dispose()` после завершения работы. Пропуск этого шага может привести к утечкам памяти, особенно в длительных пакетных заданиях.

```python
# Always the last line of your script
engine.dispose()
```

## Полный пример от начала до конца

Собрав всё вместе, вот один

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}