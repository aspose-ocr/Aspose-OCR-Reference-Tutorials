---
category: general
date: 2026-03-21
description: Узнайте, как исправлять наклон изображений и распознавать текст на них
  с помощью Aspose OCR. Конвертируйте JPG в текст и корректируйте вращение изображения
  всего в несколько строк кода C#.
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: ru
og_description: Как исправить наклон изображения и извлечь текст из JPEG с помощью
  Aspose OCR. Следуйте этому пошаговому руководству, чтобы преобразовать JPG в текст
  и скорректировать вращение изображения.
og_title: Как выровнять изображение в C# – Быстрый учебник по Aspose OCR
tags:
- OCR
- C#
- Aspose
title: Как выпрямить изображение в C# – Полное руководство по использованию Aspose
  OCR
url: /ru/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как исправить наклон изображения в C# – Полное руководство с использованием Aspose OCR

Когда‑нибудь задумывались **как исправить наклон изображения** файлов, полученных со сканера под странным углом? Вы не одиноки — многие разработчики сталкиваются с этой проблемой, когда пытаются извлечь текст из чеков, счетов или рукописных заметок. Хорошая новость в том, что с Aspose OCR вы можете скорректировать вращение изображения и получить чистый, индексируемый текст всего в несколько строк.

В этом руководстве мы пройдем весь процесс: от установки библиотеки, включения автоматического исправления наклона, до распознавания текста на изображении и, наконец, преобразования JPG в текст. К концу вы получите готовое к запуску консольное приложение, которое **распознает текст в jpg** файлах без предварительного ручного вращения.

## Что понадобится

- **.NET 6.0** или новее (код работает как на .NET Core, так и на .NET Framework)  
- **Aspose.OCR for .NET** пакет NuGet — рекомендуется версия 23.12 или новее  
- Пример **искаженного JPEG** (например, `skewed_receipt.jpg`), размещенный в месте, доступном вашему приложению  
- Visual Studio, VS Code или любой предпочитаемый вами редактор C#  

Никакие другие сторонние инструменты не требуются. Библиотека самостоятельно обрабатывает исправление наклона, OCR и даже определение языка.

![пример исправления наклона изображения](/images/deskew-example.png "как исправить наклон изображения с помощью Aspose OCR")

## Шаг 1: Настройка проекта и установка Aspose.OCR

Чтобы всё было аккуратно, создайте новый консольный проект:

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

Команда `dotnet add package` загружает бинарники **Aspose.OCR** и все нативные зависимости. Если вы работаете в Windows, нативные DLL будут получены автоматически; в Linux/macOS может потребоваться пакет `libgdiplus`, но это одноразовая установка.

## Шаг 2: Включение автоматического исправления наклона (корректировка вращения изображения)

Откройте `Program.cs` и замените его содержимое кодом ниже. Ключевая строка здесь — `ocrEngine.Settings.Deskew = true;` — это флаг, который сообщает движку **как исправить наклон изображения** автоматически.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Почему включать исправление наклона?

Когда сканер подаёт страницу под углом, базовая линия текста наклонена. Традиционные OCR‑движки будут считывать каждый символ как наклоненную версию, что резко снижает точность. Установив `Deskew = true`, Aspose OCR запускает быстрый Hough‑transform «под капотом», поворачивает bitmap обратно в горизонтальное положение и затем выполняет распознавание. Результат такой же, как если бы вы вручную повернули изображение в Photoshop — только быстрее и полностью автоматизировано.

## Шаг 3: Распознавание текста на изображении и преобразование JPG в текст

Вызов `Recognize` делает сразу две вещи:

1. **Исправляет наклон** изображения (поскольку флаг включён).  
2. **Извлекает** текстовое содержимое, возвращая его в объекте `OcrResult`.

Вы можете использовать `ocrResult.Text` как обычную строку, записать её в файл или передать в последующие конвейеры обработки. Если нужны необработанные оценки уверенности для каждого слова, `ocrResult.Words` предоставляет коллекцию с полями `Confidence`.

### Пример вывода

Предположим, что `skewed_receipt.jpg` содержит простой чек, вы можете увидеть что‑то вроде:

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

Обратите внимание, как цифры выровнены, несмотря на то, что исходное изображение было повернуто примерно на 7°. Это магия **корректного вращения изображения**, встроенного в библиотеку.

## Шаг 4: Запуск примера и проверка результатов

Скомпилируйте и запустите:

```bash
dotnet run
```

Если всё настроено правильно, вы увидите извлечённый текст, выведенный в консоль. Если возникнет исключение вроде `FileNotFoundException`, проверьте путь к вашему JPEG и убедитесь, что файл доступен для чтения.

### Распространённые подводные камни и профессиональные советы

- **Большие изображения** — потребление памяти OCR растёт с размерами изображения. Перед подачей в движок уменьшите слишком большие файлы (например, ширина > 3000 px).  
- **Нелатинские скрипты** — по умолчанию движок предполагает английский язык. Установите `ocrEngine.Settings.Language = OcrLanguage.French;` (или любой поддерживаемый язык), если вам нужно **распознавать текст на изображении** в других алфавитах.  
- **Пакетная обработка** — для большого количества файлов переиспользуйте один экземпляр `OcrEngine`; создание нового движка для каждого файла создаёт лишние накладные расходы.  
- **Проверка качества** — после исправления наклона вы можете экспортировать скорректированный bitmap через `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");`, чтобы визуально убедиться в исправлении вращения.

## Полный рабочий пример (все вместе)

Ниже приведена полная, автономная программа, которую можно скопировать и вставить в `Program.cs`. Она включает комментарии, обработку ошибок и необязательный шаг сохранения исправленного изображения.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

Запуск программы позволит **распознавать текст в jpg** файлах, автоматически исправлять любой наклон и выводить чистый, индексируемый текст в консоль.

## Подведение итогов

Теперь у вас есть надёжный, готовый к продакшну фрагмент кода, демонстрирующий **как исправить наклон изображения** файлов и извлечь их содержимое с помощью Aspose OCR. Этот подход работает с чеками, счетами, отсканированными контрактами или любыми JPEG, где текст не идеально горизонтален.

Следующие шаги, которые вы можете изучить:

- **Пакетная обработка** папки JPEG и запись каждого результата в файл `.txt` (связанно с *преобразованием jpg в текст*).  
- Интеграция шага OCR в API ASP.NET Core, чтобы клиенты могли загружать изображения и получать текст в формате JSON.  
- Эксперименты с различными настройками OCR, такими как `ocrEngine.Settings.Language` или `ocrEngine.Settings.RecognitionMode`, для повышения точности при работе с документами не на английском языке.

Попробуйте, настройте параметры и позвольте движку выполнить тяжёлую работу. Как всегда, если столкнётесь с проблемой или хотите поделиться умной оптимизацией, оставьте комментарий ниже. Счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}