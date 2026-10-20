---
category: general
date: 2026-02-09
description: كيفية استخدام Aspose OCR مع تسريع GPU في C#. تعلم التعرف على النص من
  ملفات JPG، استخراج النص من الصورة، وتمكين GPU في دقائق قليلة.
draft: false
keywords:
- how to use aspose
- recognize text from jpg
- extract text from image
- how to enable gpu
- how to set gpu
language: ar
og_description: كيفية استخدام Aspose OCR مع وحدة معالجة الرسومات (GPU) في C#. يوضح
  هذا الدليل كيفية التعرف على النص من ملف JPG واستخراج النص من الصورة باستخدام تسريع
  GPU.
og_title: كيفية استخدام Aspose OCR مع وحدة معالجة الرسومات – دليل برمجي كامل
tags:
- Aspose
- OCR
- C#
- GPU Acceleration
title: كيفية استخدام Aspose OCR مع وحدة معالجة الرسومات – دليل خطوة بخطوة
url: /ar/net/ocr-optimization/how-to-use-aspose-ocr-with-gpu-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام Aspose OCR مع GPU – دليل برمجة كامل

هل احتجت يوماً إلى معالجة مجموعة من الفواتير الممسوحة ضوئياً بسرعة، لكن المعالج كان يعرقل العملية؟ هذه مشكلة شائعة عندما تحاول **how to use aspose** للتعرف الضوئي على الأحرف (OCR) على نطاق واسع. في هذا الدرس سنرشدك عبر مثال واقعي يُظهر **how to use aspose** للتعرف على النص من ملفات jpg، استخراج النص من الصورة، والاستفادة القصوى من وحدة معالجة الرسومات الخاصة بك.

فكر في الأمر كدليل سريع أثناء فنجان القهوة—بدون إطالة، فقط الأجزاء التي يمكنك نسخ‑لصقها في Visual Studio ومشاهدة السحر يحدث. في النهاية ستحصل على تطبيق C# Console مستقل يعمل على أي جهاز Windows حديث مزود بوحدة معالجة رسومات NVIDIA أو AMD.

![كيفية استخدام Aspose OCR مع GPU](/images/aspose-gpu-example.png)

## ما ستحتاجه

- **.NET 6.0** (أو أحدث) – الشيفرة تستهدف .NET 6 لكنها تعمل مع .NET 5 و .NET Framework 4.8 مع بعض التعديلات البسيطة.
- حزمة **Aspose.OCR for .NET** عبر NuGet – قم بتثبيتها باستخدام `dotnet add package Aspose.OCR`.
- جهاز **يدعم GPU** – يوضح الدرس كيفية **how to enable gpu** و **how to set gpu** لحدود الذاكرة، لكن الشيفرة ستعود تلقائياً إلى المعالج إذا لم يتم العثور على GPU متوافق.
- صورة مثل `invoice_01.jpg` موجودة في مجلد يمكنك الإشارة إليه.

هل لديك كل ذلك؟ رائع، لنبدأ.

## كيفية استخدام Aspose OCR مع GPU – الإعداد الأولي

أول شيء عليك فعله هو إنشاء نسخة من محرك OCR وإخبارها باستخدام الـ GPU. هذه الخطوة حاسمة لأنه بدون العلامة، سيستخدم Aspose المعالج الافتراضي، مما يُفقدنا الفائدة من تحسين الأداء.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 1: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Enable GPU acceleration – this is the core of **how to use aspose** with a graphics card
ocrEngine.Configuration.UseGpu = true;

// Optional: limit GPU memory to avoid OOM on low‑end cards
ocrEngine.Configuration.GpuMemoryLimit = 1024; // in MB
```

**لماذا هذا مهم:** تفعيل الـ GPU ينقل نوى معالجة الصور الثقيلة إلى المعالج الرسومي، والذي يمكن أن يكون أسرع 10‑20× من المعالج للصور الكبيرة. `GpuMemoryLimit` هو صمام أمان؛ ضبطه على 1024 ميغابايت يعمل مع معظم البطاقات المتوسطة مع الحفاظ على استجابة التطبيق.

> **نصيحة احترافية:** إذا شغلت التطبيق على جهاز لا يحتوي على GPU متوافق، سيعود Aspose تلقائياً إلى وضع المعالج ويسجل تحذيراً. لا يحدث تعطل، فقط تشغيل أبطأ.

## التعرف على النص من JPG – تحميل الصورة

الآن بعد أن أصبح المحرك جاهزاً، نحتاج إلى إمداده بصورة. يستخدم المثال JPEG لأن **recognize text from jpg** هو سيناريو شائع للفواتير، الإيصالات، وجوازات السفر.

```csharp
// Step 2: Load the JPEG image you want to process
// Replace the path with the location of your own image
var inputImage = ImageStream.FromFile(@"C:\OCR\Samples\invoice_01.jpg");

// Verify that the file exists (helps avoid a FileNotFoundException)
if (!System.IO.File.Exists(@"C:\OCR\Samples\invoice_01.jpg"))
{
    Console.WriteLine("Image file not found. Check the path and try again.");
    return;
}
```

**لماذا نتحقق من الملف:** الملف المفقود هو أكثر الأسباب شيوعاً لأخطاء وقت التشغيل في العروض السريعة. بمعالجته مبكراً، تجعل الدرس صديقاً للمبتدئين.

## استخراج النص من الصورة – تشغيل محرك OCR

مع الصورة في المتناول، الخطوة التالية هي تشغيل عملية OCR فعلياً. هنا يقوم Aspose بالعمل الشاق ويعيد كائن `OcrResult` يحتوي على النص الصافي، درجات الثقة، وحتى إطارات الحدود إذا احتجت إليها لاحقاً.

```csharp
// Step 3: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(inputImage);

// Step 4: Output the extracted plain‑text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrResult.PlainText);
```

**ما ستراه:** يطبع الـ console الأحرف الخام التي اكتشفها Aspose. لفاتورة نظيفة، قد تحصل على شيء مثل:

```
=== Extracted Text ===
Invoice #: 2023‑00123
Date: 02/08/2023
Total: $1,245.67
...
```

إذا كان الإخراج مشوّشاً، ربما تحتاج إلى ضبط جودة الصورة أو تفعيل خيارات ما قبل المعالجة الإضافية (مثل تصحيح الميل، التحويل إلى ثنائي). هذه الأمور خارج نطاق هذا الدليل السريع لكنها موثقة في مرجع API الخاص بـ Aspose.

## كيفية تمكين GPU – تكوين المحرك

قد تتساءل **how to enable gpu** لـ Aspose إذا فاتتك الخطوة الأولى. الجواب ببساطة هو تفعيل علم `UseGpu` في كائن تكوين المحرك، كما هو موضح سابقاً. إليك مقتطف مختصر يمكنك وضعه في أي مشروع موجود:

```csharp
ocrEngine.Configuration.UseGpu = true;   // Enables GPU
```

خلف الكواليس، يقوم Aspose بتحميل مكتبات CUDA/OpenCL الأصلية التي تتطابق مع عتادك. إذا لم يتمكن وقت التشغيل من العثور عليها، يسجل تحذيراً ويعود إلى المعالج. لا توجد خطوات تثبيت إضافية مطلوبة لمعظم إعدادات Windows.

## كيفية ضبط GPU – تحسين استخدام الذاكرة

أحياناً قد تواجه خطأ “نفاد الذاكرة” على GPU منخفض الأداء. هنا يأتي دور **how to set gpu** لتحديد حدود الذاكرة. الخاصية `GpuMemoryLimit` تقبل عددًا صحيحًا يمثل الميجابايت.

```csharp
// Example: restrict GPU usage to 512 MB
ocrEngine.Configuration.GpuMemoryLimit = 512;
```

**متى يجب الضبط:** إذا كنت تعالج العديد من الصور بالتوازي، قلل الحد لتجنب إشباع البطاقة. وعلى العكس، في محطة عمل ذات 8 جيجابايت من VRAM يمكنك رفعه بأمان إلى 4096 ميغابايت لمعالجة دفعات أسرع.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه إلى مشروع Console جديد (`dotnet new console`). يتضمن جميع الأجزاء التي ناقشناها، بالإضافة إلى قليل من معالجة الأخطاء لجعله أكثر صلابة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Create the OCR engine and enable GPU
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.Configuration.UseGpu = true;            // how to enable gpu
        ocrEngine.Configuration.GpuMemoryLimit = 1024;   // how to set gpu

        // -------------------------------------------------
        // Step 2: Load the JPEG image you want to process
        // -------------------------------------------------
        string imagePath = @"C:\OCR\Samples\invoice_01.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }

        var inputImage = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // Step 3: Run the OCR engine
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 4: Display the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.PlainText);
    }
}
```

**الناتج المتوقع:** بعد تشغيل `dotnet run`، سيطبع الـ console النص الخام المستخرج من `invoice_01.jpg`. إذا كانت الصورة تحتوي على نص مطبوع واضح، يجب أن يكون الناتج شبه مطابق للوثيقة الأصلية.

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | لماذا تحدث | الحل السريع |
|-------|----------------|-----------|
| **GPU غير مكتشف** | نقص تعريفات CUDA أو GPU غير مدعوم | تثبيت أحدث تعريف NVIDIA/AMD؛ التحقق باستخدام `nvidia-smi` أو ما يعادله |
| **خطأ نفاد الذاكرة** | `GpuMemoryLimit` مرتفع جداً بالنسبة للبطاقة | خفض الحد إلى 512 ميغابايت أو أقل |
| **إخراج غير مفهوم** | JPG منخفض الدقة أو ضغط عالي | استخدم صورة مصدر ذات جودة أعلى أو فعل `ocrEngine.Preprocessing.Deskew = true` |
| **`ocrResult` فارغ** | فشل تحميل تدفق الصورة | تحقق من مسار الملف وتأكد أن الملف غير مقفل |

معالجة هذه الأمور مسبقاً سيوفر عليك الوقت في مطاردة الأخطاء الغامضة لاحقاً.

## الخطوات التالية

الآن بعد أن أتقنت **how to use aspose** للـ OCR السريع، قد ترغب في استكشاف:

- **المعالجة الدفعية** – تكرار عبر مجلد من JPGs وكتابة كل نتيجة إلى ملف `.txt`.
- **الاستخراج المنظم** – استخدام `ocrResult.Regions` للحصول على إطارات الحدود واستخلاص حقول محددة مثل أرقام الفواتير.
- **الوضع المختلط CPU/GPU** – تشغيل المعالج للصور الصغيرة والتحول إلى GPU فقط للملفات الكبيرة لتحقيق توازن بين السرعة والذاكرة.

جميع هذه الامتدادات تبني على الأساس نفسه الذي أنشأته الآن، وهي مواضيع مثالية لمغامرة الدرس التالي.

---

*برمجة سعيدة! إذا واجهت أي صعوبات، اترك تعليقاً أدناه أو تواصل مع منتديات مجتمع Aspose. الـ GPU جاهز—لنُجعل OCR سريعاً كالبرق.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}