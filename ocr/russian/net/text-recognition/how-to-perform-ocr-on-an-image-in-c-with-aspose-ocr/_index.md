---
category: general
date: 2026-10-18
description: Быстро выполните OCR изображения в C#. Узнайте, как извлекать текст из
  JPG, преобразовывать изображение в текст и считывать текст с изображения с помощью
  Aspose.OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- convert image to text
- read text from image
- load image for OCR
language: ru
lastmod: 2026-10-18
og_description: Выполните OCR изображения в C# с помощью Aspose.OCR. Этот учебник
  показывает, как извлечь текст из JPG, преобразовать изображение в текст и прочитать
  текст с изображения за несколько минут.
og_image_alt: Console output displaying recognized Cyrillic text after performing
  OCR on an image
og_title: Выполнить OCR изображения в C# – полное руководство
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Perform OCR on an image in C# quickly. Learn to extract text from JPG,
    convert image to text and read text from image using Aspose.OCR.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
title: Как выполнить OCR изображения в C# с Aspose.OCR
url: /ru/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнить OCR на изображении в C# с Aspose.OCR

Если вам нужно **выполнять OCR на изображении** в .NET‑приложении, это руководство покажет вам полное, готовое к запуску решение. Вы увидите, как **загружать изображение для OCR**, распознавать кириллические символы и **извлекать текст из JPG** файлов без написания какого‑либо низкоуровневого кода обработки изображений.

В этом руководстве вы:

* Установите пакет Aspose.OCR NuGet.  
* Загрузите файл изображения (JPG, PNG, BMP и т.д.).  
* Запустите OCR‑движок для **преобразования изображения в текст**.  
* **Считайте текст из изображения** и выведите его в консоль.  

Эти шаги работают с любым совместимым с .NET изображением, поэтому их можно адаптировать для PDF, сканированных чеков или скриншотов.

## Требования

* .NET 6.0 SDK или новее (код также работает с .NET Framework 4.7+).  
* Visual Studio 2022 или любой другой предпочитаемый редактор C#.  
* Доступ в Интернет при первом запуске — Aspose.OCR автоматически загружает модуль кириллического языка.  

> **Pro tip:** Держите пакет NuGet в актуальном состоянии; более новые версии повышают точность распознавания и добавляют языковые пакеты.

## Шаг 1: Установите Aspose.OCR

Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.OCR
```

Пакет содержит класс `OcrEngine`, используемый для **выполнения OCR на файлах изображений**. После завершения команды ссылка на пакет появится в вашем файле *.csproj*.

## Шаг 2: Создайте каркас консольного приложения

Создайте новый консольный проект, если у вас его ещё нет:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Замените сгенерированный *Program.cs* кодом, показанным в следующих разделах. Каркас включает необходимые директивы `using` и метод `Main`, который управляет процессом OCR.

## Шаг 3: Загрузите изображение для OCR

Первая рабочая строка кода **загружает изображение**, которое вы хотите проанализировать. Aspose.OCR принимает любой поток, поэтому вы можете загрузить файл с диска, веб‑URL или встроенный ресурс.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Step 3: Load the image containing Cyrillic text
        // Replace the path with the location of your JPG file.
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);
```

*Почему это важно*: `ImageStream.FromFile` абстрагирует работу с форматами, гарантируя, что OCR‑движок получит согласованный bitmap независимо от исходного типа файла. Поток также автоматически освобождается благодаря оператору `using`.

## Шаг 4: Инициализируйте OCR‑движок и задайте язык (необязательно)

По умолчанию Aspose.OCR пытается автоматически определить язык. Для кириллического текста вы можете явно указать модуль `Language.Cyrillic`, что ускорит первую загрузку.

```csharp
        // Step 4: Initialize the OCR engine
        var engine = new OcrEngine();

        // Optional: force Cyrillic language to avoid auto‑detection overhead
        engine.Language = Language.Cyrillic;
```

Если не указать язык, движок загрузит необходимый модуль при первом вызове `Recognize`. Загрузка происходит по HTTPS и кэшируется локально для последующих запусков.

## Шаг 5: Выполните OCR и преобразуйте изображение в текст

Теперь вы действительно **выполняете OCR на изображении** и получаете строку обычного текста. Метод `Recognize` делает всю тяжелую работу: предобработку, анализ макета и классификацию символов.

```csharp
        // Step 5: Perform OCR – convert image to text
        engine.Image = image;
        string recognizedText = engine.Recognize();
```

Возвращаемый `recognizedText` содержит разрывы строк, соответствующие оригинальному макету, что упрощает пост‑обработку или сохранение в базе данных.

## Шаг 6: Выведите результат — прочитайте текст из изображения

Наконец, **прочитайте текст из изображения**, записав результат в консоль. Этот шаг подтверждает успешность OCR и показывает, что именно было извлечено.

```csharp
        // Step 6: Display the recognized text – read text from image
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

При запуске программы (`dotnet run`) вы должны увидеть вывод, похожий на:

```
=== OCR Result ===
Пример текста на кириллице
```

> **Примечание:** Точный вывод зависит от качества исходного JPG. Четкие, высокоразрешающие изображения дают наилучшие результаты.

## Полный, готовый к запуску исходный код

Ниже представлена полная программа, которую можно скопировать в *Program.cs* и выполнить без изменений (за исключением пути к изображению).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Load the image containing Cyrillic text
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);

        // Initialize the OCR engine
        var engine = new OcrEngine
        {
            // Force Cyrillic language; optional but speeds up first run
            Language = Language.Cyrillic,
            Image = image
        };

        // Recognize the text – this converts the image to text
        string recognizedText = engine.Recognize();

        // Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

Запуск программы выводит извлечённые символы в консоль, подтверждая, что вы успешно **извлекли текст из JPG** и **преобразовали изображение в текст**.

## Обработка распространённых вариантов

| Сценарий | Корректировка |
|----------|---------------|
| **Другой язык** | Установите `engine.Language = Language.English;` или другой поддерживаемый enum. |
| **Многостраничный PDF** | Преобразуйте каждую страницу в изображение (например, с помощью `Aspose.PDF`) и вызовите OCR‑цикл для каждого изображения. |
| **Большая партия** | Оберните вызов OCR в цикл `Parallel.ForEach`; переиспользуйте один экземпляр `OcrEngine` для снижения нагрузки памяти. |
| **Низкое разрешение изображения** | Предобработайте с помощью `engine.Image = ImageProcessing.Filters.GaussianBlur(image, 1.5);` для уменьшения шума перед распознаванием. |

Эти варианты позволяют **извлекать текст из JPG** файлов любого языка, размера и качества.

## Советы по производительности

* **Кешировать языковые модули** — первая загрузка может занять несколько секунд; последующие запуски мгновенны. |
* **Переиспользовать экземпляр `OcrEngine`** для нескольких изображений, чтобы избежать повторных расходов на инициализацию. |
* **Ограничить размер изображения** — очень большие фотографии увеличивают потребление памяти. Сократите ширину до максимум 2000 px перед передачей в движок.

## Заключение

Теперь вы знаете, как **выполнять OCR на изображениях** в C# с помощью Aspose.OCR. Загрузив изображение, настроив движок и вызвав `Recognize`, вы можете **извлекать текст из JPG**, **преобразовывать изображение в текст** и **читать текст из изображения** всего несколькими строками кода.  

Далее вы можете исследовать:

* Сохранение результатов OCR в базе данных для поисковых архивов.  
* Интеграцию процесса в веб‑API, принимающее загруженные изображения.  
* Использование других языковых модулей (Arabic, Hindi и т.д.) для расширения возможностей вашего приложения.

Не бойтесь экспериментировать с различными форматами изображений, языками и стратегиями пакетной обработки. Основной шаблон — **загрузить изображение для OCR → распознать → обработать полученный текст** — остается тем же, обеспечивая надёжную основу для любого проекта по извлечению текста.

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Извлечение текста из изображения C# с выбором языка с помощью Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Преобразование изображения в текст — выполнение OCR на изображении по URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Как извлечь текст из изображения с помощью Aspose.OCR для .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}