---
category: general
date: 2026-03-07
description: Извлекайте текст из PNG‑файлов с помощью C#. Узнайте, как преобразовать
  изображение в текст на C# и быстро считывать текст со сканированных изображений.
draft: false
keywords:
- extract text from png
- convert image to text c#
- read text from scanned images
- how to run ocr on images
language: ru
og_description: Извлекать текст из PNG‑файлов с помощью C#. Это руководство показывает,
  как преобразовать изображение в текст на C# и читать текст со сканированных изображений
  с помощью Aspose OCR.
og_title: Извлечение текста из PNG в C# – Полное руководство по OCR
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Извлечение текста из PNG в C# – Полное руководство по OCR
url: /ru/net/text-recognition/extract-text-from-png-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из PNG в C# – Полное руководство по OCR

Когда‑нибудь вам нужно было **извлечь текст из PNG** файлов, но вы не знали, с чего начать? Вы не одиноки — большинство разработчиков сталкиваются с этой проблемой, когда впервые встречают отсканированную графику или скриншоты, которые нужно превратить в поисковый текст. Хорошая новость? С несколькими строками C# и Aspose OCR вы можете мгновенно превратить любой PNG в редактируемые строки.

В этом руководстве мы пройдем весь процесс: от поиска PNG‑файлов на диске, запуска OCR‑задач параллельно, до отображения аккуратного предварительного просмотра каждого результата. К концу вы узнаете, как **convert image to text C#** в стиле, сможете **read text from scanned images** эффективно, и также увидите лучший способ **run OCR on images** без перегрузки UI‑потока.

## Что понадобится

- .NET 6.0 или новее (код работает и на .NET Core, и на .NET Framework)  
- NuGet‑пакет Aspose.OCR (`Install-Package Aspose.OCR`)  
- Папка, полная файлов *.png*, которые нужно обработать  
- Любая IDE по вашему выбору (Visual Studio, VS Code, Rider…)

Дополнительная конфигурация не требуется; библиотека поставляется со всем необходимым для декодирования PNG, JPEG, TIFF и т.д.

## Шаг 1: Найти все PNG‑файлы – начинается «Extract Text from PNG»

Сначала нам нужно найти каждый PNG, для которого мы планируем выполнить OCR. Использование `Directory.GetFiles` быстро и надёжно.

```csharp
// Step 1: Find all PNG images in the input folder
string[] imageFiles = Directory.GetFiles("YOUR_DIRECTORY", "*.png");

// Quick sanity check – throw if nothing was found
if (imageFiles.Length == 0)
    throw new FileNotFoundException("No PNG files found in the specified folder.");
```

*Почему это важно:* Однократный скан каталогa упрощает остальную часть конвейера, а ранняя проверка предотвращает тихую ситуацию «нет вывода», которую потом трудно отладить.

## Шаг 2: Запустить параллельные OCR‑задачи – эффективно **run OCR on images**

Последовательный запуск OCR подходит для небольшого количества файлов, но в реальных проектах часто приходится иметь дело с десятками или сотнями. Запуская `Task` для каждого изображения, мы загружаем процессор, пока библиотека выполняет тяжёлую работу.

```csharp
// Step 2: Prepare a list to hold OCR tasks (one per image)
var ocrTasks = new List<Task<string>>();

// Step 3: Launch a parallel task for each image
foreach (var filePath in imageFiles)
{
    ocrTasks.Add(Task.Run(() =>
    {
        // Load the image and run OCR
        var engine = new OcrEngine();
        engine.Image = ImageStream.FromFile(filePath);
        engine.Recognize();
        return engine.Text;          // This is the extracted string
    }));
}
```

*Совет профессионала:* `Task.Run` передаёт работу в пул потоков, что означает, что ваш UI (если он есть) остаётся отзывчивым. На сервере тот же шаблон хорошо масштабируется по ядрам.

## Шаг 3: Ожидать все задачи – собрать результаты

Теперь мы ждём завершения каждой OCR‑операции. `Task.WhenAll` возвращает массив, порядок которого соответствует исходному порядку файлов, что упрощает сопоставление результатов с именами файлов.

```csharp
// Step 4: Await all tasks and gather the recognized texts
string[] ocrResults = await Task.WhenAll(ocrTasks);
```

*Примечание о граничных случаях:* Если какое‑то изображение вызывает исключение (повреждённый файл, неподдерживаемый формат), весь `WhenAll` пробросит исключение. Вы можете обернуть внутренний `Task.Run` в try/catch и вернуть пустую строку или диагностическое сообщение, если нужна отказоустойчивость.

## Шаг 4: Показать предварительный просмотр – проверить вывод **convert image to text C#**

Быстрый предварительный просмотр помогает убедиться, что OCR сработал, прежде чем сохранять данные где‑то ещё.

```csharp
// Step 5: Show a short preview of each result
for (int i = 0; i < ocrResults.Length; i++)
{
    string fileName = Path.GetFileName(imageFiles[i]);
    string preview = ocrResults[i].Length > 100
        ? ocrResults[i][..100] + "..."
        : ocrResults[i];
    Console.WriteLine($"{fileName}: {preview}");
}
```

Типичный вывод консоли выглядит так:

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
```

Если в предварительном просмотре отображается мусор, проверьте качество изображения или рассмотрите предобработку (например, бинаризацию) — но для большинства чистых PNG Aspose OCR справляется с первой попытки.

## Необязательно: Сохранить результаты в CSV – реальный пример использования

Большинству проектов нужен извлечённый текст в структурированном виде. Ниже небольшой помощник, который записывает имя файла и полный OCR‑текст в CSV‑файл.

```csharp
string csvPath = Path.Combine("YOUR_DIRECTORY", "ocr-results.csv");
using var writer = new StreamWriter(csvPath);
writer.WriteLine("FileName,ExtractedText");

for (int i = 0; i < imageFiles.Length; i++)
{
    string escaped = ocrResults[i].Replace("\"", "\"\"");
    writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
}
Console.WriteLine($"All results saved to {csvPath}");
```

Теперь вы можете импортировать CSV в Excel, Power BI или любую downstream‑систему, ожидающую **read text from scanned images**.

## Часто задаваемые вопросы

**Что если мои PNG‑файлы огромные (более 5 МБ)?**  
Aspose OCR автоматически уменьшает масштаб больших изображений, чтобы расход памяти оставался приемлемым, но вы можете вручную изменить размер с помощью `engine.Image = ImageStream.FromFile(filePath).Resize(2000, 0);`, ограничив ширину 2000 px при сохранении пропорций.

**Можно ли запускать это на Linux?**  
Да. Aspose OCR кросс‑платформенный; просто убедитесь, что установлены нативные зависимости (`libgdiplus` в некоторых дистрибутивах).

**По умолчанию язык OCR установлен на английский?**  
Верно. Если нужен другой язык, задайте `engine.Language = OcrLanguage.French;` (или любой поддерживаемый enum) перед вызовом `Recognize()`.

**Как обрабатывать защищённые паролем PDF, содержащие PNG?**  
Сначала преобразуйте страницы PDF в изображения (используя Aspose PDF или другую библиотеку), затем передайте эти PNG в тот же конвейер. Принцип **how to run OCR on images** остаётся тем же.

## Полный рабочий пример (Async Main)

Ниже самостоятельная программа, которую можно скопировать и вставить в консольный проект. Она включает все вышеописанные части, а также небольшой помощник для проверки входной папки.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // -------------------------------------------------
        // 1️⃣ Locate PNGs – the heart of “extract text from png”
        // -------------------------------------------------
        const string folder = @"YOUR_DIRECTORY";   // <-- change this
        if (!Directory.Exists(folder))
        {
            Console.WriteLine($"Folder not found: {folder}");
            return;
        }

        string[] imageFiles = Directory.GetFiles(folder, "*.png");
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to do.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Fire off OCR tasks – best way to “run OCR on images”
        // -------------------------------------------------
        var ocrTasks = new List<Task<string>>();
        foreach (var filePath in imageFiles)
        {
            ocrTasks.Add(Task.Run(() =>
            {
                var engine = new OcrEngine();
                engine.Image = ImageStream.FromFile(filePath);
                engine.Recognize();
                return engine.Text;
            }));
        }

        // -------------------------------------------------
        // 3️⃣ Await results
        // -------------------------------------------------
        string[] ocrResults = await Task.WhenAll(ocrTasks);

        // -------------------------------------------------
        // 4️⃣ Show previews
        // -------------------------------------------------
        for (int i = 0; i < ocrResults.Length; i++)
        {
            string fileName = Path.GetFileName(imageFiles[i]);
            string preview = ocrResults[i].Length > 100
                ? ocrResults[i][..100] + "..."
                : ocrResults[i];
            Console.WriteLine($"{fileName}: {preview}");
        }

        // -------------------------------------------------
        // 5️⃣ Optional: write CSV – perfect for “read text from scanned images”
        // -------------------------------------------------
        string csvPath = Path.Combine(folder, "ocr-results.csv");
        using var writer = new StreamWriter(csvPath);
        writer.WriteLine("FileName,ExtractedText");
        for (int i = 0; i < imageFiles.Length; i++)
        {
            string escaped = ocrResults[i].Replace("\"", "\"\"");
            writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
        }

        Console.WriteLine($"✅ OCR complete – results saved to {csvPath}");
    }
}
```

**Ожидаемый вывод** (пример для двух PNG):

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
✅ OCR complete – results saved to C:\MyImages\ocr-results.csv
```

## Итоги

Мы только что рассмотрели всё, что вам нужно для **extract text from PNG** файлов с помощью C#. От поиска файлов, запуска параллельных OCR‑задач, предварительного просмотра строк до их сохранения в CSV — это руководство предоставляет готовый к продакшну шаблон для сценариев **convert image to text C#**.  

Если вы готовы к следующему шагу, попробуйте подать в тот же конвейер JPEG или TIFF файлы, поэкспериментировать с разными языками OCR, или подключить результаты к поисковому индексу, чтобы сразу **read text from scanned images**.  

Есть вопросы о граничных случаях, оптимизации производительности или лицензировании? Оставьте комментарий или напишите в сообщество Aspose — happy coding!  

![Extract text from PNG example](extract-text-png.png "Extract text from PNG using Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}