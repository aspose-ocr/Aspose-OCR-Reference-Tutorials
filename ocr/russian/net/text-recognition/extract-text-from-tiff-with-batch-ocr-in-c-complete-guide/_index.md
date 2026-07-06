---
category: general
date: 2026-04-11
description: Извлекайте текст из TIFF‑файлов с помощью пакетной обработки OCR в Aspose
  на C#. Узнайте, как эффективно обрабатывать пакетный OCR и получать обратную связь
  о прогрессе в реальном времени.
draft: false
keywords:
- extract text from tiff
- process batch ocr
- OCR batch processing
- Aspose OCR C#
- TIFF image OCR
language: ru
og_description: Извлекайте текст из файлов TIFF с помощью пакетной обработки OCR Aspose
  в C#. Этот учебник пошагово показывает, как выполнять пакетный OCR и отслеживать
  прогресс.
og_title: Извлечение текста из TIFF с помощью пакетного OCR в C# – Полное руководство
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Извлечение текста из TIFF с помощью пакетного OCR в C# — полное руководство
url: /ru/net/text-recognition/extract-text-from-tiff-with-batch-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из TIFF – Полное руководство по пакетному OCR

Когда‑нибудь вам нужно было **извлечь текст из TIFF** файлов, но вы застряли на этапе пакетной обработки? Вы не одиноки. Во многих проектах автоматизации документов обработка десятков изображений высокого разрешения TIF может быстро стать узким местом — особенно когда требуется мгновенная обратная связь о прогрессе.  

Хорошие новости? С Aspose OCR вы можете **process batch OCR** в несколько строк, получать события прогресса в реальном времени и выводить распознанный текст для каждого изображения. В этом руководстве мы пройдем готовое консольное приложение C#, которое делает именно это.

Мы охватим всё, что вам нужно знать: необходимые пакеты, почему каждая строка важна, граничные случаи, такие как отсутствие файлов, и как проверить результаты. К концу вы сможете добавить пример в своё решение и сразу начать извлекать текст из TIFF‑изображений.

## Что понадобится

- **.NET 6 или новее** (код также компилируется с .NET Core)  
- **Aspose.OCR for .NET** NuGet‑пакет – `Install-Package Aspose.OCR`  
- Папка, содержащая несколько **TIFF**‑изображений, которые вы хотите прочитать (в демо используются `img1.tif`, `img2.tif`, `img3.tif`)  
- Любая IDE — Visual Studio, Rider или VS Code подойдёт  

Дополнительная конфигурация не требуется; библиотека поставляется со своим OCR‑движком, так что вам не придётся устанавливать внешние нативные бинарники.

---

## Шаг 1 – Создание экземпляра OCR Engine  

Первое, что вы делаете, — создаёте `OcrEngine`. Считайте его мозгом, который будет анализировать каждый пиксель и превращать его в символы.

```csharp
using Aspose.OCR;

// Step 1: Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **Почему это важно:**  
> Движок хранит внутренние языковые модели и настройки (например, DPI, язык). Создать его один раз и переиспользовать для пакета гораздо эффективнее, чем инстанцировать новый движок для каждого изображения.

---

## Шаг 2 – Подключение событий прогресса в реальном времени  

Если вы обрабатываете десятки TIFF‑файлов, индикатор прогресса спасёт вас от вопросов, «застрял ли процесс».

```csharp
using Aspose.OCR.Events;

// Step 2: Subscribe to progress updates
ocrEngine.ProgressChanged += Ocr_ProgressChanged;

// Event handler definition (placed later in the file)
```

Событие `ProgressChanged` срабатывает после завершения обработки каждого изображения, предоставляя `Current`, `Total` и `Percentage`. Это **process batch OCR**‑обратная связь, которую большинство разработчиков забывают реализовать.

---

## Шаг 3 – Создание списка потоков изображений  

Aspose.OCR работает с объектами `ImageStream`. Самый простой способ — загрузить каждый TIFF с диска.

```csharp
using Aspose.OCR;
using System.Collections.Generic;

// Step 3: Prepare the batch of TIFF images
List<ImageStream> imageFiles = new List<ImageStream>
{
    ImageStream.FromFile(@"YOUR_DIRECTORY/img1.tif"),
    ImageStream.FromFile(@"YOUR_DIRECTORY/img2.tif"),
    ImageStream.FromFile(@"YOUR_DIRECTORY/img3.tif")
};
```

> **Подсказка:**  
> Если у вас динамическая папка, замените жёстко заданный список на `Directory.GetFiles(path, "*.tif")` и `Select(ImageStream.FromFile)` — так вы действительно **process batch OCR** без ручных обновлений.

---

## Шаг 4 – Запуск пакетного OCR процесса  

Теперь происходит тяжёлая работа. `ProcessBatch` возвращает только‑для‑чтения список объектов `OcrResult`, каждый из которых содержит извлечённый текст и оценки уверенности.

```csharp
// Step 4: Execute batch OCR and collect results
IReadOnlyList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imageFiles);
```

> **Почему это эффективно:**  
> Движок переиспользует одну и ту же языковую модель для всех изображений, резко снижая нагрузку на память по сравнению с вызовами по отдельному изображению.

---

## Шаг 5 – Отображение или сохранение распознанного текста  

Наконец, пройдитесь по результатам. В реальном проекте вы, вероятно, запишете их в базу данных или JSON‑файл, но для этой демонстрации мы просто выведем их в консоль.

```csharp
// Step 5: Output the recognised text for each TIFF
foreach (var result in ocrResults)
{
    Console.WriteLine("=== OCR Result ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();
}
```

**Ожидаемый вывод в консоль** (усечённый для краткости):

```
=== OCR Result ===
Invoice #12345
Date: 03/15/2026
Total: $1,250.00

=== OCR Result ===
Meeting Minutes
1. Project kickoff...
```

Если какое‑либо изображение не удалось обработать, `result.Text` будет пустой строкой, а событие `ProgressChanged` всё равно сообщит, что элемент обработан — так что вы можете отдельно логировать ошибки.

---

## Обработчик события прогресса (полный код)

Разместите этот метод где‑угодно внутри класса `BatchDemo` — предпочтительно после `Main`.

```csharp
private static void Ocr_ProgressChanged(object sender, ProgressChangedEventArgs e)
{
    // Gives you a live view of how many files have been processed
    Console.WriteLine($"Processed {e.Current}/{e.Total} – {e.Percentage}%");
}
```

> **Pro tip:**  
> Перенаправьте этот вывод в индикатор прогресса UI, если вы создаёте настольное приложение; то же событие работает для WinForms, WPF или даже уведомлений ASP.NET Core SignalR.

---

## Полный готовый к запуску пример  

Объединив всё вместе, получаем полную программу, которую можно скопировать‑вставить в новый консольный проект.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Events;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Subscribe to progress events
        ocrEngine.ProgressChanged += Ocr_ProgressChanged;

        // 3️⃣ Load TIFF images into a list
        List<ImageStream> imageFiles = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/img1.tif"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/img2.tif"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/img3.tif")
        };

        // 4️⃣ Run batch OCR
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imageFiles);

        // 5️⃣ Print results
        foreach (var result in ocrResults)
        {
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();
        }
    }

    // Progress event handler
    private static void Ocr_ProgressChanged(object sender, ProgressChangedEventArgs e)
    {
        Console.WriteLine($"Processed {e.Current}/{e.Total} – {e.Percentage}%");
    }
}
```

Сохраните файл как `Program.cs`, выполните `dotnet add package Aspose.OCR`, замените `YOUR_DIRECTORY` реальным путём и нажмите **Ctrl+F5**. Вы увидите номера прогресса, за которыми следует извлечённый текст для каждого TIFF.

---

## Обработка распространённых граничных случаев  

| Ситуация | На что обратить внимание | Быстрое решение |
|-----------|-------------------|-----------|
| **Отсутствующий или повреждённый TIFF** | `ImageStream.FromFile` бросает `FileNotFoundException` или `ArgumentException`. | Оберните создание списка в `try/catch` и пропускайте недействительные файлы, записывая проблему в лог. |
| **Очень большие изображения ( >10 MP )** | OCR может потреблять много ОЗУ и замедляться. | Снизьте DPI перед обработкой: `ocrEngine.ImagePreprocessing.Dpi = 300;` |
| **Текст не на английском** | Модель языка по умолчанию — английская. | Установите `ocrEngine.Language = Language.Spanish;` (или любой поддерживаемый язык). |
| **Необходимо сохранять результаты** | Вывод в консоль не сохраняется. | Запишите `result.Text` в файл `.txt` с помощью `File.WriteAllText`. |

Устранение этих сценариев делает решение надёжным и демонстрирует, что вы продумали работу за пределами «счастливого пути».

## Следующие шаги и связанные темы  

- **Extract text from PDF** – аналогичный API, просто замените `ImageStream` на `PdfDocument`.  
- **Parallel batch OCR** – для огромных нагрузок запустите несколько экземпляров `OcrEngine` в отдельных потоках; не забудьте учитывать ограничения лицензии.  
- **Post‑processing** – пропустите вывод OCR через проверку орфографии или регулярные выражения, чтобы очистить типичные артефакты OCR.  

Все эти расширения всё ещё опираются на основную идею **process batch OCR** и могут добавляться поэтапно.

## Заключение  

Мы только что продемонстрировали, как **извлечь текст из TIFF** файлов эффективно, используя **process batch OCR** с Aspose OCR в C#. Пример создаёт один движок, подписывается на события прогресса, загружает список потоков изображений, запускает пакетную обработку и выводит каждый результат.  

Отсюда вы можете интегрировать вывод в базы данных, генерировать поисковые PDF‑файлы или передавать текст в последующие NLP‑конвейеры. Возможности безграничны — экспериментируйте с настройками языка, параметрами DPI и параллельным выполнением, чтобы подобрать оптимальный вариант под вашу нагрузку.

Есть вопросы или хотите поделиться, как вы кастомизировали пакет? Оставьте комментарий ниже, и счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}