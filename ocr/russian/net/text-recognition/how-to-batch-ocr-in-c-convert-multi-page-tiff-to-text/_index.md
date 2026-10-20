---
category: general
date: 2026-03-28
description: Узнайте, как выполнять пакетное OCR на C# и легко преобразовывать TIFF
  в текст. Это пошаговое руководство показывает, как извлекать текст из файлов TIFF
  с помощью Aspose OCR.
draft: false
keywords:
- how to batch ocr
- convert tiff to text
- extract text from tiff
- c# ocr tutorial
language: ru
og_description: Как выполнять пакетное OCR в C#? Следуйте этому полному руководству,
  чтобы преобразовать многостраничные TIFF‑файлы в поисковый текст с помощью Aspose
  OCR.
og_title: Как пакетно выполнять OCR в C# — преобразовать многостраничный TIFF в текст
tags:
- OCR
- C#
- Aspose
title: Как пакетно выполнять OCR в C# — преобразовать многостраничный TIFF в текст
url: /ru/net/text-recognition/how-to-batch-ocr-in-c-convert-multi-page-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять пакетное OCR в C# – Преобразование многостраничного TIFF в текст

Вы когда‑нибудь задумывались **как выполнять пакетное OCR** стопку отсканированных страниц без написания цикла для каждого изображения? Вы не одиноки. Во многих проектах — например, обработка счетов или оцифровка архивов — необходимость **преобразовать TIFF в текст** возникает ежедневно, а обработка по одной странице за раз быстро превращается в кошмар.

Хорошая новость? С несколькими строками C# и Aspose OCR вы можете передать целый многостраничный TIFF в движок и получить словарь, где номера страниц сопоставлены с извлечёнными строками. В этом руководстве мы пройдём полный, готовый к запуску пример, который показывает точно **как выполнять пакетное OCR**, как **извлекать текст из TIFF**, и почему этот подход лучше ручного варианта.

## Что вы узнаете

- Настроить библиотеку Aspose OCR в .NET‑проекте.  
- Загрузить многостраничный TIFF‑файл с помощью `Image.FromMultiPageFile`.  
- Запустить `RecognizeBatch`, чтобы получить `Dictionary<int,string>` с результатами по страницам.  
- Вывести результат в чистом, читаемом формате.  

К концу вы получите готовое к запуску консольное приложение, которое преобразует любой многостраничный TIFF в обычный текст — без дополнительных инструментов.  

### Требования

- .NET 6.0 SDK (или любая современная версия .NET).  
- Visual Studio 2022 или VS Code — ваш любимый IDE подойдёт.  
- Действительная лицензия Aspose OCR или бесплатный оценочный ключ (API работает без лицензии, но добавляет водяной знак).  
- Пример многостраничного TIFF с именем `multipage.tif`, размещённый в папке, к которой вы можете обратиться.

> **Pro tip:** Если вы работаете в Windows, папка проекта по умолчанию — удобное место для размещения TIFF; в Linux/macOS просто скорректируйте путь соответственно.

## Шаг 1: Установить NuGet‑пакет Aspose OCR

Прежде чем писать код, нам нужна библиотека OCR. Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.OCR
```

Это загрузит последнюю стабильную версию (на март 2026 v23.9) и добавит необходимые DLL‑файлы в ваш проект. Дополнительная конфигурация для простого консольного приложения не требуется.

## Шаг 2: Создать каркас консольного приложения

Сформируем минимальную программу, которая ссылается на OCR‑движок. Директивы `using` критически важны — без них компилятор будет ругаться на недостающие типы.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Required for Image class
```

> **Почему это важно:** Класс `Image` находится в под‑пространстве имён, и если забыть импорт `ImageProcessing`, вы получите ошибку «type or namespace not found», что может отнять час отладки.

Теперь добавьте метод `Main` и короткий комментарий, описывающий цель:

```csharp
/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        // Implementation will go here
    }
}
```

## Шаг 3: Инициализировать OCR‑движок

`OcrEngine` — это рабочая лошадка. Создавать его один раз и переиспользовать для всех страниц одновременно экономит память и ускоряет работу.

```csharp
// Step 3: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **Что происходит под капотом?** Движок загружает языковые модели и предварительно настраивает параметры по умолчанию (например, английский, авто‑поворот). Позже их можно изменить, но значения по умолчанию подходят для большинства документов.

## Шаг 4: Загрузить многостраничный TIFF

Aspose упрощает загрузку многокадровых изображений. Укажите полный путь или относительный от рабочей директории исполняемого файла.

```csharp
// Step 4: Load a multi‑page TIFF image
string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // ← replace with your actual path
var multiPageImage = Image.FromMultiPageFile(tiffPath);
```

Если файл не найден, `FromMultiPageFile` бросит `FileNotFoundException`. Оберните вызов в `try/catch`, если нужна плавная обработка ошибок — это мы покажем в следующем шаге.

## Шаг 5: Выполнить пакетное OCR

Настало время звёздного элемента: `RecognizeBatch`. Он возвращает `Dictionary<int,string>`, где ключ — индекс страницы (начиная с 0), а значение — распознанный текст.

```csharp
// Step 5: Perform batch OCR on all pages
Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);
```

> **Особый случай:** Некоторые TIFF‑файлы содержат пустые страницы. Aspose возвращает пустую строку для таких страниц, которую можно отфильтровать позже, если не хотите захламлять вывод.

## Шаг 6: Вывести результаты

Наконец, пройдитесь по словарю и выведите текст каждой страницы. Интерполированные строки делают код аккуратным.

```csharp
// Step 6: Output the recognized text for each page
foreach (var pageResult in ocrResults)
{
    Console.WriteLine($"--- Page {pageResult.Key + 1} ---"); // +1 for human‑friendly numbering
    Console.WriteLine(pageResult.Value);
    Console.WriteLine(); // Blank line for readability
}
```

Запуск программы должен дать примерно следующее:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
...

--- Page 2 ---
Terms and Conditions
...
```

Если вывод выглядит искажённым, проверьте, что исходный TIFF не повреждён и что язык текста соответствует языку по умолчанию в движке (английский). Для неанглийских документов можно установить `ocrEngine.Language = OcrLanguage.Spanish;`.

## Полный рабочий пример

Собрав все части вместе, получаем полную программу, которую можно скопировать в `Program.cs` и запустить:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Needed for Image class

/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        try
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Load a multi‑page TIFF image
            string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // Change to your actual file location
            var multiPageImage = Image.FromMultiPageFile(tiffPath);

            // Step 3: Perform batch OCR on all pages
            Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);

            // Step 4: Output the recognized text for each page
            foreach (var pageResult in ocrResults)
            {
                Console.WriteLine($"--- Page {pageResult.Key + 1} ---");
                Console.WriteLine(pageResult.Value);
                Console.WriteLine(); // Extra line for visual separation
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

Сохраните, соберите и запустите:

```bash
dotnet run
```

Вы увидите извлечённое содержимое каждой страницы в консоли. Это и есть весь **c# ocr tutorial**, который вы запросили.

## Часто задаваемые вопросы и особые случаи

### Что делать, если мой TIFF содержит десятки страниц?

`RecognizeBatch` обрабатывает все кадры одним вызовом, но потребление памяти растёт линейно с количеством страниц. Для очень больших документов (сотни страниц) рассмотрите обработку частями:

```csharp
for (int i = 0; i < multiPageImage.PageCount; i += 50)
{
    var subImage = multiPageImage.GetPages(i, Math.Min(50, multiPageImage.PageCount - i));
    var partialResults = ocrEngine.RecognizeBatch(subImage);
    // Merge partialResults into the main dictionary...
}
```

### Можно ли сохранять извлечённый текст в файлы вместо вывода в консоль?

Конечно. Замените блок `Console.WriteLine` на операции ввода‑вывода файлов:

```csharp
string outputFolder = "ExtractedText";
Directory.CreateDirectory(outputFolder);

foreach (var pageResult in ocrResults)
{
    string filePath = Path.Combine(outputFolder, $"Page_{pageResult.Key + 1}.txt");
    File.WriteAllText(filePath, pageResult.Value);
}
```

Теперь каждая страница будет сохраняться в отдельный файл `.txt` — идеально для последующей индексации.

### Как изменить язык вывода или включить авто‑поворот?

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
ocrEngine.AutoRotate = true;             // Detects rotated text automatically
```

Эти настройки необходимо применять **до** вызова `RecognizeBatch`.

## Заключение

Мы рассмотрели **как выполнять пакетное OCR** многостраничного TIFF с помощью Aspose OCR в C#. Загрузив изображение один раз, вызвав `RecognizeBatch` и пройдясь по полученному словарю, вы сможете **преобразовать TIFF в текст** за считанные секунды. Пример также показывает, как **извлекать текст из TIFF**, обрабатывать ошибки и при желании записывать результаты в файлы — всё в чистом, автономном консольном приложении.

Готовы к следующему шагу? Попробуйте сочетать этот подход с библиотекой генерации PDF, чтобы получать поисковые PDF, или подключите вывод к базе данных для архивов с поиском. Вы также можете поэкспериментировать с другими форматами изображений (PNG, JPEG), заменив `Image.FromMultiPageFile` на `Image.FromFile`.

Есть дополнительные вопросы об OCR, лицензировании или оптимизации производительности? Оставляйте комментарий ниже, и удачной разработки!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}