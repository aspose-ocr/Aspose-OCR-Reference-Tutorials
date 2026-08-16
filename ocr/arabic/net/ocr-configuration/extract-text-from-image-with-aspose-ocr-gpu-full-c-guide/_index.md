---
category: general
date: 2026-04-06
description: استخراج النص من الصورة باستخدام Aspose OCR GPU في C#. تعلم كيفية تحميل
  الصورة من ملف وتحديد حد ذاكرة GPU في هذا الدليل خطوة بخطوة.
draft: false
keywords:
- extract text from image
- load image from file
- set gpu memory limit
- aspose ocr example
- aspose ocr gpu
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR GPU في C#. تعلم كيفية تحميل
  الصورة من ملف وتحديد حد ذاكرة GPU في هذا الدليل خطوة بخطوة.
og_title: استخراج النص من الصورة باستخدام Aspose OCR GPU – دليل كامل بلغة C#
tags:
- Aspose OCR
- C#
- GPU
- OCR
title: استخراج النص من الصورة باستخدام Aspose OCR GPU – دليل كامل بلغة C#
url: /ar/net/ocr-configuration/extract-text-from-image-with-aspose-ocr-gpu-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة باستخدام Aspose OCR GPU – دليل C# كامل

هل احتجت يومًا إلى **استخراج النص من الصورة** لكن شعرت بأن الأداء هو العائق؟ لست وحدك—العديد من المطورين يواجهون نفس المشكلة عندما يصبح OCR عنق زجاجة. في هذا البرنامج التعليمي سنوضح لك بالضبط كيفية استخراج النص من الصورة باستخدام محرك Aspose OCR GPU، تحميل الصورة من ملف، وحتى ضبط حد الذاكرة على الـ GPU للتحكم الأفضل في الموارد.

سنستعرض مثالًا كاملًا جاهزًا للتنفيذ بلغة C#، نشرح لماذا كل سطر مهم، ونشير إلى الأخطاء الشائعة التي قد تواجهها. في النهاية ستحصل على أساس متين لبناء خطوط معالجة OCR سريعة وقابلة للتوسع تعمل على الـ GPU.

## ما يغطيه هذا الدليل

- **المتطلبات المسبقة**: .NET 6+ (أو .NET Framework 4.6+)، حزمة NuGet Aspose.OCR، برنامج تشغيل GPU متوافق.
- **كود خطوة بخطوة** يقوم بتحميل صورة من ملف، ضبط محرك Aspose OCR GPU، واستخراج النص.
- **لماذا** قد ترغب في ضبط حد الذاكرة على الـ GPU وكيفية القيام بذلك بأمان.
- **معالجة الحالات الطرفية**: صور منخفضة الدقة، عدم وجود GPU، واستكشاف أخطاء درجات الثقة.
- **الخطوات التالية**: المعالجة الدفعية، التكامل مع ASP.NET Core، والعودة إلى المعالجة على CPU إذا لزم الأمر.

> **نصيحة احترافية:** إذا لم تكن متأكدًا ما إذا كان الـ GPU يُستَخدم، راقب مراقب نشاط الـ GPU (مثل NVIDIA‑SMI) أثناء تشغيل OCR. ستلاحظ ارتفاعًا في استهلاك الذاكرة يتطابق مع الحد الذي ضبطته.

---

![مخطط يوضح تدفق استخراج النص من الصورة باستخدام محرك Aspose OCR GPU](extract-text-from-image-aspose-ocr-gpu.png "استخراج النص من الصورة باستخدام Aspose OCR GPU")

## الخطوة 1: تهيئة محرك Aspose OCR للمعالجة على GPU

أول شيء تحتاجه هو كائن `OcrEngine` يعرف أنه يجب أن يعمل على الـ GPU. توفر Aspose كائن `OcrEngineSettings` نظيف حيث يمكنك تحديد وقت التشغيل.

```csharp
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

// Create the OCR engine and tell it to use the GPU runtime
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
});
```

**لماذا هذا مهم:** بشكل افتراضي، يعود Aspose OCR إلى الـ CPU، وهو مناسب للصور الصغيرة لكن قد يكون بطيئًا جدًا للصور عالية الدقة. ضبط `Runtime = OcrRuntime.Gpu` صراحةً ينقل العبء الثقيل إلى بطاقة الرسومات، مما يمنحك تسارعًا ملحوظًا.

## الخطوة 2: (اختياري) ضبط حد الذاكرة على GPU

إذا كنت تعمل على محطة عمل مشتركة أو حاوية بموارد GPU محدودة، يمكنك تحديد الحد الأقصى للذاكرة التي يستهلكها محرك OCR. هذا يمنع حدوث أعطال نفاد الذاكرة ويحافظ على سعادة العمليات الأخرى.

```csharp
// Limit the GPU memory usage to 1024 MB (1 GB)
ocrEngine.Settings.GpuMemoryLimit = 1024;
```

**متى تستخدمه:**  
- **بيئات متعددة المستأجرين** حيث تشارك عدة خدمات نفس الـ GPU.  
- **خطوط أنابيب CI/CD** التي تخصص كمية ثابتة من ذاكرة الـ GPU لكل مهمة.  

إذا حذفت هذا السطر، سيستخدم Aspose كل الذاكرة التي يحتاجها، وهذا مقبول على محطة عمل مخصصة.

## الخطوة 3: تحميل الصورة من ملف

الآن نحتاج إلى جلب الصورة إلى الذاكرة. يعمل Aspose OCR مع `System.Drawing.Image`، لذا سنستخدم `Image.FromFile`. تأكد أن المسار يشير إلى ملف حقيقي؛ وإلا سيتولد استثناء.

```csharp
// Replace with the actual path to your high‑resolution image
string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

using (var image = Image.FromFile(imagePath))
{
    // The image is now ready for OCR processing
    // (the next step will happen inside this using block)
}
```

**لماذا التحميل من ملف مهم:** كثير من المطورين يحاولون تمرير مصفوفة بايت مباشرة، وهذا يعمل لكنه يضيف خطوة تحويل غير ضرورية. استخدام `Image.FromFile` مباشر، وتعليمة `using` تضمن تحرير مقبض الملف بسرعة.

## الخطوة 4: تشغيل OCR واسترجاع النتيجة

مع ضبط المحرك وتحميل الصورة، يمكننا أخيرًا استخراج النص. تُعيد طريقة `Recognize` كائن `OcrResult` يحتوي على النص الخام ودرجة الثقة.

```csharp
using (var image = Image.FromFile(imagePath))
{
    // Perform OCR on the loaded image
    var ocrResult = ocrEngine.Recognize(image);

    // Display the confidence and the extracted text
    Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(ocrResult.Text);
}
```

**فهم المخرجات:**  
- `Confidence` قيمة بين 0 و 1. درجة ثقة 0.95 (أو 95 ٪) عادةً ما تعني أن OCR دقيق جدًا.  
- `Text` يحتوي على فواصل الأسطر كما تظهر في الصورة، وهو مفيد للمعالجة اللاحقة.

## الخطوة 5: التحقق من المخرجات ومعالجة الحالات الطرفية

### فحص مستويات الثقة

إذا انخفضت الثقة إلى أقل من، لنقل، 80 ٪، قد ترغب في الرجوع إلى المعالجة على CPU أو تطبيق معالجة مسبقة للصورة (مثل التحويل إلى ثنائي).

```csharp
if (ocrResult.Confidence < 0.80)
{
    Console.WriteLine("Low confidence detected – consider preprocessing or CPU fallback.");
    // Example fallback: switch to CPU runtime temporarily
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
    Console.WriteLine(cpuResult.Text);
}
```

### التعامل مع عدم وجود GPU

ليس كل جهاز يحتوي على GPU متوافق. سيُطلق Aspose استثناء `OcrException` إذا تعذر تهيئة وقت تشغيل الـ GPU.

```csharp
try
{
    var ocrResult = ocrEngine.Recognize(image);
    // Normal processing...
}
catch (OcrException ex) when (ex.Message.Contains("GPU"))
{
    Console.WriteLine("GPU not available – falling back to CPU.");
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine(cpuResult.Text);
}
```

### الصور عالية الدقة

الصور الكبيرة جدًا (مثلاً > 4000 px عرض) قد تستهلك الكثير من ذاكرة الـ GPU. إذا وصلت إلى الحد الذي ضبطته مسبقًا، سيقوم Aspose بقطع المعالجة. في هذه الحالة، قلل أبعاد الصورة أولًا:

```csharp
using (var original = Image.FromFile(imagePath))
{
    int maxWidth = 2000;
    var resized = new Bitmap(original, new Size(maxWidth, original.Height * maxWidth / original.Width));
    var ocrResult = ocrEngine.Recognize(resized);
    // Continue as before
}
```

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع Console جديد. يتضمن جميع الخطوات، معالجة الأخطاء، ومنطق الرجوع الاختياري.

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Initialize OCR engine to use GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
        });

        // Step 2: (Optional) Limit GPU memory usage to 1 GB
        ocrEngine.Settings.GpuMemoryLimit = 1024;

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

        // Step 3: Load image from file
        using (var image = Image.FromFile(imagePath))
        {
            try
            {
                // Step 4: Run OCR on the image
                var ocrResult = ocrEngine.Recognize(image);

                // Step 5: Output confidence and extracted text
                Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
                Console.WriteLine("Extracted text:");
                Console.WriteLine(ocrResult.Text);

                // Edge‑case: low confidence handling
                if (ocrResult.Confidence < 0.80)
                {
                    Console.WriteLine("\nLow confidence detected – trying CPU fallback...");
                    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                    var cpuResult = ocrEngine.Recognize(image);
                    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                    Console.WriteLine(cpuResult.Text);
                }
            }
            catch (OcrException ex) when (ex.Message.Contains("GPU"))
            {
                Console.WriteLine("GPU not available – falling back to CPU runtime.");
                ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                var cpuResult = ocrEngine.Recognize(image);
                Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                Console.WriteLine(cpuResult.Text);
            }
        }
    }
}
```

### المخرجات المتوقعة

```
GPU OCR confidence: 96.45%
Extracted text:
This is the text that was
found in the high‑resolution
image you supplied.

```

إذا انخفضت الثقة تحت العتبة المحددة، ستظهر رسائل الرجوع إلى CPU الإضافية.

---

## الخلاصة

أنت الآن تعرف **كيفية استخراج النص من الصورة** باستخدام محرك Aspose OCR GPU، **كيفية تحميل الصورة من ملف**، ولماذا قد ترغب في **ضبط حد الذاكرة على GPU** لأعباء الإنتاج. المثال أعلاه حل كامل قابل للاقتباس يمكنك إدراجه في أي مشروع .NET.

ما الخطوة التالية؟ فكر في:

- **المعالجة الدفعية**: حلقة تمر على مجلد من الصور وتكتب النتائج إلى ملف CSV.  
- **تكامل ASP.NET Core**: إنشاء نقطة API تستقبل صورة مرفوعة وتعيد نص OCR.  
- **تحسين الأداء**: تجربة قيم مختلفة لـ `GpuMemoryLimit` ومراقبة استهلاك الـ GPU للوصول إلى النقطة المثلى.

لا تتردد في تعديل الكود ليتناسب مع سيناريوك—سواء كنت تبني خط أنابيب رقمية للوثائق، أو تطبيق ترجمة فوري، أو خدمة مسح فواتير. الأساسيات تبقى نفسها: تهيئة محرك الـ GPU، إدارة الذاكرة بحكمة، دائمًا التحقق من درجة الثقة.

هل لديك أسئلة أو واجهت مشكلة؟ اترك تعليقًا أدناه، ولنحلها معًا. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}