---
category: general
date: 2026-03-07
description: تعلم كيفية تصحيح انحراف الصورة، تعزيز التباين، واستخراج النص من المسح
  الضوئي باستخدام Aspose OCR. قم بتنفيذ OCR على الصورة مع مثال كامل بلغة C# وحمّل
  الصورة للـ OCR بسهولة.
draft: false
keywords:
- how to deskew image
- extract text from scan
- how to boost contrast
- perform ocr on image
- load image for OCR
language: ar
og_description: تعلم كيفية تصحيح انحراف الصورة، تعزيز التباين، واستخراج النص من المسح
  الضوئي باستخدام Aspose OCR في C#. قم بإجراء OCR على الصورة مع كود خطوة‑بخطوة.
og_title: كيفية تصحيح إمالة الصورة وتشغيل OCR في C# – دليل كامل
tags:
- C#
- OCR
- Image Processing
title: كيفية تصحيح انحراف الصورة وتشغيل OCR في C# – دليل كامل
url: /ar/net/ocr-optimization/how-to-deskew-image-and-run-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح انحراف الصورة وتشغيل OCR في C# – دليل شامل

إذا تساءلت يومًا **كيفية تصحيح انحراف الصورة** قبل تشغيل OCR، فأنت في المكان الصحيح. في هذا الدرس سنرشدك إلى تحسين التباين، تحميل صورة لـ OCR، وأخيرًا **استخراج النص من المسح** باستخدام Aspose OCR.  

سواء كنت تقوم برقمنة الإيصالات القديمة، أو تنظيف العقود الممسوحة ضوئيًا، أو تحتاج فقط إلى طريقة موثوقة لقراءة النص من صورة مائلة، فإن الخطوات أدناه تغطي كل ما تحتاجه. لا إطالة—فقط مثال عملي يمكنك نسخه‑ولصقه في Visual Studio.  

## ما ستحققه

* تصحيح الانحراف حتى 30° (هذا هو جزء **كيفية تصحيح انحراف الصورة**).  
* زيادة تباين الصورة للحصول على حواف أحرف أكثر وضوحًا (**كيفية تحسين التباين**).  
* تحميل صورتك إلى محرك OCR (**تحميل الصورة لـ OCR**).  
* تشغيل عملية التعرف و**استخراج النص من المسح**.  

كل هذا يعمل مع أحدث حزمة Aspose.OCR .NET NuGet (الإصدار 23.11 وقت كتابة هذا الدليل).  

---

![مثال على تصحيح انحراف الصورة](/images/deskew-example.png "كيفية تصحيح انحراف الصورة")

*الصورة أعلاه تُظهر مستندًا ممسوحًا قبل وبعد تصحيح الانحراف.*

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+).  
* Visual Studio 2022 (أو أي بيئة تطوير C# تفضلها).  
* حزمة Aspose.OCR NuGet – تثبيت عبر `dotnet add package Aspose.OCR`.  

هذا كل شيء. لا خدمات خارجية، ولا مفاتيح API.

---

## كيفية تصحيح انحراف الصورة باستخدام Aspose OCR

أول شيء نفعله هو إنشاء **ImageProcessingPipeline** وإضافة `DeskewFilter`. يقوم الفلتر تلقائيًا باكتشاف زاوية سطر النص السائدة ويُدوّر الصورة لتصبح أفقية.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Build a pipeline – Deskew is the first filter
var processingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { MaxAngle = 30 })   // how to deskew image up to 30°
    .Add(new DenoiseFilter { Level = DenoiseLevel.High }) // remove noise
    .Add(new ContrastBoostFilter { Strength = 1.5 })      // how to boost contrast
    .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize

// Attach the pipeline to the engine
ocrEngine.Settings.ImageProcessing = processingPipeline;
```

**لماذا هذا مهم:**  
المسح المائل يربك محرك OCR لأن الأحرف لم تعد محاذية للخط الأساسي. يقوم `DeskewFilter` بتحليل مدرج تكرار الصورة، يجد الزاوية، ويُدوّرها، مما يحسن دقة التعرف بشكل كبير.

> **نصيحة احترافية:** إذا كنت تعلم أن مستنداتك لا تتجاوز ميلًا قدره 15°، اضبط `MaxAngle = 15` لتسريع المعالجة.

---

## كيفية تحسين التباين للحصول على تعرّف أفضل

بعد تصحيح الانحراف، الخطوة التالية هي إبراز النص. يقوم `ContrastBoostFilter` بتمديد نطاق شدة البكسل، وهو مفيد بشكل خاص للطباعة الباهتة.

```csharp
// The ContrastBoostFilter is already in the pipeline above.
// You can tweak the Strength value (1.0 = no change, >1.0 = stronger boost)
.Add(new ContrastBoostFilter { Strength = 1.5 })
```

**لماذا يساعد ذلك:**  
المسحات ذات التباين المنخفض تنتج أحرفًا رمادية قد يفسرها محول الثنائي كخلفية. رفع التباين يجعل البكسلات الداكنة أكثر ظلامًا والفاتحة أكثر إشراقًا، مما يمنح `BinarizationFilter` التالي لوحة أنظف.

---

## تنفيذ OCR على الصورة – تحميل الملف

الآن بعد أن تم معالجة الصورة مسبقًا، نحتاج إلى **تحميل الصورة لـ OCR**. تقدم Aspose أداة مساعدة مريحة `ImageStream.FromFile`.

```csharp
// Load the source image – replace the path with your own file
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

إذا كانت صورتك موجودة في تدفق (مثلاً، تم تحميلها عبر واجهة ويب API)، يمكنك استخدام `ImageStream.FromStream(yourStream)` بدلاً من ذلك. يقبل المحرك صيغ BMP، JPEG، PNG، TIFF، والعديد غيرها.

---

## تشغيل عملية التعرف واستخراج النص من المسح

مع ربط كل شيء، استدعاء `Recognize()` يقوم بالعمل الشاق. بعد الاستدعاء، يصبح النص المعترف به متاحًا عبر `ocrEngine.Text`.

```csharp
// Run OCR
ocrEngine.Recognize();

// Output the result
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrEngine.Text);
```

**الناتج المتوقع** (مثال لفاتورة بسيطة):

```
=== Extracted Text ===
Invoice #12345
Date: 03/05/2026
Total: $1,250.00
Thank you for your business!
```

إذا كان الناتج مشوشًا، تحقق مرة أخرى من ترتيب خط الأنابيب—ابدأ بالتصحيح، ثم إزالة الضوضاء، ثم تحسين التباين، وأخيرًا التحويل إلى ثنائي. تبديل الترتيب قد يضعف النتائج.

---

## المشكلات الشائعة والحالات الخاصة

| المشكلة | السبب | الحل |
|---------|-------|------|
| **نتيجة فارغة** | الصورة مظلمة جدًا أو ساطعة جدًا بالنسبة لطريقة التحويل الثنائي الافتراضية. | زيادة `ContrastBoostFilter.Strength` أو التحويل إلى `BinarizationMethod.Otsu`. |
| **نص جزئي مفقود** | لا يزال هناك ضوضاء بعد إزالة الضوضاء. | استخدم `DenoiseLevel.Medium` للصور الأخف، أو أضف `DenoiseFilter` ثاني. |
| **اتجاه الدوران خاطئ** | المستند يحتوي على اتجاهات مختلطة (مثلاً، صورة لصفحة مائلة). | اضبط يدويًا `DeskewFilter.MaxAngle` إلى قيمة أقل وقم بتدوير الصورة مسبقًا باستخدام `ImageProcessor.Rotate`. |
| **تباطؤ الأداء** | دفعة كبيرة من الصور عالية الدقة. | قلل أبعاد الصور (`ImageProcessor.Resize`) قبل خط الأنابيب، أو عالجها بالتوازي (`Parallel.ForEach`). |

---

## مثال كامل جاهز للنسخ واللصق

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build image‑processing pipeline
        var processingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { MaxAngle = 30 })                     // how to deskew image up to 30°
            .Add(new DenoiseFilter { Level = DenoiseLevel.High })       // remove high‑level noise
            .Add(new ContrastBoostFilter { Strength = 1.5 })            // how to boost contrast
            .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize image

        // 3️⃣ Attach pipeline to OCR settings
        ocrEngine.Settings.ImageProcessing = processingPipeline;

        // 4️⃣ Load the image you want to OCR
        // Replace the path with the location of your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition engine
        ocrEngine.Recognize();

        // 6️⃣ Display the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

احفظ هذا كـ `Program.cs`، شغّل `dotnet run`، وسترى وحدة التحكم تطبع نتيجة **استخراج النص من المسح**.

---

## الخطوات التالية والمواضيع ذات الصلة

* **معالجة دفعات** – غلف المنطق السابق داخل حلقة للتعامل مع العشرات من الملفات.  
* **حزم لغات مخصصة** – إذا كنت بحاجة لقراءة نصوص غير لاتينية، حمّل نموذج لغة عبر `ocrEngine.Settings.Language = OcrLanguage.ChineseSimplified;`.  
* **إخراج PDF** – دمج Aspose.PDF مع OCR لإدراج نص قابل للبحث مباشرةً في ملف PDF.  
* **تحسين الأداء** – جرّب ترتيب `ImageProcessingPipeline`؛ أحيانًا يكون إزالة الضوضاء قبل التصحيح أسرع للصور الضوضائية.  

كل هذه تبني على المفاهيم الأساسية التي غطيناها: **كيفية تصحيح انحراف الصورة**، **كيفية تحسين التباين**، **تحميل الصورة لـ OCR**، **تنفيذ OCR على الصورة**، وأخيرًا **استخراج النص من المسح**.

---

## الخلاصة

لقد عرضنا للتو طريقة كاملة وجاهزة للإنتاج **لتصحيح انحراف الصورة** وتشغيل OCR في C#. من خلال ربط فلتر تصحيح الانحراف، خطوة إزالة الضوضاء، تحسين التباين، ومحول ثنائي، تحصل على مدخل نظيف يسمح لـ Aspose OCR باستخراج النص من المسح بشكل موثوق.  

جرّب الكود، عدّل معلمات الفلاتر لتناسب مستنداتك، وستلاحظ مدى سرعة تحسين دقة التعرف. هل لديك أسئلة؟ اترك تعليقًا، وبرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}