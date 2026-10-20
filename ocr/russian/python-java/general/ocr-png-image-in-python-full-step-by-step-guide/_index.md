---
category: general
date: 2026-06-06
description: OCR PNG‑изображение с помощью Python – узнайте, как извлекать текст из
  изображения, запустить пример OCR на Python и даже легко читать древнегреческий
  текст.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: ru
og_description: OCR PNG‑изображение в Python объяснено. Это руководство показывает,
  как извлечь текст из изображения, запустить пример OCR на Python и легко читать
  древнегреческий.
og_title: OCR PNG‑изображения в Python – Полный учебник
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR PNG‑изображения в Python – Полное пошаговое руководство
url: /ru/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR PNG Image в Python – Полное пошаговое руководство

Когда‑нибудь задавались вопросом, как **OCR PNG image** файлы прямо из скрипта Python? Возможно, у вас есть папка, полная отсканированных древних манускриптов, и вам нужно **extract text from image** файлы без ручного ввода всего текста. Хорошая новость — вам не нужен PhD в области компьютерного зрения — достаточно нескольких строк кода и правильной библиотеки, и вы будете читать древнегреческий за секунды.

В этом руководстве мы пройдем через **python OCR example**, который распознаёт текст из PNG, устанавливает язык на Greek polytonic и выводит результат. К концу вы точно будете знать, как **recognize image text**, справляться с типичными подводными камнями и адаптировать скрипт под другие языки или форматы изображений.

## Что вы узнаете

- Установить и настроить библиотеку OCR для Python (pytesseract + Tesseract OCR)
- Создать экземпляр OCR‑движка и загрузить PNG‑файл
- Установить язык распознавания на Greek polytonic, чтобы **read ancient greek**
- Вывести распознанный текст и решить типичные проблемы
- Расширить скрипт для пакетной обработки нескольких PNG или переключения на другой язык

### Требования

| Требование | Зачем это нужно |
|-------------|----------------|
| Python 3.8+ | Современный синтаксис и подсказки типов |
| `pytesseract` package | Тонкая обёртка вокруг движка Tesseract |
| Tesseract OCR binaries (≥ 5.0) | Сам движок, который выполняет основную работу |
| Greek language data (`grc.traineddata`) | Необходимы для **read ancient greek** корректно |
| A PNG image you want to analyse (e.g., `ancient_greek.png`) | Наша цель для демонстрации **ocr png image** |

Вы можете установить Python‑часть с помощью:

```bash
pip install pytesseract Pillow
```

А на Ubuntu/macOS добавить сам движок:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

Не забудьте скачать обученные данные Greek polytonic:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(Путь может отличаться; при необходимости скорректируйте `TESSDATA_PREFIX`.)*

---

## OCR PNG Image: Создание экземпляра движка

Первое, что нам нужно, — объект, который общается с Tesseract. В `pytesseract` движок вызывается через функции уровня модуля, но для ясности мы обернём его в небольшую класс‑обёртку. Это отражает концепцию «движка», которую вы видели в оригинальном фрагменте.

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**Почему оборачивать?**  
- Сохраняет публичный API идентичным фрагменту, с которым вы начали, делая миграцию безболезненной.  
- Позволяет позже добавить логирование или обработку ошибок, не меняя основной поток.  
- Продемонстрирует хорошую практику ООП — то, что ценят старшие разработчики.

---

## Извлечение текста из изображения: установка языка Greek Polytonic

Теперь, когда у нас есть движок, нужно указать, какой язык ожидать. Greek polytonic использует диакритические знаки, которые не покрыты стандартными данными «greek», поэтому мы указываем Tesseract на файл `grc`.

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

Если когда‑нибудь понадобится **extract text from image** файлы на другом языке, просто замените `"grc"` на `"eng"` для английского, `"fra"` для французского и т.д. Та же строка работает для любого установленного языка.

## Распознавание текста изображения: запуск OCR на PNG

С установленным языком мы передаём PNG в движок. В оригинальном примере путь был зашит в код; мы сделаем его гибче, используя объекты `Path`.

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**Советы и крайние случаи**

- **File not found** – оберните вызов в `try/except FileNotFoundError`, чтобы вывести дружелюбное сообщение.  
- **Low‑resolution PNG** – рассмотрите предобработку (например, изменение размера, бинаризацию) с помощью Pillow перед OCR.  
- **Non‑Greek text** – Tesseract всё равно попытается декодировать, но точность резко падает. Всегда подбирайте язык.

## Вывод распознанного текста

Наконец, мы печатаем результат. В реальном проекте вы можете записать его в базу данных, CSV‑файл или даже передать в конвейер перевода.

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

Когда вы запустите скрипт против чистого скана древнегреческой надписи, вы должны увидеть что‑то вроде:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

Если вывод выглядит искажённым, дважды проверьте, что файл **greek.traineddata** находится в правильной папке и что PNG не слишком шумный.

## Полный рабочий пример (Все шаги в одном скрипте)

Ниже полностью готовая к запуску программа. Сохраните её как `ocr_greek.py` и выполните `python ocr_greek.py`.

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Ожидаемый вывод** (усечённый для краткости):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

Если вы видите правильные греческие символы, поздравляем — вы успешно выполнили операцию **ocr png image** в Python!

## Часто задаваемые вопросы и профессиональные советы

### Как улучшить точность на шумном PNG?

- Преобразуйте изображение в градации серого: `img = img.convert('L')`
- Примените бинарный порог: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`
- Увеличьте масштаб с помощью `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`

Эти шаги часто превращают ночной кошмар **recognize image text** в чистый результат.

### Можно ли обработать всю папку PNG?

Абсолютно. Оберните вызов `recognize_image` в цикл `for` по `Path.glob("*.png")`. Сохраняйте каждый результат в словаре или записывайте в CSV для последующего анализа.

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### Что если нужно извлекать только числа?

Передайте пользовательскую строку **config** в `image_to_string`:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

Таким образом вы сможете **extract text from image** файлы, содержащие таблицы, серийные номера или метки времени.

### Как получить оценки уверенности?

Да — используйте `pytesseract.image_to_data`, который возвращает TSV с уровнем уверенности для каждого слова. Вы можете отфильтровать токены с низкой уверенностью перед сборкой окончательной строки.

## Расширение руководства

Теперь, когда вы освоили основы, рассмотрите изучение следующих тем:

- **Batch OCR with multiprocessing** – ускорьте обработку больших корпусов PNG.  
- **Hybrid OCR + NLP pipelines** – автоматически переводите извлечённый древнегреческий в современный английский.  
- **Alternative engines** – попробуйте `easyocr` или методы на основе `opencv` для специфических задач.  
- **Cloud OCR services** – Google Vision, Azure Computer Vision или AWS Textract для масштабирования без серверов.

Каждый из этих пунктов опирается на ядро **python ocr example**, которое мы только что рассмотрели, так что вы будете чувствовать себя уверенно, погружаясь глубже.

## Заключение

Мы взяли простой фрагмент кода и превратили его в надёжный рабочий процесс **ocr png image** в Python. Создав `OcrEngine`, установив язык на Greek polytonic, передав PNG и напечатав результат, вы теперь знаете, как **extract text from image** файлы, **recognize image text** и даже **read ancient greek**.

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом пособии. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Извлечение текста из изображения с Aspose OCR – пошаговое руководство](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Как установить значение порога в распознавании OCR изображения](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Распознавание текста изображения с Aspose OCR для нескольких языков](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}