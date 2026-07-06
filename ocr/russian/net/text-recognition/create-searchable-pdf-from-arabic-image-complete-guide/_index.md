---
category: general
date: 2026-02-11
description: Создайте PDF с возможностью поиска из арабского изображения на C#. Узнайте,
  как преобразовать изображение в PDF, извлечь арабский текст и добавить скрытый текст
  с помощью Aspose OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract arabic text
- pdf with hidden text
- ocr arabic image
language: ru
og_description: Создайте PDF с возможностью поиска из арабского изображения с помощью
  Aspose OCR в C#. Следуйте этому руководству, чтобы преобразовать изображение в PDF,
  извлечь арабский текст и внедрить скрытый текст.
og_title: Создать PDF с поиском из арабского изображения – пошагово
tags:
- Aspose
- OCR
- PDF
- C#
- Arabic
title: Создание поискового PDF из арабского изображения – Полное руководство
url: /ru/net/text-recognition/create-searchable-pdf-from-arabic-image-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из арабского изображения – Полное руководство

Когда‑нибудь вам нужно было **создать поисковый PDF** из отсканированного арабского счета, но вы не знали, как сохранить оригинальный вид и при этом сделать текст выделяемым? Вы не одиноки. Во многих проектах автоматизации документов проблема заключается не только в преобразовании изображения в PDF, но и в сохранении визуального макета и добавлении скрытого текстового слоя, который могут индексировать поисковые системы.

В этом руководстве мы пройдем весь процесс: **преобразовать изображение в PDF**, **извлечь арабский текст** с помощью Aspose OCR и, наконец, внедрить этот текст как **PDF со скрытым текстом**, чтобы полученный файл был полностью поисковым. К концу вы получите готовый фрагмент кода C#, который можно вставить в любое .NET‑решение. Никаких внешних сервисов, только библиотеки Aspose, которые у вас уже есть.

## Что вам понадобится

- .NET 6 или новее (код также работает с .NET Core)  
- **Aspose.OCR** и **Aspose.Pdf** пакеты NuGet (последние версии на февраль 2026)  
- Арабский файл изображения (например, `arabic_invoice.jpg`), который вы хотите превратить в поисковый PDF  
- Немного знаний C# – концепции просты, но мы объясним «почему» каждой строки.

> **Pro tip:** Если вы ещё не добавили пакеты NuGet, выполните  
> `dotnet add package Aspose.OCR` и  
> `dotnet add package Aspose.Pdf` из папки проекта.

Теперь, когда предварительные требования выполнены, давайте погрузимся в пошаговую реализацию.

## Шаг 1 – Настройка OCR‑движка для арабского текста

Первое, что нам нужно сделать, – сконфигурировать Aspose OCR для распознавания арабских символов. Арабский – это скрипт справа налево, поэтому мы должны указать движку, какой язык загрузить, и включить автоматическую загрузку ресурсов на случай, если языковые данные ещё не находятся на машине.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Configure OCR for Arabic and let Aspose fetch the language pack if needed
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Arabic,
    AutomaticResourceDownload = true
};
```

**Почему это важно:**  
Если пропустить настройку `Language = OcrLanguage.Arabic`, движок по умолчанию будет использовать английский, и вы получите искажённые символы. Включение `AutomaticResourceDownload` избавит вас от необходимости вручную размещать языковые файлы на сервере.

## Шаг 2 – Загрузка исходного изображения

Далее мы загружаем изображение, содержащее арабский текст. Использование `Image.FromFile` гарантирует, что изображение будет прочитано в объект GDI+ `Image`, который ожидает Aspose OCR.

```csharp
using System.Drawing;          // For Image
using System.IO;                // For MemoryStream

// Replace with the actual path to your Arabic invoice
string imagePath = @"YOUR_DIRECTORY/arabic_invoice.jpg";

using (var inputImage = Image.FromFile(imagePath))
{
    // The rest of the workflow lives inside this using block
```

**Пограничный случай:** Если изображение огромное (например, отсканированная страница A3), рассмотрите возможность предварительного уменьшения масштаба, чтобы улучшить производительность. OCR‑движок может обрабатывать большие файлы, но потребление памяти быстро растёт.

## Шаг 3 – Распознавание арабского текста и получение результата

Теперь мы действительно запускаем OCR. Метод `Recognize` возвращает объект `OcrResult`, содержащий обнаруженный текст, оценки уверенности и ограничивающие рамки (если они понадобятся для продвинутого анализа макета).

```csharp
    // Perform OCR on the loaded image
    OcrResult ocrResult = ocrEngine.Recognize(inputImage);
    string extractedText = ocrResult.Text;

    // Quick sanity check: print the first 200 characters to the console
    Console.WriteLine("Extracted Arabic text (preview):");
    Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Зачем сохранять предварительный просмотр?**  
Просмотр фрагмента извлечённого текста помогает убедиться, что языковой пакет загружен корректно, прежде чем тратить время на генерацию PDF.

## Шаг 4 – Создание нового PDF‑документа и добавление пустой страницы

Имея текст, мы можем приступить к построению PDF. Aspose PDF предоставляет объект `Document`, представляющий весь файл. Добавление страницы даёт нам холст, на который можно разместить как оригинальное изображение, так и скрытый текстовый слой.

```csharp
    // Initialize a new PDF document
    var pdfDocument = new Aspose.Pdf.Document();

    // Add a blank page – this will become the background for our image
    var pdfPage = pdfDocument.Pages.Add();
```

**Примечание:** Вы можете добавить несколько страниц, если обрабатываете многостраничный TIFF или PDF, но для сценария с одним изображением достаточно одной страницы.

## Шаг 5 – Вставка оригинального изображения как фонового элемента

Мы хотим, чтобы итоговый PDF выглядел точно так же, как отсканированный счет, поэтому встраиваем изображение как видимый фон. Класс `Image` из Aspose PDF ожидает поток, поэтому мы читаем файл в `MemoryStream`.

```csharp
    // Load the same image bytes for the PDF background
    var backgroundImage = new Aspose.Pdf.Image
    {
        ImageStream = new MemoryStream(File.ReadAllBytes(imagePath))
    };

    // Add the image to the page's paragraph collection
    pdfPage.Paragraphs.Add(backgroundImage);
```

**Почему использовать фоновое изображение?**  
Размещение изображения непосредственно на странице сохраняет оригинальный макет, цвета и любые печати или логотипы, которые OCR‑движок иначе проигнорировал бы.

## Шаг 6 – Добавление OCR‑текста как скрытого слоя

Секретный ингредиент **поискового PDF** – скрытый текстовый слой, расположенный поверх изображения. Установив размер шрифта в `0`, мы делаем текст невидимым для человеческого глаза, но он остаётся выделяемым и поисковым.

```csharp
    // Create a TextFragment with the extracted Arabic text
    var searchableText = new Aspose.Pdf.Text.TextFragment(extractedText)
    {
        // Hide the visible text; only the text layer remains searchable
        TextState = { FontSize = 0 }
    };

    // Add the hidden text fragment to the same page
    pdfPage.Paragraphs.Add(searchableText);
```

**Важное уточнение:**  
Если требуется, чтобы скрытый текст точно совпадал с изображением (например, когда OCR возвращает координаты), можно использовать `TextFragmentAbsorber` и позиционировать каждый фрагмент вручную. Для большинства счетов достаточно простого полно‑страничного наложения.

## Шаг 7 – Сохранение поискового PDF

Наконец, сохраняем PDF на диск. Выходной файл будет содержать как визуальное изображение, так и скрытый арабский текст, делая его полностью поисковым в Adobe Reader, Google Drive или любом просмотрщике, поддерживающем OCR.

```csharp
    // Define the output path
    string outputPath = @"YOUR_DIRECTORY/arabic_invoice_searchable.pdf";

    // Save the document
    pdfDocument.Save(outputPath);

    Console.WriteLine($"Searchable PDF created at: {outputPath}");
}
```

### Полный рабочий пример

Объединив все части, получаем полностью готовую к запуску программу:

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure OCR for Arabic
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Arabic,
            AutomaticResourceDownload = true
        };

        // 2️⃣ Load the source image
        string imagePath = @"YOUR_DIRECTORY/arabic_invoice.jpg";
        using (var inputImage = Image.FromFile(imagePath))
        {
            // 3️⃣ Run OCR and get the text
            OcrResult ocrResult = ocrEngine.Recognize(inputImage);
            string extractedText = ocrResult.Text;

            // Optional preview
            Console.WriteLine("Extracted Arabic text (preview):");
            Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));

            // 4️⃣ Create PDF document
            var pdfDocument = new Document();
            var pdfPage = pdfDocument.Pages.Add();

            // 5️⃣ Add original image as background
            var backgroundImage = new Aspose.Pdf.Image
            {
                ImageStream = new MemoryStream(File.ReadAllBytes(imagePath))
            };
            pdfPage.Paragraphs.Add(backgroundImage);

            // 6️⃣ Add hidden searchable text
            var searchableText = new TextFragment(extractedText)
            {
                TextState = { FontSize = 0 }
            };
            pdfPage.Paragraphs.Add(searchableText);

            // 7️⃣ Save the searchable PDF
            string outputPath = @"YOUR_DIRECTORY/arabic_invoice_searchable.pdf";
            pdfDocument.Save(outputPath);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Ожидаемый результат:** Откройте сгенерированный `arabic_invoice_searchable.pdf` в любом PDF‑просмотрщике, нажмите **Ctrl + F** и введите арабское слово, присутствующее в оригинальном счёте. Просмотрщик найдёт слово, хотя вы не видите никакого текстового слоя.

## Часто задаваемые вопросы и подводные камни

- **Работает ли это с другими языками?**  
  Абсолютно. Просто измените `Language = OcrLanguage.YourLanguage` и убедитесь, что соответствующий языковой пакет доступен. Остальная часть конвейера остаётся прежней.

- **Что делать, если уверенность OCR низкая?**  
  Вы можете проверить `ocrResult.Confidence` (значение от 0 до 1). Если оно падает ниже порога (например, 0.75), рассмотрите предобработку изображения – выравнивание, увеличение контрастности или преобразование в градации серого – перед передачей его в движок.

- **Можно ли добавить несколько изображений в один PDF?**  
  Да. Пройдитесь в цикле по коллекции путей к изображениям, добавьте новую страницу для каждого и повторите шаги 5‑6. Не забудьте сохранять блок `using` для каждого изображения, чтобы освободить ресурсы GDI.

- **Является ли скрытый текст действительно невидимым?**  
  Установка `FontSize = 0` делает текст невидимым в большинстве просмотрщиков. Если какой‑то просмотрщик всё‑ещё отображает лёгкий символ, можно также задать полностью прозрачный цвет текста (`TextState.FillColor = Color.Transparent`).

## Следующие шаги

Теперь, когда вы знаете, как **создать поисковый PDF** из арабского изображения, вы можете изучить:

- **Пакетную обработку** – считывать все изображения в папке и генерировать один поисковый PDF на каждый файл.  
- **Добавление координат OCR** – использовать `OcrResult.Regions` для точного размещения каждого текстового фрагмента, повышая точность поиска в сложных макетах.  
- **Шифрование PDF** – Aspose PDF позволяет добавить пароли или цифровые подписи, если нужна дополнительная безопасность.  
- **Интеграцию с Azure Blob Storage** – сохранять сгенерированные PDF‑файлы напрямую в облаке для последующих рабочих процессов.

Каждая из этих тем естественно включает вторичные ключевые слова **convert image to pdf**, **extract

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}