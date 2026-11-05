---
category: general
date: 2026-06-03
description: Учебник по OCR субтитров видео, показывающий, как извлекать кадры из
  видео и считывать текст из видеофайлов, таких как MP4, с помощью Aspose.OCR.
draft: false
keywords:
- video subtitle ocr
- extract frames from video
- read text from video
- extract text from mp4
language: ru
og_description: Изучите OCR субтитров видео с Aspose.OCR. Извлекайте кадры из видео,
  считывайте текст из видео и извлекайте текст из MP4 за несколько минут.
og_title: Оптическое распознавание субтитров видео на C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  headline: Video Subtitle OCR in C# – Complete Guide
  type: TechArticle
- description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  name: Video Subtitle OCR in C# – Complete Guide
  steps:
  - name: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
    text: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
  - name: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
    text: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
  - name: Processes each frame with Aspose’s `VideoOcrProcessor`.
    text: Processes each frame with Aspose’s `VideoOcrProcessor`.
  - name: Prints the recognized subtitle text to the console.
    text: Prints the recognized subtitle text to the console.
  type: HowTo
tags:
- C#
- Aspose.OCR
- video-processing
title: OCR субтитров видео на C# – Полное руководство
url: /ru/net/text-recognition/video-subtitle-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR субтитров видео на C# – Полное руководство

Когда‑нибудь вам нужен был **video subtitle ocr**, но вы не знали, с чего начать? Вы не одиноки. Независимо от того, оцифровываете ли вы записи лекций, извлекаете субтитры из обучающих видео или просто хотите узнать, как читать текст из видео, этот учебник покажет вам, как сделать это с помощью C# и Aspose.OCR.  

В течение нескольких минут мы извлечём кадры из видео, запустим OCR на этих кадрах и в конце отобразим текст субтитров кадр за кадром. К концу вы сможете **читать текст из видео** файлы — включая MP4 — без поиска сторонних инструментов.

## Что вы создадите

1. Декодирует MP4 (или любой поддерживаемый формат) в отдельные кадры `Bitmap`.  
2. Ограничивает область OCR до полосы субтитров, чтобы движок не отвлекался на всё изображение.  
3. Обрабатывает каждый кадр с помощью `VideoOcrProcessor` от Aspose.  
4. Выводит распознанный текст субтитров в консоль.

Без лишних деталей, только рабочий сквозной пример, который вы можете добавить в реальный проект.

## Предварительные требования

- **.NET 6.0** или новее (код также работает на .NET Framework 4.7+).  
- **Aspose.OCR for .NET** – установить через NuGet: `Install-Package Aspose.OCR`.  
- Видео файл (MP4 отлично подходит).  
- Средство для декодирования видеокадров — в демо используется заглушка, но вы можете подключить FFmpeg, OpenCV или любую библиотеку, возвращающую объекты `Bitmap`.  

> Совет: Если вы работаете в Windows, пакет `System.Drawing.Common` отлично подходит для `Bitmap`. На Linux/macOS понадобится нативная зависимость `libgdiplus`.

## Шаг 1 – Извлечение кадров из видео

Первая преграда — превратить движущееся изображение в отдельные статические кадры. Метод `GetVideoFrames` ниже намеренно оставлен пустым; замените его своим любимым декодером. Ниже быстрый набросок с использованием FFmpeg‑Core (только для иллюстрации структуры данных):

```csharp
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

/// <summary>
/// Extracts every frame from the supplied video file and yields it as a Bitmap.
/// You can swap this implementation for OpenCV, MediaToolkit, etc.
/// </summary>
static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
{
    // Create a temporary folder for the extracted PNGs
    string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
    Directory.CreateDirectory(tempDir);

    // FFmpeg command: -i input -vf fps=1 output_%04d.png (1 fps for demo)
    var startInfo = new ProcessStartInfo
    {
        FileName = "ffmpeg",
        Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
        RedirectStandardOutput = true,
        UseShellExecute = false,
        CreateNoWindow = true
    };
    Process ffmpeg = Process.Start(startInfo);
    ffmpeg.WaitForExit();

    foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
    {
        using var bmp = new Bitmap(file);
        // Clone the bitmap so the file can be deleted later
        yield return new Bitmap(bmp);
    }

    // Clean up
    Directory.Delete(tempDir, true);
}
```

> **Почему это важно:** Извлечение кадров предоставляет OCR‑движку статическое изображение для обработки, что значительно повышает точность по сравнению с попыткой читать напрямую из видеопотока.

## Шаг 2 – Настройка VideoOcrProcessor

Теперь, когда у нас есть последовательность объектов `Bitmap`, мы можем передать их Aspose.OCR. `VideoOcrProcessor` позволяет задать **Region of Interest (ROI)** — идеально подходит для субтитров, которые обычно находятся в верхней или нижней части кадра.

```csharp
using Aspose.OCR.Video;
using System.Drawing;

// Create the processor and focus on the top 200 pixels (typical subtitle band)
var ocrProcessor = new VideoOcrProcessor
{
    // ROI = new Rectangle(x, y, width, height)
    Roi = new Rectangle(0, 0, 1920, 200)   // adjust width/height to your video resolution
};
```

> **Зачем ограничивать ROI?** Игнорируя остальную часть изображения, мы уменьшаем шум, сокращаем время обработки и избегаем ложных срабатываний от фоновой графики.

## Шаг 3 – Запуск OCR на последовательности кадров

Когда процессор готов, передача кадров сводится к одной строке кода. Метод `Process` возвращает перечисление объектов `OcrResult`, каждый из которых содержит распознанный текст для соответствующего кадра.

```csharp
IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

// Execute OCR on every extracted frame
IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);
```

> **Что происходит под капотом?** Aspose.OCR внутренне нормализует каждый bitmap, запускает распознаватель на основе нейронной сети и затем постобрабатывает результат, улучшая пунктуацию и разрывы строк.

## Шаг 4 – Отображение извлечённого текста

Наконец, мы проходим по результатам и выводим каждую строку субтитров. Вы также можете записать их в файл SRT, базу данных или передать в сервис перевода.

```csharp
int frameIndex = 0;
foreach (var result in ocrResults)
{
    // result.Text contains the plain‑text subtitle for this frame
    Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
}
```

### Полный рабочий пример

Объединив всё вместе, получаем автономную консольную программу:

```csharp
using Aspose.OCR.Video;
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

class VideoSubtitleOcrDemo
{
    static void Main()
    {
        // 1️⃣ Extract frames from the MP4 (replace with your own decoder)
        IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

        // 2️⃣ Configure OCR – focus on the subtitle band
        var ocrProcessor = new VideoOcrProcessor
        {
            Roi = new Rectangle(0, 0, 1920, 200) // tweak for your video size
        };

        // 3️⃣ Run OCR across all frames
        IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);

        // 4️⃣ Output the recognized subtitle text
        int frameIndex = 0;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
        }
    }

    // --------------------------------------------------------------------
    // Helper: extract one‑frame‑per‑second PNGs using FFmpeg.
    // Replace this with any library that can return Bitmap objects.
    // --------------------------------------------------------------------
    static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
    {
        string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
        Directory.CreateDirectory(tempDir);

        var startInfo = new ProcessStartInfo
        {
            FileName = "ffmpeg",
            Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
            RedirectStandardOutput = true,
            UseShellExecute = false,
            CreateNoWindow = true
        };
        using var ffmpeg = Process.Start(startInfo);
        ffmpeg.WaitForExit();

        foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
        {
            using var bmp = new Bitmap(file);
            yield return new Bitmap(bmp);
        }

        Directory.Delete(tempDir, true);
    }
}
```

**Ожидаемый вывод (пример)**  

```
Frame 0: Welcome to the Introduction to Machine Learning.
Frame 1: In this lecture we will cover...
Frame 2: ...
```

Если OCR будет затрудняться с определённым кадром, вы увидите пустую строку — это сигнал скорректировать ROI или увеличить частоту извлечения кадров.

## Распространённые проблемы и способы их решения

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Непонятные символы** | Кадры низкого разрешения или сильное сжатие | Извлекайте кадры с более высоким битрейтом или увеличьте размер bitmap перед OCR (`Bitmap.Clone(new Size(...), ...)`). |
| **Текст не возвращается** | ROI не покрывает полосу субтитров | Проверьте координаты прямоугольника (используйте инструмент скриншотов для измерения). |
| **Узкое место в производительности** | Обработка каждого кадра при 30 fps избыточна | Снизьте частоту до 1‑2 fps для большинства потоков субтитров; вы всё равно сможете захватить каждое изменение субтитров. |
| **FFmpeg не найден** | `ffmpeg.exe` не находится в `PATH` | Укажите полный путь в `ProcessStartInfo.FileName` или установите FFmpeg глобально. |

## Расширение решения

- **Export to SRT** – объединить метки времени с текстом OCR и записать файл SubRip.  
- **Multi‑language support** – установить `ocrProcessor.Language = OcrLanguage.Spanish` (или любой поддерживаемый язык).  
- **Real‑time processing** – передавать кадры напрямую из живого потока вместо чтения с диска.  

Все эти варианты по‑прежнему основываются на основных идеях **extract frames from video**, **read text from video**, и **extract text from mp4**.

## Заключение

Мы только что прошли полный рабочий процесс **video subtitle ocr** на C#. Извлекая кадры из видео, фокусируя OCR на полосе субтитров и проходя по результатам, вы можете надёжно **read text from video** файлы, такие как MP4. Код готов к копированию и вставке, а модульный дизайн позволяет заменить любой декодер кадров по вашему выбору.

Следующие шаги? Попробуйте экспортировать результаты в файл SRT, поэкспериментировать с разными размерами ROI или передать субтитры в API перевода для многократных языков. Возможности безграничны, как только вы освоите основы извлечения текста из видео.

Удачной разработки, и пусть ваши субтитры всегда будут кристально чистыми!

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Извлечение текста из изображения C# с выбором языка с использованием Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Извлечение текста из изображения с помощью Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Извлечение текста из изображения – оптимизация OCR с Aspose.OCR для .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}