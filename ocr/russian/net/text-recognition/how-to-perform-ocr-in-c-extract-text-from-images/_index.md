---
category: general
date: 2026-10-08
description: Узнайте, как выполнять OCR в C# с помощью Aspose.OCR для извлечения текста
  из файлов изображений. Это руководство покажет, как преобразовать изображение в
  текст и распознать текст из JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- recognize text from jpeg
- c# ocr example
language: ru
lastmod: 2026-10-08
og_description: Как выполнить OCR в C# с помощью Aspose.OCR. Следуйте этому пошаговому
  руководству, чтобы извлекать текст из файлов изображений, преобразовывать изображение
  в текст и распознавать текст из JPEG.
og_image_alt: Console output displaying Cyrillic text recognized from a JPEG image
  by a C# OCR program
og_title: Как выполнить OCR в C# — извлекать текст из изображений
schemas:
- author: Aspose
  dateModified: '2026-10-08'
  description: Learn how to perform OCR in C# using Aspose.OCR to extract text from
    image files. This guide shows you how to convert image to text and recognize text
    from JPEG.
  headline: How to perform OCR in C# – extract text from images
  type: TechArticle
- description: Learn how to perform OCR in C# using Aspose.OCR to extract text from
    image files. This guide shows you how to convert image to text and recognize text
    from JPEG.
  name: How to perform OCR in C# – extract text from images
  steps:
  - name: Why each line matters
    text: '* **`OcrEngine ocrEngine = new OcrEngine();`** – Instantiates the engine
      that orchestrates the whole OCR pipeline. * **`ocrEngine.Language = Language.Cyrillic;`**
      – Selects the language model. Choosing the correct language dramatically improves
      accuracy when you **extract text from image** files tha'
  - name: 4.1 Recognizing English or multilingual text
    text: 'Replace the language assignment with the appropriate enum:'
  - name: 4.2 Processing images from a stream instead of a file
    text: 'If your image arrives via an HTTP response or a database blob, use a `MemoryStream`:'
  - name: 4.3 Handling large or low‑resolution images
    text: 'Large images increase memory consumption. You can downscale before OCR:'
  - name: 4.4 Error handling
    text: 'Wrap the recognition call in a try‑catch block to catch network or file‑access
      errors:'
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
- Image Processing
title: Как выполнить OCR в C# – извлекать текст из изображений
url: /ru/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR в C# – извлечение текста из изображений

Если вам нужно **как выполнять OCR** в .NET‑приложении, этот учебник предоставляет готовое решение, которое можно сразу запустить. С помощью Aspose.OCR вы сможете **извлекать текст из изображений**, **преобразовывать изображение в текст** и **распознавать текст из JPEG** всего несколькими строками кода.

Вы увидите весь процесс — от установки библиотеки до вывода распознанной строки — чтобы скопировать пример в свой проект и сразу начать обработку изображений.

## Что вы узнаете

* Как настроить проект C# для задач OCR.  
* Как загрузить JPEG (или любое поддерживаемое изображение) и выполнить распознавание.  
* Как получить полученный текст и использовать его в приложении.  

Единственное требование — недавний .NET SDK (≥ .NET 6) и подключение к интернету для первой загрузки языковой модели.

## Шаг 1: Настройка проекта и установка Aspose.OCR

1. Создайте новый консольный проект:

   ```bash
   dotnet new console -n OcrDemo
   cd OcrDemo
   ```

2. Добавьте пакет Aspose.OCR через NuGet:

   ```bash
   dotnet add package Aspose.OCR
   ```

   Пакет содержит OCR‑движок, языковые модели и утилиты для работы с изображениями, необходимые для **преобразования изображения в текст**.

> **Pro tip:** Если планируете выполнять OCR над множеством изображений, рассмотрите возможность добавления пакета в общую библиотеку, чтобы переиспользовать один экземпляр движка.

## Шаг 2: Написание примера OCR на C#

Создайте или замените файл `Program.cs` следующим кодом. Он демонстрирует **c# ocr example**, работающий с любым форматом изображения, поддерживаемым Aspose.OCR (JPEG, PNG, BMP и др.).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // ---------------------------------------------------------
        // Step 2.1: Create an OCR engine instance
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // Step 2.2: Choose the language model.
        // The example uses Cyrillic; replace with Language.English,
        // Language.French, etc., to match your source image.
        // ---------------------------------------------------------
        ocrEngine.Language = Language.Cyrillic; // <-- change as needed

        // ---------------------------------------------------------
        // Step 2.3: Load the image you want to process.
        // ImageStream.FromFile automatically reads JPEG, PNG, BMP…
        // ---------------------------------------------------------
        ocrEngine.Image = ImageStream.FromFile("sample_cyrillic.jpg");

        // ---------------------------------------------------------
        // Step 2.4: Run the recognition process.
        // This call downloads the required language model the first
        // time it is used, then performs the OCR.
        // ---------------------------------------------------------
        ocrEngine.Recognize();

        // ---------------------------------------------------------
        // Step 2.5: Retrieve the recognized text.
        // The Text property holds the result of the OCR engine.
        // ---------------------------------------------------------
        string recognizedText = ocrEngine.Text;

        // ---------------------------------------------------------
        // Step 2.6: Display the output.
        // This is where you can further process the string,
        // e.g., save to a database, feed to a search index, etc.
        // ---------------------------------------------------------
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

### Почему важна каждая строка

* **`OcrEngine ocrEngine = new OcrEngine();`** — создаёт экземпляр движка, управляющего всей OCR‑конвейерой.  
* **`ocrEngine.Language = Language.Cyrillic;`** — выбирает языковую модель. Правильный язык существенно повышает точность при **извлечении текста из изображений**, содержащих нелатинские символы.  
* **`ocrEngine.Image = ImageStream.FromFile(...);`** — загружает исходный JPEG (или любое другое поддерживаемое изображение). Этот шаг необходим для **распознавания текста из jpeg**.  
* **`ocrEngine.Recognize();`** — запускает основной OCR‑алгоритм. Метод блокирует выполнение, пока движок не завершит обработку.  
* **`ocrEngine.Text;`** — возвращает результат в виде обычного текста, который теперь можно **преобразовать изображение в текст** для дальнейшей логики.

## Шаг 3: Запуск программы и проверка вывода

Скомпилируйте и выполните:

```bash
dotnet run
```

Если изображение `sample_cyrillic.jpg` содержит кириллическую фразу «Привет мир», консоль выведет:

```
=== Recognized Text ===
Привет мир
```

Этот вывод подтверждает, что вы успешно освоили **как выполнять OCR** и **извлекать текст из изображений** с помощью C#.

## Шаг 4: Распространённые варианты и граничные случаи

### 4.1 Распознавание английского или многоязычного текста

Замените назначение языка на соответствующее значение enum:

```csharp
ocrEngine.Language = Language.English;           // English only
ocrEngine.Language = Language.Multilingual;      // Detects many languages automatically
```

### 4.2 Обработка изображений из потока вместо файла

Если изображение поступает через HTTP‑ответ или BLOB в базе данных, используйте `MemoryStream`:

```csharp
using (var ms = new MemoryStream(imageBytes))
{
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
}
```

### 4.3 Работа с большими или низкокачественными изображениями

Большие изображения увеличивают потребление памяти. Перед OCR их можно уменьшить:

```csharp
ocrEngine.Config.ImagePreprocessOptions.ScaleFactor = 0.5; // Reduce size by 50%
```

### 4.4 Обработка ошибок

Обёрните вызов распознавания в блок try‑catch, чтобы отлавливать сетевые или файловые ошибки:

```csharp
try
{
    ocrEngine.Recognize();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

## Шаг 5: Следующие шаги — расширение вашего OCR‑процесса

* **Пакетная обработка:** перебирайте файлы в каталоге, **преобразуя изображение в текст** для каждого JPEG.  
* **Пост‑обработка:** применяйте регулярные выражения для очистки распознанной строки, что полезно, когда нужно **извлекать текст из изображений** форм или счетов.  
* **Интеграция с Azure Cognitive Services:** сравните результаты Aspose.OCR с облачными OCR‑сервисами для повышения точности при сложных макетах.  
* **Сохранение результатов:** сохраняйте извлечённый текст в базе данных SQL или в индексе ElasticSearch для последующего поиска по документам.

---

## Заключение

Теперь вы знаете **как выполнять OCR** в C# с помощью Aspose.OCR, от установки пакета до вывода распознанной строки. Этот полный **c# ocr example** позволяет **извлекать текст из изображений**, **преобразовывать изображение в текст** и **распознавать текст из JPEG** всего в несколько строк кода. Экспериментируйте с различными языковыми моделями, источниками изображений и методами пост‑обработки, чтобы адаптировать решение под свои задачи.

---


## Что изучать дальше?


Следующие учебники охватывают близкие темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Use OCR in C# – Extract Text from Image Files](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-files/)
- [Convert Image to Text in C# with Aspose OCR – Step‑by‑Step Guide](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [How to Perform OCR in C# – Extract Text and Write JSON](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}