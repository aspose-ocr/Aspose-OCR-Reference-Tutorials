---
category: general
date: 2026-03-26
description: كيفية تصحيح إمالة الصورة باستخدام Aspose OCR في C#. تعلم كيفية تمهيد
  الصورة للتعرف الضوئي على الأحرف، وتقليل الضوضاء، والتعرف على النص من الصورة بكفاءة.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from image
- how to reduce noise
- how to use aspose
language: ar
og_description: كيفية تصحيح انحراف الصورة باستخدام Aspose OCR في C#. تعلم تمهيد الصورة
  للتعرف الضوئي على الأحرف، تقليل الضوضاء، والتعرف على النص من الصورة بكفاءة.
og_title: كيفية تصحيح ميل الصورة باستخدام Aspose OCR – دليل C# الكامل
tags:
- Aspose
- OCR
- C#
- Image Processing
title: كيفية إلغاء إمالة الصورة باستخدام Aspose OCR – الدليل الكامل لـ C#
url: /ar/net/skew-angle-calculation/how-to-deskew-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح انحراف الصورة باستخدام Aspose OCR – دليل C# الكامل

تصحيح انحراف الصورة هو عائق شائع عندما تحاول استخراج النص من صورة مائلة. إذا واجهت صعوبة في **preprocess image for OCR**، فستقدر ملفًا نظيفًا ومقوّسًا يَقلل أيضًا **reduces noise** قبل أن **recognize text from image**.  

في هذا الدرس سنستعرض الخطوات الدقيقة لبناء خط أنابيب الفلاتر باستخدام Aspose OCR، ونشرح لماذا كل فلتر مهم، ونعرض لك برنامج C# جاهز للتنفيذ يطبع النص المستخرج. لا روابط غامضة مثل “see the docs”—كل ما تحتاجه موجود هنا.

## ما ستحتاجه

- **Aspose.OCR for .NET** (أحدث حزمة NuGet، مثال: 23.12).  
- .NET 6 أو أحدث (الكود يُترجم على .NET Framework 4.8 أيضًا).  
- صورة نموذجية مائلة ومشوّشة (سنطلق عليها `skewed_noisy.png`).  
- Visual Studio، Rider، أو أي محرر تفضله—بدون تعقيدات.

هذا كل شيء. إذا كان لديك مشروع بالفعل، فقط أضف مرجع NuGet:

```bash
dotnet add package Aspose.OCR
```

الآن لنغوص في التفاصيل.

## كيفية تصحيح انحراف الصورة – بناء خط أنابيب الفلاتر

جوهر الحل هو **filter pipeline**. فكر فيه كخط تجميع حيث يقوم كل فلتر بتنظيف مشكلة معينة. بحلول الوقت الذي يصل فيه الصورة إلى محرك OCR تكون جاهزة عمليًا للقراءة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // 1️⃣  Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣  Assemble a pipeline: deskew → denoise → optional channel filter
        FilterPipeline filterPipeline = new FilterPipeline();
        filterPipeline.Add(new AdaptiveDeskewFilter());               // auto‑corrects rotation
        filterPipeline.Add(new NoiseReductionFilter());              // AI‑based denoise
        filterPipeline.Add(new ColorChannelFilter(Channel.Red));     // focus on the red channel (optional)

        // 3️⃣  Hook the pipeline to the engine
        ocrEngine.Filters = filterPipeline;

        // 4️⃣  Load the image you want to process
        OcrImage inputImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // 5️⃣  Run OCR – the engine will first apply the pipeline
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // 6️⃣  Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

**لماذا هذا يعمل:**  
- `AdaptiveDeskewFilter` يحلل خط أساس الصورة ويعيد تدويره إلى 0°، وهو خطوة *how to deskew image*.  
- `NoiseReductionFilter` يستخدم نموذج AI خفيف لتنعيم البقع دون تشويش الأحرف—مجاوبًا على *how to reduce noise*.  
- `ColorChannelFilter` اختياري لكنه مفيد عندما يبرز النص في قناة معينة (الأحمر في هذه الحالة).  

يعمل خط الأنابيب **قبل** أن ينظر محرك OCR إلى البكسلات، لذا تحصل على لوحة أنظف للتعرف.

## معالجة الصورة مسبقًا لـ OCR – تقليل الضوضاء والقناة اللونية

إذا تخطيت فلتر تقليل الضوضاء، ستلاحظ غالبًا أحرفًا مشوهة، خاصةً على الإيصالات الممسوحة أو الصور ذات الإضاءة المنخفضة. إليك تجربة سريعة يمكنك تجربتها:

```csharp
// Swap the order: denoise first, then deskew
filterPipeline = new FilterPipeline();
filterPipeline.Add(new NoiseReductionFilter());
filterPipeline.Add(new AdaptiveDeskewFilter());
ocrEngine.Filters = filterPipeline;
```

تشغيل المحرك بترتيب مبدل قد ينتج أحيانًا نتيجة أكثر وضوحًا على الصور ذات الحبيبات الكثيفة. السبب؟ إزالة الضوضاء أولاً يمنح خوارزمية تصحيح الانحراف خريطة حواف أنظف للعمل معها.

**نصيحة احترافية:** إذا كانت صورك المصدرية بالأبيض والأسود، احذف `ColorChannelFilter` تمامًا. فهو يضيف فقط عبءً بسيطًا.

## التعرف على النص من الصورة – تشغيل محرك OCR

بمجرد ربط خط الأنابيب، تقوم استدعاء `Recognize` بالعمل الشاق. تحت الغطاء، يقوم Aspose OCR بـ:

1. التحويل إلى ثنائي (يحوّل الصورة إلى أبيض‑أسود).  
2. تحليل التخطيط (يكشف الخطوط، الأعمدة، الجداول).  
3. تقسيم الأحرف (يفصل كل رمز).  
4. تصنيف الشبكة العصبية (يربط الرموز بـ Unicode).  

كل ذلك يحدث في بضع ميليثانية على معالج حديث. خاصية `OcrResult.Text` تُعيد سلسلة نصية عادية، جاهزة للحفظ أو الفهرسة أو تمريرها إلى نظام آخر.

### النتيجة المتوقعة

إذا كانت `skewed_noisy.png` تحتوي على العبارة “Invoice #12345 – Total $89.99”، سيطبع الطرفية:

```
Invoice #12345 – Total $89.99
```

إذا لاحظت فواصل أسطر إضافية أو رموز غريبة، تحقق مرة أخرى من مستوى الضوضاء؛ إضافة `NoiseReductionFilter` ثانية غالبًا ما يساعد.

## كيفية تقليل الضوضاء – نصائح وحالات خاصة

- **تمريرات متعددة:** `filterPipeline.Add(new NoiseReductionFilter());` مرتين يمكن أن يكون مفيدًا للمسحات ذات الحبيبات الشديدة.  
- **تعديل العتبة:** الفلتر يتيح خاصية `Strength` (0‑100). القيم الأقل تحافظ على التفاصيل الدقيقة؛ القيم الأعلى تنعم بقوة.  
- **أهمية تنسيق الملف:** PNG يحافظ على البيانات بدون فقد، بينما JPEG يضيف تشوهات ضغط قد يصعب على مُزيل الضوضاء التعامل معها. يُفضَّل PNG للمعالجة المسبقة.

```csharp
var heavyNoiseFilter = new NoiseReductionFilter { Strength = 80 };
filterPipeline.Add(heavyNoiseFilter);
```

## كيفية استخدام Aspose – التثبيت، الترخيص، والملاحظات الهامة

Aspose مكتبة تجارية، لكنها تُوفر **نسخة تجريبية مجانية** تعمل حتى 30 يومًا. لفتح جميع المميزات:

```csharp
// Somewhere early in your app (e.g., Main)
Aspose.OCR.License license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

ضع ملف `.lic` بجانب ملف التنفيذ أو دمجه كموارد.  

**مشكلة شائعة:** نسيان ضبط الترخيص يؤدي إلى إضافة علامة مائية إلى النص المعترف به. لا يزال المحرك يعمل، لكن الناتج يحتوي على سلاسل “Aspose OCR”.  

أيضًا، المكتبة **آمنة للخطوط** للعمليات القرائية، لكن `OcrEngine` نفسه لا ينبغي مشاركته عبر الخيوط إلا إذا أنشأت نسخة جديدة لكل طلب.

## مثال كامل يعمل – جمع كل الأجزاء معًا

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في تطبيق Console:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // OPTIONAL: Apply your Aspose license
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Build filter pipeline
        FilterPipeline pipeline = new FilterPipeline();
        pipeline.Add(new AdaptiveDeskewFilter());               // how to deskew image
        pipeline.Add(new NoiseReductionFilter());              // how to reduce noise
        pipeline.Add(new ColorChannelFilter(Channel.Red));     // optional color focus

        // 3️⃣ Attach pipeline
        ocrEngine.Filters = pipeline;

        // 4️⃣ Load image
        string imagePath = @"YOUR_DIRECTORY/skewed_noisy.png";
        OcrImage img = OcrImage.FromFile(imagePath);

        // 5️⃣ Perform OCR
        OcrResult result = ocrEngine.Recognize(img);

        // 6️⃣ Output result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
```

شغّل البرنامج، وسترى النص المنقح يُطبع في الطرفية. إذا رغبت بكتابة الناتج إلى ملف:

```csharp
System.IO.File.WriteAllText("output.txt", result.Text);
```

## النتيجة البصرية – قبل وبعد

فيما يلي توضيح placeholder يُظهر الصورة المائلة الأصلية على اليسار والإصدار المصحح والمُنقٍّ على اليمين.

![How to deskew image – before and after processing](https://example.com/deskew-before-after.png "how to deskew image example")

*نص بديل:* how to deskew image – مقارنة بصرية بين الأصل والمعالجة.

## الخلاصة

لقد غطينا **how to deskew image** باستخدام Aspose OCR، واستعرضنا **preprocess image for OCR** مع تقليل الضوضاء، وأظهرنا طريقة نظيفة لـ **recognize text from image** في C#. من خلال ربط `AdaptiveDeskewFilter`، `NoiseReductionFilter`، و`ColorChannelFilter` الاختياري، تحصل على خط أنابيب قوي يعمل على معظم الصور الواقعية.

ما الخطوة التالية؟ جرّب استبدال فلتر القناة الحمراء بـ

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}