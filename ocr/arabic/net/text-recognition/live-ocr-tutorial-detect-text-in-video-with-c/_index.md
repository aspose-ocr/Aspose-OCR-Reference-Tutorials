---
category: general
date: 2026-03-13
description: يُظهر البرنامج التعليمي المباشر لتقنية OCR كيفية ضبط لغة OCR واكتشاف
  النص في تدفقات الفيديو في الوقت الحقيقي باستخدام Aspose.OCR. اتبع الدليل خطوة بخطوة.
draft: false
keywords:
- live ocr tutorial
- set OCR language
- detect text video
- Aspose OCR live processing
- real‑time text detection
language: ar
og_description: يوضح برنامج تعليمي مباشر لتقنية OCR كيفية ضبط لغة OCR واكتشاف نص الفيديو
  باستخدام Aspose.OCR Live في C#. يتضمن الكود الكامل.
og_title: 'دورة OCR مباشرة: الكشف عن النص في الوقت الحقيقي في الفيديو'
tags:
- OCR
- C#
- Aspose
- Video Processing
title: 'دورة OCR مباشرة: اكتشاف النص في الفيديو باستخدام C#'
url: /ar/net/text-recognition/live-ocr-tutorial-detect-text-in-video-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل OCR الحي: اكتشاف النص في الفيديو باستخدام C#

هل احتجت يومًا إلى **دليل OCR حي** يعمل فعليًا على تدفق الفيديو؟ ربما تكون تبني تطبيق كاميرا ذكي أو طبقة ترجمة في الوقت الحقيقي وتواجه صعوبة في “كيف أحصل على النص من كل إطار؟”. الخبر السار هو أنك لست بحاجة إلى إعادة اختراع العجلة. في هذا الدليل سنستعرض مثالًا كاملًا قابلًا للتنفيذ ي **يضبط لغة OCR**، يلتقط إطارات من الكاميرا، و **يكشف عن نص الفيديو** مباشرة.

سنستخدم فئة `LiveOcr` من Aspose.OCR، والتي صُممت خصيصًا لسيناريوهات ذات زمن استجابة منخفض. بنهاية هذه المقالة ستحصل على تطبيق console يطبع أول قطعة نص يراها ثم يتوقف — مثالي كنقطة انطلاق لأنابيب أكثر تعقيدًا.

## المتطلبات المسبقة

- .NET 6.0 SDK (أو أي إصدار .NET حديث)  
- Visual Studio 2022 أو VS Code (بيئتك المتكاملة المفضلة)  
- حزمة NuGet `Aspose.OCR` (تثبيت عبر `dotnet add package Aspose.OCR`)  
- كاميرا ويب أو أي مصدر فيديو يمكنه توفير إطارات `Bitmap`  

لا توجد مكتبات أصلية إضافية مطلوبة؛ Aspose.OCR يأتي مع كل ما تحتاجه.

## الخطوة 1: تثبيت Aspose.OCR وإضافة المساحات الاسمية

قبل كتابة أي كود، تأكد من الإشارة إلى مكتبة Aspose OCR. افتح طرفية في مجلد المشروع وشغّل:

```bash
dotnet add package Aspose.OCR
```

بعد ذلك، في أعلى ملف `Program.cs`، استورد المساحات الاسمية التي سنستخدمها:

```csharp
using Aspose.OCR;
using Aspose.OCR.Live;
using System.Drawing;
using System.Threading;
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، سيقترح IDE عبارات `using` تلقائيًا بعد كتابة أسماء الفئات.

## الخطوة 2: إنشاء وتكوين كائن LiveOcr

جوهر الدليل هو كائن `LiveOcr`. نحتاج إلى إبلاغه بأي لغة يبحث عنها وإمكانية تطبيق مرشحات ما قبل المعالجة (مثل تصحيح الميل) لتحسين الدقة.

```csharp
// Step 2: Initialize LiveOcr with English language and a deskew filter
LiveOcr liveOcr = new LiveOcr
{
    // This is where we **set OCR language** to English.
    Language = Language.English,

    // Pre‑processing helps when the camera isn’t perfectly aligned.
    PreProcessingFilters = new FilterPipeline { new DeskewFilter() }
};
```

لماذا نضبط اللغة؟ محركات OCR تستخدم قواميس ونماذج حروف مخصصة للغة؛ تحديد الإنجليزية يقلل الإيجابيات الكاذبة ويسرّع التعرف. إذا كنت تحتاج لغة أخرى، استبدل `Language.English` بـ `Language.Spanish` أو `Language.French`، إلخ.

## الخطوة 3: التقاط إطارات من الكاميرا الخاصة بك

في مشروع حقيقي ستستبدل طريقة العنصر النائب `CaptureFrameFromCamera()` بمنطق الالتقاط الفعلي — ربما باستخدام `AForge.Video` أو `OpenCvSharp` أو واجهة برمجة تطبيقات Windows Media Capture. من أجل هذا الدليل سنبقي الطريقة مجردة، لكن سنعرض مثالًا سريعًا باستخدام `AForge`.

```csharp
// Simple wrapper that returns a Bitmap from the default webcam.
// You can replace this with any library that gives you a Bitmap.
static Bitmap CaptureFrameFromCamera()
{
    // NOTE: This is a minimal example. In production you should
    // manage the video source lifecycle and dispose objects properly.
    var videoSource = new AForge.Video.DirectShow.VideoCaptureDevice(
        new AForge.Video.DirectShow.FilterInfoCollection(
            AForge.Video.DirectShow.FilterCategory.VideoInputDevice)[0].MonikerString);

    Bitmap frame = null;
    var waitHandle = new AutoResetEvent(false);

    videoSource.NewFrame += (sender, eventArgs) =>
    {
        frame = (Bitmap)eventArgs.Frame.Clone();
        waitHandle.Set(); // signal that we have a frame
    };

    videoSource.Start();
    waitHandle.WaitOne(1000); // wait up to 1 second for a frame
    videoSource.SignalToStop();
    videoSource.WaitForStop();

    return frame;
}
```

> **حالة حدية:** إذا لم تكن الكاميرا متاحة، فإن `CaptureFrameFromCamera` سيعيد `null`. احرص دائمًا على الحماية من ذلك في كود الإنتاج.

## الخطوة 4: معالجة كل إطار حتى يتم العثور على نص

الآن نقوم بالتكرار على عدد ثابت من الإطارات (أو إلى ما لا نهاية) ونمرر كل bitmap إلى `LiveOcr.ProcessFrame`. بمجرد حصولنا على سلسلة غير فارغة، نطبعها ونخرج من الحلقة.

```csharp
// Step 4: Scan up to 100 frames or until text appears
for (int frameIndex = 0; frameIndex < 100; frameIndex++)
{
    Bitmap cameraFrame = CaptureFrameFromCamera();

    // Guard against a failed capture
    if (cameraFrame == null)
    {
        Console.WriteLine("Failed to capture a frame. Retrying...");
        Thread.Sleep(100);
        continue;
    }

    // Run OCR on the current frame
    string recognizedText = liveOcr.ProcessFrame(cameraFrame);

    // If we detected something, show it and stop
    if (!string.IsNullOrEmpty(recognizedText))
    {
        Console.WriteLine($"Detected text: {recognizedText}");
        break;
    }

    // Small pause to avoid hammering the CPU
    Thread.Sleep(30);
}
```

### لماذا التوقف؟

`Thread.Sleep(30)` يمنح برنامج تشغيل الكاميرا استراحة ويقلل من استهلاك المعالج. في سيناريوهات الأداء العالي قد تستبدله بمتحكم معدل إطارات أكثر تعقيدًا.

## الخطوة 5: تجميع كل شيء في تطبيق Console

بتجميع كل ذلك، إليك البرنامج الكامل الجاهز للنسخ واللصق. احفظه كـ `Program.cs` داخل مشروع console جديد (`dotnet new console`) وشغّل `dotnet run`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Live;
using System;
using System.Drawing;
using System.Threading;

// Optional: using AForge for demo capture (install AForge.Video via NuGet)
// using AForge.Video.DirectShow;

class Program
{
    static void Main()
    {
        // Initialize LiveOcr – **set OCR language** to English
        LiveOcr liveOcr = new LiveOcr
        {
            Language = Language.English,
            PreProcessingFilters = new FilterPipeline { new DeskewFilter() }
        };

        Console.WriteLine("Starting live OCR… Press Ctrl+C to abort.");

        // Loop through frames – **detect text video** in real time
        for (int i = 0; i < 100; i++)
        {
            Bitmap frame = CaptureFrameFromCamera();

            if (frame == null)
            {
                Console.WriteLine("No frame captured, retrying...");
                Thread.Sleep(100);
                continue;
            }

            string text = liveOcr.ProcessFrame(frame);

            if (!string.IsNullOrEmpty(text))
            {
                Console.WriteLine($"Detected text: {text}");
                break; // stop after first successful detection
            }

            Thread.Sleep(30); // throttle loop
        }

        Console.WriteLine("Live OCR session ended.");
    }

    // -----------------------------------------------------------------
    // Replace this stub with your own capture logic.
    // -----------------------------------------------------------------
    static Bitmap CaptureFrameFromCamera()
    {
        // Placeholder implementation – returns a solid‑color bitmap.
        // In a real app you would pull frames from a webcam or video file.
        Bitmap dummy = new Bitmap(640, 480);
        using (Graphics g = Graphics.FromImage(dummy))
        {
            g.Clear(Color.Black);
            g.DrawString(DateTime.Now.ToString("hh:mm:ss"), 
                new Font("Arial", 24), Brushes.White, new PointF(10, 10));
        }
        return dummy;
    }
}
```

### النتيجة المتوقعة

عندما ترى الكاميرا نصًا إنجليزيًا مقروءًا (مثلاً، ملصق مطبوع)، ستظهر لك نتيجة مشابهة لـ:

```
Starting live OCR… Press Ctrl+C to abort.
Detected text: OpenAI
Live OCR session ended.
```

إذا لم يكن هناك شيء في المشهد، ستنتهي الحلقة بعد 100 تكرار وتطبع “Live OCR session ended.” يمكنك زيادة عدد التكرارات أو استبدال حلقة `for` بـ `while (true)` للمراقبة المستمرة.

## أسئلة شائعة ومشكلات محتملة

| Question | Answer |
|----------|--------|
| **هل يمكنني معالجة لغات متعددة في وقت واحد؟** | نعم. اضبط `Language = Language.English | Language.Spanish;` (عملية OR البتية) لتمكين قاموس متعدد اللغات. |
| **ماذا لو كانت إطاراتي كبيرة ويبدو OCR بطيئًا؟** | قلل حجم الـ bitmap قبل استدعاء `ProcessFrame`. مثال: `Bitmap small = new Bitmap(frame, new Size(320, 240));` |
| **هل أحتاج إلى ترخيص لـ Aspose.OCR؟** | ترخيص تجريبي مؤقت يعمل لمدة تصل إلى 30 يومًا. للإنتاج، اشترِ ترخيصًا لإزالة العلامة المائية. |
| **كيف أتعامل مع النص المدور؟** | `DeskewFilter` يصحح بالفعل الدورانات البسيطة. للزوايا الشديدة، أضف `RotateFilter` إلى خط الأنابيب. |
| **هل هذا النهج آمن للخطوط المتعددة؟** | كائنات `LiveOcr` ليست آمنة للخطوط المتعددة. أنشئ واحدة لكل خط أو احمِ الوصول باستخدام قفل. |

## توسيع الدليل

الآن بعد أن لديك أساس **دليل OCR حي**، فكر في الخطوات التالية:

1. **Stream to a UI** – عرض الفيديو الحي مع نتائج OCR المدمجة باستخدام `Windows Forms` أو `WPF`.  
2. **Batch processing** – تمرير الإطارات إلى طابور وتشغيل OCR على مجموعة من العمال الخلفيين لزيادة الإنتاجية.  
3. **Language detection** – دمج مكتبة لتحديد اللغة لتبديل `LiveOcr.Language` في الوقت الفعلي.  
4. **Persist results** – كتابة السلاسل المكتشفة إلى قاعدة بيانات أو ملف CSV للتحليلات.  

كل من هذه الإضافات لا يزال يعتمد على المفاهيم الأساسية التي غطيناها: تهيئة `LiveOcr`، **ضبط لغة OCR**، و **اكتشاف إطارات نص الفيديو** في الوقت الحقيقي.

### ملخص سريع

- ثبت Aspose.OCR عبر NuGet.  
- أنشئ كائن `LiveOcr`، **ضبط لغة OCR** (الإنجليزية في المثال).  
- التقط إطارات `Bitmap` من الكاميرا.  
- تكرّر عبر الإطارات، استدعِ `ProcessFrame`، وتوقف عندما يظهر النص.  
- البرنامج الكامل أعلاه جاهز للتنفيذ ويشكل قاعدة صلبة لأي مشروع كشف نص في الوقت الحقيقي.

جرّبه، عدّل خط أنابيب ما قبل المعالجة، وشاهد تطبيقك يبدأ بقراءة العالم إطارًا تلو الآخر. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}