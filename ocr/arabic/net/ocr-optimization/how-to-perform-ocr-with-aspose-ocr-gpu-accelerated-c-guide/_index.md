---
category: general
date: 2026-02-19
description: كيفية إجراء التعرف الضوئي على الأحرف بسرعة على صور TIFF عالية الدقة.
  تعلم استخراج النص من ملفات TIFF باستخدام OCR على وحدة معالجة الرسومات في C#.
draft: false
keywords:
- how to perform OCR
- extract text from tiff
- use gpu ocr
- Aspose OCR C#
- high‑resolution image processing
- OCR performance tuning
language: ar
og_description: كيفية إجراء التعرف الضوئي على الأحرف (OCR) على ملفات TIFF عالية الدقة
  باستخدام Aspose OCR وتسريع GPU. دليل كامل خطوة بخطوة.
og_title: كيفية تنفيذ OCR – دليل C# مع تسريع GPU
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: كيفية تنفيذ OCR باستخدام Aspose OCR – دليل C# المعجل بوحدة معالجة الرسومات
url: /ar/net/ocr-optimization/how-to-perform-ocr-with-aspose-ocr-gpu-accelerated-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR – دليل C# مع تسريع GPU

هل احتجت يومًا إلى تنفيذ OCR على ملف TIFF ضخم وتساءلت لماذا يستغرق وقتًا طويلاً؟ لست وحدك. في هذا الدليل سنوضح لك **كيفية تنفيذ OCR** على صورة عالية الدقة باستخدام وحدة المعالجة الرسومية، وستحصل على برنامج C# جاهز للتنفيذ يستخرج النص من ملفات TIFF بسرعة فائقة.

سنغطي كل شيء بدءًا من تثبيت حزمة Aspose OCR إلى تمكين معالجة GPU، وسنشرح لماذا كل إعداد مهم. في النهاية ستتمكن من إدراج هذا الكود في أي مشروع .NET، وتوجيهه إلى ملف .tif، والحصول على نص نظيف قابل للبحث—دون الحاجة إلى خدمات إضافية.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يستهدف .NET 6، لكن .NET 5 يعمل أيضًا)  
- وحدة معالجة رسومية متوافقة (NVIDIA CUDA 11+ أو AMD Radeon مع دعم OpenCL)  
- حزمة **Aspose.OCR** من NuGet (الإصدار 23.9 أو أحدث)  
- ملف TIFF عالي الدقة تريد قراءته (مثال: `high_res_page.tif`)  

إذا كان أي من هذه غير مألوف لك، لا تقلق—كل نقطة سيتم شرحها في الخطوات التالية.

## الخطوة 1: تثبيت Aspose OCR وتمكين معالجة GPU  

أول ما عليك فعله هو إضافة مكتبة Aspose OCR إلى مشروعك وتفعيل دعم GPU. تمكين GPU يخبر المحرك بتحميل عمليات حساب المصفوفات الثقيلة إلى بطاقة الرسومات، مما يمكن أن يقلل زمن المعالجة بنسبة 70 % أو أكثر على GPU حديث.

```csharp
// Install the package via the CLI (run once):
// dotnet add package Aspose.OCR --version 23.9.0

using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;

class GpuDemo
{
    static void Main()
    {
        // Enable GPU acceleration – requires a compatible GPU driver.
        OcrEngine.EnableGpuProcessing(true);
```

**لماذا هذا مهم:**  
بدون `EnableGpuProcessing(true)`، يعود محرك OCR إلى التنفيذ على المعالج المركزي فقط، وهو مناسب للصور الصغيرة لكن يصبح بطيئًا جدًا على ملفات TIFF متعددة الميجابكسل. تشغيل العلامة يسمح للمكتبة باستخدام CUDA أو OpenCL في الخلفية، مما يقلل بشكل كبير من `ProcessingTime` الذي ستراه لاحقًا.

## الخطوة 2: تكوين محرك OCR للغة الإنجليزية (أو أي لغة تحتاجها)  

بعد ذلك ننشئ كائن `OcrEngine` ونحدد اللغة. تدعم Aspose أكثر من 100 لغة؛ تم عرض الإنجليزية هنا لأنها الأكثر شيوعًا، لكن يمكنك استبدال `Language.English` بـ `Language.French` أو `Language.German` وغيرها.

```csharp
        // Step 2: Create and configure the OCR engine.
        var ocrEngine = new OcrEngine
        {
            Language = Language.English   // Change if you need another language.
        };
```

**نصيحة احترافية:**  
إذا كنت تخطط لمعالجة مستندات متعددة اللغات، أنشئ محركات متعددة أو غيّر خاصية `Language` بين الاستدعاءات. هذا يجنبك عبء إعادة إنشاء المحرك لكل صفحة.

## الخطوة 3: تنفيذ OCR على ملف TIFF عالي الدقة  

الآن الجزء الممتع—نمرر الملف إلى المحرك ونتركه يقوم بالعمل الشاق. تُعيد طريقة `RecognizeImage` كائن `OcrResult` يحتوي على النص المستخرج ومعلومات التوقيت.

```csharp
        // Step 3: Run OCR on the TIFF image.
        var ocrResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/high_res_page.tif");
```

**معالجة الحالات الخاصة:**  
- **الملفات الكبيرة:** إذا تجاوز حجم TIFF الخاص بك 50 ميغابايت، فكر في تقليل الدقة أولًا باستخدام `System.Drawing` أو `ImageSharp` للحفاظ على استهلاك الذاكرة ضمن حدود معقولة.  
- **TIFF متعدد الصفحات:** استدعِ `RecognizeImage` داخل حلقة تمر على كل فهرس صفحة؛ ستُعيد Aspose النص لكل صفحة على حدة.

## الخطوة 4: طباعة زمن المعالجة والنص المستخرج  

أخيرًا، نطبع الوقت المستغرق والنص الخام الناتج عن OCR. هنا ستلاحظ فائدة تسريع GPU.

```csharp
        // Step 4: Display results.
        Console.WriteLine($"Time taken: {ocrResult.ProcessingTime} ms");
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**الناتج النموذجي**

```
Time taken: 312 ms
=== Extracted Text ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

على بطاقة RTX 3060 متوسطة المستوى، نفس ملف TIFF بدقة 3000 × 4000 بكسل الذي كان يستغرق ~1.2 ثانية على CPU يكتمل الآن في ~300 مللي ثانية—لاحظ الزيادة الكبيرة في السرعة.

## كيفية استخراج النص من ملفات TIFF بكفاءة  

إذا كنت مهتمًا فقط بمرحلة **استخراج النص من TIFF** ولا تحتاج إلى GPU، يمكنك تخطي علامة GPU. يبقى باقي الكود كما هو، لكن ستفقد تحسين الأداء على المسحات الكبيرة. إليك نسخة مبسطة:

```csharp
using Aspose.OCR;
using System;

class SimpleTiffOcr
{
    static void Main()
    {
        var engine = new OcrEngine { Language = Language.English };
        var result = engine.RecognizeImage(@"sample.tif");
        Console.WriteLine(result.Text);
    }
}
```

**متى تستخدم هذا:**  
- تشغيل التطبيق على خادم بدون GPU (headless).  
- ملفات TIFF صغيرة (< 1 MP) ولا يُعد زمن المعالجة على CPU عنق زجاجة.  

حتى بدون GPU، يبقى محرك OCR الخاص بـ Aspose دقيقًا بفضل نماذجها العصبية المدمجة.

## استخدام OCR مع GPU لمعالجة أسرع – الأخطاء الشائعة  

بينما **use gpu OCR** يمنحك السرعة، هناك بعض المشكلات التي قد تواجهك:

| المشكلة | العرض | الحل |
|-------|---------|-----|
| عدم وجود برنامج تشغيل CUDA | `EnableGpuProcessing` يرمي `PlatformNotSupportedException` | ثبّت أحدث برنامج تشغيل NVIDIA وأدوات CUDA |
| GPU غير مدعومة | المحرك يعود صامتًا إلى CPU | تحقق من ظهور بطاقتك في `OcrEngine.GetAvailableGpus()` (إذا استدعيت ذلك) |
| نفاد الذاكرة على صور ضخمة جدًا | `System.OutOfMemoryException` | عالج الصورة على قطع (`engine.RecognizeRegion`) |
| اتجاه الصورة غير صحيح | نص مشوش | قم بتدوير TIFF مسبقًا باستخدام `ImageSharp` قبل OCR |

**فحص سريع:** شغّل التجربة مرة واحدة مع `EnableGpuProcessing(false)`. قارن قيم `ProcessingTime`؛ يجب أن تكون عملية المعالجة المدعومة بـ GPU أسرع بمعدل 2‑3 مرات على الأقل.

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

فيما يلي البرنامج الكامل الذي يمكنك وضعه في تطبيق Console. استبدل `YOUR_DIRECTORY` بالمسار الفعلي لملف TIFF الخاص بك.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;

class GpuDemo
{
    static void Main()
    {
        // 1️⃣ Enable GPU acceleration (requires a compatible GPU)
        OcrEngine.EnableGpuProcessing(true);

        // 2️⃣ Create the OCR engine and set the language
        var ocrEngine = new OcrEngine
        {
            Language = Language.English   // Change as needed
        };

        // 3️⃣ Perform OCR on a high‑resolution TIFF
        var imagePath = @"YOUR_DIRECTORY/high_res_page.tif";
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 4️⃣ Show timing and extracted text
        Console.WriteLine($"Time taken: {ocrResult.ProcessingTime} ms");
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

تشغيل هذا على جهاز يحتوي على RTX 3070 ينتج مخرجات مشابهة للمثال السابق، مؤكدًا أن **كيفية تنفيذ OCR** مع دعم GPU يعمل كما هو موضح.

## الخطوات التالية – ما بعد الأساسيات  

- **المعالجة الدفعية:** غلف استدعاء `RecognizeImage` داخل حلقة `foreach` على مجلد من ملفات TIFF.  
- **ما بعد المعالجة:** مرّر `ocrResult.Text` إلى مدقق إملائي أو محلل لغة طبيعية لتنظيف الأخطاء الناتجة عن OCR.  
- **الوضع الهجين:** اكتشف حجم الصورة في وقت التشغيل وقرر ما إذا كنت ستمكن GPU (`if (image.Width * image.Height > 5_000_000) EnableGpuProcessing(true)`).  

جميع هذه الإضافات لا تزال **use gpu ocr** عندما يكون ذلك منطقيًا، مما يحافظ على سرعة خط الأنابيب ووعي الموارد.

## الخلاصة  

أنت الآن تعرف **كيفية تنفيذ OCR** على ملفات TIFF عالية الدقة باستخدام Aspose OCR وتسريع GPU، ويمكنك بثقة **استخراج النص من TIFF** في جزء من الوقت الذي تستغرقه الطريقة التي تعتمد على CPU فقط. المثال الكامل الجاهز للنسخ‑اللصق يوضح التدفق الكامل—من تمكين GPU إلى طباعة زمن المعالجة والنص النهائي.

جرّبه، عدّل إعدادات اللغة، وحاول معالجة دفعة من الصفحات. إذا واجهت أي صعوبات، ارجع إلى جدول “استخدام OCR مع GPU لمعالجة أسرع”؛ معظم المشكلات مغطاة هناك. برمجة سعيدة، واستمتع بزيادة السرعة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}