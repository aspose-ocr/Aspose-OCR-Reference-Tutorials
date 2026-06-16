---
category: general
date: 2026-02-17
description: تشغيل OCR على صورة باستخدام Aspose OCR في C#. تعلّم كيفية استخراج النص
  من ملف JPG، ومعالجة الصورة مسبقًا للـ OCR، وتحميل الصورة للـ OCR مع كود خطوة بخطوة.
draft: false
keywords:
- run OCR on image
- extract text from jpg
- preprocess image for OCR
- load image for OCR
language: ar
og_description: تشغيل OCR على الصورة باستخدام Aspose OCR في C#. يوضح هذا الدليل كيفية
  استخراج النص من ملف JPG، ومعالجة الصورة مسبقًا، وتحميل الصورة للتعرف الضوئي على
  الأحرف.
og_title: تشغيل OCR على الصورة باستخدام Aspose OCR – دليل C# الكامل
tags:
- Aspose OCR
- C#
- Image Processing
title: تشغيل OCR على صورة باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/text-recognition/run-ocr-on-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل OCR على صورة باستخدام Aspose OCR – دليل C# الكامل

هل احتجت يوماً إلى **تشغيل OCR على ملفات الصور** لكن لم تعرف من أين تبدأ؟ في العديد من التطبيقات الواقعية – مثل ماسحات الفواتير أو متتبعي الإيصالات – العقبة الأولى هي استخراج نص موثوق من ملف JPEG. الخبر السار؟ باستخدام Aspose OCR يمكنك **تشغيل OCR على ملفات الصور** ببضع أسطر من كود C#، وستتعلم أيضاً كيفية **استخراج النص من jpg**، **معالجة الصورة مسبقاً لـ OCR**، و**تحميل الصورة لـ OCR** دون الحاجة للبحث في وثائق متفرقة.

في هذا البرنامج التعليمي سنستعرض مثالاً كاملاً جاهزاً للنسخ واللصق يوضح بالضبط كيفية إعداد المحرك، إضافة مرشحات المعالجة المسبقة المفيدة، إمداد الصورة إلى المُعرّف، وطباعة النتيجة على وحدة التحكم. في النهاية ستحصل على برنامج مستقل يمكنك إدراجه في أي مشروع .NET والبدء في استخراج النص من الصور فوراً.

## ما الذي ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل أيضاً على .NET Core)  
- حزمة NuGet الخاصة بـ Aspose.OCR (`Install-Package Aspose.OCR`)  
- صورة JPEG تجريبية (`input.jpg`) موجودة في مجلد يمكنك الإشارة إليه  
- فهم أساسي لصياغة C# (لا شيء معقد)

إذا كان لديك كل هذه المكوّنات جاهزة، رائع – لنبدأ. إذا لم يكن كذلك، احصل على حزمة NuGet وصورة اختبار؛ باقي الدليل يفترض أنك قمت بذلك.

## الخطوة 1: إنشاء محرك OCR – جوهر تشغيل OCR على صورة

أول شيء يجب القيام به لت **تشغيل OCR على بيانات الصورة** هو إنشاء كائن `OcrEngine`. هذا الكائن يحمل جميع الإعدادات والحالة المطلوبة للتعرف.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // Step 1 – create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **لماذا هذا مهم:** `OcrEngine` هو البوابة إلى خط أنابيب التعرف في Aspose. بدون هذا الكائن لا يمكنك الوصول إلى المرشحات أو حزم اللغات أو طريقة `Recognize`.

## الخطوة 2: إضافة مرشحات المعالجة المسبقة – تحسين الدقة عند استخراج النص من JPG

الصور الملتقطة مباشرة من الكاميرا نادراً ما تكون مثالية. الزوايا المائلة أو الضوضاء العشوائية قد تعيق حتى أفضل خوارزميات OCR. إضافة بعض المرشحات قبل **استخراج النص من jpg** يمكن أن يحسّن النتائج بشكل كبير.

```csharp
        // Step 2 – add preprocessing filters
        // Deskew corrects rotation; DenoiseGaussian reduces visual noise
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });
```

> **نصيحة احترافية:** إذا كانت صورك المصدرية نظيفة بالفعل، يمكنك تخطي `DenoiseGaussianFilter`. الإفراط في التنعيم قد يمحو الأحرف الخفيفة.

## الخطوة 3: تحميل الصورة لـ OCR – إمداد المحرك بملف JPEG

الآن يأتي الجزء الذي **تحمّل الصورة لـ OCR** فيه. توفر Aspose أداة مساعدة `ImageStream.FromFile` التي تغلف مسار الملف في تدفق يفهمه المحرك.

```csharp
        // Step 3 – specify the path to the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        // Load the image and run OCR in one call
        var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));
```

> **حالة حافة:** إذا لم يكن الملف موجوداً، فإن `FromFile` يطرح استثناء `FileNotFoundException`. اح-wrap الاستدعاء داخل try/catch إذا كنت تتوقع ملفات مفقودة أثناء التشغيل.

## الخطوة 4: استرجاع وعرض النص المُعترف به

أخيراً، بعد أن ينتهي المحرك من المعالجة، يمكنك الوصول إلى النتيجة النصية عبر الخاصية `Text`. طباعتها على وحدة التحكم كافية لعرض سريع، لكن يمكنك أيضاً كتابة النص إلى قاعدة بيانات أو ملف نصي.

```csharp
        // Step 4 – output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**الناتج المتوقع**

```
=== OCR Result ===
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
```

المحتوى الفعلي سيعتمد على الصورة التي تستخدمها، لكن يجب أن ترى كتلة نصية منسقة بدلاً من رموز غير مفهومة.

![مخطط يوضح خط أنابيب OCR – تشغيل OCR على صورة، معالجة مسبقة، تحميل، التعرف](/images/ocr-pipeline.png "run OCR on image pipeline diagram")

### لماذا كل خطوة مهمة

| الخطوة | الغرض | ما يحدث إذا تم تخطيها |
|------|---------|--------------------------|
| **إنشاء المحرك** | يهيئ البُنى الداخلية | لا يتوفر مُعرّف – ستحصل على `NullReferenceException`. |
| **إضافة المرشحات** | يحسّن الدقة عبر تصحيح الدوران والضوضاء | الصور المائلة أو الضوضائية تنتج مخرجات مشوهة. |
| **تحميل الصورة** | يزوّد المحرك بالبيتماب الخام | لا شيء للمعالجة، ينتج حقل `Text` فارغ. |
| **قراءة النتيجة** | يستخرج السلسلة النصية لاستخدامها لاحقاً | تقوم بتشغيل OCR لكن لا ترى النتيجة – غير مفيد! |

## تنويعات شائعة وكيفية تعديل العملية

### تغيير حزمة اللغة

يدعم Aspose OCR عدة لغات مباشرة. إذا احتجت إلى **تشغيل OCR على ملفات الصور** التي تحتوي على نص فرنسي أو ألماني، عيّن الخاصية `Language` قبل استدعاء `Recognize`.

```csharp
ocrEngine.Language = OcrLanguage.French;
```

### معالجة ملفات PDF متعددة الصفحات

إذا كان المصدر PDF متعدد الصفحات بدلاً من JPEG واحد، يمكنك تحويل كل صفحة إلى صورة أولاً (باستخدام Aspose.PDF) ثم إمداد كل صورة إلى نفس خط الأنابيب. التكرار عبر الصفحات سهل:

```csharp
foreach (var pageImage in pdfPagesAsImages)
{
    var result = ocrEngine.Recognize(ImageStream.FromMemory(pageImage));
    Console.WriteLine(result.Text);
}
```

### التعامل مع الملفات الكبيرة

عند معالجة صور عالية الدقة، قد يرتفع استهلاك الذاكرة. فكر في تقليل حجم الصورة قبل **تحميل الصورة لـ OCR**:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

var loadOptions = new JpegLoadOptions { Width = 1024, Height = 768 };
using (var img = (Image)Image.Load(imagePath, loadOptions))
{
    var stream = new MemoryStream();
    img.Save(stream, new JpegOptions());
    var ocrResult = ocrEngine.Recognize(ImageStream.FromMemory(stream.ToArray()));
}
```

## مثال كامل جاهز للتنفيذ

فيما يلي البرنامج الكامل الذي يدمج كل ما ناقشناه. انسخه‑الصقه في مشروع وحدة تحكم جديد، استبدل `YOUR_DIRECTORY` بمسار المجلد الذي يحتوي على `input.jpg`، ثم اضغط **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Add useful preprocessing filters
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });

        // 3️⃣ Load the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        try
        {
            // Recognize text – this is where we actually run OCR on image
            var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));

            // 4️⃣ Print the extracted text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

### التحقق من النتيجة

1. شغّل البرنامج.  
2. افحص وحدة التحكم – يجب أن ترى النص الموجود في `input.jpg`.  
3. إذا كان الناتج مشوشاً، جرّب تعديل قيمة `Sigma` في `DenoiseGaussianFilter` أو أضف مرشحات إضافية مثل `ContrastEnhancementFilter`.

## ملخص وخطوات مستقبلية

لقد غطينا للتو كيفية **تشغيل OCR على ملفات الصور** باستخدام Aspose OCR، من إعداد المحرك إلى الحصول على نص نظيف وقابل للقراءة. النقاط الرئيسية:

- إنشاء كائن `OcrEngine`.  
- **معالجة الصورة مسبقاً لـ OCR** باستخدام مرشحات مثل `DeskewFilter` و `DenoiseGaussianFilter`.  
- **تحميل الصورة لـ OCR** عبر `ImageStream.FromFile`.  
- استدعاء `Recognize` وقراءة `ocrResult.Text` لـ **استخراج النص من jpg**.

هل تريد التعمق أكثر؟ جرّب الأفكار التالية:

- **معالجة دفعات** – قراءة مجلد من JPEGs وإخراج كل نتيجة إلى ملف `.txt` منفصل.  
- **التكامل مع Azure Blob Storage** – سحب الصور من السحابة، تشغيل OCR، ثم تخزين النص مرة أخرى.  
- **دمج مع NLP** – إمداد النص المستخرج إلى نموذج فهم اللغة لتصنيف الفواتير تلقائياً.  

لا تتردد في تجربة تركيبات مرشحات مختلفة، حزم لغات، أو حتى التحويل إلى PNGs و TIFFs – نفس خط الأنابيب يعمل طالما **تحمّلت الصورة لـ OCR** بشكل صحيح.

---

إذا واجهت أي صعوبات، اترك تعليقاً أدناه أو راجع وثائق Aspose OCR للإعدادات المتقدمة. Happy coding, and enjoy turning pictures into searchable text!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}