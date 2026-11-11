---
category: general
date: 2026-03-26
description: Узнайте, как выполнять OCR в Python и распознавать текст из файлов изображений.
  Это руководство показывает, как быстро извлекать текст из PNG и преобразовывать
  изображение в текст.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: ru
og_description: Как выполнить OCR в Python? Следуйте этому руководству, чтобы распознавать
  текст с изображения, извлекать текст из PNG и преобразовывать изображение в текст
  с пробной лицензией.
og_title: Как выполнить OCR в Python — Полный учебник
tags:
- OCR
- Python
- Image Processing
title: Как выполнить OCR в Python — Полный пошаговый учебник
url: /ru/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR в Python – Полный пошаговый учебник  

Когда‑нибудь задавались вопросом **как выполнять OCR** на фотографии, которую вы только что сделали на телефоне? Вы не одиноки — разработчики повсюду нуждаются в надёжном способе распознавать текст из файлов изображений, не возясь со сложными нативными библиотеками.  

В этом учебнике мы пройдём через практический пример, показывающий **как выполнять OCR**, **recognize text from image**, и **extract text from PNG** с помощью лёгкого Python‑обёртки. К концу вы сможете **convert image to text** всего в несколько строк кода, и вам не придётся беспокоиться о проблемах с лицензированием, потому что мы будем использовать встроенный пробный режим.

## Что вы узнаете  

* Как настроить пробную лицензию для OCR‑движка (не требуется путь к файлу).  
* Точный порядок вызовов для объектов **recognize text from image**.  
* Способы **extract text from PNG** файлов и обработка распространённых проблем, таких как отсутствие шрифтов.  
* Советы по масштабированию решения при переходе от пробной к производственной лицензии.  

**Требования** — вам нужен Python 3.8+ и пакет `ocr` (устанавливается через `pip install ocr`). Другие внешние инструменты не требуются.

---  

![пример выполнения OCR](https://example.com/ocr-demo.png "как выполнить OCR в Python — отображённый распознанный текст")  

*Текст alt изображения: как выполнить OCR в Python — пример вывода*  

## Шаг 1 — Активировать пробную лицензию (путь к файлу не нужен)  

Прежде чем движок сможет что‑то прочитать, ему нужна действительная лицензия. Пробный режим идеален для экспериментов и небольших проектов.

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*Почему это важно:* Объект лицензии сообщает OCR‑библиотеке, что вы работаете в песочнице. Если пропустить этот шаг, движок выбросит `LicenseError` в момент вызова `recognize()`.  

**Pro tip:** При переходе на платную лицензию замените две строки выше на `ocr.License("path/to/your/license.key").apply()`.

## Шаг 2 — Создать экземпляр OCR‑движка  

Теперь, когда пробный режим активирован, мы создаём основной движок. Считайте его «мозгом», который будет смотреть на изображение и определять, какие символы где находятся.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*Почему это важно:* `OcrEngine` хранит конфигурацию, такую как языковые пакеты и настройки DPI. Позже их можно изменить, но значение по умолчанию подходит для большинства PNG‑файлов только на английском.

## Шаг 3 — Загрузить PNG, который нужно обработать  

Здесь мы **recognize text from image**. Метод `ocr.Imaging.Image.load()` поддерживает PNG, JPEG, BMP и несколько других форматов.

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*Edge case:* Если ваш PNG использует индексированную палитру (часто встречается в скриншотах), загрузчик автоматически преобразует его в 24‑битный RGB‑буфер. Это небольшое снижение производительности, но гарантирует точные результаты OCR.

## Шаг 4 — Запустить OCR и получить текст  

Наконец, просим движок выполнить свою работу и вытянуть результат в виде обычного текста.

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**Ожидаемый вывод** (пример для простого изображения с надписью «Hello World»):

```
Hello World
```

Если изображение содержит несколько строк, вывод сохранит разрывы строк, что упрощает передачу данных в последующие процессы, такие как CSV‑парсеры или NLP‑конвейеры.

## Опционально: Тонкая настройка для повышения точности  

* **Language packs:** `ocr_engine.set_language("eng")` (по умолчанию) или `"fra"` для французского.  
* **DPI scaling:** `ocr_engine.set_dpi(300)` может улучшить результаты при сканировании с низким разрешением.  
* **Pre‑processing:** Применение бинарного порога (`ocr.Imaging.Image.threshold()`) перед `set_image` часто даёт более чистый текст на шумных фонах.

Эти настройки полезны, когда вы переходите от быстрой демонстрации к производственному **ocr tutorial python**, обрабатывающему сотни файлов в день.

## Полный скрипт — готов к копированию и вставке  

Ниже представлен полный, исполняемый скрипт, объединяющий все шаги выше. Сохраните его как `run_ocr.py` и замените `YOUR_DIRECTORY/sample1.png` на путь к вашему собственному PNG.

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

Запустите его из командной строки:

```bash
python run_ocr.py
```

Вы должны увидеть извлечённый текст, выведенный в консоль. Если получаете пустую строку, проверьте, что изображение действительно содержит чёткий, контрастный текст и что пробная лицензия применена без ошибок.

## Часто задаваемые вопросы и подводные камни  

* **«Работает ли это с JPEG?»** — Абсолютно. Метод `load()` автоматически определяет формат, так что вы можете заменить PNG на JPEG без изменения кода.  
* **«Что делать, если изображение повернуто?»** — Движок может автоматически определить ориентацию, но для лучшего результата можно предварительно повернуть изображение с помощью `input_image.rotate(90)` перед `set_image`.  
* **«Можно ли обрабатывать несколько изображений в цикле?»** — Да. Просто перенесите загрузку и вызовы `recognize()` внутрь цикла `for`; один и тот же экземпляр `ocr_engine` можно переиспользовать, что экономит небольшие ресурсы.  

## Следующие шаги — от демо к продакшн  

Теперь, когда вы знаете **как выполнять OCR**, рассмотрите следующие темы:

* **Batch processing** — Скомбинируйте этот скрипт с `os.listdir()`, чтобы **extract text from PNG** файлов пакетно.  
* **Integrate with PDF** — Используйте `pdf2image` для преобразования страниц PDF в PNG, а затем передайте их в тот же конвейер.  
* **Post‑processing** — Применяйте regex или нечеткое сравнение для очистки типичных ошибок OCR (например, «0» vs «O»).  

Каждый из этих пунктов опирается на базовую идею **convert image to text** и расширяет полезность вашего OCR‑рабочего процесса.

---  

### TL;DR  

Мы рассмотрели всё, что нужно знать, чтобы **how to perform OCR** в Python: активировать пробную лицензию, создать движок, загрузить PNG, запустить распознавание и вывести результат. Всего лишь несколькими строками кода вы можете **recognize text from image**, **extract text from PNG** и **convert image to text** для любой последующей задачи.  

Попробуйте, поиграйте с настройками DPI или языка, и позвольте движку выполнить тяжёлую работу. Приятного кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}