---
category: general
date: 2026-03-20
description: تعلم كيفية تصحيح انحراف الصورة وإزالة الضوضاء من الصورة باستخدام Aspose
  OCR. يوضح هذا الدليل خطوة بخطوة أيضًا كيفية إعداد الصورة مسبقًا للتعرف الضوئي على
  الأحرف وتحسين دقة التعرف.
draft: false
keywords:
- how to deskew image
- remove image noise
- preprocess image for OCR
- recognize text from image
- improve OCR accuracy
language: ar
og_description: تعلم كيفية تصحيح انحراف الصورة وإزالة الضوضاء باستخدام Aspose OCR.
  عزّز دقة OCR الخاصة بك في دقائق.
og_title: كيفية تصحيح ميل الصورة – دليل C# الكامل لمعالجة ما قبل OCR
tags:
- OCR
- C#
- Image Processing
title: كيفية تصحيح إمالة الصورة – دليل C# الكامل لمعالجة ما قبل OCR
url: /ar/net/ocr-optimization/how-to-deskew-image-complete-c-guide-for-ocr-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح إمالة الصورة – دليل C# الكامل لمعالجة ما قبل OCR

هل تساءلت يومًا **how to deskew image** عن ملفات الصور التي خرجت من الماسح الضوئي بزاوية غريبة؟ لست وحدك؛ العديد من المطورين يواجهون هذه المشكلة عندما يحاولون إمداد صورة إلى محرك OCR. الخبر السار هو أنه ببضع أسطر من C# و Aspose OCR يمكنك تصحيح الإمالة، إزالة الضوضاء، وتعزيز التباين في خط أنابيب واحد مرتب—بدون الحاجة إلى Photoshop.

في هذا الدرس سنستعرض كل ما تحتاج معرفته: من تحميل صورة مائلة، إلى **remove image noise**، إلى **preprocess image for OCR**، وأخيرًا إلى **recognize text from image** مع درجة عالية من **improve OCR accuracy**. في النهاية ستحصل على تطبيق console جاهز للتشغيل يحول مسحًا فوضويًا إلى نص نظيف قابل للبحث.

## ما ستحتاجه

- .NET 6 أو أحدث (الكود يستخدم بناء جملة `using var`، المدعوم من C# 8)
- حزمة NuGet لـ Aspose OCR (`Aspose.OCR`) – تثبيت عبر `dotnet add package Aspose.OCR`
- صورة نموذجية تكون مائلة ومليئة بالضوضاء (مثال: `skewed_noisy.png`)
- بيئة تطوير أو محرر حسب اختيارك (Visual Studio، VS Code، Rider… اختر ما يناسبك)

> **نصيحة احترافية:** إذا لم يكن لديك ملف عينة، فقط قم بتدوير لقطة شاشة واضحة بضع درجات وأضف بعض ضوضاء “ملح‑وفلفل” باستخدام محرر صور. يعمل خط الأنابيب بنفس الطريقة.

## الخطوة 1: كيفية تصحيح إمالة الصورة باستخدام مرشح Deskew

أول شيء نفعله هو تصحيح الدوران. توفر Aspose مرشح `DeskewFilter` يمكنه اكتشاف الزوايا تلقائيًا حتى `MaxAngle` القابلة للتكوين. ضبطه على **5°** هو الإعداد الافتراضي الآمن لمعظم المستندات الممسوحة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image class

// Initialize the OCR engine – English is the most common language
using var ocrEngine = new OcrEngine
{
    Language = Language.English
};

// Build the preprocessing pipeline
var preprocessPipeline = new PreprocessPipeline()
    .Add(new DeskewFilter { MaxAngle = 5 })          // This is where we answer “how to deskew image”
    .Add(new DespeckleFilter { Strength = 2 })      // Next we’ll remove image noise
    .Add(new ContrastFilter { Level = 1.5 });        // Finally we boost contrast for OCR
```

**لماذا هذا مهم:**  
إذا كان النص مائلًا، قد يفسر خوارزمية OCR الأحرف بشكل خاطئ—مثلاً “l” تصبح “i”. من خلال **deskewing** أولاً، تمنح المحرك لوحة قماشية مستقيمة للعمل عليها.

## الخطوة 2: إزالة ضوضاء الصورة باستخدام Despeckle

المسحات الضوئية من هواتف رخيصة أو ماسحات قديمة غالبًا ما تحتوي على بقع تشبه النقاط العشوائية. تلك البقع تربك مُعرّف الأحرف. يقوم `DespeckleFilter` بتنقية الصورة مع الحفاظ على الحواف.

```csharp
// The DespeckleFilter is already part of the pipeline (see Step 1)
// Strength = 2 is a balanced setting; increase for very noisy pics
```

إذا كنت بحاجة إلى **remove image noise** بشكل أكثر حدة، زد قيمة `Strength` إلى 3 أو 4—لكن احذر من فقدان الخطوط الرفيعة.

## الخطوة 3: معالجة الصورة مسبقًا لـ OCR – تعزيز التباين

المسحات ذات التباين المنخفض (رمادي فاتح على ورق أبيض) قد تجعل OCR يفوت الحروف الخفيفة. يقوم `ContrastFilter` بتمديد نطاق النغمات، مما يجعل البكسلات الداكنة أكثر ظلامًا والفاتحة أكثر إضاءة.

```csharp
// Contrast level of 1.5 is a good starting point.
// You can experiment with values between 1.0 (no change) and 2.0 (strong boost).
```

**حالة خاصة:** إذا كانت صورتك المصدرية ذات تباين عالي بالفعل، قد يؤدي تطبيق هذا المرشح إلى تلاشي التفاصيل. في هذه الحالة، اضبط `Level` إلى `1.0` (يعني تعطيله فعليًا).

## الخطوة 4: تحميل وتنظيف الصورة المصدرية

الآن نقوم بتحميل الصورة فعليًا وتشغيلها عبر خط الأنابيب الذي جمعناه للتو.

```csharp
// Load the source image – replace the path with your own file location
var sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_noisy.png");

// Apply the entire preprocessing pipeline
var cleanedImage = preprocessPipeline.Apply(sourceImage);
```

> **ملاحظة:** طريقة `Apply` تُعيد كائن `Image` جديد؛ الأصل يبقى دون تعديل. هذا يجعل من السهل مقارنة “قبل” و “بعد” إذا أردت تتبع العملية.

## الخطوة 5: التعرف على النص من الصورة باستخدام Aspose OCR

مع صورة مستقيمة، خالية من الضوضاء، ذات تباين عالي في المتناول، نمررها أخيرًا إلى محرك OCR.

```csharp
// Perform OCR on the cleaned image
var ocrResult = ocrEngine.Recognize(cleanedImage);

// Output the recognized text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**ما يجب أن تراه:** يطبع الـ console محتوى النص للمسح الأصلي، عادةً مع أخطاء أقل بكثير مقارنةً إذا كنت قد أرسلت الملف الخام مباشرة.

## الخطوة 6: التحقق وتحسين دقة OCR

حتى مع خط أنابيب قوي، قد لا تزال بعض الأحرف غير صحيحة—خاصة إذا كان الخط الأصلي غير شائع. إليك بعض الحيل السريعة لـ **improve OCR accuracy**:

| المشكلة | الحل السريع |
|-------|-----------|
| فقدان علامات الترقيم الصغيرة | أضف `BinaryThresholdFilter` قبل خطوة التباين |
| لغات مختلطة (مثال: English + Spanish) | Set `ocrEngine.Language = Language.English | Language.Spanish;` |
| خلفية داكنة جدًا | اعكس الصورة (`new InvertFilter()`) قبل تصحيح الإمالة |
| مستندات كبيرة | معالجة الصفحات بشكل متوازي (`Parallel.ForEach`) لتسريع العملية |

جرّب تغيير ترتيب الفلاتر؛ أحيانًا تطبيق **contrast** قبل **despeckle** يعطي نتائج أفضل على المسحات ذات الجودة المنخفضة.

## مثال عملي كامل

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑ولصقه في مشروع console جديد. يتضمن جميع الأجزاء التي ناقشناها، بالإضافة إلى بعض فحوصات الأمان.

```csharp
// File: Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine (English language)
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // -------------------------------------------------
        // 2️⃣ Build preprocessing pipeline:
        //    Deskew → Despeckle → Contrast Boost
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
            .Add(new DeskewFilter { MaxAngle = 5 })          // how to deskew image
            .Add(new DespeckleFilter { Strength = 2 })      // remove image noise
            .Add(new ContrastFilter { Level = 1.5 });        // preprocess image for OCR

        // -------------------------------------------------
        // 3️⃣ Load the source image (adjust path as needed)
        // -------------------------------------------------
        const string imagePath = "YOUR_DIRECTORY/skewed_noisy.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ File not found: {imagePath}");
            return;
        }

        var sourceImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // 4️⃣ Apply the pipeline → cleaned image
        // -------------------------------------------------
        var cleanedImage = preprocessPipeline.Apply(sourceImage);

        // -------------------------------------------------
        // 5️⃣ Recognize text (this is the “recognize text from image” step)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(cleanedImage);

        // -------------------------------------------------
        // 6️⃣ Output the result
        // -------------------------------------------------
        Console.WriteLine("\n=== OCR Output ===\n");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**الناتج المتوقع** (بافتراض أن الصورة النموذجية تحتوي على “Hello World!”):

```
=== OCR Output ===

Hello World!
```

إذا رأيت أحرفًا مشوشة، تحقق مرة أخرى من ترتيب خط الأنابيب أو زد قيمة `DespeckleFilter.Strength`.

## الخاتمة

لقد غطينا **how to deskew image**، **remove image noise**، **preprocess image for OCR**، وأخيرًا **recognize text from image** باستخدام Aspose OCR—مع مراعاة **improve OCR accuracy**. المثال الكامل القابل للتنفيذ يُظهر كل خطوة في سياقها، بحيث يمكنك إدراجه في أي مشروع .NET والبدء في استخراج النص فورًا.

هل أنت مستعد للتحدي التالي؟ جرّب توسيع خط الأنابيب لمعالجة ملفات PDF متعددة الصفحات، أو جرب حزم اللغات للمستندات متعددة اللغات. المفاهيم نفسها تنطبق—فقط غيّر علم `Language` وربما أضف `RotateFilter` للصفحات المقلوبة.

هل لديك أسئلة أو صورة صعبة لا تتعاون؟ اترك تعليقًا أدناه، وسنحل المشكلة معًا. برمجة سعيدة!

![مثال على كيفية تصحيح إمالة الصورة](/images/deskew-example.png "توضيح كيفية تصحيح إمالة الصورة باستخدام Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}