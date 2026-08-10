---
category: general
date: 2026-07-05
description: Как быстро исправить наклон изображения. Узнайте, как предобрабатывать
  изображение для OCR, корректировать вращение изображения и преобразовывать скан
  в текст с помощью Python.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: ru
og_description: Как исправить наклон изображения и предобработать его для OCR. Это
  руководство показывает, как скорректировать вращение изображения и извлечь текст
  из него с помощью Python.
og_title: Как выпрямить изображение — пошаговая предобработка OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: Как выпрямить изображение — Полное руководство по предобработке для OCR
url: /ru/python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как исправить наклон изображения – Полное руководство по предобработке для OCR

Когда‑нибудь задумывались **как исправить наклон изображения**, которое выглядит так, будто его отсканировали криво? Вы не одиноки. Во многих реальных проектах первой задачей перед тем, как **извлечь текст из изображения**, является выравнивание этого наклона.  

В этом руководстве мы пройдём пошаговый, сквозной пример, который **подготавливает изображение для OCR**, исправляет вращение и, наконец, **преобразует скан в текст** с помощью библиотеки OCR на Python. Никаких расплывчатых ссылок, только рабочий скрипт, который можно скопировать‑вставить, плюс советы по типичным подводным камням.  

## Что вы получите

К концу этого руководства вы сможете:

* Загрузить любой отсканированный JPEG или PNG, слегка наклонённый.  
* Применить фильтр исправления наклона и шаг бинаризации для повышения точности OCR.  
* Запустить OCR‑движок и **надёжно извлечь текст из изображения**.  
* Понять, почему **правильное вращение изображения** важно для последующего извлечения текста.  

### Предварительные требования

* Python 3.9+ установленный на вашем компьютере.  
* Пакет OCR, устанавливаемый через pip, который использует пространство имён `ocr`, как в примере (например, лёгкая обёртка над Tesseract).  
* Базовое знакомство с функциями Python и концепциями обработки изображений.  

Если всё это у вас есть, давайте начинать.

![how to deskew image example](deskew_before_after.png){alt="как исправить наклон изображения – до и после коррекции"}

## Шаг 1: Настройка OCR‑движка – Как исправить наклон изображения с помощью Python

Первым делом вам нужен OCR‑движок, способный понять язык вашего документа. Ниже показан минимальный шаблон для создания движка и указания, что вы работаете с английским текстом.

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*Почему это важно:* Настройка языка движка определяет набор символов и словарь, которые он будет использовать. Пропуск этого шага может привести к неверному распознаванию обычных слов, особенно после **коррекции вращения изображения**.

## Шаг 2: Загрузка отсканированного изображения, которое нужно выпрямить

Теперь загружаем файл в память. Замените `"YOUR_DIRECTORY/skewed_scan.jpg"` на путь к вашему собственному изображению.

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

Если изображение уже находится в массиве NumPy или в объекте OpenCV `Mat`, вы можете адаптировать загрузчик соответствующим образом – главное, чтобы объект предоставлял метод `apply_filter`, используемый позже.

## Шаг 3: Предобработка изображения для OCR – исправление наклона и бинаризация

Здесь происходит волшебство. Мы последовательно применяем два фильтра:

1. **Deskew** – автоматически определяет доминирующую базовую линию текста и вращает изображение обратно в горизонтальное положение.  
2. **Binarize (Otsu)** – переводит картинку в чистый чёрно‑белый вид, что резко повышает коэффициент распознавания.

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*Полезный совет:* Если после бинаризации текст всё ещё выглядит размытым, попробуйте подрегулировать контраст или использовать иной метод пороговой обработки. В модуле `ocr.Filter` часто есть `adaptive_threshold()` для более сложных случаев.

## Шаг 4: Запуск OCR – извлечение текста из изображения

С чистым, выпрямленным холстом передаём изображение движку. Объект результата содержит распознанную строку, оценки уверенности и даже ограничивающие рамки, если они понадобятся позже.

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

Типичный вывод выглядит так:

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

Заметьте, как переносы строк выровнены идеально? Это преимущество **правильного вращения изображения** – OCR больше не нужно угадывать ориентацию строк.

## Шаг 5: Собираем всё вместе – скрипт в одном файле для преобразования скана в текст

Ниже полный, готовый к запуску скрипт, объединяющий все обсуждённые части. Сохраните его как `deskew_ocr.py` и выполните `python deskew_ocr.py`.

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### Почему это работает

* **Сначала Deskew** – вращение изображения перед бинаризацией гарантирует, что алгоритм пороговой обработки работает на ровном горизонте.  
* **Бинаризация после Deskew** – метод Оцу предполагает би‑модальную гистограмму; наклонённая страница разрушит это предположение.  
* **Модель английского языка** – сообщает OCR, какие символы ожидать, уменьшая количество ложных срабатываний.  

Если нужно поддержать другие языки, просто замените `ocr.Language.ENGLISH` на соответствующий элемент перечисления.

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|----------|--------|
| *Что делать, если скан перевёрнут вверх ногами?* | Фильтр `deskew()` обычно обнаруживает и вращение на 180°. Если не сработает, вызовите `apply_filter(ocr.Filter.rotate(180))` перед исправлением наклона. |
| *В моём документе есть цветная графика – будет ли она удалена при бинаризации?* | Да. Для смешанного контента рассмотрите возможность использовать только `ocr.Filter.deskew()`, а затем запускать OCR на цветном изображении. Текст всё равно будет извлечён, а графика сохранится. |
| *Можно ли обработать пакет файлов?* | Оберните логику в цикл, считывайте каждый путь из списка и сохраняйте `result.text` в отдельный `.txt` файл. |
| *Как повысить точность при сканах низкого разрешения?* | Перед Deskew увеличьте изображение с помощью бикубической фильтрации **до** исправления наклона, затем примените фильтр резкости. Больше пикселей дают OCR‑движку больше подсказок. |

## Бонус: визуальная проверка исправления наклона

Если хотите увидеть «до‑и‑после» рядом, добавьте небольшой фрагмент кода Matplotlib:

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

Наглядный контроль выровненности может быть очень полезен, особенно при отладке сложных наборов сканов.

## Заключение

Мы рассмотрели **как исправить наклон изображения**, почему **предобработка изображения для OCR** так важна, и как **извлечь текст из изображения**, чтобы наконец **преобразовать скан в текст**. Последовательность «загрузка → исправление наклона → бинаризация → распознавание» гарантирует, что OCR получает чистую, ровную страницу, что приводит к более высокой точности и меньшему количеству ручных исправлений.

Что дальше в вашем OCR‑путешествии? Попробуйте поэкспериментировать с:

* Разными языковыми пакетами (`ocr.Language.FRENCH` и др.).  
* Добавлением шага анализа макета для обнаружения колонок или таблиц.  
* Экспортом результатов OCR в поисковые PDF с помощью библиотеки для работы с PDF.

Оставляйте комментарии, если столкнётесь с проблемой, или делитесь своими настройками для особенно упорных сканов. Приятного кодинга, и пусть ваши изображения всегда остаются идеально ровными!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гайде. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}