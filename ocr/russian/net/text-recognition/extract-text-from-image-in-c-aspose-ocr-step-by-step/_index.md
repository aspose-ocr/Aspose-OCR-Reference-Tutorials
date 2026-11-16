---
category: general
date: 2026-03-05
description: Извлекать текст из изображения с помощью Aspose OCR в C#. Научитесь читать
  файлы изображений в C#, конвертировать DJVU в текст и быстро получать результаты
  OCR изображения в виде строки.
draft: false
keywords:
- extract text from image
- read image file c#
- convert djvu to text
- ocr image to string
- recognize text from djvu
language: ru
og_description: Извлекать текст из изображения с помощью Aspose OCR в C#. Это руководство
  показывает, как читать файл изображения в C#, конвертировать DJVU в текст и легко
  преобразовывать изображение OCR в строку.
og_title: Извлечение текста из изображения в C# – Полное руководство по Aspose OCR
tags:
- Aspose OCR
- C#
- Image Processing
title: Извлечение текста из изображения в C# – пошаговое руководство Aspose OCR
url: /ru/net/text-recognition/extract-text-from-image-in-c-aspose-ocr-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# извлечение текста из изображения в C# – Полное руководство по Aspose OCR

Когда‑нибудь вам нужно было **извлечь текст из изображения**, но вы не были уверены, какая библиотека даст надёжные результаты? Возможно, у вас есть пакет сканов DJVU, и вы хотите просто получить простой текст без возни с сторонними инструментами. В этом руководстве мы решим эту задачу за несколько минут, используя Aspose OCR для .NET.

Мы пройдем процесс чтения файла изображения в C#, преобразования документа DJVU в текст и превращения любого OCR‑изображения в чистую строку. К концу вы получите готовое к запуску консольное приложение, которое выводит распознанный текст в консоль. Никаких расплывчатых ссылок «см. документацию» — только полное решение, готовое к копированию и вставке.

## Что понадобится

- **.NET 6.0** или новее (код также работает на .NET Framework 4.6+).  
- **Aspose.OCR for .NET** пакет NuGet (бесплатная пробная лицензия подходит для тестов).  
- Файл DJVU или любое поддерживаемое изображение (PNG, JPEG, BMP и т.д.).  
- Visual Studio, Rider или ваш любимый редактор.

Если у вас чего‑то не хватает, просто установите пакет NuGet:

```bash
dotnet add package Aspose.OCR
```

Это всё, что нужно для настройки. Погружаемся.

## Шаг 1: Инициализация OCR‑движка – извлечение текста из изображения

Первое, что вы делаете, — создаёте экземпляр `OcrEngine`. Считайте его мозгом, который будет читать пиксели и превращать их в символы.

```csharp
using Aspose.OCR;
using System;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

Почему мы создаём движок *до* загрузки файла? Дизайн Aspose отделяет конфигурацию (например, лицензирование) от самих данных изображения, поэтому один и тот же движок можно переиспользовать для нескольких файлов без повторного создания объектов — небольшой выигрыш в производительности.

## Шаг 2: Примените лицензию Aspose OCR (необязательно, но рекомендуется)

Если у вас есть коммерческая лицензия, укажите её сейчас. Пропуск этого шага переводит движок в демо‑режим, который добавляет водяной знак к результату и ограничивает количество страниц.

```csharp
        // Apply license – remove this line if you’re using the free trial
        ocrEngine.SetLicense("Aspose.OCR.lic");
```

**Pro tip:** Храните файл лицензии вне системы контроля версий (например, в переменной окружения), чтобы случайно не закоммитить его.

## Шаг 3: Загрузка изображения – чтение файла изображения в C# легко

Aspose умеет читать множество форматов, включая редкий DJVU. Мы будем использовать вспомогательный метод `ImageStream.FromFile`, чтобы загрузить файл в движок.

```csharp
        // Load the image (DJVU, PNG, JPEG, etc.)
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.djvu");
```

Если вам удобнее работать с `byte[]` (например, когда изображение берётся из базы данных), используйте `ImageStream.FromBytes(byteArray)`. Такая гибкость полезна, когда нужно **read image file C#** из потока, а не с диска.

## Шаг 4: Выполнение OCR – преобразование изображения в строку одним вызовом

Теперь происходит магия. Вызов `Recognize()` запускает OCR‑движок и возвращает `RecognitionResult`, содержащий извлечённый текст, оценки уверенности и многое другое.

```csharp
        // Run OCR and get the result
        var result = ocrEngine.Recognize();

        // Extract plain text
        string recognizedText = result.Text;
```

Почему бы просто не вызвать `Recognize().Text`? Разделение вызова позволяет позже исследовать `result.Confidence` или `result.Regions`, если нужны более детальные данные — это удобно для отладки или построения UI, выделяющего слова с низкой уверенностью.

## Шаг 5: Вывод извлечённого текста – ваш окончательный результат

Наконец, выводим текст в консоль. В реальном приложении вы, вероятно, запишете его в файл, базу данных или отправите через API.

```csharp
        // Show the result
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognizedText);
    }
}
```

**Expected output** (truncated for brevity):

```
=== OCR Output ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Если OCR‑движок не смог распознать ни одного символа, `recognizedText` будет пустой строкой. В этом случае проверьте качество изображения или попробуйте скорректировать настройки языка движка (например, `ocrEngine.Language = Language.English;`).

## Преобразование DJVU в текст – распознавание текста из DJVU массово

Возможно, у вас есть десятки файлов DJVU для обработки. Оберните предыдущую логику в цикл:

```csharp
string[] files = Directory.GetFiles("YOUR_DIRECTORY", "*.djvu");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    string text = ocrEngine.Recognize().Text;
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), text);
    Console.WriteLine($"Converted {Path.GetFileName(file)} → {Path.GetFileNameWithoutExtension(file)}.txt");
}
```

Этот фрагмент **converts DJVU to text** автоматически, создавая файл `.txt` рядом с каждым исходным. Это быстрый способ построить поисковый архив из устаревших отсканированных документов.

## Обработка граничных случаев – что если изображение шумное?

Точность OCR падает, когда изображение размыто, имеет низкий контраст или содержит цветные фоны. Aspose OCR предлагает варианты предобработки:

```csharp
// Example: Binarize the image to improve contrast
ocrEngine.Image = ImageProcessing.Binarize(ocrEngine.Image, threshold: 128);
```

Кроме того, вы можете настроить автоматическое определение языка движком:

```csharp
ocrEngine.Language = Language.Detect; // Detects language based on content
```

Эти настройки часто повышают точность с 60 % до 95 %. Поэкспериментируйте с методами `Threshold`, `Denoise` или `Deskew`, если столкнётесь с проблемами.

## Полный рабочий пример – копировать, вставить, запустить

Ниже представлен полный код программы, готовый к компиляции. Замените `"YOUR_DIRECTORY/input.djvu"` на путь к вашему файлу и убедитесь, что файл лицензии доступен.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Apply license (optional)
        // ocrEngine.SetLicense("Aspose.OCR.lic"); // Uncomment if you have a license

        // 3️⃣ Load the image (DJVU, PNG, JPEG, etc.)
        string imagePath = "YOUR_DIRECTORY/input.djvu";
        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 4️⃣ Perform OCR
        var result = ocrEngine.Recognize();
        string recognizedText = result.Text;

        // 5️⃣ Output the text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognizedText);
    }
}
```

Запустите его так:

```bash
dotnet run
```

Вы должны увидеть извлечённый текст, выведенный в консоль, точно как в предыдущем примере.

## Часто задаваемые вопросы и подводные камни

- **Does this work with PDF files?**  
  Not directly. Aspose OCR handles raster images; for PDFs you’d first convert each page to an image (e.g., using Aspose.PDF) and then feed those images to the OCR engine.

- **What if I need to process a large batch on a server?**  
  Instantiate a **single** `OcrEngine` and reuse it across threads. The engine is thread‑safe for read‑only operations, but you must avoid sharing the same `Image` instance concurrently.

- **Can I extract formatted text (fonts, sizes)?**  
  Aspose OCR returns plain Unicode text only. For layout‑preserving extraction you’d need a more advanced solution like OCR with OCR‑ML or a PDF library that retains layout.

## Следующие шаги – расширьте ваш рабочий процесс

Теперь, когда вы можете **extract text from image** надёжно, рассмотрите следующие варианты:

- Сохранение результатов в Elasticsearch для полнотекстового поиска.  
- Передача текста в языковую модель для суммирования.  
- Добавление простого UI на ASP.NET Core для загрузки файлов и мгновенного просмотра OCR‑результатов.  

Все эти идеи базируются на том же базовом коде, который мы только что разобрали, так что вы хорошо подготовлены к расширению решения.

---

### Краткое резюме

- Мы **initialized** `OcrEngine` (the heart of Aspose OCR).  
- Applied a **license** to unlock full features.  
- **Loaded** a DJVU file using `ImageStream.FromFile`.  
- Called `Recognize()` to get an **ocr image to string** result.  
- Printed the **extracted text** to the console.  

Это полный рецепт превращения любого поддерживаемого изображения — включая DJVU — в поисковый текст с помощью C#.

---

Feel free to experiment with different image formats, tweak preprocessing settings, or chain this code with other Aspose libraries. If you hit a snag, drop a comment below—happy coding!  

![extract text from image example](/images/ocr-example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}