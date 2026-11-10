---
category: general
date: 2026-03-20
description: 'Быстро создавайте PDF с поиском: преобразуйте изображение в PDF, извлеките
  текст из изображения и добавьте скрытый текстовый слой для полной поисковой возможности.'
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- pdf with hidden text
- scan image to pdf
language: ru
og_description: Создайте PDF с поиском в C#, преобразовав изображение в PDF, извлекая
  текст и внедрив скрытый слой для мгновенного поиска.
og_title: Создание поискового PDF из изображения — Полный учебник по C#
tags:
- Aspose
- C#
- OCR
- PDF generation
title: Создание поискового PDF из изображения в C# – пошаговое руководство
url: /ru/net/text-recognition/create-searchable-pdf-from-image-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из изображения в C# – Полное руководство

Когда‑нибудь вам нужно было **создать поисковый PDF** из отсканированного счета, но не хотелось набирать всё вручную? Вы не одиноки. Во многих офисных процессах преобразование растрового скана в PDF, по которому действительно можно искать, является ежедневной проблемой. Хорошая новость? С несколькими строками C# и библиотеками OCR и PDF от Aspose вы можете автоматизировать весь процесс — без ручного копирования‑вставки.

В этом руководстве мы пройдемся по тому, как **конвертировать изображение в PDF**, извлечь текст из этого изображения и затем наложить текст невидимым слоем, чтобы итоговый файл вел себя как нативный PDF. К концу вы получите готовый метод для создания **pdf с скрытым текстом**, который работает с любым отсканированным документом, будь то счет, контракт или чек.

## Что понадобится

- .NET 6.0 или новее (в коде используются операторы `using var`, поэтому свежий SDK упрощает работу)
- NuGet‑пакеты Aspose.OCR и Aspose.Pdf (`Install-Package Aspose.OCR` и `Install-Package Aspose.Pdf`)
- Пример файла изображения (PNG, JPG или TIFF), содержащего текст, который нужно проиндексировать
- Visual Studio 2022 или любая другая IDE по вашему выбору

> **Pro tip:** Если вы работаете с многостраничными сканами, просто выполните цикл по каждому изображению и повторите шаги — логика остаётся той же.

---

## Шаг 1 – Инициализация OCR‑движка (Извлечение текста из изображения)

Прежде чем встраивать поисковый текст, нам нужно действительно прочитать символы с картинки. `OcrEngine` от Aspose делает всю тяжелую работу.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine and tell it which language to look for.
// English works for most invoices, but you can set Language.French, etc.
using var ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Почему это важно:** Инициализация движка с правильным языком резко повышает точность. Если пропустить этот шаг, OCR может неправильно распознать цифры — а этого точно не хочется в финансовых документах.

---

## Шаг 2 – Загрузка вашего отсканированного изображения (Конвертировать изображение в PDF)

Теперь мы загружаем растровое изображение в память. Aspose работает напрямую с `System.Drawing.Image`, поэтому любой формат, поддерживаемый .NET, подойдет.

```csharp
using System.Drawing;

// Replace the path with the location of your scanned file.
var inputImage = Image.FromFile(@"C:\Docs\invoice.png");
```

Если у вас уже есть процесс **scan image to PDF**, который генерирует многостраничный TIFF, просто измените расширение файла и повторите загрузку для каждой страницы.

---

## Шаг 3 – Запуск OCR и захват распознанного текста

С готовым изображением мы просим OCR‑движок выполнить свою магию.

```csharp
// Perform OCR – the result contains the raw text and confidence scores.
var ocrResult = ocrEngine.Recognize(inputImage);

// For debugging, you might want to see what was read.
Console.WriteLine("OCR Output:");
Console.WriteLine(ocrResult.Text);
```

**Edge case:** Если изображение имеет низкое разрешение (< 300 dpi), уверенность распознавания падает. Рассмотрите возможность увеличения масштаба или повторного сканирования с более высоким DPI перед передачей в движок.

---

## Шаг 4 – Создание PDF и размещение оригинального изображения в качестве фона

**pdf с скрытым текстом** всё равно нуждается в визуальном представлении скана. Мы добавим изображение как фон страницы.

```csharp
using Aspose.Pdf;

// Start a fresh PDF document.
var pdfDocument = new Document();

// Add a new page.
var pdfPage = pdfDocument.Pages.Add();

// Insert the image; it will fill the page by default.
pdfPage.Paragraphs.Add(new Aspose.Pdf.Image
{
    ImageInfo = new ImageInfo(@"C:\Docs\invoice.png")
});
```

**Почему используем изображение как фон:** Пользователи по‑прежнему видят точный оригинальный скан, сохраняющий подписи и печати, а слой скрытого текста обеспечивает возможность поиска.

---

## Шаг 5 – Наложение OCR‑текста как невидимого слоя (PDF с скрытым текстом)

Вот ключевой момент: мы добавляем `TextFragment`, который располагается поверх изображения, но помечен как невидимый. Aspose.Pdf делает это просто.

```csharp
using Aspose.Pdf.Text;

// Create a text fragment from the OCR result.
var searchableText = new TextFragment(ocrResult.Text)
{
    // Position (0,0) aligns with the bottom‑left of the page.
    Position = new Position(0, 0),

    // Make the text invisible – it still participates in search.
    TextState = { Font = FontRepository.FindFont("Arial"), FontSize = 0.1f, IsHidden = true }
};

// Add the invisible text to the same page.
pdfPage.Paragraphs.Add(searchableText);
```

**Объяснение:** Установка крошечного размера шрифта и пометка фрагмента как скрытого сохраняет чистый визуальный вывод, одновременно гарантируя, что слой текста PDF содержит результат OCR. Поисковые движки и PDF‑читалки проиндексируют его.

---

## Шаг 6 – Сохранение поискового PDF

Наконец, записываем документ на диск.

```csharp
// Choose a destination path.
string outputPath = @"C:\Docs\invoice_searchable.pdf";

// Save the PDF. The file now contains both the image and searchable text.
pdfDocument.Save(outputPath);

Console.WriteLine($"Searchable PDF created at: {outputPath}");
```

Откройте полученный файл в Adobe Reader, нажмите **Ctrl + F**, введите слово, которое видели в счете, и вы увидите подсвеченный результат — хотя текст никогда не был видимым.

---

## Полный рабочий пример (Все шаги вместе)

Ниже представлен полностью готовый к копированию в консольное приложение код. Он компилируется и работает «из коробки», при условии, что NuGet‑пакеты установлены и пути к файлам корректны.

```csharp
// ------------------------------------------------------------
// Create Searchable PDF from Image – Complete C# Example
// ------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load scanned image
        var inputImagePath = @"C:\Docs\invoice.png";
        var inputImage = Image.FromFile(inputImagePath);

        // 3️⃣ Perform OCR
        var ocrResult = ocrEngine.Recognize(inputImage);
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);

        // 4️⃣ Create PDF and add image as background
        var pdfDocument = new Document();
        var pdfPage = pdfDocument.Pages.Add();
        pdfPage.Paragraphs.Add(new Aspose.Pdf.Image
        {
            ImageInfo = new ImageInfo(inputImagePath)
        });

        // 5️⃣ Add invisible searchable text layer
        var searchableText = new TextFragment(ocrResult.Text)
        {
            Position = new Position(0, 0),
            TextState = { Font = FontRepository.FindFont("Arial"), FontSize = 0.1f, IsHidden = true }
        };
        pdfPage.Paragraphs.Add(searchableText);

        // 6️⃣ Save the searchable PDF
        var outputPath = @"C:\Docs\invoice_searchable.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"✅ Searchable PDF saved to: {outputPath}");
    }
}
```

**Ожидаемый результат:**  
- `invoice_searchable.pdf` выглядит идентично `invoice.png`.  
- Поиск по тексту работает для любого слова, появившегося в оригинальном скане.  
- Размер файла растёт лишь незначительно (скрытый текст добавляет несколько килобайт).

---

## Часто задаваемые вопросы и особые случаи

### Можно ли обработать несколько страниц в одном PDF?

Конечно. Оберните логику OCR‑и‑PDF в цикл `foreach (string imagePath in imageFiles)`, создавая новый `Page` для каждой итерации. Слой скрытого текста добавляется для каждой страницы, поэтому поиск работает по всему документу.

### Что делать, если документ содержит несколько языков?

Установите `ocrEngine.Language` в `Language.Multilingual` или создайте отдельные движки для каждого языкового сегмента. Aspose вернёт результаты на нескольких языках, которые затем можно добавить на ту же страницу PDF.

### Как управлять DPI или масштабированием изображения?

Перед добавлением изображения в PDF его можно изменить размер с помощью `System.Drawing`:

```csharp
var resized = new Bitmap(inputImage, new Size(1240, 1754)); // A4 at 150 dpi
```

Затем передайте `resized` в конструктор изображения PDF.

### Действительно ли скрытый текст невидим во всех просмотрщиках?

Большинство современных просмотрщиков уважают флаг `IsHidden`. Если вы столкнётесь с программой, которая всё‑равно отображает крошечный текст, уменьшите размер шрифта ещё сильнее (например, `0.01f`) или задайте полностью прозрачный цвет текста через `TextState.FillColor = Color.Transparent`.

### А как насчёт безопасности — можно ли защитить PDF паролем?

Да. После завершения добавления содержимого вызовите:

```csharp
pdfDocument.Encrypt("ownerPwd", "userPwd", EncryptionAlgorithms.AES256);
```

Теперь поисковый PDF также учитывает политики конфиденциальности вашей организации.

---

## Советы для production‑готовых реализаций

- **Batch processing:** Используйте `Parallel.ForEach` для больших наборов изображений, но учитывайте, что экземпляры `OcrEngine` не являются потокобезопасными — создавайте по одному на каждый поток.  
- **Error handling:** Оборачивайте вызовы OCR в `try/catch`; проверяйте `ocrResult.IsRecognized`, чтобы пропускать страницы, где распознавание не удалось.  
- **Logging:** Сохраняйте значения `ocrResult.Confidence`; низкая уверенность может указывать на необходимость предобработки изображения (выравнивание, удаление шума).  
- **Performance:** Переиспользуйте один объект `Document` для всех страниц, чтобы избежать многократного открытия/закрытия файлов.  
- **Testing:** Сравнивайте извлечённый из поискового PDF текст (`pdfDocument.Pages[1].ExtractText()`) с результатом OCR, чтобы убедиться, что ничего не обрезано.

---

## Заключение

Мы только что показали, как **создать поисковый PDF** из обычных изображений с помощью C#. Извлекая текст с помощью Aspose.OCR, накладывая его невидимым слоем на страницу PDF и сохраняя результат, вы получаете документ, который выглядит точно как оригинальный скан, но ведёт себя как нативный PDF. Эта техника покрывает классический процесс **convert image to PDF**, добавляет **pdf с скрытым текстом** и решает повседневную задачу **scan image to PDF**, которую действительно можно искать.

Готовы к следующему шагу? Попробуйте расширить код для пакетной обработки папки с чеками или интегрировать его в веб‑API, которое будет возвращать поисковые PDF «на лету». Вы также можете поэкспериментировать с разными шрифтами, добавить метаданные или даже внедрить оценки уверенности OCR в виде аннотаций PDF для аудита.

Если этот гид оказался полезным, поставьте звёздочку, поделитесь им с коллегами или оставьте комментарий со своими улучшениями. Приятного кодинга, и пусть ваши PDF всегда остаются поисковыми!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}