---
category: general
date: 2026-03-15
description: قم بتنفيذ التعرف الضوئي على الأحرف (OCR) على الصورة باستخدام Aspose OCR
  في C#. تعلم كيفية معالجة الصورة مسبقًا قبل الـ OCR لتحسين دقة التعرف الضوئي على
  الأحرف والتعرف على النص من الصورة بكفاءة.
draft: false
keywords:
- perform OCR on image
- recognize text from image
- improve OCR accuracy
- preprocess image before OCR
language: ar
og_description: قم بإجراء التعرف الضوئي على الأحرف (OCR) على الصورة باستخدام Aspose
  OCR. يوضح هذا الدليل كيفية معالجة الصورة مسبقًا قبل الـ OCR، تحسين دقة الـ OCR،
  والتعرف على النص من الصورة باستخدام C#.
og_title: إجراء التعرف الضوئي على الأحرف في الصورة – تعزيز الدقة مع Aspose OCR
tags:
- C#
- Aspose OCR
- Image Processing
title: إجراء التعرف الضوئي على الحروف في الصورة – تعزيز الدقة باستخدام Aspose OCR
url: /ar/net/ocr-optimization/perform-ocr-on-image-boost-accuracy-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تنفيذ OCR على الصورة – تحسين الدقة باستخدام Aspose OCR

هل احتجت يومًا إلى **تنفيذ OCR على الصورة** لكنك حصلت على مخرجات مشوشة؟ لست وحدك. في العديد من المشاريع الواقعية، يمكن أن يتسبب مسح ضوضائي أو مائل في إرباك حتى أفضل محركات OCR، لتظهر لك نصوصًا تبدو كأنها مكتوبة بواسطة قطة تمشي على لوحة المفاتيح.

الأمر هو أن الصورة الخام ليست سوى نصف المعركة. من خلال **معالجة الصورة قبل OCR**، يمكنك تحسين **دقة OCR** بشكل كبير وأخيرًا **استخراج النص من الصورة** بشكل موثوق. في هذا الدرس سنستعرض مثالًا كاملًا وجاهزًا للتنفيذ بلغة C# يوضح بالضبط كيفية القيام بذلك باستخدام Aspose.OCR.

سنتناول:

* تثبيت حزمة NuGet الخاصة بـ Aspose.OCR.  
* بناء خط أنابيب للمعالجة المسبقة (إزالة الميل، إزالة الضوضاء، تعزيز التباين، التحويل إلى أبيض‑أسود).  
* تشغيل محرك OCR وطباعة النص المستخرج.  

بدون إطالة، بدون اختصارات “انظر الوثائق لاحقًا” — مجرد حل متكامل يمكنك إدراجه في تطبيق كونسول الآن.

---

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي:

* **.NET 6+** (أو .NET Framework 4.6.2+).  
* حزمة NuGet حديثة من **Aspose.OCR** (الإصدار 23.10 أو أحدث).  
* ملف صورة غير مرتب قليلًا — مثلاً مائل، ضوضائي، منخفض التباين.  
* Visual Studio، VS Code، أو أي بيئة تطوير تفضلها.

هذا كل شيء. إذا كنت تفتقد حزمة NuGet، نفّذ:

```bash
dotnet add package Aspose.OCR
```

الآن لنبدأ العمل.

---

## ## تنفيذ OCR على الصورة – إعداد المحرك

الخطوة الأولى هي إنشاء كائن `OcrEngine`. هذا الكائن هو قلب Aspose OCR؛ فهو يحمل الإعدادات، خطوط الأنابيب، ومنطق التعرف الفعلي.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System.Drawing;          // For Image class
using System;                  // For Console

// Step 1: Instantiate the OCR engine
var ocrEngine = new OcrEngine();
```

> **لماذا هذا مهم:**  
> إنشاء المحرك يمنحك لوحة نظيفة. يمكنك لاحقًا تعديل الإعدادات (اللغة، وضع التعرف، إلخ) دون الحاجة لتغيير باقي الكود.

---

## ## معالجة الصورة قبل OCR – بناء خط الأنابيب

المسحات الخام نادرًا ما تكون مثالية. يمكن لخط أنابيب معالجة مسبقة جيد أن **يحسن دقة OCR** بنسبة تصل إلى 30 % في بعض الحالات. أدناه نربط أربعة فلاتر:

| الفلتر | ما الذي يفعله | القيم النموذجية |
|--------|--------------|----------------|
| `DeskewFilter` | يكتشف ويصحح الدوران | `Angle = 0.0` (اكتشاف تلقائي) |
| `DenoiseFilter` | يزيل البقع والحبوب | `Strength = 70` (من 100) |
| `ContrastBoostFilter` | يجعل النص الداكن بارزًا | `Strength = 40` |
| `BinarizationFilter` | يحول الصورة إلى أبيض وأسود نقي | `Threshold = 128` |

```csharp
// Step 2: Create a preprocessing pipeline
var preprocessingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { Angle = 0.0 })               // auto‑detect skew angle
    .Add(new DenoiseFilter { Strength = 70 })           // reduce noise
    .Add(new ContrastBoostFilter { Strength = 40 })     // enhance contrast
    .Add(new BinarizationFilter { Threshold = 128 });   // convert to B/W

// Attach the pipeline to the OCR engine
ocrEngine.Configuration.PreProcessing = preprocessingPipeline;
```

> **نصيحة احترافية:** إذا كانت صورك المصدرية نظيفة بالفعل، يمكنك تخطي `DenoiseFilter` أو تقليل قيمة `Strength`. الإفراط في الفلترة قد يمحو الأحرف الخفيفة.

---

## ## تحميل الصورة – أين تجد ملفك

الآن نوجه المحرك إلى الصورة التي نريد قراءتها. طريقة `Image.FromFile` تعمل مع أي صيغة يدعمها System.Drawing (JPEG، PNG، BMP، إلخ).

```csharp
// Step 3: Load the image you want to recognize
var inputImagePath = @"C:\Images\skewed_noisy.jpg";   // change to your path
var inputImage = Image.FromFile(inputImagePath);
```

> **حالة خاصة:** إذا كان مسار الملف يحتوي على مسافات أو أحرف يونيكود، احطه في سلسلة حرفية (`@"..."`) كما هو موضح أعلاه. أيضًا، احرص دائمًا على معالجة استثناء `FileNotFoundException` في الكود الإنتاجي.

---

## ## استخراج النص من الصورة – تشغيل محرك OCR

بعد تكوين المحرك وتحميل الصورة، يصبح التعرف الفعلي سطرًا واحدًا. النتيجة تحتوي على النص المستخرج بالإضافة إلى مقاييس الثقة التي يمكنك فحصها لاحقًا.

```csharp
// Step 4: Perform OCR and get the result
var ocrResult = ocrEngine.Recognize(inputImage);

// Display the recognized text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مشابهًا لـ:

```
=== OCR Output ===
Invoice #12345
Date: 03/12/2026
Total: $1,250.00
```

إذا كان الناتج غير دقيق، عدّل قيم الفلاتر أو جرّب قيمة `Threshold` مختلفة. التعديلات الصغيرة غالبًا ما تُحدث فرقًا كبيرًا.

---

## ## المشكلات الشائعة وكيفية إصلاحها

1. **النتيجة فارغة أو مليئة بالحروف العشوائية**  
   *تحقق من خط الأنابيب.* قد يؤدي الإفراط في إزالة الضوضاء إلى محو الخطوط الرفيعة. قلل `Strength` أو علق الفلتر مؤقتًا.

2. **لم يتم تصحيح الميل**  
   يعمل `DeskewFilter` بأفضل شكل على المستندات التي يكون خط النص فيها أفقيًا تقريبًا. إذا كانت الصورة مائلة بأكثر من 15°، قد تحتاج إلى تدويرها يدويًا باستخدام `RotateFlip`.

3. **الأحرف غير اللاتينية غير مُعترف بها**  
   بشكل افتراضي يستخدم Aspose OCR نماذج اللغة الإنجليزية. اضبط `ocrEngine.Configuration.Language` إلى رمز ISO المناسب (مثال: `"fr"` للفرنسية) قبل استدعاء `Recognize`.

```csharp
ocrEngine.Configuration.Language = "fr";   // for French text
```

4. **الأداء بطيء**  
   إذا كنت تعالج مئات الصفحات، أعد استخدام كائن `OcrEngine` واحد فقط واستبدل كائن `Image` في كل دورة. إنشاء محرك جديد في كل مرة يضيف عبئًا غير ضروري.

---

## ## النتيجة البصرية – كيف تبدو الصورة المعالجة

فيما يلي توضيح سريع قبل‑وبعد (قد يختلف الناتج الفعلي لديك).

![Perform OCR on Image result](https://example.com/ocr-before-after.png "Perform OCR on Image – preprocessed vs original")

*النص البديل:* “تنفيذ OCR على الصورة – مقارنة بين المسح الضوضائي الأصلي والإصدار المعالج جاهزًا لـ OCR”.

---

## ## الختام: مثال كامل يعمل

انسخ المقتطف الكامل أدناه إلى مشروع كونسول جديد (`dotnet new console`) واضغط **F5**. سيُترجم، يُنفّذ، ويطبع النص المستخرج على الشاشة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System.Drawing;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build a preprocessing pipeline (improve OCR accuracy)
        var preprocessingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { Angle = 0.0 })               // auto‑detect skew angle
            .Add(new DenoiseFilter { Strength = 70 })           // reduce noise
            .Add(new ContrastBoostFilter { Strength = 40 })     // enhance contrast
            .Add(new BinarizationFilter { Threshold = 128 });   // convert to B/W

        ocrEngine.Configuration.PreProcessing = preprocessingPipeline;

        // 3️⃣ Load the image you want to read
        var imagePath = @"YOUR_DIRECTORY\skewed_noisy.jpg";   // ← update this path
        var inputImage = Image.FromFile(imagePath);

        // 4️⃣ Run OCR – recognize text from image
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Show the result
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**الناتج المتوقع:** يطبع الكونسول النسخة النصية من ما كان موجودًا في الصورة — سواءً فاتورة، مسح جواز سفر، أو ملاحظة مكتوبة يدويًا.

---

## ## الخطوات التالية – التعمق

* **معالجة دفعات:** ضع استدعاء التعرف داخل حلقة `foreach` لمعالجة مجلد من الصور.  
* **حزم اللغات:** ثبّت بيانات لغة إضافية من Aspose لتتمكن من **استخراج النص من الصورة** باللغات الإسبانية، الألمانية، الصينية، إلخ.  
* **معالجة ما بعد مخصصة:** استخدم تعبيرات نمطية لاستخراج التواريخ، المبالغ، أو أرقام الهوية من سلسلة OCR.  
* **مكتبات بديلة:** قارن النتائج مع Tesseract أو Microsoft Azure Computer Vision لترى كيف يتفوق **معالجة الصورة قبل OCR** عبر المنصات المختلفة.

---

## ## الخلاصة

لقد استعرضنا كيفية **تنفيذ OCR على الصورة** باستخدام Aspose OCR، بنينا خط أنابيب معالجة ذكي، ورأينا أن **معالجة الصورة قبل OCR** يمكن أن **يحسن دقة OCR** بشكل كبير. باتباع الخطوات أعلاه يمكنك الآن **استخراج النص من الصورة** في أي تطبيق C# — لا مزيد من الإحباط من المخرجات المشوشة.

لا تتردد في تجربة قيم الفلاتر، تجربة صيغ صور مختلفة، أو دمج هذا الكود في خدمة معالجة مستندات أكبر. السماء هي الحد عندما يصبح خط أنابيب OCR ثابتًا.

هل لديك أسئلة أو حالة استخدام مميزة؟ اترك تعليقًا أسفل المقال، وبرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}