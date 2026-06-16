---
category: general
date: 2026-04-03
description: تعلم كيفية تنفيذ التعرف الضوئي على الحروف (OCR) على دفعات باستخدام Aspose.OCR
  في C#. يوضح لك هذا الدليل كيفية استخراج النص من صور PNG وتحويل الصور إلى نص بكفاءة.
draft: false
keywords:
- how to batch ocr
- extract text png
- convert images to text
- Aspose OCR
- C# parallel processing
language: ar
og_description: اكتشف كيفية تنفيذ OCR دفعيًا في C# لاستخراج النص من صور PNG وتحويل
  الصور إلى نص باستخدام Aspose.OCR. يتضمن الكود الكامل.
og_title: كيفية تنفيذ OCR دفعيًا في C# – دليل سريع
tags:
- OCR
- C#
- Aspose
title: كيفية تنفيذ OCR دفعيًا في C# – طريقة سريعة لاستخراج النص من ملفات PNG
url: /ar/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعيًا في C# – طريقة سريعة لاستخراج نص ملفات PNG

هل تساءلت يومًا **كيف تقوم بعمل OCR دفعي** لمجلد كامل من لقطات الشاشة دون كتابة حلقة لكل ملف؟ لست وحدك. في العديد من المشاريع—مثل رقمنة الفواتير أو أرشفة الإيصالات الممسوحة ضوئيًا—تنتهي بك الأمر بوجود عشرات، وأحيانًا مئات، من ملفات PNG التي تحتاج إلى استخراج نصها. الخبر السار؟ مع Aspose.OCR يمكنك **استخراج نص PNG** للصور بشكل متوازي، ويمكن إكمال العملية بأكملها في بضع أسطر فقط من C#.

في هذا الدرس سنستعرض مثالًا كاملًا جاهزًا للتنفيذ يوضح لك كيفية **تحويل الصور إلى نص** باستخدام معالج دفعي. سنغطي المتطلبات المسبقة، ونشرح لماذا كل سطر مهم، وسنضيف بعض النصائح الاحترافية لتجنب المشكلات الشائعة لاحقًا.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- **.NET 6.0** (أو أحدث) مثبت على جهازك. الإصدارات القديمة تعمل، لكن الأحدث يمنحك أداءً أفضل ودعمًا للـ async.
- حزمة **Aspose.OCR for .NET**. يمكنك الحصول عليها عبر NuGet: `dotnet add package Aspose.OCR`.
- مجلد يحتوي على صور **PNG** تريد معالجتها. سنشير إليه بـ `YOUR_DIRECTORY` طوال الدليل.
- كمية معتدلة من الذاكرة RAM—فـ OCR الدفعي يمكن أن يستهلك الكثير من الذاكرة إذا زادت التوازي، لكن استخدام `Environment.ProcessorCount` يبقي الأمور آمنة.

> **نصيحة احترافية:** إذا كنت تعمل على خط أنابيب CI/CD، أضف ملف ترخيص Aspose كسرّ لتجنب حد الـ 20 صفحة في التقييم المجاني.

الآن، دعنا نتعمق.

## الخطوة 1: إعداد معالج OCR الدفعي (Primary Keyword in Header)

أول شيء تحتاجه هو نسخة من `BatchOcrProcessor`. هذه الفئة تُجرد منطق الخيوط وتتيح لك التركيز على ما ستفعله بكل صورة.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Create a batch OCR processor and tell it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };
```

**لماذا هذا مهم:**  
- `Engine = new OcrEngine()` يمنحك محرك OCR جديد لكل خيط، مما يجنب التعارض.  
- `MaxDegreeOfParallelism = Environment.ProcessorCount` يتكيف تلقائيًا مع عدد الأنوية، مما يوفر أعلى معدل معالجة ممكن دون ضبط يدوي.

## الخطوة 2: ربط أحداث التقدم (Helps Track Extraction)

رؤية التقدم أمر أساسي عند معالجة مئات الملفات. حدث `ProgressChanged` يُطلق بعد الانتهاء من كل ملف، مما يتيح لك تسجيل الحالة.

```csharp
        // Subscribe to progress updates so we know which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");
```

**لماذا ستحب ذلك:**  
- التغذية الراجعة في الوقت الحقيقي تمنعك من التساؤل إذا ما كان التطبيق عالقًا.  
- إذا احتجت يومًا لإيقاف أو إلغاء العملية، لديك بالفعل نقطة ربط لتفحص `e.Current` مقابل `e.Total`.

## الخطوة 3: تعريف فحص المجلد ونمط الملفات (Extract Text PNG)

الآن نخبر المعالج أين يبحث وأي نوع من الملفات يلتقط. النمط `"*.png"` يضمن أننا نتعامل فقط مع صور PNG.

```csharp
        // Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"YOUR_DIRECTORY",          // folder containing the images
            "*.png",                    // file pattern
            (imagePath, ocrText) =>     // callback for each processed file
            {
                // Step 4 is inside this callback – see next section
            });
```

**لماذا هذا أساسي:**  
- استخدام نمط glob يبقي الكود مرنًا؛ غيّر `*.png` إلى `*.jpg` إذا احتجت لاحقًا لمعالجة JPEGs.  
- الدالة الراجعة تستقبل كل من مسار الصورة والنص المعترف به، مما يمنحك التحكم الكامل فيما ستفعله بعد ذلك.

## الخطوة 4: حفظ النص المعترف به بجوار المصدر (Convert Images to Text)

داخل الدالة الراجعة سنكتب ناتج OCR إلى ملف `.txt` يُوضع بجوار ملف PNG الأصلي. هذه أبسط طريقة **لتحويل الصور إلى نص** للمعالجة اللاحقة.

```csharp
                // Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
```

**لماذا نختار ملف `.txt` جنبًا إلى جنب:**  
- يبقي العلاقة واضحة—افتح PNG، افتح TXT، قارن.  
- لا حاجة لقاعدة بيانات أو طبقة تخزين إضافية في المشاريع الصغيرة.

## الخطوة 5: إنهاء البرنامج برسالة إكمال ودية

رسالة وحدة تحكم أنيقة تخبرك عندما يكتمل كل شيء.

```csharp
        // Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

عند تشغيل البرنامج، ستظهر لك مخرجات مثل:

```
Processed 1/27: C:\Images\invoice1.png
Processed 2/27: C:\Images\invoice2.png
...
Batch processing completed.
```

كل ملف PNG الآن لديه ملف `.txt` شقيق يحتوي على النص المستخرج.

## مثال عملي كامل (All Steps Combined)

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع وحدة تحكم جديد. لا أجزاء مفقودة—فقط استبدل `YOUR_DIRECTORY` بالمسار المطلق لصورك.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create a batch OCR processor and configure it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };

        // Step 2: Subscribe to progress updates to see which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");

        // Step 3: Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"C:\MyImages",          // folder containing the images
            "*.png",                // file pattern
            (imagePath, ocrText) => // callback for each processed file
            {
                // Step 4: Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
            });

        // Step 5: Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

### النتيجة المتوقعة

- لكل `image.png` في `C:\MyImages`، يظهر ملف `image.txt` بجواره.  
- تُطبع وحدة التحكم سطور التقدم، مما يسهل مراقبة الدفعات الكبيرة.  
- لا حاجة للدوارات اليدوية أو إدارة الخيوط—`BatchOcrProcessor` يتولى كل شيء.

## أسئلة شائعة وحالات حافة

### ماذا لو لم تكن صوري PNG؟

فقط غير الوسيط الثاني في `ProcessFolder` إلى `"*.jpg"` أو `"*.*"` لتضمين جميع الملفات. يعمل محرك OCR مع معظم صيغ الرسوم النقطية.

### كم من الذاكرة يستهلك هذا؟

`BatchOcrProcessor` يحمل صورة واحدة لكل خيط. مع ضبط `Environment.ProcessorCount` على سبيل المثال إلى 8 أنوية، سيكون لديك ثماني صور في الذاكرة في آنٍ واحد. إذا واجهت استثناءات OutOfMemory، قلل من التوازي:

```csharp
MaxDegreeOfParallelism = 4; // or any number that fits your machine
```

### هل يمكنني تخصيص لغة OCR؟

بالطبع. بعد إنشاء المحرك، عيّن خاصية `Language` الخاصة به:

```csharp
Engine = new OcrEngine { Language = Language.English };
```

Aspose يدعم العديد من اللغات؛ فقط أضف حزمة NuGet المناسبة إذا لزم الأمر.

### ماذا عن معالجة الأخطاء؟

غلف الدالة الراجعة بكتلة try/catch وسجّل الفشل. سيستمر المعالج مع الملف التالي، مما يمنع فشل صورة واحدة من إيقاف العملية بالكامل.

```csharp
(imagePath, ocrText) =>
{
    try
    {
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, ocrText);
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {imagePath}: {ex.Message}");
    }
}
```

## نصائح احترافية للتوسع

- **تقسيم المجلد**: إذا كان لديك عشرات الآلاف من الملفات، قسّمها إلى مجلدات فرعية وشغّل وظائف دفعية متعددة بالتتابع.  
- **استخدام VM سحابي**: آلة ذات عدد أكبر من الأنوية (مثلاً 32 نواة) ستنتهي العملية أسرع بكثير. فقط تذكّر تعديل حدود الترخيص.  
- **معالجة النص لاحقًا**: بعد الاستخراج، قد ترغب في تشغيل تعبيرات regex لاستخراج أرقام الفواتير أو التواريخ. ملفات `.txt` هي مدخل مثالي لمثل هذه الأنابيب.

## الخلاصة

أصبح لديك الآن وصفة جاهزة للإنتاج حول **كيفية تنفيذ OCR دفعي** لمجلد PNGs، **استخراج نص PNG**، و**تحويل الصور إلى نص** باستخدام Aspose.OCR في C#. المثال مستقل، يشرح “السبب” وراء كل سطر، ويتضمن نصائح للتعامل مع أحمال أكبر أو أنواع ملفات مختلفة.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال الدالة الراجعة بدفع النتائج إلى قاعدة بيانات، أو أضف معالجة مسبقة للصور (مثل تصحيح الميل) قبل OCR. النمط قابل للتوسع بسهولة، لذا يمكنك تكييفه مع أي سيناريو معالجة دفعي تواجهه.

برمجة سعيدة، ولتكن خطوط OCR الخاصة بك سريعة وخالية من الأخطاء!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}