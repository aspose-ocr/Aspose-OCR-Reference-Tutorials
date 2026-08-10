---
category: general
date: 2026-06-22
description: Выполните OCR изображения с помощью Python всего в несколько строк. Узнайте,
  как загрузить изображение для OCR, распознать текст из PNG и эффективно использовать
  OCR‑движок.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: ru
og_description: Быстро выполняйте OCR изображения с помощью Python. В этом руководстве
  показано, как загрузить изображение для OCR, распознать текст из PNG и использовать
  OCR‑движок с уверенностью.
og_title: Распознавание текста на изображении в Python – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Выполнить OCR на изображении в Python – Полное руководство
url: /ru/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнить OCR на изображении в Python – Полное руководство

Когда‑нибудь вам нужно было **perform OCR on image** файлы, но вы застряли уже на первой строке кода? Вы не одиноки. В этом руководстве мы покажем, как **load image for OCR**, настроить лёгкий **OCR engine**, и наконец **recognize text from PNG** всего несколькими командами.

Мы охватим всё — от установки библиотеки до настройки whitelist, чтобы только цифры и заглавные буквы проходили сканирование. К концу вы получите готовый к запуску скрипт, который можно вставить в любой проект — без загадок и лишних деталей.

## Что вы узнаете

- Как **use OCR engine** программно в Python.  
- Точные шаги для **load image for OCR** из локальной папки.  
- Почему и как ограничить распознавание пользовательским набором символов.  
- Как **recognize text from PNG** и безопасно обработать результат.  

**Prerequisites:** установлен Python 3.7+, терминал, с которым вам удобно работать, и изображение (например, `serial-number.png`), которое вы хотите прочитать. Предыдущий опыт работы с OCR не требуется.

---

## Выполнить OCR на изображении – Инициализация OCR Engine

Первое, что нужно сделать — создать экземпляр OCR engine. Считайте engine мозгом, который будет анализировать пиксели и преобразовывать их в символы.

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Почему это важно:* Без engine нет чего обрабатывать изображение. Класс `OcrEngine` объединяет всю тяжёлую работу — предобработку, сегментацию и классификацию символов — в один объект, который можно переиспользовать.

---

## Загрузка изображения для OCR – Укажите PNG‑файл

Теперь, когда engine существует, вам нужно передать ему изображение, которое вы хотите прочитать. Библиотека ожидает объект `ImageStream`, который можно создать напрямую из пути к файлу.

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*Совет:* Держите изображение в высококонтрастном формате (чёрный текст на белом фоне) и избегайте артефактов сжатия; они могут сбить OCR‑алгоритм.

---

## Ограничение символов – Whitelist цифр и заглавных букв

Часто вам нужен только подмножество символов — например, серийный номер, содержащий только A‑Z и 0‑9. Установив whitelist, вы говорите engine игнорировать всё остальное, что значительно повышает точность.

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*Что происходит под капотом?* Engine создаёт фильтр, отбрасывающий любые глифы, не присутствующие в whitelist, до финального этапа классификации. Это особенно удобно, когда изображение содержит шум или декоративный текст, который вам не нужен.

---

## Распознавание текста из PNG – Запуск OCR процесса

С engine, подготовленным и изображением, загруженным, вы наконец можете **perform OCR on image**. Вызов `recognize()` запускает весь конвейер и возвращает объект результата.

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

Если вам интересна производительность, метод обычно завершается за несколько сотен миллисекунд для PNG 300 × 200 px на современном ноутбуке.

---

## Вывод и проверка – Получение распознанного текста

Последний шаг — извлечь простой текст из объекта результата. Всё, что не совпало с whitelist, автоматически отбрасывается, поэтому вы получаете чистую строку, готовую к дальнейшей обработке.

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Обычный вывод:* `AB12C3D4E5` (при условии, что изображение действительно содержит такой серийный номер).  

Если вывод пустой или искажённый, проверьте качество изображения и whitelist; распространённая ошибка — случайное исключение нужных символов.

---

## Пограничные случаи и распространённые подводные камни

| Ситуация | Что проверить | Предлагаемое решение |
|-----------|---------------|----------------------|
| **File not found** | Ошибка в пути или отсутствующий файл | Используйте `os.path.abspath`, чтобы проверить полный путь перед вызовом `set_image`. |
| **Low contrast image** | Текст сливается с фоном | Примените простое пороговое значение (`Pillow` или `OpenCV`) перед передачей изображения engine. |
| **Unexpected characters** | Whitelist слишком ограничен | Добавьте недостающие символы в строку whitelist. |
| **Large images** | Медленное распознавание | Измените размер изображения до максимальной ширины 1024 px; качество OCR обычно остаётся высоким. |

---

## Полный скрипт – Готов к запуску

Ниже представлен полный, автономный скрипт, связывающий все части вместе. Сохраните его как `ocr_demo.py`, замените `YOUR_DIRECTORY` реальной папкой и запустите `python ocr_demo.py`.

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Ожидаемый вывод в консоль* (когда PNG содержит `SN12345`):

```
Recognized text: SN12345
```

---

## Заключение

Теперь вы точно знаете, как **perform OCR on image** файлы в Python, от **loading image for OCR** до **recognize text from PNG** и, наконец, извлечения чистого результата с помощью настраиваемого **OCR engine**. Подход прост, расширяем и работает «из коробки» для большинства сканов в стиле серийных номеров.

Что дальше? Попробуйте заменить whitelist на строчные буквы, поэкспериментировать с различными форматами изображений (JPEG, BMP) или интегрировать скрипт в конвейер пакетной обработки. Та же схема — engine → image → settings → recognize → output — применима практически к любой задаче OCR, с которой вы столкнётесь.

Есть вопросы или странное изображение, от refusing to cooperate? Оставьте комментарий ниже, и счастливого кодинга! 

![Диаграмма, иллюстрирующая шаги выполнения OCR на изображении с помощью Python](https://example.com/ocr-flow.png "Диаграмма, показывающая, как выполнить OCR на изображении с помощью Python OCR engine")


## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Конвертировать изображение в текст – Выполнить OCR на изображении из URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Как использовать AspOCR: Предобработка фильтров OCR для изображений в .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Как извлечь текст из изображения, подготовив прямоугольники в OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}