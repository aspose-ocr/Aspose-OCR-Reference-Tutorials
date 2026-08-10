---
category: general
date: 2026-02-17
description: تعلم كيفية إجراء التعرف الضوئي على الأحرف (OCR) للصور باستخدام Aspose
  OCR على وحدة معالجة الرسومات (GPU). كود خطوة بخطوة للتعرف على النص من الصورة، تحميل
  صورة عالية الدقة، تعيين معرف جهاز GPU واستخراج النص باستخدام Aspose.
draft: false
keywords:
- how to ocr image
- recognize text from image
- load high resolution image
- set gpu device id
- extract text using aspose
language: ar
og_description: كيفية تنفيذ OCR للصورة باستخدام Aspose OCR على وحدة معالجة الرسومات
  (GPU). اتبع الدرس الكامل بلغة C# للتعرف على النص من الصورة، تحميل صورة عالية الدقة،
  تعيين معرف جهاز GPU واستخراج النص باستخدام Aspose.
og_title: كيفية التعرف الضوئي على النص في الصورة باستخدام Aspose OCR – دليل C# المدعوم
  بتسريع GPU
tags:
- Aspose OCR
- C#
- GPU acceleration
title: كيفية إجراء OCR للصور باستخدام Aspose OCR – دليل C# المدعوم بتقنية GPU
url: /ar/net/ocr-optimization/how-to-ocr-image-with-aspose-ocr-gpu-accelerated-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية OCR الصورة باستخدام Aspose OCR – دليل C# مع تسريع GPU

هل تساءلت يومًا **how to OCR image** عندما يكون الملف مسحًا ضخمًا بدقة 300 DPI وتحتاج إلى النتائج في ثوانٍ؟ لست وحدك—المطورون يواجهون باستمرار محركات OCR البطيئة التي تعمل على CPU فقط، خاصةً مع الصور عالية الدقة. الخبر السار؟ Aspose OCR يتيح لك الاستفادة من وحدة معالجة الرسومات GPU، مما يقلل وقت المعالجة بشكل كبير مع الحفاظ على دقة عالية.

في هذا البرنامج التعليمي سنستعرض مثالًا كاملًا وقابلًا للتنفيذ ي **recognizes text from image**، يوضح لك كيفية **load high resolution image**، يتيح لك **set GPU device ID**، وأخيرًا **extract text using Aspose**. في النهاية ستحصل على برنامج مستقل يمكنك إدراجه في أي مشروع .NET.

## ما ستحتاجه

- **.NET 6.0** أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+)
- حزمة NuGet **Aspose.OCR for .NET** (الإصدار 23.11 أو أحدث)
- جهاز مزود بـ GPU يدعم CUDA 11+ (اختياري لكن يُنصح به)
- صورة JPEG/PNG عالية الدقة تريد إجراء OCR عليها (مثال: `highres_scan.jpg`)

إذا كنت تفتقد أيًا من هذه المتطلبات، احصل على حزمة NuGet باستخدام:

```bash
dotnet add package Aspose.OCR
```

لا توجد مكتبات أصلية إضافية مطلوبة؛ Aspose يضم بيئة تشغيل CUDA لك.

![مخطط كيفية OCR الصورة](image-placeholder.png "مخطط يوضح خط أنابيب OCR المعزز بـ GPU – كيفية OCR الصورة")

## الخطوة 1: إنشاء محرك OCR وتعيين معرف جهاز GPU  

أول شيء يجب عليك القيام به هو إخبار Aspose بالعمل على الـ GPU. هنا يأتي دور **set GPU device ID**—إذا كان لديك عدة وحدات GPU يمكنك اختيار الأنسب لحمولة العمل.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialize the OCR engine with GPU processing mode
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    ProcessingMode = ProcessingMode.Gpu, // Enable GPU acceleration
    GpuDeviceId = 0                     // Choose GPU #0 (change if you have several)
});
```

> **لماذا هذا مهم:** معالجة الـ GPU تفرغ عمل تحليل الصورة الثقيلة إلى الأنوية المتوازية، مما يمنحك تسريعًا بمقدار 3‑5× على المسحات النموذجية. إذا لم تقم بتعيين `GpuDeviceId`، فإن Aspose يستخدم الجهاز الأول افتراضيًا، وهذا مناسب لأجهزة GPU الوحيدة.

## الخطوة 2: تحميل صورة عالية الدقة  

بعد ذلك، نقوم **load high resolution image** إلى صيغة يفهمها محرك OCR. Aspose يوفر `ImageStream.FromFile`، الذي يقرأ الملف إلى الذاكرة دون تحويلات غير ضرورية.

```csharp
// Path to your high‑resolution scan (300 DPI or more)
string imagePath = @"YOUR_DIRECTORY/highres_scan.jpg";

// Load the image; ImageStream handles large files efficiently
var image = ImageStream.FromFile(imagePath);
```

> **نصيحة:** إذا كانت صورتك مخزنة في سحابة، يمكنك أيضًا تزويد `Stream` مباشرة—فقط استبدل `FromFile` بـ `FromStream(yourStream)`. سيظل المحرك يتعامل معها كمصدر عالي الدقة.

## الخطوة 3: التعرف على النص من الصورة  

الآن بعد أن أصبح المحرك جاهزًا وتم تحميل الصورة، يمكننا **recognize text from image**. طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على النص العادي، درجات الثقة، وحتى إطارات الحدود إذا احتجتها لاحقًا.

```csharp
// Perform OCR; this call is where the GPU does its magic
OcrResult recognitionResult = ocrEngine.Recognize(image);

// For debugging, you can also inspect recognitionResult.Regions
```

> **حالة خاصة:** إذا كانت الصورة مظلمة جدًا أو تحتوي على الكثير من الضوضاء، فكر في معالجتها مسبقًا (مثلاً زيادة التباين) قبل استدعاء `Recognize`. Aspose يقدم واجهة `Preprocess`، لكن بالنسبة لمعظم المسحات النظيفة الإعداد الافتراضي يعمل جيدًا.

## الخطوة 4: استخراج النص باستخدام Aspose وعرضه  

أخيرًا، نقوم **extract text using Aspose** بقراءة خاصية `Text` من النتيجة. لنطبعها في وحدة التحكم، لكن يمكنك أيضًا كتابتها إلى ملف أو قاعدة بيانات.

```csharp
// Output the plain‑text result
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(recognitionResult.Text);
```

**الناتج المتوقع** (مثال لفاتورة ممسوحة):

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,254.00
Thank you for your business!
```

إذا رأيت أحرفًا مشوشة، تحقق مرة أخرى من أن الصورة عالية الدقة فعلاً وأن اللغة الصحيحة مضبوطة في `OcrEngineSettings` (مثال: `Language = Language.English`).

## مثال كامل يعمل  

بجمع كل ما سبق، إليك البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع وحدة تحكم جديد:

```csharp
// ------------------------------------------------------------
// Full OCR example – Aspose OCR with GPU acceleration
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine for GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            ProcessingMode = ProcessingMode.Gpu, // GPU acceleration
            GpuDeviceId = 0                      // Change if you have multiple GPUs
        });

        // 2️⃣ Load a high‑resolution image
        string imagePath = @"YOUR_DIRECTORY/highres_scan.jpg";
        var image = ImageStream.FromFile(imagePath);

        // 3️⃣ Recognize text from the image
        OcrResult result = ocrEngine.Recognize(image);

        // 4️⃣ Extract and display the plain text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

شغّل البرنامج باستخدام `dotnet run`. على GPU جيد ستظهر نتيجة OCR في أقل من ثانية، حتى لمسح بحجم 5 MB ودقة 300 DPI.

## أسئلة شائعة ونصائح احترافية  

### ماذا لو لم يكن لدي GPU؟  
لا يزال بإمكانك استخدام Aspose OCR على الـ CPU عن طريق تعيين `ProcessingMode = ProcessingMode.Cpu`. تظل الواجهة البرمجية (API) نفسها؛ فقط الأداء يتغير.

### كيف أتعامل مع لغات متعددة؟  
أضف `Language = Language.Multilingual` (أو تعداد محدد مثل `Language.French`) داخل `OcrEngineSettings`. سيقوم Aspose بتحميل حزم اللغة المناسبة تلقائيًا.

### هل يمكنني معالجة ملفات PDF مباشرة؟  
نعم—Aspose OCR يمكنه استخراج الصور من ملفات PDF أولاً، ثم تشغيل OCR على كل صفحة. اجمع `Aspose.PDF` مع نفس `OcrEngine` لإنشاء خط أنابيب سلس.

### متى يجب تعديل `GpuDeviceId`؟  
إذا كان الخادم يشغل كلًا من مهام معالجة الصور وتعلم الآلة، قد تخصص GPU 1 لـ OCR (`GpuDeviceId = 1`) وتترك GPU 0 حرًا لمهام الاستدلال.

### كيف تحسن الدقة في المسحات الضوضائية؟  
قم بمعالجة الصورة مسبقًا:  
```csharp
image = image.AdjustContrast(1.2f).ApplyThreshold(0.5f);
```
هذه الأساليب هي جزء من أدوات معالجة الصور في Aspose.

## الخاتمة  

أنت الآن تعرف **how to OCR image** باستخدام Aspose OCR مع تسريع GPU، وكيفية **recognize text from image**، والطريقة الصحيحة لـ **load high resolution image**، وكيفية **set GPU device ID**، وأخيرًا كيفية **extract text using Aspose** في برنامج C# نظيف وجاهز للإنتاج.  

جرّب تشغيل الكود على عدة ملفات مختلفة—جرب إيصالًا غير واضح، أو منشورًا لامعًا، أو حتى ملاحظة مكتوبة يدويًا. جرب إعدادات اللغة وخطوات المعالجة المسبقة لترى كيف تتغير الدقة.  

بعد ذلك، قد تستكشف **batch processing** (التكرار على مجلد من المسحات) أو دمج نتيجة OCR في **search index** لاسترجاع المستندات بسرعة. كلا الموضوعين يبنيان بشكل طبيعي على المفاهيم التي تم تغطيتها هنا ويعدان مشاريع متابعة مثالية.  

برمجة سعيدة، ولتكن خطوط OCR الخاصة بك سريعة وخالية من الأخطاء!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}