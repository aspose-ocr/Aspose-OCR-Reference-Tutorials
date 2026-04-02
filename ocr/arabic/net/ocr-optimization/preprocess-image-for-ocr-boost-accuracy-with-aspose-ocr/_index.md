---
category: general
date: 2026-04-01
description: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف (OCR) لتحسين دقة التعرف.
  تعلّم كيفية تطبيق تصحيح الميل التلقائي، إزالة الضوضاء، وتحويل الصورة إلى أبيض وأسود
  باستخدام Aspose.OCR.
draft: false
keywords:
- preprocess image for OCR
- improve OCR accuracy
- black and white OCR
- Aspose OCR preprocessing
- image deskew C#
- OCR noise reduction
language: ar
og_description: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف (OCR) لتحسين دقة OCR.
  يوضح هذا الدليل خطوة بخطوة تصحيح الميل تلقائيًا، إزالة الضوضاء، وتحويل الصورة إلى
  أبيض وأسود باستخدام C#.
og_title: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف – تعزيز الدقة باستخدام Aspose.OCR
tags:
- OCR
- C#
- Image Processing
title: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف – تحسين الدقة باستخدام Aspose.OCR
url: /ar/net/ocr-optimization/preprocess-image-for-ocr-boost-accuracy-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# معالجة الصورة مسبقًا للتعرف الضوئي على الحروف – تحسين الدقة باستخدام Aspose.OCR

هل تساءلت يومًا لماذا تبدو نتائج التعرف الضوئي على الحروف (OCR) فوضوية رغم أن صورة المصدر تبدو جيدة؟ أنت على الأرجح تفتقد خطوة حاسمة: **preprocess image for OCR**.  
في هذا الدرس سنستعرض بالضبط كيفية تنظيف صورة مائلة ومشوَّشة حتى يتمكن المحرك من قراءتها باحتراف. في النهاية ستلاحظ قفزة ملحوظة في **improve OCR accuracy** وستعتاد على تقنية **black and white OCR** التي تجعلها Aspose.OCR أمرًا بسيطًا.

## ما ستتعلمه

سنغطي كل شيء بدءًا من تثبيت حزمة Aspose.OCR NuGet إلى تكوين `PreprocessOptions` التي تقوم تلقائيًا بإزالة الميل، وإزالة الضوضاء، وتحويل صورتك إلى ثنائية. ستحصل أيضًا على نصائح عملية للتعامل مع الحالات الخاصة—مثل الدوران الشديد أو المسحات منخفضة التباين—حتى تتمكن من الحفاظ على جودة التعرف عالية مهما كان. لا حاجة إلى وثائق خارجية؛ الحل الكامل موجود هنا.

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (العينة تُجمع باستخدام .NET 6، لكن الإصدارات الأقدم تعمل أيضًا)
- إلمام أساسي بـ C# و Visual Studio (أو أي بيئة تطوير تفضلها)
- ملف صورة مائل أو مشوَّش (سنسميه `skewed_noisy.jpg`)

إذا كان لديك كل ذلك، فلنبدأ.

## معالجة الصورة مسبقًا للتعرف الضوئي على الحروف – لماذا المعالجة المسبقة مهمة

تخيل محرك OCR كقارئ صعب الإرضاء: إذا كانت الصفحة مائلة، أو مليئة بالبقع، أو رمادية جدًا، سيتعثر في الكلمات. المعالجة المسبقة تتعامل مع ثلاثة أعداء شائعين:

1. **Rotation** – يقوم Auto‑deskew بتصحيح الميل لتصبح الخطوط أفقية.  
2. **Noise** – يزيل Denoising البكسلات العشوائية التي قد تبدو كحروف عشوائية.  
3. **Contrast** – التحويل إلى ثنائي (تحويل إلى أبيض وأسود) يمنح المحرك فصلًا واضحًا بين المقدمة والخلفية.

معًا يشكلون العمود الفقري لأي سير عمل يرغب في **improve OCR accuracy**.

![preprocess image for OCR example](https://example.com/ocr-preprocess.png "preprocess image for OCR example")

*(نص بديل: “preprocess image for OCR example showing before and after binarization”)*

## الخطوة 1: تثبيت Aspose.OCR

أولًا وقبل كل شيء—احصل على المكتبة. افتح الطرفية (أو Package Manager Console) وشغّل:

```bash
dotnet add package Aspose.OCR
```

أو، إذا كنت تفضّل واجهة Visual Studio، انقر بزر الماوس الأيمن على **Dependencies → Manage NuGet Packages**, ابحث عن **Aspose.OCR**, ثم اضغط **Install**. الحزمة تضم كل ما تحتاجه، بما في ذلك مساحة الاسم `Filters` المستخدمة في المعالجة المسبقة.

## الخطوة 2: إنشاء محرك OCR

الآن بعد أن أصبحت المكتبة موجودة، يمكننا إنشاء نسخة من `OcrEngine`. هذا الكائن هو نقطة الدخول لجميع عمليات التعرف.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Step 2: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the steps follow...
    }
}
```

لماذا ننشئ المحرك أولًا؟ المحرك يحتفظ بالإعدادات العامة (اللغة، المنطقة، إلخ) وبشكل أساسي `PreprocessOptions` التي سنقوم بتكوينها لاحقًا.

## الخطوة 3: تكوين خيارات المعالجة المسبقة

هنا يحدث السحر. سنفعل ثلاثة إعدادات:

- `AutoDeskew` – يكتشف ويصحح الميل تلقائيًا.
- `DenoiseLevel = DenoiseLevel.Medium` – يوازن بين إزالة الضوضاء والحفاظ على التفاصيل الدقيقة.
- `Binarize` – يفرض إخراجًا أبيض وأسود، وهو النهج الكلاسيكي لـ **black and white OCR**.

```csharp
// Step 3: Set up preprocessing to clean the image
PreprocessOptions preprocessOptions = new PreprocessOptions
{
    AutoDeskew = true,                     // Correct rotation automatically
    DenoiseLevel = DenoiseLevel.Medium,   // Reduce noise while preserving details
    Binarize = true                        // Convert to black‑and‑white for better recognition
};

// Attach options to the engine
ocrEngine.PreprocessOptions = preprocessOptions;
```

**لماذا هذه الإعدادات؟** Auto‑deskew يتعامل مع معظم الانحناءات الشائعة (حتى ~15°). مستوى الضوضاء المتوسط يناسب المستندات الممسوحة النموذجية؛ يمكنك رفعه إلى `High` للمسحات المشبعة جدًا، لكن احذر من فقدان الأحرف الصغيرة. التحويل إلى ثنائي هو أساس **black and white OCR**—يزيل التدرجات الرمادية الدقيقة التي تربك المحرك.

## الخطوة 4: تشغيل التعرف على صورة مشوشة

مع تحضير المحرك، قدم له مسار الصورة المشكلة. طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على النص المستخرج ودرجات الثقة.

```csharp
// Step 4: Recognize text from a skewed and noisy image
// Replace the path with your actual image location
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/skewed_noisy.jpg");

// Output the raw text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

إذا سارت الأمور بسلاسة، سترى كتلة نص نظيفة في وحدة التحكم. كما يتيح المحرك الوصول إلى `ocrResult.Confidence` إذا احتجت مقياسًا رقميًا لـ **improve OCR accuracy**.

## الخطوة 5: التحقق من النتيجة وضبطها للحصول على دقة أفضل

رؤية المخرجات أمر رائع، لكن قد تلاحظ بعض الأخطاء—خاصةً مع الخطوط غير المعتادة. إليك بعض الفحوصات السريعة:

1. **Inspect Confidence** – القيم التي تقل عن 0.7 غالبًا ما تشير إلى منطقة مشكلة. يمكنك تسجيلها وتقرير ما إذا كنت ستعيد المعالجة بمستوى `DenoiseLevel` أعلى.
2. **Adjust Binarization Threshold** – يتيح لك Aspose تمرير عتبة مخصصة عبر `PreprocessOptions.BinarizationThreshold`. الأرقام الأقل تحتفظ بالمزيد من الرمادي، والأرقام الأعلى تفرض أبيض وأسود أكثر صرامة.
3. **Crop or Resize** – إذا كانت الصورة ضخمة، قلل حجمها إلى ~150 DPI قبل تمريرها إلى المحرك؛ هذا يسرّع المعالجة ويمكن أن يزيد الدقة فعليًا.

```csharp
// Example: Increase denoise for a very dirty scan
ocrEngine.PreprocessOptions.DenoiseLevel = DenoiseLevel.High;

// Re‑run recognition
var refinedResult = ocrEngine.Recognize("YOUR_DIRECTORY/very_dirty.jpg");
Console.WriteLine(refinedResult.Text);
```

## إضافي: استخدام Black and White OCR للحصول على نتائج أفضل

أحيانًا قد تسمع المطورين يقولون “اكتفِ بالتحويل إلى تدرج الرمادي”—لكن نهج **black and white OCR** غالبًا ما يتفوق عليه، خاصةً عندما يكون للمواد المصدر إضاءة غير متساوية. بفرض صورة ثنائية، تزيل الظلال الدقيقة التي قد يخطئ المحرك في اعتبارها أحرفًا.

إذا رغبت في تجربة المزيد، يمكنك إنشاء الصورة الثنائية بنفسك وتمريرها إلى المحرك:

```csharp
// Generate a binary bitmap manually (optional)
Bitmap binaryBitmap = ocrEngine.PreprocessOptions.ApplyFilters(
    Image.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg")
);

// Pass the bitmap directly
var bitmapResult = ocrEngine.Recognize(binaryBitmap);
Console.WriteLine(bitmapResult.Text);
```

هذا يمنحك سيطرة كاملة على خط أنابيب المعالجة المسبقة، وهو مفيد عندما تحتاج إلى دمج فلاتر مخصصة أو مكتبات صور من طرف ثالث.

## مثال كامل يعمل

بجمع كل ذلك، إليك تطبيق وحدة تحكم جاهز للتشغيل يمكنك نسخه ولصقه في مشروع C# جديد:

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (auto‑deskew, denoise, binarize)
        PreprocessOptions preprocessOptions = new PreprocessOptions
        {
            AutoDeskew = true,
            DenoiseLevel = DenoiseLevel.Medium,
            Binarize = true
        };
        ocrEngine.PreprocessOptions = preprocessOptions;

        // 3️⃣ Recognize the image (replace with your file path)
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 4️⃣ Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);

        // 5️⃣ Optional: tweak settings if confidence is low
        if (ocrResult.Confidence < 0.7)
        {
            Console.WriteLine("\nLow confidence detected – increasing denoise level.");
            ocrEngine.PreprocessOptions.DenoiseLevel = DenoiseLevel.High;
            var retryResult = ocrEngine.Recognize("YOUR_DIRECTORY/skewed_noisy.jpg");
            Console.WriteLine("=== Refined Output ===");
            Console.WriteLine(retryResult.Text);
        }
    }
}
```

**المخرجات المتوقعة في وحدة التحكم**

```
=== OCR Output ===
The quick brown fox jumps over the lazy dog.

=== Refined Output ===
The quick brown fox jumps over the lazy dog.
```

*بالطبع سيختلف النص الفعلي لديك، لكن يجب أن تلاحظ نفس التنسيق النظيف.*

## الخاتمة

لقد أوضحنا لك الآن كيفية **preprocess image for OCR** باستخدام Aspose.OCR، ولماذا كل خطوة—auto‑deskew، denoise، وتحويل إلى أبيض وأسود—تلعب دورًا محوريًا في **improve OCR accuracy**. باتباع الكود أعلاه ستحصل على نتائج موثوقة على مسحات مشوشة ومائلة دون الحاجة للبحث في الوثائق.

ما الخطوة التالية؟ جرّب دمج هذا الخط الأنابيب مع إعدادات خاصة باللغة (مثال: `ocrEngine.Language = Language.English`) أو مرّر الصورة المنقحة إلى نموذج NLP لاحق. يمكنك أيضًا تجربة `BinarizationThreshold` لضبط تأثير **black and white OCR** للوصلات منخفضة التباين أو الملاحظات المكتوبة يدويًا.

لا تتردد في ترك تعليق إذا واجهت أي صعوبات، أو مشاركة حيلك الخاصة للحصول على دقة أعلى من OCR. برمجة سعيدة، ولتكن نصوصك دائمًا قابلة للقراءة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}