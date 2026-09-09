---
category: general
date: 2026-01-01
description: كيفية تنفيذ OCR دفعيًا باستخدام محرك Aspose OCR في C#. تعلم كيفية التعرف
  على النص من الصور واستخراج النص من ملفات TIFF مع تسريع GPU.
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from TIFF
language: ar
og_description: كيفية تنفيذ التعرف الضوئي على الأحرف (OCR) على دفعات في C# باستخدام
  محرك Aspose OCR. يوضح هذا الدليل كيفية التعرف على النص من الصور واستخراج النص من
  ملفات TIFF بكفاءة.
og_title: كيفية تنفيذ OCR دفعيًا في C# – دليل Aspose الكامل
tags:
- OCR
- C#
- Aspose
- GPU
title: كيفية تنفيذ OCR دفعيًا في C# باستخدام محرك Aspose OCR
url: /ar/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعةً في C# باستخدام محرك Aspose OCR Engine

هل تساءلت يومًا **كيف تقوم بعملية OCR دفعةً** عندما يكون لديك العشرات من المستندات الممسوحة ضوئيًا مخزنة في مجلد؟ لست وحدك—فالعديد من المطورين يواجهون هذه المشكلة عند الانتقال من التعرف على صورة واحدة إلى معالجة مجموعة كاملة. الخبر السار هو أن Aspose OCR يجعل الأمر سهلًا للغاية، سواء كنت تعمل على CPU أو تستفيد من تسريع GPU.

في هذا الدرس سنستعرض مثالًا كاملًا وقابلًا للتنفيذ ي **يتعرف على النص من الصور** وحتى **يستخرج النص من ملفات TIFF** بشكل دفعي. لا اختصارات غامضة مثل “انظر إلى الوثائق”—بل حل مستقل يمكنك نسخه ولصقه وتشغيله اليوم.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث مثبت (الكود يستهدف .NET 6، لكن .NET 5 يعمل أيضًا).
* حزمة NuGet Aspose.OCR لـ .NET (يتوفر كل من إصداري CPU وGPU؛ قم بتثبيت الإصدار الذي يتوافق مع عتادك).
* مجلد يحتوي على بعض ملفات TIFF أو PNG التجريبية التي ترغب في معالجتها.
* Visual Studio 2022 أو أي بيئة تطوير تفضّلها.

> **نصيحة احترافية:** إذا كنت تنوي استخدام نسخة GPU، تأكد من أن برنامج تشغيل الرسوميات محدث وأن CUDA 11+ مثبتة. سيعود المحرك تلقائيًا إلى CPU إذا لم يجد GPU متوافق.

## الخطوة 1 – إعداد المشروع وتثبيت Aspose.OCR

### H2: إنشاء تطبيق Console جديد وإضافة Aspose.OCR

افتح الطرفية (أو Package Manager Console في Visual Studio) وشغّل:

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

إذا كان لديك ترخيص يدعم GPU، أضف حزمة GPU بدلاً من ذلك:

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

هذا كل شيء—الآن مشروعك يراجع مكتبة OCR التي سنستخدمها لـ **OCR دفعةً**.

## الخطوة 2 – تهيئة محرك OCR (CPU أو GPU)

### H2: كيفية تنفيذ OCR دفعةً – تهيئة المحرك

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class GpuBatchDemo
{
    static void Main()
    {
        // Create the OCR engine. It works with both CPU and GPU builds.
        var ocrEngine = new OcrEngine();

        // OPTIONAL: Force GPU usage if a compatible device is present.
        // Setting this to true won’t break on CPU‑only machines—it simply tries GPU first.
        ocrEngine.Settings.UseGpu = true;
```

**لماذا هذا مهم:** من خلال تبديل `UseGpu`، تسمح لـ Aspose باختيار أسرع مسار. إذا لم يكن GPU متاحًا، يتحول المحرك بهدوء إلى CPU، لذا لا يتعطل عمل الدفعة بسبب نقص العتاد.

## الخطوة 3 – جمع الملفات التي تريد معالجتها

### H2: التعرف على النص من الصور – بناء قائمة الملفات

```csharp
        // Prepare a list of image files (TIFF, PNG, JPEG, etc.).
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // You could also populate the list dynamically:
        // var imageFiles = Directory.GetFiles(@"C:\OCR\Input", "*.tif").ToList();
```

**ملاحظة حالة حافة:** إذا كان لديك مزيج من الصيغ، غيّر نمط البحث إلى `"*.*"` وقم بالفلترة حسب الامتداد داخل الحلقة. هذا يحافظ على مرونة الدفعة.

## الخطوة 4 – معالجة كل صورة وعرض معاينة

### H2: استخراج النص من TIFF – التكرار عبر الملفات

```csharp
        // Loop through each file, run OCR, and print a short preview.
        foreach (var filePath in imageFiles)
        {
            // Load the image into Aspose's OcrImage object.
            var ocrImage = OcrImage.FromFile(filePath);

            // Run recognition.
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Display the first 50 characters of the recognized text.
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");
        }
    }
}
```

**ما ستراه:** لكل ملف TIFF، يطبع الطرفية شيئًا مثل:

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```

تؤكد هذه المعاينة أن الدفعة نجحت دون الحاجة لفتح كل ملف يدويًا.

## الخطوة 5 – حفظ النتائج (اختياري لكن مفيد)

### H3: حفظ مخرجات OCR إلى ملفات نصية

إذا كنت بحاجة إلى النص الكامل للمعالجة اللاحقة، أضف هذا داخل حلقة `foreach`:

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

الآن يحصل كل ملف TIFF على ملف `.txt` مرفق يحتوي على مخرجات OCR الكاملة—مثالي للفهرسة، البحث، أو إمداده إلى نموذج لغة.

## الخطوة 6 – تشغيل العرض والتحقق

1. بناء المشروع: `dotnet build`.
2. تشغيله: `dotnet run --project GpuBatchDemo.csproj`.

يجب أن ترى سطور المعاينة مطبوعة في الطرفية، و(إذا أضفت الخطوة الاختيارية) مجموعة من ملفات `.txt` بجوار صور المصدر.

### H3: المشكلات الشائعة وكيفية إصلاحها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| **Empty `ocrResult.Text`** | الصورة مظلمة جدًا أو DPI منخفض | معالجة مسبقة للصور (زيادة التباين، تكبير) أو تعيين `ocrEngine.Settings.PreprocessImage = true`. |
| **GPU error “CUDA driver version is insufficient”** | برنامج تشغيل قديم | تحديث برنامج تشغيل GPU، أو تعيين `UseGpu = false` لإجبار الاستخدام على CPU. |
| **Exception “File not found”** | فاصل مسار غير صحيح على Linux/macOS | استخدم `Path.Combine` أو الشرطات المائلة للأمام (`/`). |

## الخطوة 7 – التوسع (أكثر من عدد قليل من الملفات)

عند الانتقال من عدد قليل من ملفات TIFF إلى آلاف، ضع في الاعتبار:

* **المعالجة المتوازية:** غلف `foreach` بـ `Parallel.ForEach` (تأكد من أن نسخة المحرك آمنة للخطوط المتعددة؛ وإلا أنشئ نسخة لكل خط).
* **الإدخال/الإخراج المجزأ:** اقرأ الصور على دفعات لتجنب استنفاد الذاكرة RAM.
* **التسجيل (Logging):** اكتب التقدم إلى ملف سجل؛ يساعد على الاستئناف بعد حدوث عطل.

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **تذكر:** ذاكرة GPU مشتركة، لذا إنشاء عدد كبير جدًا من وظائف GPU المتوازية قد يبطئ الأداء فعليًا. جرّب مع عدد قليل من الخيوط أولاً.

## مثال كامل يعمل (جاهز للنسخ واللصق)

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1 – Create OCR engine (CPU or GPU)
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.UseGpu = true; // Try GPU, fallback to CPU automatically

        // Step 2 – List of TIFF files to process
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // Step 3 – Process each file
        foreach (var filePath in imageFiles)
        {
            var ocrImage = OcrImage.FromFile(filePath);
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Show a short preview
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");

            // Optional: Save full text to a .txt file
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
        }
    }
}
```

تشغيل هذا البرنامج سي **يتعرف على النص من الصور**، **يستخرج النص من TIFF**، ويظهر **كيفية تنفيذ OCR دفعةً** بكفاءة.

## الخاتمة

أصبح لديك الآن مثال شامل من البداية إلى النهاية لـ **كيفية تنفيذ OCR دفعةً** في C# باستخدام محرك OCR من Aspose. غطى الدرس كل شيء من إعداد المشروع، وتبديل تسريع GPU، وبناء قائمة الملفات، ومعالجة كل صورة، وحفظ النتائج. سواء كنت تستخرج النص من ملفات TIFF أو أي صيغة صورة أخرى، فإن النمط نفسه ينطبق—فقط غير امتدادات الملفات.

هل أنت مستعد للخطوة التالية؟ جرّب دمج مخرجات OCR مع فهرس بحث، أو إمداد النص إلى نموذج لغة كبير، أو جرب المعالجة المتوازية لتقليل دقائق من الدفعات الضخمة. السماء هي الحد، ولديك الأساس للبناء عليه.

هل لديك أسئلة أو ترغب في مشاركة حيلك الخاصة في OCR الدفعي؟ اترك تعليقًا أدناه—برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}