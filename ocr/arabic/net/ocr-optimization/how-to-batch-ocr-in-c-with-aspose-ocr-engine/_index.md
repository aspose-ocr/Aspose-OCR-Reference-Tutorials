---
category: general
date: 2026-09-13
description: كيفية إجراء OCR دفعي باستخدام Aspose OCR GPU في C# باستخدام .NET. تعلم
  كيفية التعرف على النص من الصور، استخراج النص من ملفات TIFF، وتسريع المعالجة بدعم
  GPU.
draft: false
keywords:
- aspose ocr gpu
- process multiple images
- how to batch ocr
- install aspose ocr
lastmod: 2026-09-13
og_description: كيفية إجراء OCR دفعي باستخدام Aspose OCR GPU في C# باستخدام .NET.
  يوضح هذا الدليل كيفية التعرف على النص من الصور، استخراج النص من ملفات TIFF، والاستفادة
  من تسريع GPU للمعالجة high‑performance processing.
og_image_alt: Screenshot of Aspose OCR GPU batch processing console output in C#
og_title: كيفية إجراء OCR دفعي باستخدام Aspose OCR GPU في C# باستخدام .NET
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: How to batch OCR with Aspose OCR GPU in C# using .NET. Learn to recognize
    text from images, extract text from TIFF files, and accelerate processing with
    GPU support.
  headline: How to batch OCR with Aspose OCR GPU in C# using .NET
  type: TechArticle
- questions:
  - answer: Yes, as long as the server has a CUDA‑compatible GPU and the appropriate
      driver libraries installed; no display is required.
    question: Can I run the GPU version on a headless Linux server?
  - answer: Absolutely. The engine treats each page as a separate image and returns
      concatenated text, preserving page order.
    question: Does Aspose OCR support multi‑page TIFF files out of the box?
  - answer: Benchmarks show Aspose OCR achieves ≥ 96 % character accuracy on clean
      printed documents and ≥ 90 % on low‑contrast scans, matching leading SaaS providers
      while keeping data on‑premises.
    question: How accurate is the OCR output compared with cloud services?
  - answer: The library imposes no hard limit; practical limits are driven by available
      disk space and GPU memory. Processing 10 000 pages on an RTX 3080 typically
      stays under 2 GB of GPU memory.
    question: Is there a limit to the number of files I can process in one run?
  - answer: Yes, set `ocrEngine.Language = OcrLanguage.Spanish` (or any supported
      language) before calling `Recognize`. The engine supports 30+ languages, including
      Arabic, Chinese, and Hindi.
    question: Can I customize the language model for non‑English scripts?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- GPU
title: كيفية إجراء OCR دفعي باستخدام Aspose OCR GPU في C# باستخدام .NET
url: /ar/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ التعرف الضوئي على الحروف (OCR) على دفعات باستخدام Aspose OCR GPU في C# باستخدام .NET

إذا كنت بحاجة إلى **batch OCR** لمئات الصفحات الممسوحة ضوئياً بسرعة، فإن محرك Aspose OCR GPU يوفر لك طريقة سريعة وموثوقة للتعرف على النص من الصور وملفات TIFF في تشغيل واحد. في هذا الدليل ستتعرف على كيفية إعداد مشروع .NET، تمكين تسريع GPU، ومعالجة مجلد كامل من الصور دون كتابة سطر واحد من الشيفرة النمطية بنفسك.

## إجابات سريعة
- **ما معنى “batch OCR”؟** هو المعالجة الآلية للعديد من ملفات الصور في عملية واحدة، مع إرجاع النص المستخرج لكل ملف.  
- **هل يمكنني استخدام نسخة GPU على أي جهاز؟** نعم، طالما أن النظام يحتوي على GPU متوافق مع CUDA وتم تثبيت برنامج التشغيل المناسب.  
- **هل أحتاج إلى ترخيص للتطوير؟** ترخيص تجريبي مجاني يكفي للاختبار؛ الترخيص التجاري مطلوب للإنتاج.  
- **ما إصدارات .NET المدعومة؟** .NET 6.0 وما بعده مدعومان بالكامل؛ .NET 5 يعمل أيضاً مع بعض التعديلات الطفيفة.  
- **هل المحرك آمن للاستخدام المتعدد الخيوط؟** محرك CPU آمن للاستخدام المتعدد الخيوط؛ محرك GPU يتطلب نسخة واحدة لكل خيط أو استراتيجية متوازية مُتحكم بها.

## ما هو Aspose OCR GPU؟
محرك `Aspose.OCR` GPU هو مكتبة OCR عالية الأداء تُعيد تحميل عمل تحليل الصور إلى بطاقة رسومية مدعومة بـ CUDA، مما يحقق سرعة تصل إلى 4× مقارنةً بالمعالجة على CPU فقط. يدعم مجموعة واسعة من صيغ الصور، ويوفر نماذج لغوية مدمجة، ويمكن دمجه في أي تطبيق .NET مع تغييرات شيفرة قليلة.

## لماذا نستخدم Aspose OCR GPU للمعالجة على دفعات؟
يدعم Aspose OCR **أكثر من 30 صيغة صورة** (بما في ذلك PNG، JPEG، BMP، وTIFF متعدد الصفحات) ويمكنه التعامل مع ملفات تصل إلى **2 GB** لكل منها دون تحميل المستند بالكامل في الذاكرة. عند تمكين تسريع GPU، تُعالج صفحات TIFF بدقة 300 dpi في أقل من 0.2 ثانية لكل صفحة على بطاقة RTX 3080 حديثة.

## المتطلبات المسبقة
- .NET 6.0 SDK (أو أحدث) مثبت على جهاز التطوير الخاص بك.  
- حزمة NuGet الخاصة بـ Aspose.OCR للـ .NET – اختر حزمة `Aspose.OCR.Gpu` إذا كان لديك GPU متوافق، وإلا قم بتثبيت `Aspose.OCR`.  
- مجلد يحتوي على الصور التي تريد معالجتها (TIFF، PNG، JPEG، إلخ).  
- Visual Studio 2022، Rider، أو أي محرر يمكنه بناء تطبيقات .NET console.

> **نصيحة احترافية:** تأكد من تثبيت CUDA 11+ وأن الأمر `nvidia-smi` يُظهر أن الـ GPU “متوافق”. ستعود المكتبة تلقائياً إلى CPU إذا لم تجد GPU مناسب.

## كيفية إعداد المشروع وتثبيت Aspose OCR
أنشئ تطبيق console جديد لـ .NET، أضف حزمة Aspose OCR من NuGet، واستعد الاعتمادات. هذا يُعد مشروعًا خفيفًا يمكن تجميعه وتشغيله على أي منصة تدعم .NET 6 أو أحدث. بعد تثبيت الحزمة، يمكنك استدعاء فئات OCR مباشرة في الشيفرة، مما يتيح المعالجة على دفعات دون إعداد إضافي.

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

إذا كان لديك ترخيص يدعم GPU، فقم بتثبيت الحزمة الخاصة بـ GPU بدلاً من ذلك. تحتوي هذه النسخة على ربطات CUDA أصلية تسمح للمحرك بالعمل على بطاقة الرسوميات، مما يمنحك الزيادة في الأداء المذكورة سابقًا.

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

مشروعك الآن ي référencer مكتبة OCR المطلوبة لـ **batch OCR**.

## كيفية تهيئة محرك OCR (CPU أو GPU)
فئة `OcrEngine` هي نقطة الدخول الرئيسية لأداء عمليات OCR. هي تُجرد العتاد الأساسي وتوفر API بسيط لكل من تنفيذ CPU وGPU. حمّل محرك OCR وأخبره ما إذا كان سيستخدم GPU:

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

**لماذا هذا مهم:** ضبط `UseGpu` يسمح لـ Aspose باختيار أسرع مسار تنفيذ. عندما يكون هناك GPU متوافق، يعمل المحرك على بطاقة الرسوميات؛ وإلا يعود إلى CPU دون إلقاء خطأ، مما يضمن عدم تعطل مهمة الدفعة بسبب نقص العتاد.

## كيفية جمع الملفات التي تريد معالجتها
جمع الصور المستهدفة هو الخطوة الأولى في أي سير عمل دفعي. أنشئ قائمة بمسارات الملفات التي تطابق الامتدادات المدعومة، ثم مرّر تلك القائمة إلى حلقة OCR. هذا النهج يبقي الشيفرة بسيطة ويسهل إضافة تصفية لاحقًا.

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

**ملاحظة حالة حافة:** إذا كان مجلدك يحتوي على صيغ مختلطة، استبدل نمط البحث بـ `"*.*"` وقم بالتصفيّة حسب الامتداد داخل الحلقة. هذا يحافظ على مرونة الدفعة ويتجنب فقدان الملفات.

## كيفية معالجة كل صورة وعرض معاينة
لكل ملف، استدعِ محرك OCR، استرجع النص المُعترف به، واعرض مقتطفًا قصيرًا على وحدة التحكم. تساعد المعاينة في التحقق من أن الدفعة تعمل بشكل صحيح دون فتح كل ملف ناتج.

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

**ما ستراه:** لكل صورة، تطبع وحدة التحكم أول 100 حرف من النص المُعترف به، مؤكدًا أن الدفعة نجحت دون الحاجة لفتح كل ملف يدويًا.

## كيفية حفظ نتائج OCR (اختياري لكنه مفيد)
حفظ الإخراج الكامل لـ OCR يتيح الفهرسة اللاحقة، التحليل الذكي، أو التحويل إلى ملفات PDF قابلة للبحث. اكتب النص إلى ملف `.txt` بجوار الصورة الأصلية، مستخدمًا نفس الاسم الأساسي لتسهيل الارتباط.

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

الآن كل صورة لديها ملف نصي مرفق يحتوي على الإخراج الكامل لـ OCR، جاهز لمحركات البحث، نماذج اللغة، أو خطوط تحليل مخصصة.

## كيفية تشغيل العرض التجريبي والتحقق من النتيجة
بناء وتشغيل تطبيق console لرؤية عملية الدفعة قيد التنفيذ. خطوة البناء تُجَمِّع الشيفرة، بينما خطوة التشغيل تعالج كل صورة في المجلد المستهدف وتكتب سطور المعاينة إلى وحدة التحكم. إذا فعلت خطوة الحفظ الاختيارية، ستجد أيضًا ملف `.txt` لكل صورة مصدر.

1. بناء المشروع: `dotnet build`.  
2. تشغيل البرنامج: `dotnet run --project GpuBatchDemo.csproj`.

سترى سطور معاينة في وحدة التحكم، وإذا أضفت الخطوة الاختيارية، ستحصل على مجموعة من ملفات `.txt` بجانب صورك المصدرية.

## المشكلات الشائعة وكيفية إصلاحها
| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| **Empty `ocrResult.Text`** | الصورة مظلمة جدًا أو DPI منخفض | قم بتمهيد الصور (زيادة التباين، تكبير) أو فعّل `ocrEngine.Settings.PreprocessImage = true`. |
| **GPU error “CUDA driver version is insufficient”** | برنامج تشغيل قديم | حدّث برنامج تشغيل GPU، أو اضبط `UseGpu = false` لإجبار المعالجة على CPU. |
| **Exception “File not found”** | فاصل مسار غير صحيح على Linux/macOS | استخدم `Path.Combine` أو الشرط المائل للأمام (`/`). |

## كيفية التوسع إلى ما وراء عدد قليل من الملفات
عند الانتقال من العشرات إلى الآلاف من الصور، ضع في اعتبارك الاستراتيجيات التالية: استخدم المعالجة المتوازية مع نسخ منفصلة من المحرك لكل خيط، حمّل الصور على دفعات قابلة للإدارة، وسجّل التقدم إلى ملف لتسهيل الاستعادة. هذه التقنيات تحافظ على استهلاك الذاكرة منخفضًا وتضمن معدل نقل عالي.

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **تذكر:** ذاكرة GPU مشتركة عبر العملية. بدء عدد كبير جدًا من وظائف GPU المتوازية قد يملأ الذاكرة ويبطئ الدفعة فعليًا. ابدأ بـ 2‑4 خيوط وراقب استهلاك GPU.

## الأسئلة المتكررة

**س: هل يمكن تشغيل نسخة GPU على خادم Linux بدون واجهة رسومية؟**  
ج: نعم، طالما أن الخادم يحتوي على GPU متوافق مع CUDA ومكتبات برنامج التشغيل المناسبة؛ لا يلزم وجود شاشة.

**س: هل يدعم Aspose OCR ملفات TIFF متعددة الصفحات مباشرةً؟**  
ج: بالطبع. يعامل المحرك كل صفحة كصورة منفصلة ويعيد النص المتسلسل، محافظًا على ترتيب الصفحات.

**س: ما مدى دقة ناتج OCR مقارنةً بخدمات السحابة؟**  
ج: تُظهر المعايير أن Aspose OCR يحقق ≥ 96 % دقة حرفية على المستندات المطبوعة النظيفة و≥ 90 % على المسحات منخفضة التباين، مساويًا لمزودي SaaS الرائدين مع الحفاظ على البيانات داخل المؤسسة.

**س: هل هناك حد لعدد الملفات التي يمكن معالجتها في تشغيل واحد؟**  
ج: لا تفرض المكتبة حدًا ثابتًا؛ الحدود العملية تُحدَّد بمساحة القرص المتاحة وذاكرة GPU. معالجة 10 000 صفحة على RTX 3080 عادةً لا تتجاوز 2 GB من ذاكرة GPU.

**س: هل يمكن تخصيص نموذج اللغة للخطوط غير الإنجليزية؟**  
ج: نعم، اضبط `ocrEngine.Language = OcrLanguage.Spanish` (أو أي لغة مدعومة) قبل استدعاء `Recognize`. يدعم المحرك أكثر من 30 لغة، بما فيها العربية، الصينية، والهندية.

## الخلاصة
أصبح لديك الآن حل كامل من البداية للنهاية لـ **batch OCR مع Aspose OCR GPU في C#**. غطى الدليل إعداد المشروع، تفعيل GPU، تعداد الملفات، معالجة كل صورة، حفظ النتائج اختياريًا، وتقنيات التوسع للعبء الكبير. باستخدام هذا الأساس يمكنك توجيه ناتج OCR إلى فهارس البحث، إمداده إلى نماذج اللغة الكبيرة، أو بناء خطوط معالجة مستندات مخصصة.

هل أنت مستعد للتحدي التالي؟ جرّب دمج نص OCR مع Aspose .PDF لإنشاء ملفات PDF قابلة للبحث، أو دمج النتيجة مع Azure Cognitive Search للحصول على بحث نص كامل فوري عبر آلاف المستندات الممسوحة.

---

**آخر تحديث:** 2026-09-13  
**تم الاختبار مع:** Aspose.OCR 24.5 للـ .NET (حزم CPU & GPU)  
**المؤلف:** Aspose  

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```
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

## دروس ذات صلة

- [كيفية استخدام OCR في C لاستخراج النص من الصور مع تسريع GPU](/ocr/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/)
- [التعرف على النص من صورة باستخدام Aspose OCR GPU في C](/ocr/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}