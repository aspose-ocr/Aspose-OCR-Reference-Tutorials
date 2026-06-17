---
category: general
date: 2026-02-16
description: Узнайте, как выполнять OCR в C# с помощью Aspose.OCR — распознавать текст
  с фотографии, считывать текст со сканирования и извлекать текст из чека с высокой
  точностью.
draft: false
keywords:
- how to perform OCR
- recognize text from photo
- read text from scan
- extract text from receipt
- improve OCR accuracy
language: ru
og_description: Узнайте, как выполнять OCR в C# с помощью Aspose.OCR. Это руководство
  покажет, как распознавать текст с фотографии, читать текст со сканированного изображения
  и извлекать текст из чека.
og_title: Как выполнить OCR в C# – Полное руководство Aspose
tags:
- C#
- Aspose.OCR
- Image Processing
title: Как выполнить OCR в C# – полное руководство Aspose
url: /ru/net/text-recognition/how-to-perform-ocr-in-c-complete-aspose-guide/
---

Now produce final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR в C# – Полное руководство Aspose

Когда‑нибудь задумывались **как выполнять OCR** на размытом чеке или случайном фото, которое вы сделали на телефоне? Вы не одиноки. Во многих реальных приложениях нам нужно **распознавать текст с фото** файлов, **читать текст со сканированных** документов или **извлекать текст из изображений чеков**, не отправляя данные в облачный сервис.  

В этом руководстве мы пройдем через автономный пример, который покажет вам **как выполнять OCR** с помощью Aspose.OCR, и добавим советы о том, как **повысить точность OCR** по ходу. К концу у вас будет готовая к запуску консольная программа на C#, которая извлекает обычный текст из любого изображения, которое вы укажете.

> **Что понадобится**  
> * .NET 6 SDK (или любая современная версия .NET)  
> * NuGet‑пакет Aspose.OCR (`Install-Package Aspose.OCR`)  
> * Пример изображения — например, фото чека с именем `photo_receipt.jpg`  

Если это вам знакомо, отлично — давайте погрузимся.

![how to perform OCR example](image.png){alt="как выполнять OCR"}

## Как выполнять OCR с Aspose.OCR в C#

Первый шаг — настроить OCR‑движок и загрузить модель английского языка. Это ядро **как выполнять OCR** с Aspose; без языковой модели движок не будет знать, какие символы искать.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the English language model – change this if you need another language
ocrEngine.LoadLanguage(LanguageModel.English);
```

*Почему это важно*: Загрузка правильной языковой модели напрямую влияет на скорость распознавания и точность. Английский — самый распространённый вариант, но Aspose поставляется с десятками других, если вам когда‑нибудь понадобится **читать текст со сканированных** документов на французском, немецком и т.д.

## Распознавание текста с фото

Фотографии, сделанные телефоном, часто страдают от поворота, шума или низкого контраста. Прежде чем попросить движок **распознать текст с фото**, мы настраиваем некоторые параметры предобработки, которые очищают изображение.

```csharp
// Configure preprocessing to boost OCR results
PreprocessingOptions preprocessingOptions = new PreprocessingOptions
{
    Deskew = true,                     // Auto‑correct rotation (helps with tilted receipts)
    Denoise = DenoiseLevel.Medium,    // Reduce graininess
    Binarize = BinarizeMethod.Otsu,   // Convert to black‑and‑white for sharper edges
    ContrastEnhancement = true        // Boost contrast for faint characters
};

// Apply the preprocessing configuration
ocrEngine.Preprocessing = preprocessingOptions;
```

*Совет профессионала*: Если вы замечаете пропущенные символы, попробуйте переключить `DenoiseLevel` на `High` или использовать `BinarizeMethod.Sauvola`. Эти настройки являются частью стратегий **повышения точности OCR**.

## Чтение текста со сканированных документов

Теперь, когда движок подготовлен, мы загружаем изображение. Будь то отсканированная страница PDF, сохранённая как JPEG, или фото печатной формы, код остаётся тем же.

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/photo_receipt.jpg");
```

Если у вас есть `Stream` вместо пути к файлу, просто замените `FromFile` на `FromStream`. Такая гибкость удобна, когда вы **читаете текст со сканированных** изображений, полученных из веб‑загрузки.

## Извлечение текста из чека

Когда всё настроено, фактический вызов OCR — это одна строка. Метод возвращает извлечённую строку обычного текста, которую мы затем можем отобразить, сохранить или передать в другую систему.

```csharp
// Perform OCR and capture the result
string extractedText = ocrEngine.Recognize();

// Output the text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(extractedText);
```

**Ожидаемый вывод** (пример простого чека):

```
=== OCR RESULT ===
Store: CoffeeShop
Date: 2024-02-15
Item      Qty   Price
Latte      2    4.50
Bagel      1    2.75
Total            7.25
```

Если вывод выглядит искажённым, вернитесь к разделу предобработки — это самое распространённое место для **повышения точности OCR**.

## Повышение точности OCR — продвинутые настройки

Хотя настройки по умолчанию работают во многих случаях, производственные конвейеры часто требуют дополнительного внимания:

| Situation | Adjustment | Reason |
|-----------|------------|--------|
| Очень тёмный фон | `ContrastEnhancement = true` + `Binarize = BinarizeMethod.Sauvola` | Увеличивает разделение текста и фона |
| Рукописные заметки | `ocrEngine.LoadLanguage(LanguageModel.EnglishHandwritten)` | Специализированная модель для курсивных штрихов |
| Многостраничные сканы | Loop over each page image and call `Recognize()` per iteration | Сохраняет небольшой объём памяти |
| Большие изображения (> 2000 px) | Resize before feeding to OCR (`Image.Resize(width, height)`) | Быстрее обработка, меньше нагрузки на память |

Помните, **как выполнять OCR** — это не универсальный рецепт; вам часто придётся экспериментировать с этими настройками, пока вывод не достигнет требуемого уровня качества.

## Полный рабочий пример

Ниже представлен полный готовый к копированию и вставке код программы. Он включает все обсуждаемые части, а также небольшую вспомогательную функцию, проверяющую наличие файла перед попыткой чтения.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine and load language
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.LoadLanguage(LanguageModel.English);

        // 2️⃣ Set up preprocessing to improve OCR accuracy
        ocrEngine.Preprocessing = new PreprocessingOptions
        {
            Deskew = true,
            Denoise = DenoiseLevel.Medium,
            Binarize = BinarizeMethod.Otsu,
            ContrastEnhancement = true
        };

        // 3️⃣ Path to the image – change this to your own file
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo_receipt.jpg");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"⚠️  Image not found: {imagePath}");
            return;
        }

        // 4️⃣ Load the image (recognize text from photo / read text from scan)
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 5️⃣ Perform OCR – this is the core of how to perform OCR
        string extractedText = ocrEngine.Recognize();

        // 6️⃣ Show the result – you can now extract text from receipt, invoice, etc.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(extractedText);
    }
}
```

Запустите программу командой `dotnet run`. Если всё настроено правильно, вы увидите извлечённый текст, выведенный в консоль.

## Часто задаваемые вопросы и особые случаи

**В: Что если изображение — PDF?**  
О: Сначала преобразуйте каждую страницу PDF в изображение (например, с помощью `Aspose.Pdf` или `PdfSharp`), а затем передайте полученный bitmap в `ocrEngine.Image`.

**В: Можно ли обрабатывать изображения параллельно?**  
О: Да, но создавайте отдельный `OcrEngine` для каждого потока. Движок не является потокобезопасным, поэтому совместное использование одной инстанции может вызвать состояния гонки.

**В: Работает ли это на Linux?**  
О: Абсолютно. Aspose.OCR кросс‑платформенный; просто убедитесь, что установлены нативные зависимости (`libgdiplus` для .NET Core на Linux).

**В: Как обрабатывать многоязычные чеки?**  
О: Загрузите несколько языковых моделей перед распознаванием:  
```csharp
ocrEngine.LoadLanguage(LanguageModel.English);
ocrEngine.LoadLanguage(LanguageModel.Spanish);
```  
Движок будет последовательно пробовать каждую модель.

## Заключение

Теперь у вас есть надёжное, сквозное решение **как выполнять OCR** в C# с Aspose.OCR. Руководство охватило всё: от инициализации движка, **распознавания текста с фото**, **чтения текста со сканированных** документов, до **извлечения текста из чека**, и предоставило практические способы **повысить точность OCR**.  

Следующие шаги? Попробуйте заменить английскую модель на модель рукописного текста, поэкспериментировать с различными значениями `BinarizeMethod` или интегрировать вызов OCR в ASP.NET API, который обрабатывает загрузки «на лету». Возможности так же безграничны, как и изображения, которые вы подаёте.  

Есть дополнительные вопросы по OCR, предобработке изображений или библиотекам Aspose? Оставьте комментарий или изучите официальную документацию Aspose.OCR для более глубокого погружения. Счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}