---
category: general
date: 2026-02-24
description: Как включить GPU в примере Aspose OCR на C# – быстро преобразовать изображение
  в обычный текст. Включает установку ID GPU‑устройства и руководство по чтению текста
  из изображения на C#.
draft: false
keywords:
- how to enable gpu
- image to plain text
- aspose ocr example
- set gpu device id
- read image text c#
language: ru
og_description: Как включить GPU в примере Aspose OCR на C#. Узнайте, как задать идентификатор
  GPU‑устройства и эффективно считывать текст изображения в C#.
og_title: Как включить GPU для Aspose OCR в C# – Быстрое преобразование изображения
  в обычный текст
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Как включить GPU для Aspose OCR в C# — быстрое преобразование изображения в
  обычный текст
url: /ru/net/ocr-optimization/how-to-enable-gpu-for-aspose-ocr-in-c-fast-image-to-plain-te/
---

terms in English.

We must ensure we keep all headings, lists, tables, etc.

We need to translate everything except code block placeholders and shortcodes. Also the table content: "Issue", "Why it Happens", "Quick Fix" etc. Should we translate those? Yes, translate text content, but keep the table formatting. So translate the column headers and rows.

Also translate the description text.

We must preserve markdown syntax.

Let's produce the translated version.

We need to keep the shortcodes exactly as they are.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как включить GPU для Aspose OCR в C# – Быстрое преобразование изображения в обычный текст

Задумывались ли вы **как включить GPU** при использовании Aspose OCR для преобразования картинки в редактируемый текст? Вы не одиноки — многие разработчики сталкиваются с проблемой производительности при обработке больших счетов или отсканированных договоров. Хорошая новость? Преобразование изображения в обычный текст может стать молниеносным, как только вы задействуете видеокарту.

В этом руководстве мы пройдем полный **пример Aspose OCR**, который покажет, как включить GPU, задать идентификатор GPU‑устройства и **читать текст изображения в стиле C#**. К концу вы получите готовую к запуску программу, извлекающую текст из любого поддерживаемого изображения за доли времени, требуемого при работе только на CPU.

## Что понадобится

Прежде чем начать, убедитесь, что у вас есть:

- .NET 6.0 или новее (API работает с .NET Core и .NET Framework)
- Совместимая с CUDA видеокарта с установленным последним драйвером
- Лицензия Aspose.OCR для .NET (или бесплатная пробная версия, подходящая для разработки)
- Visual Studio 2022 (или любой другой редактор C# по вашему выбору)

Никаких дополнительных пакетов NuGet помимо `Aspose.OCR` не требуется — только сама библиотека.

---

## Шаг 1 – Установите пакет Aspose OCR из NuGet

Для начала добавьте официальную библиотеку Aspose OCR в ваш проект. Откройте консоль диспетчера пакетов и выполните:

```powershell
Install-Package Aspose.OCR
```

Это загрузит `Aspose.OCR.dll` и все его зависимости. Если предпочитаете графический интерфейс, щелкните правой кнопкой мыши по проекту → **Manage NuGet Packages** → найдите *Aspose.OCR* и нажмите **Install**.  

*Совет:* После установки проверьте, что папка `Aspose.OCR` появилась в разделе **Dependencies** в обозревателе решений.

---

## Шаг 2 – Создайте простой скелет консольного приложения

Мы построим небольшое консольное приложение, демонстрирующее весь процесс. Создайте новый проект:

```bash
dotnet new console -n GpuOcrDemo
cd GpuOcrDemo
```

Замените сгенерированный `Program.cs` полным кодом, который будет показан ниже. Этот скелет дает чистую точку входа и позволяет сосредоточиться на логике OCR.

---

## Шаг 3 – Как включить GPU и задать идентификатор GPU‑устройства

А теперь к главному: **как включить GPU** в Aspose OCR. Библиотека предоставляет объект `OcrSettings`, где можно переключить `UseGpu` и, при желании, указать конкретное CUDA‑устройство через `GpuDeviceId`. Ниже приведён точный фрагмент, который вы вставите в свою программу:

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration – this is the crucial “how to enable gpu” step
        ocrEngine.Settings = new OcrSettings()
        {
            UseGpu = true,          // Turn on GPU processing
            GpuDeviceId = 0         // Optional: select the first CUDA‑compatible device
        };

        // 3️⃣ Recognise text from an image (any supported format)
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/large_invoice.png");

        // 4️⃣ Output the plain‑text result to the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Почему стоит включать GPU?

Включение GPU переносит тяжёлые операции — предобработку пикселей, сегментацию символов и вывод нейронных сетей — на видеокарту. На скромной GTX 1650 вы можете увидеть **ускорение в 2‑3 раза** по сравнению с режимом только CPU, особенно при работе с документами высокого разрешения.

### Выбор идентификатора устройства

Если в вашем компьютере несколько видеокарт, `GpuDeviceId` позволяет выбрать конкретную. `0` — первая карта; `1` — вторая и т.д. Доступные ID можно узнать с помощью утилиты NVIDIA `nvidia-smi` или запросив класс `GpuInfo` Aspose (не показано здесь для краткости).

---

## Шаг 4 – Полный рабочий пример (готов к копированию)

Ниже полностью готовая к запуску программа. Вставьте её в `Program.cs`, замените путь к изображению на реальный файл на вашем диске и нажмите **F5**.

```csharp
// Program.cs – Complete Aspose OCR GPU example
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate the input argument (optional but handy)
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image_path>");
                return;
            }

            string imagePath = args[0];

            // Initialise the OCR engine
            var ocrEngine = new OcrEngine();

            // -------------------- How to Enable GPU --------------------
            // Turn on GPU acceleration and optionally pick a device
            ocrEngine.Settings = new OcrSettings()
            {
                UseGpu = true,          // Enables GPU processing
                GpuDeviceId = 0         // Selects the first CUDA‑compatible GPU
            };
            // ---------------------------------------------------------

            try
            {
                // Recognise the image – this is the “image to plain text” core
                var ocrResult = ocrEngine.RecognizeImage(imagePath);

                // Display the extracted text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – helpful when the GPU is unavailable
                Console.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

### Ожидаемый вывод

Если предоставленное изображение содержит строку *“Invoice #12345 – Total $1,250.00”*, консоль выведет:

```
=== Extracted Text ===
Invoice #12345 – Total $1,250.00
```

Результат — обычный текст, готовый к дальнейшей обработке (например, загрузке в базу данных или передаче в парсер естественного языка).

---

## Шаг 5 – Проверка использования GPU (по желанию)

Чтобы убедиться, что GPU действительно используется, откройте инструмент мониторинга видеокарты (например, **NVIDIA‑Smi** или **GPU‑Z**) во время выполнения программы. Вы должны увидеть всплеск нагрузки на выбранном устройстве. Если видна только активность CPU, проверьте следующее:

- Драйвер видеокарты обновлён до последней версии.
- Флаг `UseGpu` установлен в `true`.
- Формат изображения поддерживается (PNG, JPEG, TIFF и т.д.).

---

## Распространённые проблемы и способы их избежать

| Проблема | Почему происходит | Быстрое решение |
|----------|-------------------|-----------------|
| **GPU не обнаружен** | Устаревший драйвер или отсутствует среда CUDA | Установите последний драйвер NVIDIA и набор инструментов CUDA |
| **`Aspose.OCR` бросает “GPU not supported”** | Запуск на видеокарте без поддержки CUDA (например, старый AMD) | Установите `UseGpu = false` или замените видеокарту на совместимую |
| **Неправильный путь к изображению** | Относительный путь указывает не туда | Используйте абсолютный путь или передавайте путь как аргумент командной строки |
| **Лицензия не применена** | Режим оценки может ограничивать использование GPU | Зарегистрируйте лицензию: `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Расширение примера: пакетная обработка с GPU

Если нужно обработать десятки счетов, оберните вызов распознавания в цикл. Поскольку GPU остаётся «разогретой», последующие изображения выигрывают от **кеширования прогрева**, экономя ещё больше миллисекунд на каждый запуск.

```csharp
string[] files = Directory.GetFiles(@"C:\Invoices\", "*.png");
foreach (var file in files)
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Trim()}");
}
```

Помните, что следует использовать один и тот же экземпляр `OcrEngine` — создание нового движка для каждого файла заново инициализирует контекст GPU и сильно снижает производительность.

---

## Заключение

Теперь у вас есть полноценный, сквозной **пример Aspose OCR**, показывающий **как включить GPU**, **как задать идентификатор GPU‑устройства** и **как читать текст изображения в стиле C#**. Переключив `UseGpu` и указав нужное устройство, вы превращаете медленную OCR‑задачу, ограниченную CPU, в высокопроизводительный конвейер, способный обрабатывать большие счета, чеки или любые отсканированные документы.

Экспериментируйте: пробуйте разные форматы изображений, меняйте `GpuDeviceId` на системах с несколькими GPU или комбинируйте это с другими библиотеками Aspose для генерации PDF. Возможности безграничны, как только GPU включён в работу.

---

<img src="gpu-ocr.png" alt="how to enable gpu with Aspose OCR in C# – convert image to plain text quickly">

*Счастливого кодинга! Если возникнут трудности, оставляйте комментарий ниже или загляните на официальные форумы Aspose для более глубоких разборов.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}