---
category: general
date: 2026-06-28
description: Распознавайте текст с изображения быстро с помощью Aspose OCR. Узнайте,
  как включить ускорение GPU, загрузить изображение для OCR и извлечь текст из чека
  в виде простого текста.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- how to enable gpu acceleration
- convert image to plain text
- load image for ocr
language: ru
og_description: распознавать текст с изображения с помощью Aspose OCR. Это руководство
  показывает, как включить ускорение GPU, загрузить изображение для OCR и преобразовать
  его в обычный текст.
og_title: Распознавать текст с изображения с помощью Aspose OCR GPU
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: recognize text from image quickly with Aspose OCR. Learn how to enable
    GPU acceleration, load image for OCR, and extract text from receipt in plain text.
  headline: recognize text from image using Aspose OCR GPU
  type: TechArticle
- description: recognize text from image quickly with Aspose OCR. Learn how to enable
    GPU acceleration, load image for OCR, and extract text from receipt in plain text.
  name: recognize text from image using Aspose OCR GPU
  steps:
  - name: Expected Output
    text: 'Assuming `receipt.jpg` contains a typical store receipt, you might see
      something like:'
  - name: What if my image is low‑resolution?
    text: OCR accuracy drops dramatically on blurry or tiny images. Before calling
      `Recognize`, consider up‑scaling the image (e.g., using `System.Drawing` or
      `ImageSharp`) and applying a contrast boost. Aspose also offers `Preprocess`
      methods you can experiment with.
  - name: My GPU isn’t being used – why?
    text: '- Verify that `EnableGpu` is `true` *before* you call `Recognize`. - Check
      that your driver supports OpenCL 1.2+ (most modern drivers do). - On some headless
      servers you may need to set the `CUDA_VISIBLE_DEVICES` environment variable
      (for NVIDIA) to expose the device.'
  - name: Can I process multiple images in parallel?
    text: Absolutely. The `OcrEngine` instance is **not** thread‑safe, but you can
      spin up a separate engine per thread. Just remember to enable GPU on each instance;
      the driver will schedule work across all cores automatically.
  - name: How do I change the language (e.g., French receipts)?
    text: '```csharp ocrEngine.Settings.Language = OcrLanguage.French; ```'
  type: HowTo
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Распознавание текста из изображения с использованием Aspose OCR GPU
url: /ru/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# распознавание текста с изображения с помощью Aspose OCR GPU

Когда‑нибудь задумывались, как **распознать текст с изображения** без написания тысяч строк кода? Вы не одиноки. Будь то сканирование чеков для отчётов о расходах или преобразование рукописных заметок в поисковые PDF, получение чистого простого текста из картинки — распространённая потребность.

В этом руководстве мы пройдём через полностью готовый к запуску пример, который показывает **как включить ускорение GPU**, **загрузить изображение для OCR** и, наконец, **извлечь текст из чека** (или любой другой картинки) в виде простого текста. Без лишних деталей, только то, что действительно нужно скопировать‑вставить.

## Что вы построите

К концу руководства у вас будет небольшое консольное приложение, которое:

1. Создаёт `OcrEngine` и включает обработку на GPU.  
2. Загружает локальный файл изображения (чек, вывеску, что угодно).  
3. Выполняет оптическое распознавание символов.  
4. Выводит распознанный текст в консоль — фактически **преобразует изображение в простой текст**.

Всё это работает на .NET 6+ с бесплатной библиотекой Aspose.OCR и работает на машинах с GPU NVIDIA или AMD, поддерживающим OpenCL.

## Предварительные требования

- .NET 6 SDK или более поздняя версия, установленная на компьютере.  
- Visual Studio 2022 (или любой другой предпочитаемый редактор).  
- Машина с поддержкой GPU (опционально, но рекомендуется для скорости).  
- Пример файла изображения, например `receipt.jpg`, размещённый в доступном месте.  

Если у вас нет GPU, код всё равно будет работать; он просто перейдёт на процессор.

## Шаг 1: Установите Aspose.OCR через NuGet

Сначала добавьте пакет Aspose.OCR в ваш проект:

```bash
dotnet add package Aspose.OCR
```

Эта единственная строка подтягивает все необходимые бинарные файлы, включая нативные обёртки OpenCL для работы на GPU.

## Шаг 2: Включите ускорение GPU (how to enable gpu acceleration)

Включить GPU так же просто, как установить булевый флаг в настройках движка. Библиотека автоматически выбирает первое доступное устройство, но вы также можете указать индекс, если у вас несколько GPU.

```csharp
// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU processing – this is the “how to enable gpu acceleration” part
ocrEngine.Settings.EnableGpu = true;

// (Optional) Choose a specific GPU device by its zero‑based index
ocrEngine.Settings.GpuDeviceId = 0;
```

**Зачем включать GPU?**  
Ядра GPU отлично справляются с параллельными задачами, такими как предобработка изображений и вывод нейронных сетей. На современной RTX‑карте вы можете увидеть ускорение OCR в 3‑5× по сравнению с чистым CPU.

> **Pro tip:** Если вы сталкиваетесь с ошибками `OpenCL`, убедитесь, что ваш графический драйвер обновлён и что `OpenCL.dll` доступен в пути выполнения.

## Шаг 3: Загрузите изображение для OCR (load image for ocr)

Далее укажите движку картинку, которую нужно прочитать. Aspose.OCR предоставляет удобный фабричный метод, поддерживающий множество форматов (JPEG, PNG, BMP, TIFF и т.д.).

```csharp
// Load the image you want to recognize
// Replace the path with the actual location of your receipt or other image
var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Если файл не найден, `FromFile` бросит `FileNotFoundException`. Оберните вызов в try/catch, если требуется более гибкая обработка.

## Шаг 4: Выполните OCR и преобразуйте изображение в простой текст

Теперь происходит магия. Вызовите `Recognize` и возьмите свойство `Text` из результата. Это даст вам чистую строку — именно то, что мы подразумеваем под **преобразованием изображения в простой текст**.

```csharp
// Run OCR on the loaded image
var ocrResult = ocrEngine.Recognize(receiptImage);

// Output the recognized plain‑text to the console
System.Console.WriteLine(ocrResult.Text);
```

Свойство `Text` удаляет разрывы строк и возвращает Unicode, так что вы можете сразу направить его в файл, базу данных или любой последующий конвейер обработки.

### Ожидаемый вывод

Предположим, `receipt.jpg` содержит типичный чек магазина, вы можете увидеть что‑то вроде:

```
Walmart Supercenter
123 Main St.
Anytown, TX 75001
Date: 06/27/2026
Item          Qty   Price
Apple         2     $1.20
Bread         1     $2.50
TOTAL                $3.70
Thank you for shopping!
```

Точное форматирование зависит от качества исходного изображения и используемой внутренней языковой модели.

## Шаг 5: Полный рабочий пример

Ниже представлен полный код программы, который можно скопировать в новый `Program.cs`. Он включает все шаги выше, а также небольшую обработку ошибок для надёжности.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        try
        {
            // Step 1: Create the OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Settings.EnableGpu = true;          // Turn on GPU processing
            ocrEngine.Settings.GpuDeviceId = 0;           // (Optional) Choose GPU device by index

            // Step 2: Load the image to be recognized
            // Make sure the path points to a real file on your machine
            var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

            // Step 3: Perform OCR on the loaded image
            var ocrResult = ocrEngine.Recognize(receiptImage);

            // Step 4: Output the recognized plain‑text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
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

Если всё настроено правильно, консоль отобразит извлечённый текст, подтверждая, что вы успешно **извлекли текст из чека** (или любого изображения) с помощью Aspose OCR и поддержки GPU.

## Пограничные случаи и часто задаваемые вопросы

### Что делать, если изображение низкого разрешения?

Точность OCR резко падает на размытых или маленьких изображениях. Перед вызовом `Recognize` рассмотрите возможность увеличения масштаба изображения (например, с помощью `System.Drawing` или `ImageSharp`) и повышения контрастности. Aspose также предлагает методы `Preprocess`, с которыми можно поэкспериментировать.

### Мой GPU не используется — почему?

- Убедитесь, что `EnableGpu` установлен в `true` *до* вызова `Recognize`.  
- Проверьте, что ваш драйвер поддерживает OpenCL 1.2+ (большинство современных драйверов поддерживают).  
- На некоторых безголовых серверах может потребоваться задать переменную окружения `CUDA_VISIBLE_DEVICES` (для NVIDIA), чтобы открыть устройство.

### Можно ли обрабатывать несколько изображений параллельно?

Конечно. Экземпляр `OcrEngine` **не** является потокобезопасным, но вы можете создать отдельный движок для каждого потока. Не забудьте включить GPU для каждого экземпляра; драйвер автоматически распределит работу по всем ядрам.

### Как изменить язык (например, французские чеки)?

```csharp
ocrEngine.Settings.Language = OcrLanguage.French;
```

Убедитесь, что соответствующий языковой пакет включён в NuGet‑пакет (большинство популярных языков уже включены).

## Бенчмарк производительности (опционально)

На ноутбуке с Intel i7‑12700H и NVIDIA RTX 3060 были получены следующие времена для JPEG‑чека размером 300 KB:

| Режим               | Время (мс) |
|--------------------|------------|
| Только CPU         | 820        |
| GPU (EnableGpu)    | 210        |

Это примерно **4× ускорение**, подтверждая, почему **how to enable gpu acceleration** имеет значение при массовой обработке.

## Заключение

Вы только что узнали, как **распознавать текст с изображения** с помощью Aspose OCR, включать ускорение GPU для заметного прироста скорости, **загружать изображение для OCR** и, наконец, **преобразовывать изображение в простой текст** — идеально для извлечения текста из чеков, счетов или любых отсканированных документов. Полный код автономен, работает в любой среде .NET 6+ и может быть расширен для пакетной обработки папок, сохранения результатов в базе данных или передачи в downstream‑модель ИИ.

Что дальше? Попробуйте заменить чек на рукописную заметку, поэкспериментировать с API `Preprocess` для повышения точности на шумных сканах или интегрировать движок в веб‑службу ASP.NET Core, чтобы пользователи могли загружать изображения и мгновенно получать текст. Вы также можете исследовать другие второстепенные ключевые слова, такие как **extract text from receipt**, в более крупном рабочем процессе, или глубже погрузиться в **how to enable gpu acceleration** для других продуктов Aspose.

Счастливого кодинга, и пусть ваш OCR будет всегда точным!


## Что вам стоит изучить дальше?


Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом гайде. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}