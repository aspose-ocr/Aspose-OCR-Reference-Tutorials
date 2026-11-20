---
category: general
date: 2026-06-03
description: دورة تعليمية للتعرف الضوئي على النصوص في ترجمات الفيديو تُظهر كيفية استخراج
  الإطارات من الفيديو وقراءة النص من ملفات الفيديو مثل MP4 باستخدام Aspose.OCR.
draft: false
keywords:
- video subtitle ocr
- extract frames from video
- read text from video
- extract text from mp4
language: ar
og_description: تعلم تقنية التعرف الضوئي على الأحرف للترجمة المصاحبة للفيديو باستخدام
  Aspose.OCR. استخرج الإطارات من الفيديو، اقرأ النص من الفيديو، واستخرج النص من ملفات
  MP4 في بضع دقائق.
og_title: التعرف الضوئي على الأحرف في ترجمات الفيديو باستخدام C# – دليل خطوة بخطوة
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
title: دليل شامل للتعرف الضوئي على الأحرف في ترجمات الفيديو باستخدام C#
url: /ar/net/text-recognition/video-subtitle-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف الضوئي على الأحرف (OCR) للترجمات في الفيديو باستخدام C# – دليل كامل

هل احتجت يومًا إلى **video subtitle ocr** لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك. سواءً كنت تقوم برقمنة تسجيلات المحاضرات، أو استخراج الترجمات من مقاطع الفيديو التدريبية، أو مجرد فضول حول قراءة النص من الفيديو، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك باستخدام C# و Aspose.OCR.  

في الدقائق القليلة القادمة سنستخرج إطارات من الفيديو، نشغّل OCR على تلك الإطارات، وأخيرًا نعرض نص الترجمة إطارًا بإطار. في النهاية ستتمكن من **read text from video** للملفات—including MP4—دون الحاجة للبحث عن أدوات طرف ثالث.

## ما ستبنيه

سننشئ تطبيقًا صغيرًا من نوع console يقوم بـ:

1. فك تشفير ملف MP4 (أو أي صيغة مدعومة) إلى إطارات `Bitmap` منفصلة.  
2. حصر منطقة OCR على شريط الترجمة حتى لا يتشتت المحرك مع الصورة بالكامل.  
3. معالجة كل إطار باستخدام `VideoOcrProcessor` من Aspose.  
4. طباعة نص الترجمة المعترف به إلى وحدة التحكم.

لا إطالة، مجرد مثال عملي من البداية إلى النهاية يمكنك دمجه في مشروع حقيقي.

## المتطلبات المسبقة

- **.NET 6.0** أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+).  
- **Aspose.OCR for .NET** – تثبيت عبر NuGet: `Install-Package Aspose.OCR`.  
- ملف فيديو (MP4 يعمل بشكل ممتاز).  
- طريقة لفك تشفير إطارات الفيديو – العرض التجريبي يستخدم طريقة placeholder، لكن يمكنك ربط FFmpeg أو OpenCV أو أي مكتبة تُعيد كائنات `Bitmap`.  

> **نصيحة احترافية:** إذا كنت على Windows، حزمة `System.Drawing.Common` تعمل جيدًا مع `Bitmap`. على Linux/macOS ستحتاج إلى تبعية `libgdiplus` الأصلية.

## الخطوة 1 – استخراج إطارات من الفيديو

العقبة الأولى هي تحويل الصورة المتحركة إلى صور ثابتة. الطريقة `GetVideoFrames` أدناه تركت فارغة عمدًا؛ استبدلها بالمفكك المفضل لديك. إليك مخططًا سريعًا باستخدام FFmpeg‑Core (فقط لتوضيح شكل البيانات):

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

> **لماذا هذا مهم:** استخراج الإطارات يوفّر لمحرك OCR صورة ثابتة للعمل عليها، مما يحسّن الدقة بشكل كبير مقارنةً بمحاولة القراءة مباشرةً من تدفق الفيديو.

## الخطوة 2 – إعداد VideoOcrProcessor

الآن بعد أن لدينا تسلسلًا من كائنات `Bitmap`، يمكننا تمريرها إلى Aspose.OCR. يتيح لنا `VideoOcrProcessor` تعريف **منطقة الاهتمام (ROI)** – مثالي للترجمات التي عادةً ما تكون في أعلى أو أسفل الإطار.

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

> **لماذا نحدّ الـ ROI؟** بتجاهل باقي الصورة نقلل الضوضاء، نقلل زمن المعالجة، ونتجنب الإيجابيات الزائفة من الرسومات الخلفية.

## الخطوة 3 – تشغيل OCR على تسلسل الإطارات

مع جاهزية المعالج، إطعام الإطارات يصبح سطرًا واحدًا. طريقة `Process` تُعيد مجموعة من كائنات `OcrResult`، كل منها يحتوي على النص المعترف به للإطار المقابل.

```csharp
IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

// Execute OCR on every extracted frame
IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);
```

> **ما الذي يحدث خلف الكواليس؟** Aspose.OCR يُعيد تطبيع كل bitmap داخليًا، يُشغّل مُعرّفًا قائمًا على الشبكات العصبية، ثم يُجري معالجة لاحقة لتحسين علامات الترقيم وفواصل الأسطر.

## الخطوة 4 – عرض النص المستخرج

أخيرًا، نُكرّر النتائج ونطبع كل سطر ترجمة. يمكنك أيضًا كتابة النتائج إلى ملف SRT، قاعدة بيانات، أو تمريرها إلى خدمة ترجمة.

```csharp
int frameIndex = 0;
foreach (var result in ocrResults)
{
    // result.Text contains the plain‑text subtitle for this frame
    Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
}
```

### مثال كامل يعمل

دمج كل ما سبق ينتج برنامج console مستقل:

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

**الناتج المتوقع (عينة)**  

```
Frame 0: Welcome to the Introduction to Machine Learning.
Frame 1: In this lecture we will cover...
Frame 2: ...
```

إذا واجه OCR صعوبة مع إطار معين، ستظهر سلسلة فارغة – وهذا إشارة لتعديل الـ ROI أو زيادة معدل استخراج الإطارات.

## المشكلات الشائعة وكيفية إصلاحها

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| **حروف غير مفهومة** | إطارات منخفضة الدقة أو ضغط عالي | استخراج الإطارات بمعدل بت أعلى، أو تكبير الـ bitmap قبل OCR (`Bitmap.Clone(new Size(...), ...)`). |
| **عدم إرجاع نص** | الـ ROI لا يغطي شريط الترجمة فعليًا | تحقق من إحداثيات المستطيل (استخدم أداة لقطة شاشة للقياس). |
| **عنق زجاجة الأداء** | معالجة كل إطار بـ 30 fps تُعد مبالغة | خفض العينة إلى 1‑2 fps لمعظم تدفقات الترجمات؛ لا يزال بإمكانك التقاط كل تغيير في الترجمة. |
| **FFmpeg غير موجود** | `ffmpeg.exe` غير موجود في `PATH` | قدّم المسار الكامل في `ProcessStartInfo.FileName` أو ثبّت FFmpeg عالميًا. |

## توسيع الحل

- **تصدير إلى SRT** – دمج الطوابع الزمنية مع نص OCR وكتابة ملف SubRip.  
- **دعم متعدد اللغات** – ضبط `ocrProcessor.Language = OcrLanguage.Spanish` (أو أي لغة مدعومة).  
- **معالجة في الوقت الفعلي** – تمرير الإطارات مباشرةً من تدفق مباشر بدلاً من القراءة من القرص.  

كل هذه الاختلافات لا تزال تدور حول الأفكار الأساسية لـ **extract frames from video**, **read text from video**, و **extract text from mp4**.

## الخلاصة

لقد استعرضنا للتو سير عمل كامل للـ **video subtitle ocr** باستخدام C#. من خلال استخراج إطارات الفيديو، تركيز OCR على شريط الترجمة، وتكرار النتائج، يمكنك بثقة **read text from video** للملفات مثل MP4. الكود جاهز للنسخ واللصق، والتصميم المعياري يتيح لك استبدال أي مُفكك إطارات تفضله.

ما الخطوة التالية؟ جرّب تصدير النتائج إلى ملف SRT، جرب أحجام ROI مختلفة، أو مرّر الترجمات إلى واجهة برمجة تطبيقات ترجمة للحصول على تسميات متعددة اللغات. السماء هي الحد عندما تتقن أساسيات استخراج النص من الفيديو.

برمجة سعيدة، ولتظل ترجماتك دائمًا واضحة كالكريستال!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}