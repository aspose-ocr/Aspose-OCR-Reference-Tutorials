---
category: general
date: 2026-03-29
description: Извлеките текст из изображения с помощью Aspose OCR на C#. Узнайте, как
  автоматически вращать OCR и как исправлять наклон отсканированного изображения для
  идеальных результатов.
draft: false
keywords:
- extract text from image
- auto rotate ocr
- how to deskew scanned image
- Aspose OCR C#
- image preprocessing OCR
language: ru
og_description: Извлечение текста из изображения с помощью Aspose OCR. В этом руководстве
  показано автоматическое вращение OCR и как исправить наклон отсканированного изображения
  в C#.
og_title: Извлечение текста из изображения в C# – автоповорот OCR и исправление наклона
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Извлечение текста из изображения в C# – Руководство по авто‑повороту OCR и
  исправлению наклона
url: /ru/net/ocr-optimization/extract-text-from-image-in-c-auto-rotate-ocr-deskew-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения в C# – руководство по авто‑повороту OCR и исправлению наклона

Когда‑то вам нужно **извлечь текст из изображения**, но файл пришёл под странным углом? Это частая проблема — особенно с отсканированными счетами, сфотографированными чеками или кривыми PDF‑файлами. Хорошая новость: писать собственный алгоритм вращения не требуется. С помощью встроенной функции *auto rotate OCR* в Aspose OCR вы можете позволить движку выпрямить картинку и затем **извлечь текст из изображения** за один плавный шаг.

В этом руководстве мы пройдём полный, готовый к запуску пример на C#, который:

* Инициализирует OCR‑движок с автоматическим определением ориентации и исправлением наклона,
* Распознаёт повернутое или искажённое изображение,
* Возвращает как обнаруженный угол поворота, так и извлечённый текст.

Никаких внешних сервисов, никаких сложных вычислений — лишь несколько строк кода и чёткое объяснение *how to deskew scanned image* при необходимости.

## Что понадобится

| Требование | Зачем это нужно |
|------------|-----------------|
| .NET 6.0 или новее (или .NET Framework 4.6+) | Aspose OCR поставляется как NuGet‑пакет, поддерживающий эти рантаймы. |
| Visual Studio 2022 (или любой редактор C#) | Упрощает добавление NuGet‑пакетов и запуск консольного приложения. |
| Пример изображения (`rotated_document.jpg`) | Файл должен быть JPEG, PNG, BMP или TIFF и не быть идеально вертикальным. |
| NuGet‑пакет Aspose.OCR (`Install-Package Aspose.OCR`) | Содержит `OcrEngine`, `PreprocessingFilters` и связанные типы. |

Если все пункты отмечены, можно начинать. В противном случае скачайте последнюю версию Aspose OCR из NuGet — установка в один клик.

---

## Шаг 1 – Инициализация OCR‑движка (Primary Keyword in Action)

Первым делом создаём экземпляр `OcrEngine` и указываем ему **auto rotate OCR** и **deskew** для любого входящего изображения. Эти два флага объединяются побитовым ИЛИ (`|`), потому что `PreprocessingFilters` — это enum с атрибутом `[Flags]`.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine with English language and preprocessing options
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Enable both auto‑rotate and auto‑deskew
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };
```

> **Почему это важно:**  
> *Auto‑rotate OCR* анализирует базовую линию текста на изображении, определяет правильную ориентацию и вращает её внутренне перед распознаванием. *Auto‑deskew* делает то же самое для небольших наклонов, часто встречающихся в сканах. Включив оба флага, вы получаете наилучшие результаты **extract text from image** без ручного редактирования изображения.

---

## Шаг 2 – Распознавание изображения и получение результата

Теперь передаём движку путь к файлу. Метод `RecognizeImage` возвращает объект `OcrResult`, содержащий обнаруженный угол поворота, оценки уверенности и простой текстовый вывод.

```csharp
        // Recognise the image file and obtain the OCR result
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/rotated_document.jpg");
```

> **Подсказка:** Если работаете со стримом (например, загруженным файлом), используйте `ocrEngine.RecognizeImage(Stream)`. Те же флаги предобработки применяются, так что вы всё равно получаете преимущества **auto rotate OCR**.

---

## Шаг 3 – Вывод угла поворота и извлечённого текста

В конце выводим в консоль два значения: угол, который, по мнению движка, нужно было повернуть, и сам текст, который он извлек.

```csharp
        // Show the detected rotation and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Ожидаемый вывод** (числа будут другими в зависимости от вашего изображения):

```
Detected rotation: 12.3°
----- Extracted Text -----
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Если изображение уже было вертикальным, угол поворота будет `0°`, а текст всё равно будет чистым благодаря алгоритму *auto‑deskew*.

---

## Шаг 4 – Понимание того, как исправить наклон сканированного изображения (Secondary Keyword Deep‑Dive)

Возможно, вы задаётесь вопросом *how to deskew scanned image*, когда OCR‑движок сообщает ненулевой угол. Под капотом Aspose OCR использует **преобразование Хафа** для определения доминирующей ориентации строк текста. Затем он вращает bitmap на обратный к этому углу, эффективно выпрямляя текст.

**Когда это важно?**  
* Сканеры, подающие листы под небольшим углом (часто в офисах).  
* Фотографии, сделанные смартфоном вручную — горизонт редко бывает идеален.  

**Обработка граничных случаев:**  
Если `RotationAngle` в результате слишком большой (например, > 45°), движок мог неверно интерпретировать изображение (возможно, это логотип или графика без текста). В таком случае можно:

1. Вручную повернуть изображение с помощью `System.Drawing` перед передачей его в движок, или  
2. Отключить `AutoRotate` и оставить только `AutoDeskew`, если вы уверены, что документ уже вертикален.

```csharp
// Example: manually rotate 90° clockwise before OCR
using (var img = Aspose.OCR.Image.Load("rotated_document.jpg"))
{
    img.Rotate(90);
    OcrResult result = ocrEngine.RecognizeImage(img);
    Console.WriteLine(result.Text);
}
```

---

## Шаг 5 – Частые ошибки и профессиональные советы (E‑E‑A‑T в действии)

| Ошибка | Почему происходит | Как исправить |
|--------|-------------------|---------------|
| **Размытые или низкокачественные изображения** | Точность OCR резко падает; определение угла может не сработать. | Используйте сканы не менее 300 dpi; примените фильтр резкости перед OCR. |
| **Смешанные языки** | По умолчанию движок выбирает английский; иностранные символы искажаются. | Установите `Language = Language.English | Language.Spanish` (или нужную комбинацию). |
| **Большие файлы (> 10 MB)** | Давление на память может вызвать `OutOfMemoryException`. | Сначала уменьшите размер изображения или обрабатывайте его частями через `OcrEngine.RecognizeRegion`. |
| **Неправильный путь к файлу** | `FileNotFoundException` останавливает программу. | Используйте `Path.Combine(Environment.CurrentDirectory, "rotated_document.jpg")` для надёжности. |

> **Профессиональный совет:** Всегда логируйте `ocrResult.RotationAngle` и `ocrResult.Confidence` (если доступно). Эти метрики помогают решить, стоит ли повторять попытку с другими настройками предобработки.

---

## Шаг 6 – Расширение примера (Что дальше?)

Теперь, когда вы умеете **extract text from image** с авто‑поворотом и исправлением наклона, можно рассмотреть следующие шаги:

* **Пакетная обработка** — перебрать папку с изображениями, сохранять каждый результат в базе данных и помечать те, у которых `RotationAngle > 5°`, для ручной проверки.  
* **Конвертация в PDF** — объединить извлечённый текст с оригинальным изображением в поисковый PDF с помощью Aspose.PDF.  
* **Определение языка** — использовать флаг `AutoDetectLanguage` в Aspose.OCR, чтобы движок автоматически выбирал лучший язык.  

Все эти варианты опираются на один и тот же принцип: библиотека сама решает проблему ориентации, а вы сосредотачиваетесь на бизнес‑логике.

---

## Полный рабочий пример (готов к копированию)

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine with auto‑rotate and auto‑deskew
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };

        // 2️⃣ Recognise the image – replace the path with your own file
        string imagePath = "YOUR_DIRECTORY/rotated_document.jpg";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 3️⃣ Output the rotation angle and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Сохраните файл как `Program.cs`, выполните `dotnet add package Aspose.OCR`, затем `dotnet run`. Вы увидите угол и чистый текст, выведенные в консоль.

---

## Заключение

Мы продемонстрировали, как **extract text from image** в C#, позволяя Aspose OCR заниматься *auto rotate OCR* и сложной задачей *how to deskew scanned image*. Включив два флага предобработки, движок автоматически выпрямляет кривые картинки, определяет правильную ориентацию и выдаёт точный текст — без ручного редактирования изображений.

Экспериментируйте с большими партиями, разными языками или интегрируйте вывод в поисковый PDF. Возможности безграничны, когда OCR‑движок берёт на себя тяжёлую работу.

**Готовы улучшить ваш документооборот?** Возьмите код, укажите свои сканы и наблюдайте, как исчезают углы поворота. Если возникнут вопросы, оставляйте комментарий ниже — happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}