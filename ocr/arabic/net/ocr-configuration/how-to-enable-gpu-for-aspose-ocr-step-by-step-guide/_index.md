---
category: general
date: 2025-12-30
description: كيفية تمكين وحدة معالجة الرسومات (GPU) في Aspose OCR لمعالجة الدُفعات
  واستخراج نص OCR. تعلّم كيفية تعيين جهاز GPU وكيفية استخدام Aspose بفعالية.
draft: false
keywords:
- how to enable gpu
- batch ocr processing
- ocr text extraction
- set gpu device
- how to use aspose
language: ar
og_description: كيفية تمكين وحدة معالجة الرسومات (GPU) في Aspose OCR. اتبع هذا الدليل
  لمعالجة OCR على دفعات، استخراج نص OCR، ضبط جهاز GPU، وتعلم كيفية استخدام Aspose.
og_title: كيفية تمكين وحدة معالجة الرسومات (GPU) لـ Aspose OCR – دليل كامل
tags:
- Aspose
- OCR
- GPU
- C#
title: كيفية تمكين GPU لتقنية Aspose OCR – دليل خطوة بخطوة
url: /ar/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين GPU لـ Aspose OCR – دليل كامل

هل تساءلت يومًا **how to enable GPU** عند استخدام Aspose OCR؟ لست وحدك—المطورون الذين يتعاملون مع أحجام مستندات هائلة غالبًا ما يواجهون جدران أداء لأن محرك OCR عالق على الـ CPU. الخبر السار؟ تشغيل تسريع GPU أمر بسيط إلى حد ما، ويمكنه تقليل الثواني لكل صفحة. في هذا الدليل سنستعرض **how to enable GPU**، تشغيل **batch OCR processing**، استخراج النص المعترف به، وحتى اختيار جهاز GPU المناسب. في النهاية ستعرف **how to use Aspose** لاستخراج نص OCR بسرعة البرق.

## ما يغطيه هذا الدليل

سنبدأ بإعداد مكتبة Aspose OCR، ثم تمكين دعم GPU، وأخيرًا تشغيل دفعة من صور TIFF عبر المحرك. على طول الطريق سنشرح لماذا قد ترغب في **set GPU device** يدويًا، ما هي العقبات التي يجب الانتباه لها، وكيفية التحقق من أن استخراج النص قد نجح فعلاً. لا مستندات خارجية، مجرد حل كامل يمكن نسخه ولصقه وتشغيله اليوم.

> **Prerequisites**  
> - .NET 6.0 أو أحدث (الكود يستخدم صsyntax C# حديث)  
> - حزمة NuGet Aspose.OCR لـ .NET (الإصدار 23.10 أو أحدث)  
> - GPU متوافق مع CUDA مع تثبيت برنامج التشغيل المناسب  
> - مجلد يحتوي على بعض ملفات `.tif` التجريبية لتشغيل الدفعة  

إذا كنت قد غطيت هذه الأساسيات، دعنا نغوص في التفاصيل.

## كيفية تمكين GPU في Aspose OCR

أول شيء تحتاج إلى القيام به هو إخبار `OcrEngine` باستخدام الـ GPU. يتم ذلك عبر خاصيتين بسيطتين: `UseGpu` و `GpuDeviceId` (اختياري). ضبط `UseGpu` إلى `true` يحوّل المحرك إلى وضع GPU، بينما تسمح لك `GpuDeviceId` باختيار أي GPU (إذا كان لديك أكثر من واحد) سيتولى المهمة الثقيلة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;
using System.Collections.Generic;

// Step 1: Create the OCR engine and enable GPU acceleration
var ocrEngine = new OcrEngine
{
    // Turn on GPU support – this is the core of “how to enable gpu”
    UseGpu = true,

    // (optional) Choose GPU index 0; change if you have multiple devices
    GpuDeviceId = 0
};
```

> **Why this matters** – نسخة الـ CPU تعالج كل بكسل بشكل متسلسل، مما قد يصبح عنق زجاجة للصور عالية الدقة. نسخة الـ GPU تشغّل آلاف الخيوط بالتوازي، مما يقلل الوقت لكل صفحة بشكل كبير.

### نظرة بصرية  

![مخطط يوضح كيف يقوم محرك OCR بتحميل العمل إلى GPU عندما يتم ضبط “how to enable gpu”](/images/enable-gpu-diagram.png){: .center .responsive alt="كيفية تمكين GPU"}

*(إذا لم تتمكن من رؤية الصورة، تخيل مخطط تدفق حيث يسلم محرك OCR مخزن الصورة إلى نواة CUDA.)*

## معالجة OCR على دفعات مع Aspose

الآن بعد أن أصبح المحرك جاهزًا للـ GPU، دعنا نزوده بقائمة من الملفات. معالجة الدفعات بسيطة كالتكرار على `List<string>` التي تحتوي على مسارات صورك. لأننا نستخدم الـ GPU، سيقوم المحرك تلقائيًا بجدولة كل صورة إلى الجهاز، مما يبقي خط الأنابيب مشغولًا.

```csharp
// Step 2: Define the image files you want to process
var imageFiles = new List<string>
{
    @"C:\OCRSamples\page1.tif",
    @"C:\OCRSamples\page2.tif",
    @"C:\OCRSamples\page3.tif"
};

// Step 3: Process each image and report the character count
foreach (var imagePath in imageFiles)
{
    // Recognize the image – the GPU does the heavy lifting behind the scenes
    var ocrResult = ocrEngine.Recognize(imagePath);

    // Show how many characters were extracted – a quick sanity check
    Console.WriteLine($"{imagePath}: {ocrResult.Text.Length} characters");
}
```

> **Pro tip** – للدفعات الضخمة حقًا، فكر في استخدام `Parallel.ForEach` مع `ocrEngine.Clone()` لتجنب مشاكل سلامة الخيوط. طريقة `Clone` تنشئ نسخة سطحية من المحرك لا تزال تشير إلى نفس سياق الـ GPU.

### المخرجات المتوقعة

```
C:\OCRSamples\page1.tif: 1245 characters
C:\OCRSamples\page2.tif: 1130 characters
C:\OCRSamples\page3.tif: 1389 characters
```

إذا كانت الأرقام تبدو معقولة، فإن **batch OCR processing** يعمل والـ GPU يتم استغلاله.

## استخراج نص OCR – الحصول على النتائج

طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على النص الخام، درجات الثقة، وحتى الصناديق المحيطة إذا احتجت إليها. لنستخرج النص العادي ونكتبه إلى ملف حتى تتمكن من التحقق من عملية الاستخراج.

```csharp
foreach (var imagePath in imageFiles)
{
    var ocrResult = ocrEngine.Recognize(imagePath);
    var extractedText = ocrResult.Text;

    // Save the text to a .txt file with the same base name
    var outputPath = System.IO.Path.ChangeExtension(imagePath, ".txt");
    System.IO.File.WriteAllText(outputPath, extractedText);

    Console.WriteLine($"Extracted text saved to {outputPath}");
}
```

> **Why extract to a file?** – تخزين نص OCR يسمح بمعالجة لاحقة (فهرسة بحث، تنقيب بيانات، إلخ) دون الحاجة لإعادة تشغيل المحرك. كما يمنحك سجلًا دائمًا للتصحيح.

## ضبط جهاز GPU لأداء أمثل

إذا كان جهازك يحتوي على عدة بطاقات GPU—مثلاً RTX مخصص للتعلم الآلي وبطاقة رسومية مدمجة—ستحتاج إلى التأكد من أنك تستهدف البطاقة الصحيحة. خاصية `GpuDeviceId` تقبل عددًا صحيحًا يتطابق مع فهرس الجهاز الذي تُرجعه `CudaDeviceInfo.GetDevices()`.

```csharp
using Aspose.OCR.Gpu;

// List all available GPU devices
var devices = CudaDeviceInfo.GetDevices();
for (int i = 0; i < devices.Length; i++)
{
    Console.WriteLine($"Device {i}: {devices[i].Name} (Compute Capability {devices[i].ComputeCapability})");
}

// Suppose you want to use the second GPU (index 1)
ocrEngine.GpuDeviceId = 1;
Console.WriteLine($"Switched to GPU device {ocrEngine.GpuDeviceId}");
```

> **Edge case** – بعض بطاقات GPU القديمة لا تدعم نسخة CUDA المطلوبة. في هذه الحالة، `UseGpu = true` سيعود إلى الـ CPU بصمت، لذا تحقق دائمًا من `ocrEngine.IsGpuEnabled` بعد التهيئة.

## كيفية استخدام Aspose OCR في مشروع واقعي

بدمج كل ما سبق، إليك تطبيق كونسول صغير جاهز للتنفيذ يوضح **how to enable GPU**، يُجري **batch OCR processing**، يستخرج النص، ويسمح لك باختيار جهاز GPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine with GPU support
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,
            GpuDeviceId = 0 // change if you have multiple GPUs
        };

        // -------------------------------------------------
        // 2️⃣ (Optional) Show available GPU devices
        // -------------------------------------------------
        var devices = CudaDeviceInfo.GetDevices();
        Console.WriteLine("Available GPU devices:");
        for (int i = 0; i < devices.Length; i++)
        {
            Console.WriteLine($"  [{i}] {devices[i].Name} – Compute {devices[i].ComputeCapability}");
        }

        // -------------------------------------------------
        // 3️⃣ Define the batch of images to process
        // -------------------------------------------------
        var imageFiles = new List<string>
        {
            @"C:\OCRSamples\page1.tif",
            @"C:\OCRSamples\page2.tif",
            @"C:\OCRSamples\page3.tif"
        };

        // -------------------------------------------------
        // 4️⃣ Process each image, extract text, and save it
        // -------------------------------------------------
        foreach (var imagePath in imageFiles)
        {
            var result = ocrEngine.Recognize(imagePath);
            var text = result.Text;

            var txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, text);

            Console.WriteLine($"{Path.GetFileName(imagePath)} → {Path.GetFileName(txtPath)} ({text.Length} chars)");
        }

        Console.WriteLine("All done! GPU‑accelerated OCR batch completed.");
    }
}
```

### تشغيل العينة

1. ثبّت حزمة NuGet: `dotnet add package Aspose.OCR --version 23.10.0`  
2. استبدل المسارات في `imageFiles` بموقع ملفات `.tif` الخاصة بك.  
3. ابنِ وشغّل: `dotnet run`.  

سترى قائمة بطاقات الـ GPU، تليها سطر لكل صورة يُظهر عدد الأحرف ومسار ملف `.txt` المُولد.

## أسئلة شائعة ومشكلات محتملة

- **هل يعمل هذا على جهاز لا يحتوي إلا على CPU؟**  
  نعم—إذا كان `UseGpu` مضبوطًا على `true` ولكن لا توجد بطاقة GPU متوافقة، سيعود Aspose إلى الـ CPU. يمكنك التحقق من الوضع عبر `ocrEngine.IsGpuEnabled`.

- **ماذا لو حصلت على خطأ “إصدار برنامج تشغيل CUDA غير كافٍ”؟**  
  حدّث برنامج تشغيل NVIDIA إلى أحدث نسخة تتطابق مع مجموعة أدوات CUDA المرفقة مع Aspose. المكتبة تتطلب على الأقل CUDA 11.0 للميزات الحديثة للـ GPU.

- **هل يمكنني معالجة ملفات PDF مباشرة؟**  
  Aspose OCR يعمل على الصور النقطية. حوّل صفحات PDF إلى صور أولاً (مثلاً باستخدام Aspose.PDF) ثم مرّرها إلى محرك OCR.

- **كيف أحسن الدقة في المسحات الضوضائية؟**  
  فعّل خيارات ما قبل المعالجة مثل `ocrEngine.Preprocess = true` أو استخدم صورًا بدقة أعلى (300 dpi أو أكثر). لا يزال تسريع الـ GPU ساريًا.

## الخلاصة

غطّينا **how to enable GPU** لـ Aspose OCR، استعرضنا **batch OCR processing**، عرضنا **OCR text extraction**، وأظهرنا لك كيفية **set GPU device** لأداء أمثل. باتباع عينة الكود الكاملة يمكنك الآن دمج OCR سريع مدعوم بالـ GPU في أي مشروع .NET والإجابة بثقة على سؤال “how to use Aspose” المتكرر.

هل أنت مستعد للخطوة التالية؟ جرّب إضافة كشف اللغة، إمداد النص المستخرج إلى فهرس بحث، أو تجربة توسيع متعدد الـ GPU لأرشيفات مستندات ضخمة. السماء هي الحد عندما تجمع بين API القوي لـ Aspose وقوة بطاقات الـ GPU الحديثة.

برمجة سعيدة، ولتعمل وظائف OCR بأسرع ما يمكن للـ GPU الخاص بك!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}