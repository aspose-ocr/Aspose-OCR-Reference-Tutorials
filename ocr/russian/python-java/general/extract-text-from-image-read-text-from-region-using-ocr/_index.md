---
category: general
date: 2026-07-05
description: Извлеките текст из изображения с помощью OCR на Python. Узнайте, как
  загрузить изображение для OCR, считать текст из области и извлечь текст из счета‑фактуры
  несколькими строками кода.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: ru
og_description: Извлечение текста из изображения с помощью Python OCR. Это руководство
  показывает, как загрузить изображение для OCR, считать текст из области и быстро
  извлечь текст из счета.
og_title: Извлечение текста из изображения – чтение текста из области с помощью OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Извлечение текста из изображения – чтение текста из области с помощью OCR
url: /ru/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения – чтение текста из области с помощью OCR

Когда‑нибудь вам нужно было **извлечь текст из изображения**, но важна только определённая часть — например, общая сумма в счёте? Вы не одиноки. Во многих реальных проектах вам придётся **читать текст из области**, а не разбирать всё изображение. К счастью, с несколькими строками кода на Python вы можете загрузить изображение для OCR, определить область интереса (ROI) и получить именно те символы, которые нужны.

В этом руководстве мы пройдём через полностью готовый к запуску пример, показывающий, как **загрузить изображение для OCR**, настроить ROI и, наконец, **извлечь текст из счёта**. К концу вы получите готовый фрагмент кода, который работает с любой популярной библиотекой OCR, поддерживающей распознавание по областям.

---

## Что понадобится

- Python 3.8+ (код также работает на 3.10)  
- OCR‑пакет, предоставляющий класс `OcrEngine` (для демонстрации мы используем вымышленный модуль `ocr`; замените его на `pytesseract`, `easyocr` или любую библиотеку, поддерживающую ROI)  
- Пример изображения — например, `invoice.png` — с чётким печатным текстом  
- Базовое знакомство с функциями и классами Python (глубокие знания в области машинного обучения не требуются)

Если у вас уже всё есть, отлично — приступаем. Если нет, скачайте последнюю версию Python с python.org и установите OCR‑пакет командой `pip install your-ocr-lib`.

![Пример извлечения текста из изображения](extract-text-from-image.png "Извлечение текста из изображения – демонстрация OCR по области")

*На изображении выше показана область (красный прямоугольник), которую мы будем использовать для **извлечения текста из изображения**.*

## Шаг 1: Установить и импортировать библиотеку OCR

Сначала убедитесь, что библиотека OCR доступна в вашей среде. Ниже показанный шаблон импорта работает для большинства пакетов, предоставляющих высокоуровневый класс `OcrEngine`.

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **Pro tip:** Если вы используете `pytesseract`, вам потребуется установить бинарный файл Tesseract отдельно и задать `pytesseract.pytesseract.tesseract_cmd` с указанием его пути.

## Шаг 2: Создать OCR‑движок и задать язык

Создание движка простое, но указание языка значительно повышает точность, особенно для счетов, содержащих цифры и английские слова.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

Почему мы это делаем? OCR‑движок использует языковые модели для предсказания символов; указав, что ожидается английский язык, мы уменьшаем количество ложных срабатываний, например, ошибочное распознавание «0» как «O».

## Шаг 3: Загрузить изображение для OCR

Теперь мы действительно **загружаем изображение для OCR**. Большинство библиотек принимает путь к файлу или объект Pillow. Здесь мы используем встроенный загрузчик библиотеки для простоты.

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

Убедитесь, что путь указывает на правильный каталог; распространённая ошибка — забыть относительный путь, когда скрипт запускается из другой рабочей директории.

## Шаг 4: Определить область интереса (ROI)

Определение ROI — это суть **чтения текста из области**. Представьте, что вы рисуете прямоугольник вокруг той части счёта, где указана общая сумма.

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` и `top` представляют координаты X и Y левого верхнего угла прямоугольника.  
- `width` и `height` задают размеры коробки.  
- Вы можете экспериментировать с разными значениями, используя просмотрщик изображений, показывающий пиксельные координаты.

> **Why ROI matters:** Выполнение OCR на всей странице тратит процессорные ресурсы и часто добавляет шум от несвязного текста, таблиц или графики. Сфокусировавшись на области, вы получаете более чистый результат и ускоряете обработку.

## Шаг 5: Выполнить OCR в указанной области

С учётом всех настроек мы наконец **извлекаем текст из изображения** — но только внутри заданного ROI.

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

Метод `recognize` возвращает объект, который обычно содержит необработанную строку, оценки уверенности и иногда ограничивающие рамки для каждого слова. Для наших целей нам нужен лишь простой текст.

## Шаг 6: Вывести извлечённый текст

Выведем результат и посмотрим, что получилось. Этот шаг демонстрирует **извлечение текста из счёта** в реальном сценарии.

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### Ожидаемый вывод

```
Text inside ROI:
Total Amount: $1,245.67
```

Если ваш счёт имеет иной макет, вы увидите любой текст, находящийся внутри прямоугольника — возможно, номер счёта, дату или ссылку на заказ.

## Шаг 7: Обернуть всё в переиспользуемую функцию (опционально)

Чтобы решение было переиспользуемым для множества счетов, инкапсулируем логику в функцию. Это также иллюстрирует **ocr on region** как универсальную утилиту.

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

Теперь вы можете вызвать функцию для любого счёта:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

## Распространённые ошибки и как их избежать

| Проблема | Почему происходит | Как исправить |
|----------|-------------------|---------------|
| **Пустой вывод** | ROI не покрывает текст (неверные координаты). | Дважды проверьте пиксельные значения в редакторе изображений; добавьте визуальный отладочный оверлей. |
| **Мусорные символы** | Низкое разрешение изображения или плохой контраст. | Предобработайте изображение: преобразуйте в градации серого, примените пороговую обработку (`cv2.threshold`). |
| **Неправильный язык** | Движок по умолчанию использует язык без нужного набора символов. | Явно задайте `ocr_engine.language` в `ENGLISH` или нужную локаль. |
| **Задержка производительности** | Повторный запуск OCR на больших изображениях. | Измените размер изображения перед загрузкой или обрабатывайте только ROI, предварительно обрезав его. |

## Расширение примера: несколько ROI

Иногда в счёте требуется несколько полей — например, **извлечение текста из счёта** как для общей суммы, так и для даты. Можно пройтись по списку прямоугольников:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

Такой подход сохраняет код чистым и упрощает добавление новых областей в дальнейшем.

## Заключение

Мы только что рассмотрели полный сквозной процесс **извлечения текста из изображения** с помощью Python OCR, сосредоточившись на конкретной области. **Загружая изображение для OCR**, определяя **область интереса** и вызывая движок, вы можете надёжно **читать текст из области** — идеально для получения сумм из счетов, дат из чеков или любых других локализованных данных.  

Не стесняйтесь экспериментировать

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом пособии. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}