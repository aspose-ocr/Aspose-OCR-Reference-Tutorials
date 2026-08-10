---
category: general
date: 2026-05-31
description: تعلم كيفية التعرف على النص من الصورة في C# باستخدام Aspose OCR، بما في
  ذلك كيفية استخراج النص من ملفات TIFF وتحميل الصورة للتعرف الضوئي على الأحرف بكفاءة.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: ar
og_description: دليل خطوة بخطوة للتعرف على النص من الصورة باستخدام Aspose OCR، يغطي
  استخراج النص من ملفات TIFF وتحميل الصورة بشكل صحيح للتعرف الضوئي على الأحرف.
og_title: التعرف على النص من الصورة في C# باستخدام Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: التعرف على النص من الصورة في C# باستخدام Aspose OCR
url: /ar/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من صورة في C# باستخدام Aspose OCR

هل احتجت يومًا إلى **التعرف على النص من صورة** لكن لم تكن متأكدًا من أين تبدأ في C#؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عند التعامل مع المستندات الممسوحة أو ملفات TIFF متعددة الصفحات. في هذا الدليل سنرشدك عبر مثال كامل جاهز للتنفيذ **يتعرف على النص من صورة** باستخدام مكتبة Aspose OCR، وسنوضح لك أيضًا كيفية **استخراج النص من tiff** وأفضل طريقة **لتحميل صورة للـ OCR** دون عناء.

سنغطي كل شيء من تثبيت حزمة NuGet إلى التعامل مع تسريع GPU والعودة إلى CPU عند الحاجة. في نهاية هذا الشرح ستحصل على تطبيق console يطبع النص المعترف به ووقت المعالجة—بدون أجزاء مفقودة أو إشارات غامضة.

## ما ستبنيه

- تطبيق console بسيط على .NET يقوم بتحميل صورة (بما في ذلك TIFF متعددة الصفحات)  
- محرك OCR مُعد لاستخدام GPU، مع إمكانية الرجوع إلى CPU بسلاسة  
- استخراج النص العادي من الصورة وعرضه في الـ console  
- معلومات زمنية لتتمكن من رؤية تأثير الأداء بين GPU و CPU  

**المتطلبات المسبقة**

- .NET 6 SDK أو أحدث (الكود يعمل مع .NET Core و .NET Framework)  
- إلمام أساسي بـ C# وسطر الأوامر  
- اتصال بالإنترنت لتحميل حزمة Aspose.OCR من NuGet  

إذا كان لديك هذه المتطلبات، لنبدأ.

![كود C# للتعرف على النص من صورة باستخدام Aspose OCR](image.png "كود C# للتعرف على النص من صورة باستخدام Aspose OCR")

## الخطوة 1 – التعرف على النص من صورة: إعداد محرك OCR

أولاً، نحتاج إلى إنشاء كائن `OcrEngine`. يتيح لك Aspose OCR اختيار جهاز المعالجة—GPU للسرعة، أو CPU كخطة احتياطية. كما يقبل المحرك تلميحًا لحد الذاكرة، وهو مفيد على الأجهزة المشتركة.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**لماذا هذا مهم:**  
اختيار `OcrDevice.Gpu` يمكن أن يقلل الثواني من وقت التعرف على الصور الكبيرة، خاصة ملفات TIFF متعددة الصفحات. `GpuMemoryLimit` يمنع تطبيقك من استهلاك كل ذاكرة الـ GPU على محطة عمل مشتركة.

## الخطوة 2 – تحميل صورة للـ OCR (دعم TIFF)

الآن نقوم بتمرير الصورة إلى المحرك. `ImageStream.FromFile` في Aspose يقبل **أي** صيغة تدعمها المكتبة—TIFF، PNG، JPEG، إلخ. هذه الخطوة تلبي مباشرةً متطلب **تحميل صورة للـ OCR**.

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**نصيحة احترافية:** إذا كنت تتعامل مع ملف TIFF متعدد الصفحات، يقوم Aspose تلقائيًا بمعالجة كل صفحة كإطار منفصل، وسيعالج المحرك هذه الإطارات بالتتابع. لا تحتاج إلى كود إضافي.

## الخطوة 3 – تشغيل التعرف و**استخراج النص من tiff**

بعد تجهيز المحرك وتحميل الصورة، نبدأ عملية OCR. تُعيد طريقة `Recognize` كائن `OcrResult` يحتوي على النص العادي، درجات الثقة، وتفاصيل الوقت.

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**معالجة الحالات الخاصة:**  
إذا لم يتوفر GPU، فإن `engine.Recognize()` لا يزال يعمل لأن المحرك يتحول صامتًا إلى CPU. يمكنك فحص `engine.Device` بعد التعرف إذا أردت تسجيل الجهاز الفعلي المستخدم.

## الخطوة 4 – استرجاع النص العادي المعترف به

استخراج النص سهل—فقط اقرأ الخاصية `Text`. هنا نُكمل **استخراج النص من tiff** (أو أي صورة أخرى) ونقدمه للمستخدم.

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

سترى الأحرف الأصلية مع الحفاظ على فواصل الأسطر كما تظهر في الصورة المصدر. للحصول على مخرجات أكثر هيكلة (مثل JSON أو CSV)، يمكنك استكشاف `result.Regions` و `result.Lines`، لكن النص العادي يكفي عادةً للسكريبتات السريعة.

## الخطوة 5 – قياس وقت المعالجة ومعالجة الرجوع إلى GPU

الأداء مهم، خاصةً عند معالجة عشرات الصفحات. خاصية `ProcessingTime` تخبرك بالمدة التي استغرقها الـ OCR، بغض النظر عما إذا تم تشغيله على GPU أو CPU.

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**لماذا يهمك ذلك:**  
إذا لاحظت زيادة ملحوظة في الوقت، قد تحتاج إلى تعديل `GpuMemoryLimit` أو التحول صراحةً إلى CPU (`Device = OcrDevice.Cpu`). وعلى العكس، إذا حصلت على نتيجة بأقل من ثانية على ملف TIFF كبير فهذا يعني أن تسريع الـ GPU يؤدي وظيفته.

## مثال كامل جاهز للتنفيذ

انسخ الشيفرة أدناه إلى مشروع console جديد (`dotnet new console -n OcrDemo`) ثم نفّذ `dotnet add package Aspose.OCR`. بعد ذلك استبدل `YOUR_DIRECTORY/sample_multi_page.tif` بالمسار إلى صورتك.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**الناتج المتوقع (مقتطع للوضوح):**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

إذا كان جهازك يفتقر إلى GPU قوي، قد يكون الوقت المستغرق بضع ثوانٍ أطول، لكن النص سيظل يُستخرج بشكل صحيح.

## أسئلة شائعة ومشكلات محتملة

- **ماذا لو كانت الصورة ضخمة (أكثر من 10 ميغابايت)؟**  
  قلل دقتها قبل تمريرها إلى المحرك، أو زد `GpuMemoryLimit` إذا كان لديك ذاكرة VRAM كافية.  
- **هل يمكن معالجة عدة صور داخل حلقة؟**  
  بالتأكيد. أعد استخدام نفس كائن `OcrEngine` وعين `ImageStream` جديد في كل تكرار.  
- **هل يجب تحرير أي موارد؟**  
  `OcrEngine` يطبق `IDisposable`. احفظه داخل كتلة `using` لإدارة الموارد بشكل نظيف، خاصةً عند التعامل مع موارد GPU.  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **ماذا عن اللغات غير الإنجليزية؟**  
  عيّن `engine.Language = OcrLanguage.Spanish` (أو أي لغة مدعومة) قبل استدعاء `Recognize()`.  

## الخلاصة

أصبح لديك الآن حل كامل من البداية إلى النهاية **يتعرف على النص من صورة** في C# باستخدام Aspose OCR. غطى الشرح كيفية **تحميل صورة للـ OCR**، وكيفية **استخراج النص من tiff**، وكيفية قياس الأداء مع معالجة الرجوع إلى GPU بسلاسة.

من هنا يمكنك:

- تجربة صيغ صور مختلفة (BMP، PDF) لمعرفة كيفية تعامل Aspose معها.  
- الغوص في `result.Regions` للحصول على بيانات إطارات الحدود إذا كنت تحتاج إلى تخطيط واعٍ للصفحات  

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

- [How to Use Aspose to Recognize Image from Stream in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}