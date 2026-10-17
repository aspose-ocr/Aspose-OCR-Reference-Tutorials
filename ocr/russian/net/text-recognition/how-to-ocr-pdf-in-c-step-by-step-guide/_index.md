---
category: general
date: 2025-12-29
description: Узнайте, как выполнять OCR PDF‑файлов в C# и извлекать текст со страниц
  PDF. Этот учебник также охватывает преобразование PDF в текст и техники чтения страниц
  PDF на C#.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- extract pdf text c#
- read pdf page c#
language: ru
og_description: Как выполнить OCR PDF в C# — краткое руководство. Получите полный
  код для извлечения текста из PDF, преобразования PDF в текст и чтения страниц PDF
  на C#.
og_title: Как распознавать PDF с помощью OCR в C# – Полное руководство по программированию
tags:
- OCR
- C#
- PDF processing
title: Как выполнять OCR PDF в C# – пошаговое руководство
url: /ru/net/text-recognition/how-to-ocr-pdf-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнить OCR PDF в C# – Пошаговое руководство

Когда‑нибудь задумывались **how to OCR PDF** прямо из вашего C# приложения? Возможно, у вас есть стопка отсканированных счетов, и нужно извлечь из них текст без ручного копирования. Это распространённая проблема, особенно когда PDF‑файлы основаны на изображениях и традиционный извлечения текста не работает.  

В этом руководстве мы пройдем полный, готовый к запуску пример, который не только покажет, **how to OCR PDF**, но и продемонстрирует, как *extract text from PDF*, *convert PDF to text* и *read PDF page C#* с помощью библиотеки Aspose.OCR. Никаких расплывчатых ссылок — только код, который можно вставить в Visual Studio и сразу начать экспериментировать.

## Что понадобится

- **.NET 6.0** или новее (код также работает на .NET Framework 4.7+)  
- **Aspose.OCR** пакет NuGet – установить командой `dotnet add package Aspose.OCR`  
- Отсканированный PDF (например, `invoice.pdf`), размещённый в папке, к которой вы можете обратиться  
- Базовые знания о консольных приложениях C#  

Вот и всё. Если у вас уже есть проект, просто добавьте пакет и вы готовы к работе.

## Шаг 1: Создайте проект и добавьте Aspose.OCR

Сначала создайте новый консольный проект (или используйте существующий) и подключите библиотеку OCR.

```csharp
// Create a new console app (run this in a terminal)
// > dotnet new console -n OcrPdfDemo
// > cd OcrPdfDemo
// > dotnet add package Aspose.OCR
```

Почему это важно: Aspose.OCR берёт на себя тяжёлую работу по анализу изображений, определению макета и распознаванию символов. Без неё вам пришлось бы собирать растризатор, движок Tesseract и множество вспомогательного кода.

## Шаг 2: Подключите пространства имён и подготовьте OCR‑движок

Теперь откройте `Program.cs` (или любой другой .cs файл) и добавьте необходимые директивы `using`.

```csharp
using System;
using Aspose.OCR;   // Core OCR classes
```

Создание движка простое, но мы также настроим пару параметров, повышающих точность на типичных сканах счетов.

```csharp
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // Enable automatic language detection (optional but handy)
    Language = Language.English,
    // Turn on deskew to correct rotated pages
    ImagePreprocessingOptions = new ImagePreprocessingOptions
    {
        Deskew = true,
        Binarization = true
    }
};
```

**Pro tip:** Если язык известен заранее, задайте `Language` явно — это ускорит процесс.

## Шаг 3: Укажите путь к вашему PDF‑файлу

Задайте абсолютный или относительный путь к PDF, который нужно обработать. Для примера будем считать, что файл находится в папке `Samples`.

```csharp
// Path to the PDF you want to OCR
string pdfFilePath = @"Samples/invoice.pdf";

// Verify the file exists early to avoid runtime surprises
if (!System.IO.File.Exists(pdfFilePath))
{
    Console.WriteLine($"File not found: {pdfFilePath}");
    return;
}
```

Проверка существования файла — небольшая, но полезная мера, которая избавит от непонятных исключений позже.

## Шаг 4: Выберите страницу(ы) для чтения

PDF может содержать десятки страниц, но часто нужен только один конкретный лист — скажем, вторая страница счёта, где указана итоговая сумма. Метод `RecognizePdf` позволяет указать отдельную страницу или весь документ.

```csharp
// Extract text from page 2 (page numbers are 1‑based)
int pageNumber = 2;

// The method returns an OcrResult containing the recognized text
OcrResult ocrResult = ocrEngine.RecognizePdf(pdfFilePath, pageNumber);
```

Если нужно *convert PDF to text* для всего документа, просто опустите аргумент `pageNumber`:

```csharp
// OcrResult fullResult = ocrEngine.RecognizePdf(pdfFilePath);
```

## Шаг 5: Выведите или сохраните извлечённый текст

После того как OCR‑движок завершил работу, вы можете вывести текст в консоль, записать его в файл `.txt` или передать в другую систему (например, в базу данных).

```csharp
// Show the recognized text in the console
Console.WriteLine("=== OCR Result (Page {0}) ===", pageNumber);
Console.WriteLine(ocrResult.Text);

// Optionally, save to a .txt file
string outputPath = $"output_page{pageNumber}.txt";
System.IO.File.WriteAllText(outputPath, ocrResult.Text);
Console.WriteLine($"Text saved to {outputPath}");
```

**Почему это важно:** Сохраняя результат, вы создаёте переиспользуемый артефакт — идеальный для последующего анализа или индексации поиска.

## Полный рабочий пример

Собрав всё вместе, получаем автономную программу, которую можно скопировать в `Program.cs` и сразу запустить.

```csharp
using System;
using Aspose.OCR;

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine with helpful options
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                ImagePreprocessingOptions = new ImagePreprocessingOptions
                {
                    Deskew = true,
                    Binarization = true
                }
            };

            // 2️⃣ Define the PDF path
            string pdfFilePath = @"Samples/invoice.pdf";
            if (!System.IO.File.Exists(pdfFilePath))
            {
                Console.WriteLine($"Error: File not found -> {pdfFilePath}");
                return;
            }

            // 3️⃣ Choose which page to OCR (change as needed)
            int pageNumber = 2; // read PDF page C# example

            // 4️⃣ Perform OCR on the selected page
            OcrResult ocrResult = ocrEngine.RecognizePdf(pdfFilePath, pageNumber);

            // 5️⃣ Output the result
            Console.WriteLine($"--- OCR Result for page {pageNumber} ---");
            Console.WriteLine(ocrResult.Text);

            // 6️⃣ Save to a text file for later use
            string outputPath = $"output_page{pageNumber}.txt";
            System.IO.File.WriteAllText(outputPath, ocrResult.Text);
            Console.WriteLine($"Extracted text saved to: {outputPath}");
        }
    }
}
```

### Ожидаемый вывод

```
--- OCR Result for page 2 ---
Invoice #12345
Date: 2024‑11‑30
Total: $1,250.00
...
Extracted text saved to: output_page2.txt
```

Если PDF содержит чёткие, высоко‑разрешённые сканы, вывод будет почти безошибочным. При более низком качестве изображений может потребоваться дополнительная предобработка (например, увеличение DPI или применение фильтров); параметры `ImagePreprocessingOptions` в Aspose.OCR можно настроить под такие сценарии.

## Часто задаваемые вопросы и особые случаи

### 1️⃣ Что делать, если PDF защищён паролем?
Перегрузка `RecognizePdf` в Aspose.OCR принимает объект `PdfLoadOptions`, где можно указать пароль:

```csharp
var loadOptions = new PdfLoadOptions { Password = "mySecret" };
OcrResult result = ocrEngine.RecognizePdf(pdfFilePath, pageNumber, loadOptions);
```

### 2️⃣ Можно ли выполнить OCR всего документа за один проход?
Да — просто вызовите `RecognizePdf(pdfFilePath)` без указания номера страницы. Метод вернёт один `OcrResult` с конкатенированным текстом всех страниц.

### 3️⃣ Чем это отличается от «extract text from PDF» с помощью библиотеки, работающей с текстом?
Чистое извлечение текста (например, через iTextSharp) работает только с PDF, где уже присутствует выбираемый текст. **How to OCR PDF** необходимо, когда PDF представляет собой набор изображений, как в случае отсканированных счетов. В этих случаях OCR‑движок выполняет оптическое распознавание символов, превращая картинки в поисковый текст.

### 4️⃣ Какова производительность на больших PDF?
Время обработки примерно линейно растёт с количеством страниц и разрешением изображений. Для массовой обработки рекомендуется:
- Запускать OCR параллельно (`Parallel.ForEach`)  
- Снижать DPI изображения перед OCR (`Resolution = 150`)  
- Кешировать экземпляр `OcrEngine` вместо создания нового для каждого файла

### 5️⃣ Можно ли получить ограничивающие рамки (bounding boxes) каждого слова?
`OcrResult` предоставляет коллекцию объектов `OcrRegion`, каждый из которых содержит координаты. Их можно перебрать, чтобы построить поисковые PDF или подсвечивать результаты в UI.

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} – ({region.Bounds.X}, {region.Bounds.Y}, {region.Bounds.Width}, {region.Bounds.Height})");
}
```

## Советы для production‑готовых реализаций

- **Обработка ошибок:** Оборачивайте вызовы OCR в блоки try/catch, чтобы отлавливать специфические исключения библиотеки.  
- **Логирование:** Записывайте номера страниц и время обработки; это помогает выявлять проблемные сканы.  
- **Управление памятью:** Освобождайте большие объекты `Bitmap`, если вы вручную конвертируете страницы PDF в изображения перед OCR.  
- **Безопасность:** Никогда не храните оригинальные PDF на небезопасных дисках; лучше передавать их потоково непосредственно в OCR‑движок.  

## Заключение

Теперь у вас есть полное, сквозное решение **how to OCR PDF** с использованием C#. В руководстве рассмотрены все шаги: от установки Aspose.OCR, выбора конкретной страницы, извлечения текста и обработки типичных краевых случаев. С этой базой вы сможете *extract text from PDF*, *convert PDF to text* и *read PDF page C#* в любой конвейер обработки документов.

Готовы к следующему шагу? Попробуйте передать результат OCR в полнотекстовый поисковый движок, например Lucene.NET, или сгенерировать поисковые PDF, накладывая распознанный текст на оригинальные изображения. Возможности безграничны, а теперь у вас есть инструменты, чтобы их реализовать.

---

![how to ocr pdf example](image-placeholder.png "Illustration of OCR processing on a PDF page")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}