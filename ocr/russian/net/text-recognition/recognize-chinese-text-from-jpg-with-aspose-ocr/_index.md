---
category: general
date: 2026-04-08
description: Узнайте, как распознавать китайский текст на JPG‑изображениях с помощью
  Aspose OCR. Это пошаговое руководство также покажет, как быстро извлекать текст
  из изображения.
draft: false
keywords:
- recognize chinese text
- extract text from image
- recognize text from jpg
- Aspose OCR C#
- offline OCR resources
language: ru
og_description: распознавать китайский текст на JPG‑изображениях с помощью Aspose
  OCR. Следуйте этому полному руководству, чтобы извлечь текст из изображения офлайн.
og_title: распознавать китайский текст из JPG с помощью Aspose OCR
tags:
- OCR
- C#
- Aspose
title: распознать китайский текст из JPG с помощью Aspose OCR
url: /ru/net/text-recognition/recognize-chinese-text-from-jpg-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# распознавание китайского текста из JPG с помощью Aspose OCR

Когда‑нибудь вам нужно было **распознать китайский текст** из JPG‑файла, но вы не знали, с чего начать? Вы не одиноки — многие разработчики сталкиваются с этой проблемой при создании многоязычных приложений сканирования. Хорошая новость в том, что Aspose OCR делает это проще простого, даже когда нужно работать офлайн.

В этом руководстве мы пройдем весь процесс извлечения текста из изображения, в стиле **extract text from image**, и покажем, как именно **recognize text from jpg** с помощью C#. К концу вы получите исполняемую программу, которая читает изображение на китайском языке и выводит распознанные символы в консоль.

## Что понадобится

- .NET 6.0 или новее (подойдет любая актуальная версия)
- Пакет NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Файл ресурсов китайского языка (в руководстве показано, как загрузить его офлайн)
- Файл изображения с именем `chinese_sample.jpg`, размещённый в папке, которой вы управляете

Никаких сложных трюков в IDE не требуется — подойдут Visual Studio, Rider или даже VS Code.

## Шаг 1: Создание проекта и установка Aspose OCR

Сначала создайте новый консольный проект и подключите библиотеку Aspose OCR.

```bash
dotnet new console -n ChineseOcrDemo
cd ChineseOcrDemo
dotnet add package Aspose.OCR
```

**Pro tip:** Если вы находитесь за корпоративным прокси, добавьте флаг `--no-cache`, чтобы принудительно выполнить новое скачивание.

## Шаг 2: Отключение автоматической загрузки ресурсов

Aspose OCR может загружать языковые пакеты «на лету», но в продакшене обычно требуется поставлять файлы вместе с приложением. Отключение автоматической загрузки предотвращает неожиданные сетевые запросы.

```csharp
using Aspose.Ocr;

// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Turn off the auto‑download feature
ocrEngine.Options.EnableAutomaticResourceDownload = false;
```

Зачем мы это делаем? Хранение ресурсов локально гарантирует стабильную производительность и позволяет запускать приложение на машинах без доступа к интернету.

## Шаг 3: Загрузка китайских языковых ресурсов офлайн

Aspose поставляет языковые данные в виде отдельных файлов. Предположим, вы разместили китайский пакет (`zh`) в папке `Resources` рядом с исполняемым файлом, загрузите его так:

```csharp
// Path to the folder that contains the language files
string resourcePath = Path.Combine(AppContext.BaseDirectory, "Resources");

// Tell the engine where to look for resources
ocrEngine.Options.ResourcesFolder = resourcePath;

// Load the Simplified Chinese resources (offline = true)
ocrEngine.LoadLanguageResources("zh", offline: true);
```

**Watch out:** Если путь указан неверно, вы получите `FileNotFoundException`. Проверьте правильность имени папки и регистр символов в Linux.

## Шаг 4: Установка языка движка на китайский

Теперь, когда данные загружены, укажите движку правильный код языка.

```csharp
ocrEngine.Language = "zh"; // “zh” = Simplified Chinese
```

Явная установка языка повышает точность, поскольку OCR не будет тратить ресурсы на угадывание скриптов.

## Шаг 5: Распознавание текста из JPG‑изображения

Это основная часть руководства — передать JPG движку и извлечь текст.

```csharp
// Full path to the image you want to process
string imagePath = Path.Combine(AppContext.BaseDirectory, "chinese_sample.jpg");

// Run the OCR operation
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

// Output the raw result
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

Если всё прошло успешно, консоль отобразит китайские символы, содержащиеся в `chinese_sample.jpg`. Вы также можете получить `ocrResult.Confidence` для оценки качества.

## Шаг 6: Полный рабочий пример

Собрав все части вместе, вы получаете готовую к запуску программу. Сохраните её как `Program.cs` в папке вашего проекта.

```csharp
using System;
using System.IO;
using Aspose.Ocr;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // 2️⃣ Disable automatic resource download
        // -------------------------------------------------
        ocrEngine.Options.EnableAutomaticResourceDownload = false;

        // -------------------------------------------------
        // 3️⃣ Load Chinese language resources (offline)
        // -------------------------------------------------
        string resourcePath = Path.Combine(AppContext.BaseDirectory, "Resources");
        ocrEngine.Options.ResourcesFolder = resourcePath;
        ocrEngine.LoadLanguageResources("zh", offline: true);

        // -------------------------------------------------
        // 4️⃣ Set language to Simplified Chinese
        // -------------------------------------------------
        ocrEngine.Language = "zh";

        // -------------------------------------------------
        // 5️⃣ Recognize text from a JPG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppContext.BaseDirectory, "chinese_sample.jpg");
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // -------------------------------------------------
        // 6️⃣ Show the result
        // -------------------------------------------------
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine($"\nConfidence: {ocrResult.Confidence:P2}");
    }
}
```

### Ожидаемый вывод

```
=== Recognized Chinese Text ===
欢迎使用Aspose OCR示例
Confidence: 96.45%
```

Точный вывод будет зависеть от исходного изображения, но вы должны увидеть блок китайских символов, за которым следует процент уверенности.

## Шаг 7: Распространённые варианты и граничные случаи

### Распознавание текста из PNG или BMP

Метод `RecognizeImage` принимает любой формат, поддерживаемый `System.Drawing` в .NET. Просто измените расширение файла:

```csharp
ocrEngine.RecognizeImage("sample.png");
```

### Обработка нескольких языков

Если вам нужно **extract text from image**, содержащий смесь английского и китайского, загрузите оба языковых пакета и установите `ocrEngine.Language = "zh,en";`. Движок автоматически переключится между скриптами.

### Работа с изображениями низкого разрешения

Низкое DPI может сильно ухудшить точность OCR. Перед вызовом `RecognizeImage` вы можете увеличить масштаб изображения:

```csharp
using System.Drawing;

Bitmap bmp = new Bitmap(imagePath);
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
highRes.Save("highres.jpg");
ocrResult = ocrEngine.RecognizeImage("highres.jpg");
```

Помните, увеличение масштаба не добавит деталей волшебным образом, но даст алгоритму больше пикселей для обработки.

## Шаг 8: Тестирование и проверка

Быстрая проверка — сравнить вывод OCR с известной эталонной строкой.

```csharp
string expected = "欢迎使用Aspose OCR示例";
bool matches = ocrResult.Text.Trim() == expected;
Console.WriteLine($"Match with expected? {matches}");
```

Если `matches` равно `false`, попробуйте скорректировать изображение (например, увеличить контраст) или включить `ocrEngine.Options.UseAdvancedPreprocessing = true`.

## Заключение

Вы только что узнали, как **recognize chinese text** из JPG‑файла с помощью Aspose OCR, и теперь знаете, как **extract text from image** в полностью офлайн‑сценарии. Полное решение — инициализация, загрузка ресурсов, выбор языка и обработка изображения — помещается в одно простое консольное приложение.

Что дальше? Попробуйте передать пакет изображений в тот же движок, поэкспериментировать с разными языковыми пакетами или интегрировать шаг OCR в ASP .NET Web API, чтобы пользователи могли загружать картинки и получать перевод текста в реальном времени. Возможности безграничны, когда вы сочетаете надёжный OCR с современными инструментами .NET.

Удачной разработки, и не стесняйтесь оставлять комментарий, если столкнётесь с проблемами!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}