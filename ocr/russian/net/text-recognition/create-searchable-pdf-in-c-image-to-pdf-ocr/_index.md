---
category: general
date: 2026-02-28
description: Создайте поисковый PDF из многостраничного TIFF в C#. Это руководство
  показывает, как выполнить преобразование изображения в поисковый PDF с полным примером
  OCR на C#.
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- convert tiff to pdf
- c# ocr example
- c# image to pdf
language: ru
og_description: Создайте PDF с возможностью поиска из TIFF с помощью Aspose.OCR. Следуйте
  этому пошаговому примеру OCR на C#, чтобы преобразовать изображения в PDF с возможностью
  поиска.
og_title: Создать поисковый PDF в C# – изображение в PDF OCR
tags:
- OCR
- PDF
- C#
- Aspose
title: Создание поискового PDF в C# – изображение в PDF с OCR
url: /ru/net/text-recognition/create-searchable-pdf-in-c-image-to-pdf-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF в C# – Изображение в PDF OCR

Когда‑нибудь вам нужно было **создать поисковый PDF** из отсканированного документа, но вы не знали, с чего начать? Вы не одиноки. Во многих офисных процессах поисковый PDF — это разница между тупиковой файлом и поисковым архивом.  

В этом руководстве мы пройдем полный **c# ocr example**, который преобразует многостраничный TIFF в поисковый PDF, используя Aspose.OCR. К концу вы точно будете знать, как **image to searchable pdf**, как **convert tiff to pdf**, и у вас будет готовый к запуску фрагмент кода, который можно вставить в любой проект .NET.

## Что вы узнаете

* Как установить и подключить Aspose.OCR в проект C#.
* Точные шаги по загрузке TIFF, установке языка и вызову `RecognizeToPdf`.
* Почему каждый шаг важен — от управления памятью до выбора языка.
* Советы по работе с большими документами, устранению распространённых проблем OCR и расширению решения на другие форматы изображений.

**Prerequisites** – недавний .NET SDK (4.6+ или .NET Core 3.1+), Visual Studio (или ваша любимая IDE) и лицензия Aspose.OCR (бесплатная пробная версия подходит для тестирования). Другие внешние библиотеки не требуются.

---

## Создание поискового PDF – Обзор

На высоком уровне процесс выглядит так:

1. **Initialize** `OcrEngine`.  
2. **Load** исходное изображение (в нашем случае TIFF).  
3. **Configure** настройки языка для повышения точности.  
4. **Run** OCR и **save** результат напрямую в виде поискового PDF.  

Вот и всё. API Aspose делает всю тяжелую работу, поэтому вам не нужно комбинировать отдельные библиотеки OCR и PDF.

---

## Шаг 1: Установить Aspose.OCR и настроить проект

First, add the Aspose.OCR NuGet package:

```bash
dotnet add package Aspose.OCR
```

Or, if you prefer the Package Manager Console in Visual Studio:

```powershell
Install-Package Aspose.OCR
```

After the package restores, open your project file and verify the reference:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
</ItemGroup>
```

> **Pro tip:** Используйте последнюю стабильную версию (проверьте сайт Aspose), чтобы получить исправления ошибок и новейшие языковые пакеты.

---

## Шаг 2: Преобразовать TIFF в PDF – Загрузка изображения

Теперь мы загрузим TIFF, который хотите сделать поисковым. Метод `Image.Load` из Aspose поддерживает многостраничные TIFF‑файлы из коробки.

```csharp
using Aspose.OCR;
using System.Drawing;

// Load the multi‑page TIFF. Replace the path with your actual file.
using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");
```

> **Why this matters:** Загрузка изображения внутри блока `using` гарантирует своевременное освобождение неуправляемых ресурсов — это критично при обработке больших документов.

---

## Шаг 3: Изображение в поисковый PDF – Конфигурация OCR‑движка

Прежде чем запускать OCR, мы укажем движку, какой язык ожидать. Английский подходит для большинства случаев, но вы можете заменить его любым значением перечисления `OcrLanguage`.

```csharp
// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// (Optional) Specify language for better accuracy
ocrEngine.Language = OcrLanguage.English;
```

> **Expert note:** Выбор правильного языка значительно уменьшает количество ошибок распознавания. Если у вас смешанные языки, их можно комбинировать оператором `|`, например, `OcrLanguage.English | OcrLanguage.French`.

---

## Шаг 4: Пример C# OCR – Распознавание и сохранение

Когда движок готов, вызовите `RecognizeToPdf`. Метод записывает поисковый PDF напрямую на диск, внедряя невидимый текстовый слой позади оригинального изображения.

```csharp
// Define the output path for the searchable PDF
string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";

// Perform OCR and write the searchable PDF
ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);
```

После выполнения этой строки `output.pdf` будет содержать оригинальные страницы TIFF плюс скрытый текстовый слой, который любой PDF‑просмотрщик может искать.

---

## Шаг 5: C# Image to PDF – Проверка результата

Давайте убедимся, что всё сработало. Откройте сгенерированный PDF в Adobe Reader (или любом другом просмотрщике) и попробуйте найти слово, которое, как вы знаете, присутствует в исходном TIFF.

```csharp
Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
```

Если поиск возвращает результаты, вы успешно **create searchable pdf** из изображения. Если нет, проверьте ещё раз настройки языка или качество исходного TIFF.

---

## Полный рабочий пример

Собрав все части вместе, представляем автономное консольное приложение, которое вы можете скомпилировать и запустить:

```csharp
using Aspose.OCR;
using System.Drawing;

class SearchablePdfDemo
{
    static void Main()
    {
        // Step 1: Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑page TIFF
        using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");

        // Step 3: (Optional) Set language for better accuracy
        ocrEngine.Language = OcrLanguage.English;

        // Step 4: Convert the image to a searchable PDF
        string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);

        // Step 5: Inform the user
        System.Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
    }
}
```

**Expected output** (в консоли):

```
Searchable PDF created at: C:\MyFolder\output.pdf
```

Откройте `output.pdf`, и вы сможете ввести любое слово из оригинального TIFF в поле поиска просмотрщика и увидеть выделенные совпадения.

---

![Create searchable PDF example](placeholder-image.png){: .align-center alt="пример создания поискового pdf"}

*Скриншот выше показывает открытый в просмотрщике поисковый PDF с активным скрытым текстовым слоем.*

---

## Часто задаваемые вопросы и особые случаи

### Что если мой TIFF огромный (сотни страниц)?

Aspose.OCR обрабатывает страницы по одной, но вы всё равно можете столкнуться с ограничениями памяти. Рассмотрите обработку TIFF пакетами:

```csharp
for (int i = 0; i < tiffImage.PageCount; i++)
{
    using var singlePage = tiffImage.ExtractPage(i);
    ocrEngine.RecognizeToPdf(singlePage, $"page_{i}.pdf");
}
```

Позже объедините PDF‑файлы каждой страницы с помощью библиотеки PDF (например, Aspose.PDF).

### Можно ли вывести в другой формат, например, поисковый DOCX?

Да — используйте `RecognizeToDocument` вместо `RecognizeToPdf`. API аналогичен методу для PDF, просто измените расширение целевого файла.

### Как работать с языками, отличными от английского?

Замените `OcrLanguage.English` на соответствующее значение перечисления, например `OcrLanguage.Spanish`. Вы также можете комбинировать языки:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.German;
```

### Что насчёт PDF с паролем?

После шага OCR вы можете открыть сгенерированный PDF с помощью Aspose.PDF и применить шифрование:

```csharp
var pdfDoc = new Aspose.Pdf.Document(outputPdfPath);
pdfDoc.Encrypt("ownerPassword", "userPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save(outputPdfPath);
```

---

## Итоги

Мы рассмотрели всё, что необходимо для **create searchable PDF** файлов из TIFF‑изображений с помощью C#. Начиная с установки Aspose.OCR, загрузки изображения, настройки языка, запуска OCR и окончательной проверки поискового результата, у вас теперь есть надёжный **c# ocr example**, который можно адаптировать к другим форматам.  

Если вы готовы идти дальше, попробуйте:

* **Convert TIFF to PDF** для не‑поисковых архивов (просто пропустите шаг OCR).  
* Поэкспериментируйте с **image to searchable pdf**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}