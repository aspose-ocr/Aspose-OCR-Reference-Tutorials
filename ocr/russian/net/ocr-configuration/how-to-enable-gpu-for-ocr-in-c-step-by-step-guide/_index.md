---
category: general
date: 2026-04-04
description: Как быстро включить GPU в Aspose OCR. Узнайте, как извлекать текст из
  изображения, загружать изображение для OCR и распознавать текст с помощью C#.
draft: false
keywords:
- how to enable gpu
- extract text from image
- how to extract text
- how to recognize text
- load image for ocr
language: ru
og_description: Как быстро включить GPU в Aspose OCR. Следуйте этому руководству,
  чтобы извлечь текст из изображения, загрузить изображение для OCR и распознать текст
  с помощью C#.
og_title: Как включить GPU для OCR в C# – Полное руководство
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Как включить GPU для OCR в C# – пошаговое руководство
url: /ru/net/ocr-configuration/how-to-enable-gpu-for-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как включить GPU для OCR в C# – Полный пошаговый гид

Когда‑нибудь задавались вопросом **как включить GPU** при использовании Aspose OCR? Возможно, вы столкнулись с ограничением производительности при обработке сотен чеков, и процессор просто не успевает. Хорошая новость в том, что включить ускорение GPU — проще простого, и как только оно включено, вы увидите, как движок OCR мчится сквозь изображения.

В этом руководстве мы не только переключим GPU, но и покажем, как **load image for OCR**, **recognize text** и, в конечном итоге, **extract text from image** с помощью чистого примера на C#. К концу у вас будет готовая к запуску программа, извлекающая обычный текст из любого поддерживаемого изображения — без внешних сервисов.

## Что понадобится

- .NET 6+ (или .NET Framework 4.7.2 и новее).  
- Aspose.OCR for .NET, версия 24.2.0 или новее (флаг GPU был добавлен в этом выпуске).  
- Машина с поддержкой GPU и соответствующими драйверами (NVIDIA CUDA 11+ отлично работает).  
- Файл изображения, который вы хотите обработать — представьте сканированный чек, сфотографированный счёт или рукописную заметку.

Если у вас уже есть всё это, отлично — приступим.

## Шаг 1: Как включить GPU – Настройка OCR‑движка

Первое, что нужно сделать, — сообщить Aspose OCR использовать GPU. Это делается установкой свойства `UseGpu` у экземпляра `OcrEngine`. По умолчанию свойство имеет значение `false`, поэтому мы явно включаем его.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // <-- GPU module namespace

// Create the OCR engine and enable GPU acceleration (available from version 24.2.0)
var ocrEngine = new OcrEngine
{
    // Enabling GPU can speed up recognition by 2‑5× on a modern card
    UseGpu = true
};
```

**Почему это важно:** Когда `UseGpu` равно `true`, библиотека передаёт тяжёлые матричные вычисления графическому процессору. На скромной RTX 3060 вы заметите, как задержка падает с нескольких секунд за изображение до доли секунды.

> **Pro tip:** Если вы работаете в безголовом CI‑окружении, убедитесь, что драйвер GPU установлен и учетная запись службы имеет разрешение на доступ к устройству. В противном случае движок тихо переключится в режим CPU.

## Шаг 2: Загрузка изображения для OCR – Указание движку вашего файла

Далее нам нужно **load image for OCR**. Aspose OCR принимает любой формат изображения, поддерживаемый System.Drawing (PNG, JPEG, BMP, TIFF и т.д.). Помощник `ImageStream.FromFile` оборачивает файл в требуемый объект потока.

```csharp
// Replace the path with the location of your receipt or document
string imagePath = @"C:\MyImages\receipt.jpg";

ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Если вы предпочитаете загружать из `byte[]` (например, когда изображение берётся из базы данных), можете использовать `ImageStream.FromBytes(byteArray)` — тот же результат, просто другой источник.

## Шаг 3: Как распознать текст – Запуск OCR‑процесса

Теперь, когда движок настроен и изображение загружено, пришло время **recognize text**. Метод `Recognize` выполняет всю тяжёлую работу и возвращает объект `OcrResult`, содержащий обычный текст, оценки уверенности и даже ограничивающие рамки, если они понадобятся позже.

```csharp
// Run the recognition process (English is the default language)
OcrResult ocrResult = ocrEngine.Recognize();
```

Вы также можете изменить язык, установив `ocrEngine.Language = OcrLanguage.French;` перед вызовом `Recognize()`. Ускорение GPU работает независимо от загруженного языкового пакета.

## Шаг 4: Как извлечь текст из изображения – Вывод результата

Наконец мы **extract text from image**, читая свойство `Text` у объекта результата. Для демонстрации мы просто выведем его в консоль, но вы можете записать его в файл, базу данных или передать в другой сервис.

```csharp
// Output the extracted plain‑text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(ocrResult.Text);
```

**Ожидаемый вывод** (ваш реальный текст будет отличаться в зависимости от изображения):

```
=== OCR RESULT ===
Store: Coffee Corner
Date: 03/28/2026
Item          Qty   Price
Latte          2    $5.00
Muffin         1    $2.50
Total                 $12.50
```

Если вам нужны сырые значения уверенности, вы можете пройтись по `ocrResult.Regions` и проверить каждое `Region.Confidence`.

## Полный рабочий пример – Один файл, готовый к запуску

Ниже приведена полная программа. Скопируйте её в новый консольный проект, восстановите пакет NuGet Aspose.OCR и нажмите **F5**.

```csharp
// ------------------------------------------------------------
// How to enable gpu for OCR in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU module namespace

class Program
{
    static void Main()
    {
        // -------- Step 1: Enable GPU ----------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true   // <-- crucial for acceleration
        };

        // -------- Step 2: Load image ----------
        // Make sure the file exists; otherwise an exception is thrown.
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------- Step 3: Recognize text -------
        OcrResult ocrResult = ocrEngine.Recognize();

        // -------- Step 4: Extract text ----------
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Note:** Замените `YOUR_DIRECTORY/receipt.jpg` на фактический путь к вашему изображению. Если программа бросит `FileNotFoundException`, дважды проверьте путь и права доступа к файлу.

## Часто задаваемые вопросы и особые случаи

### Что делать, если GPU не обнаружен?

Aspose OCR автоматически переключится в режим CPU и запишет предупреждение в журнал. Чтобы проверить, какой режим активен, посмотрите `ocrEngine.IsGpuEnabled` после создания — он возвращает `true` только когда драйвер GPU успешно загружен.

### Можно ли обрабатывать несколько изображений в цикле?

Конечно. Просто перенесите строку `ocrEngine.Image = …` внутрь цикла `foreach (var file in files)`. Используйте тот же экземпляр `OcrEngine`; повторное его использование избавляет от накладных расходов на многократное выделение GPU‑ресурсов.

```csharp
foreach (var file in Directory.GetFiles(@"C:\MyImages", "*.jpg"))
{
    ocrEngine.Image = ImageStream.FromFile(file);
    var result = ocrEngine.Recognize();
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Length} characters");
}
```

### Как работать с неанглийскими языками?

Установите язык перед вызовом `Recognize()`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;   // or any supported language enum
```

Ускорение GPU работает так же; меняется только языковая модель.

### Что делать с большими, высокоразрешёнными фотографиями?

Если вы столкнётесь с ошибками нехватки памяти, сначала уменьшите масштаб изображения. Aspose OCR предоставляет `ImageHelper.Resize` — быстрый способ уменьшить размер без значительной потери деталей.

```csharp
ocrEngine.Image = ImageHelper.Resize(
    ImageStream.FromFile(imagePath), 
    maxWidth: 2000, 
    maxHeight: 2000);
```

## Заключение

Мы рассмотрели **how to enable gpu** для Aspose OCR, показали, как **load image for OCR**, прошли через **how to recognize text** и продемонстрировали **how to extract text from image** с помощью лаконичной, готовой к продакшену программы на C#. Переключив флаг `UseGpu`, вы получаете заметный прирост скорости, особенно при обработке пакетов чеков, счетов или любого потока документов большого объёма.

Готовы к следующему шагу? Попробуйте связать этот OCR‑конвейер с базой данных для хранения извлечённых чеков или передать обычный текст в модель обработки естественного языка для классификации расходов. Вы также можете изучить коллекцию `OcrResult.Regions`, чтобы получить координаты ограничивающих рамок и построить интерфейс, подсвечивающий каждое слово на оригинальном изображении.

Удачной разработки и наслаждайтесь дополнительной мощью, которую ускорение GPU приносит вашим задачам OCR!

---

![how to enable gpu illustration](gpu-ocr-diagram.png "how to enable gpu illustration")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}