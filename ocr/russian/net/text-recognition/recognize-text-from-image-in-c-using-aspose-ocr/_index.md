---
category: general
date: 2026-05-31
description: Узнайте, как распознавать текст на изображении в C# с помощью Aspose
  OCR, включая извлечение текста из файлов TIFF и эффективную загрузку изображения
  для OCR.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: ru
og_description: Пошаговое руководство по распознаванию текста на изображении с помощью
  Aspose OCR, охватывающее извлечение из TIFF и правильную загрузку изображения для
  OCR.
og_title: распознавание текста с изображения в C# с использованием Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: распознавание текста с изображения в C# с использованием Aspose OCR
url: /ru/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# распознавание текста с изображения в C# с помощью Aspose OCR

Когда‑то вам нужно было **распознать текст с изображения**, но вы не знали, с чего начать в C#? Вы не одиноки — многие разработчики сталкиваются с этой проблемой при работе со сканированными документами или многостраничными TIFF‑файлами. В этом руководстве мы пройдемся по полностью готовому к запуску примеру, который **распознает текст с изображения** с использованием библиотеки Aspose OCR, а также покажем, как **извлечь текст из tiff** и лучший способ **загрузить изображение для OCR**, не теряя волосы.

Мы рассмотрим всё: от установки пакета NuGet до работы с ускорением GPU и переходом на CPU при необходимости. К концу этого урока у вас будет консольное приложение, которое выводит распознанный текст и время обработки — без пропусков и расплывчатых ссылок.

## Что вы создадите

- Простое консольное приложение .NET, которое загружает изображение (включая многостраничный TIFF)  
- OCR‑движок, настроенный для использования GPU, с плавным откатом на CPU  
- Извлечение обычного текста из изображения, вывод в консоль  
- Информация о времени выполнения, чтобы увидеть разницу между GPU и CPU  

**Требования**

- .NET 6 SDK или новее (код работает с .NET Core и .NET Framework)  
- Базовые знания C# и работы в командной строке  
- Доступ в Интернет для загрузки пакета Aspose.OCR из NuGet  

Если всё это у вас есть, приступим.

![C# code to recognize text from image using Aspose OCR](image.png "C# code to recognize text from image using Aspose OCR")

## Шаг 1 – Распознавание текста с изображения: настройка OCR‑движка

Прежде всего, нам нужен экземпляр `OcrEngine`. Aspose OCR позволяет выбрать устройство обработки — GPU для скорости, CPU как запасной вариант. Движок также принимает подсказку о лимите памяти, что может быть полезно на общих машинах.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**Почему это важно:**  
Выбор `OcrDevice.Gpu` может сократить время распознавания на несколько секунд для больших изображений, особенно многостраничных TIFF. Параметр `GpuMemoryLimit` не позволяет приложению захватывать всю видеопамять на совместном рабочем месте.

## Шаг 2 – Загрузка изображения для OCR (поддержка TIFF)

Теперь передаём изображение движку. `ImageStream.FromFile` от Aspose принимает **любой** поддерживаемый формат — TIFF, PNG, JPEG и т.д. Этот шаг напрямую отвечает требованию **загрузить изображение для OCR**.

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**Совет:** Если вы работаете с многостраничным TIFF, Aspose автоматически рассматривает каждую страницу как отдельный кадр, и движок будет обрабатывать их последовательно. Дополнительный код не нужен.

## Шаг 3 – Запуск распознавания и **извлечение текста из tiff**

С готовым движком и загруженным изображением запускаем OCR‑операцию. Метод `Recognize` возвращает `OcrResult`, содержащий обычный текст, оценки уверенности и детали времени.

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**Обработка граничных случаев:**  
Если GPU недоступен, `engine.Recognize()` всё равно работает, потому что движок тихо переключается на CPU. При необходимости вы можете проверить `engine.Device` после распознавания, чтобы узнать, какое устройство использовалось.

## Шаг 4 – Получение распознанного обычного текста

Извлечение текста простое — достаточно обратиться к свойству `Text`. Здесь мы наконец **извлекаем текст из tiff** (или любого другого изображения) и показываем его пользователю.

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

Вы увидите «сырые» символы, переносы строк сохраняются так, как они находятся в исходном изображении. Для более структурированного вывода (например, JSON или CSV) можно обратиться к `result.Regions` и `result.Lines`, но обычный текст обычно достаточно для быстрых скриптов.

## Шаг 5 – Измерение времени обработки и обработка отката GPU

Производительность важна, особенно при обработке десятков страниц. Свойство `ProcessingTime` точно показывает, сколько времени занял OCR, независимо от того, работал ли он на GPU или CPU.

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Почему это стоит учитывать:**  
Если время резко возрастает, попробуйте отрегулировать `GpuMemoryLimit` или явно переключиться на CPU (`Device = OcrDevice.Cpu`). И наоборот, субсекундный результат на большом TIFF означает, что ускорение GPU делает своё дело.

## Полный готовый к запуску пример

Скопируйте код ниже в новый консольный проект (`dotnet new console -n OcrDemo`) и выполните `dotnet add package Aspose.OCR`. Затем замените `YOUR_DIRECTORY/sample_multi_page.tif` на путь к вашему изображению.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Ожидаемый вывод (усечённый для краткости):**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

Если на вашем компьютере нет подходящего GPU, время выполнения может быть на несколько секунд дольше, но текст всё равно будет извлечён корректно.

## Часто задаваемые вопросы и подводные камни

- **Что делать, если изображение огромное (более 10 МБ)?**  
  Снизьте его разрешение перед передачей в движок или увеличьте `GpuMemoryLimit`, если у вас достаточно видеопамяти.  
- **Можно ли обрабатывать несколько изображений в цикле?**  
  Конечно. Просто переиспользуйте один экземпляр `OcrEngine` и присваивайте новый `ImageStream` на каждой итерации.  
- **Нужно ли что‑то освобождать?**  
  `OcrEngine` реализует `IDisposable`. Оберните его в блок `using` для корректного управления ресурсами, особенно при работе с GPU.  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **А как насчёт других языков, кроме английского?**  
  Установите `engine.Language = OcrLanguage.Spanish` (или любой поддерживаемый язык) перед вызовом `Recognize()`.  

## Заключение

Теперь у вас есть полное сквозное решение, которое **распознаёт текст с изображения** в C# с помощью Aspose OCR. В руководстве показано, как **загрузить изображение для OCR**, как **извлечь текст из tiff** и как измерять производительность, плавно обрабатывая откат с GPU на CPU.

Дальше вы можете:

- Поэкспериментировать с различными форматами изображений (BMP, PDF), чтобы увидеть, как их обрабатывает Aspose.  
- Погрузиться в `result.Regions` для получения данных о ограничивающих прямоугольниках, если вам нужен анализ макета.

## Что изучать дальше?

- [Как использовать Aspose для распознавания изображения из потока в OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Извлечение текста из изображения – оптимизация OCR с Aspose.OCR для .NET](/ocr/english/net/ocr-optimization/)
- [Извлечение текста из изображения – распознавание строк с Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}