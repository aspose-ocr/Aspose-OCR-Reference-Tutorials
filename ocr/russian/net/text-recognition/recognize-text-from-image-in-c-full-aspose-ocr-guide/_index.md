---
category: general
date: 2026-04-03
description: распознавать текст с изображения с помощью Aspose OCR в C#. Узнайте,
  как загрузить изображение для OCR, извлечь текст из изображения, записать JSON‑файл
  в C# и выполнить OCR для PNG.
draft: false
keywords:
- recognize text from image
- write json file c#
- load image for ocr
- extract text from image
- perform ocr on png
language: ru
og_description: распознавать текст с изображения с помощью Aspose OCR в C#. Пошаговое
  руководство по загрузке изображения для OCR, извлечению текста из изображения, записи
  JSON‑файла в C# и выполнению OCR для PNG.
og_title: распознавание текста с изображения в C# – Полный учебник по Aspose OCR
tags:
- OCR
- C#
- Aspose
title: Распознавание текста с изображения в C# – Полное руководство по Aspose OCR
url: /ru/net/text-recognition/recognize-text-from-image-in-c-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# распознавание текста с изображения в C# – Полный учебник Aspose OCR

Когда‑нибудь нужно было **распознать текст с изображения**, но не знали, какую библиотеку выбрать? Возможно, у вас есть пачка отсканированных чеков, PNG‑скриншот или рукописная записка, которую вы хотите превратить в поисковые данные. Хорошая новость: с Aspose.OCR это можно сделать в несколько строк кода C#, и вы даже получите аккуратный JSON‑файл, который можно передать в другие системы.

В этом учебнике мы пройдёмся по загрузке изображения для OCR, извлечению текста из изображения, сериализации результата в JSON‑файл и, наконец, обработке PNG‑файлов без лишних усилий. К концу вы получите готовое консольное приложение, которое **распознаёт текст с изображения** и записывает вывод в *output.json*.

## Что понадобится

- .NET 6.0 или новее (код также работает с .NET Framework)
- NuGet‑пакет Aspose.OCR (`Install-Package Aspose.OCR`)
- PNG (или любой поддерживаемый формат), который нужно обработать
- Visual Studio, VS Code или любой другой редактор C#

Дополнительные сторонние библиотеки не требуются — только движок Aspose OCR и встроенный сериализатор `System.Text.Json`.

## Шаг 1: Распознавание текста с изображения с помощью Aspose OCR

Первое, что нужно сделать, — создать экземпляр `OcrEngine`. Этот объект выполняет всю тяжёлую работу за кулисами.

```csharp
using Aspose.OCR;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this is where the magic starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image for OCR – replace the path with your own file.
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/input.png");

        // Perform OCR on the loaded image and get a structured result.
        OcrResult ocrResult = ocrEngine.RecognizeToResult(sourceImage);

        // Serialize the result into a nicely indented JSON string.
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // Write JSON file C# – this will create output.json next to your exe.
        File.WriteAllText(@"YOUR_DIRECTORY/output.json", json);
    }
}
```

**Почему это важно:** Создание `OcrEngine` один раз и повторное его использование эффективнее, чем создание нового движка для каждого файла. Вызов `RecognizeToResult` возвращает объект `OcrResult`, который уже содержит извлечённый текст, оценки уверенности и ограничивающие рамки — идеально для последующей обработки.

## Шаг 2: Загрузка изображения для OCR — обработка разных форматов

Aspose OCR умеет читать PNG, JPEG, BMP и многие другие форматы. Если вы работаете с PNG, содержащим прозрачность, возможно, потребуется «сплющить» его, чтобы избежать неожиданных пустот.

```csharp
// Optional: flatten PNG with transparency to a white background.
if (sourceImage.RawFormat.Equals(System.Drawing.Imaging.ImageFormat.Png))
{
    Bitmap flat = new Bitmap(sourceImage.Width, sourceImage.Height);
    using (Graphics g = Graphics.FromImage(flat))
    {
        g.Clear(Color.White);
        g.DrawImage(sourceImage, 0, 0);
    }
    sourceImage = flat;
}
```

**Совет:** Всегда проверяйте, что размеры изображения разумные (например, ширина > 50 px). Слишком маленькие изображения могут привести к пропуску символов OCR‑движком, что снизит оценки уверенности.

## Шаг 3: Запись JSON‑файла в C# — делаем вывод пригодным для использования

Сериализатор `System.Text.Json` быстрый и встроенный, но при необходимости вы можете заменить его на `Newtonsoft.Json` для кастомных конвертеров. В примере выше уже используется `WriteIndented = true`, поэтому полученный файл читаем человеком.

```csharp
// Expected output (truncated):
{
  "Text": "Hello World",
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello World",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 120, "Height": 30 }
        }
      ]
    }
  ]
}
```

Наличие OCR‑данных в JSON упрощает импорт в базы данных, отправку по HTTP или передачу в конвейеры машинного обучения.

## Шаг 4: Проверка результата — быстрая sanity‑check

После выполнения программы откройте `output.json` и найдите поле `"Text"`. Если в нём содержится ожидаемая строка, вы успешно **извлекли текст из изображения**. Если уверенность низкая, рассмотрите предварительную обработку изображения (например, увеличение контрастности или применение бинарного порога).

```csharp
Console.WriteLine($"Extracted text: {ocrResult.Text}");
Console.WriteLine($"Overall confidence: {ocrResult.Confidence:P2}");
```

Запуск консоли выведет что‑то вроде:

```
Extracted text: Hello World
Overall confidence: 98.00%
```

Это явный признак того, что OCR сработал как задумано.

## Распространённые подводные камни и особые случаи

| Проблема | Почему происходит | Как исправить |
|----------|-------------------|---------------|
| **Пустой вывод** | Изображение слишком тёмное или имеет неподдерживаемое цветовое пространство | Перевести в градации серого, увеличить яркость или сплющить PNG (см. Шаг 2) |
| **Мусорные символы** | Низкое DPI (< 72) или сильный шум | Увеличить разрешение изображения или применить фильтр шумоподавления перед `RecognizeToResult` |
| **Большие файлы вызывают нагрузку на память** | Загрузка многомегапиксельного PNG в `Bitmap` потребляет ОЗУ | Обрабатывать изображения порциями или уменьшать их масштаб, сохраняя читаемость |
| **Ошибка сериализации JSON** | `OcrResult` содержит циклические ссылки (маловероятно) | Использовать `JsonSerializerOptions { ReferenceHandler = ReferenceHandler.IgnoreCycles }` |

## Бонус: OCR PNG в пакетном цикле

Если у вас есть папка, полная PNG‑файлов, вы можете расширить демонстрацию, чтобы перебрать их все:

```csharp
string[] pngFiles = Directory.GetFiles(@"YOUR_DIRECTORY", "*.png");
foreach (var file in pngFiles)
{
    Image img = Image.FromFile(file);
    OcrResult res = ocrEngine.RecognizeToResult(img);
    string outPath = Path.ChangeExtension(file, ".json");
    File.WriteAllText(outPath, JsonSerializer.Serialize(res, new JsonSerializerOptions { WriteIndented = true }));
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(outPath)}");
}
```

Теперь программа **выполняет OCR PNG** файлов массово, создавая соответствующий JSON‑файл для каждого изображения.

## Заключение

Вы только что узнали, как **распознавать текст с изображения** в C# с помощью Aspose OCR, **загружать изображение для OCR**, **извлекать текст из изображения** и **записывать JSON‑файл в C#** для сохранения результатов. Полный, готовый к запуску пример охватывает основные шаги, объясняет, почему каждый элемент важен, и даже показывает, как справляться с особенностями PNG.

Что дальше? Попробуйте загрузить JSON в поисковый индекс, объединить его с определением языка или интегрировать в веб‑API, которое обрабатывает загрузки «на лету». Вы также можете изучить поддержку Aspose распознавания рукописного текста, если ваш сценарий требует этого.

Есть вопросы о крайних случаях или настройке производительности? Оставляйте комментарий ниже — happy coding! 

![демонстрация распознавания текста с изображения](/images/ocr-demo.png "Диаграмма, показывающая, как Aspose OCR распознаёт текст с изображения")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}