---
category: general
date: 2026-09-08
description: تعلم كيفية تمكين GPU لـ Aspose OCR، تشغيل معالجة OCR على دفعات، واستخراج
  النص من الصور بكفاءة باستخدام .NET.
draft: false
keywords:
- how to enable gpu
- extract text from images
- batch ocr processing
- ocr gpu acceleration
- aspose ocr .net
lastmod: 2026-09-08
og_description: كيفية تمكين GPU لـ Aspose OCR. يوضح هذا الدليل معالجة OCR على دفعات،
  واستخراج النص من الصور، واختيار جهاز GPU الأمثل في .NET.
og_image_alt: Diagram of Aspose OCR engine offloading work to GPU for faster text
  extraction
og_title: كيفية تمكين GPU لـ Aspose OCR – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  headline: How to enable GPU for Aspose OCR – complete tutorial
  type: TechArticle
- description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  name: How to enable GPU for Aspose OCR – complete tutorial
  steps:
  - name: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
    text: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
  - name: Replace the paths in `imageFiles` with the location of your own `.tif` files.
    text: Replace the paths in `imageFiles` with the location of your own `.tif` files.
  - name: 'Build and run: `dotnet run`.'
    text: 'Build and run: `dotnet run`.'
  type: HowTo
- questions:
  - answer: Yes, a commercial Aspose.OCR license is needed for production deployments;
      a free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Any NVIDIA GPU that supports CUDA 11.0 or newer, such as RTX 2060, RTX
      3070, RTX 4090, and the corresponding Tesla series.
    question: Which GPU models are officially supported?
  - answer: Absolutely. The same `OcrEngine` instance can be reused across requests;
      just ensure thread safety by cloning the engine per request.
    question: Can I run this code in an ASP.NET Core web API?
  - answer: Yes, you can set `ocrEngine.Language = Language.English | Language.Spanish`
      to enable simultaneous recognition of multiple languages.
    question: Does Aspose OCR handle multi‑language documents?
  - answer: The engine streams image data, so you can process images up to 10,000
      × 10,000 pixels without exhausting GPU memory, though performance may vary.
    question: What is the maximum image size the GPU can handle?
  type: FAQPage
tags:
- Aspose OCR
- GPU acceleration
- C#
- .NET
title: كيفية تمكين GPU لـ Aspose OCR – دليل كامل
url: /ar/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين GPU لـ Aspose OCR – دليل كامل

هل تساءلت يومًا **كيفية تمكين GPU** عند استخدام Aspose OCR؟ لست وحدك—المطورون الذين يتعاملون مع أحجام هائلة من المستندات غالبًا ما يواجهون جدران أداء لأن محرك OCR عالق على وحدة المعالجة المركزية. الخبر السار؟ تشغيل تسريع GPU سهل إلى حد ما، ويمكنه تقليل الثواني من كل صفحة. في هذا الدليل سنستعرض **كيفية تمكين GPU**، تشغيل **معالجة OCR دفعة**، استخراج النص المعترف به، وحتى اختيار جهاز GPU المناسب. في النهاية ستعرف **كيفية استخدام Aspose** لاستخراج نص OCR بسرعة البرق.

## إجابات سريعة
- **ماذا يفعل تمكين GPU؟** ينقل تحليل مستوى البكسل إلى بطاقة الرسومات، مما يقلل زمن المعالجة حتى 80 % على الصور ذات 300 dpi النموذجية.  
- **هل أحتاج إلى ترخيص خاص؟** لا، حزمة Aspose.OCR NuGet القياسية تتضمن دعم GPU.  
- **ما نسخة .NET المطلوبة؟** .NET 6.0 أو أحدث؛ الـ API يستخدم ميزات C# الحديثة.  
- **هل يمكنني التشغيل على جهاز يملك CPU فقط؟** نعم—إذا لم يُعثر على GPU متوافق، يعود المحرك تلقائيًا إلى CPU.  
- **كم عدد الصور التي يمكنني معالجتها في آن واحد؟** يمكنك وضع مئات الملفات في الطابور؛ سيتعامل GPU معها بشكل متسلسل بينما يمكن لكودك إمداد الصورة التالية بمجرد انتهاء السابقة.

## ما هو كيفية تمكين GPU؟
`كيفية تمكين GPU` هي عملية تكوين `OcrEngine` الخاص بـ Aspose OCR لتوجيه أحمال معالجة الصور إلى بطاقة رسومات متوافقة مع CUDA بدلاً من المعالج المركزي. يتم التحكم في هذا التحويل عبر خاصيتين: `UseGpu` و `GpuDeviceId`. تمكين هذه العلامة ينقل تحليل البكسل المكثف حسابيًا إلى GPU، الذي يمكنه معالجة آلاف الخيوط بالتوازي، مما يقلل زمن المعالجة بشكل كبير.

فئة `OcrEngine` هي المكوّن الأساسي لـ Aspose OCR الذي يقوم بتحليل الصور والتعرف على النص.

## لماذا استخدام تسريع GPU مع Aspose OCR؟
يدعم Aspose OCR **أكثر من 50 تنسيق صورة** ويمكنه معالجة دفعات مئات الصفحات دون تحميل المستند بالكامل في الذاكرة. عند تمكين تسريع GPU، تُظهر اختبارات الأداء **انخفاضًا بنسبة 70 %‑80 %** في متوسط زمن معالجة كل صفحة على RTX 3080 مقارنةً بالتنفيذ على CPU فقط. هذه الزيادة في السرعة تتحول مباشرة إلى تقليل تكاليف السحابة ونتائج أسرع للمستخدم في التطبيقات التي تتعامل مع مستندات كثيرة.

## المتطلبات المسبقة
- .NET 6.0 أو أحدث (الكود يستخدم بنية C# الحديثة)  
- حزمة Aspose.OCR لـ .NET عبر NuGet (الإصدار 23.10 أو أحدث)  
- GPU متوافق مع CUDA مع تثبيت برنامج التشغيل المناسب (الحد الأدنى CUDA 11.0)  
- مجلد يحتوي على ملفات `.tif` نموذجية لتشغيل الدفعة  

إذا كنت قد غطيت هذه الأساسيات، فلنغوص في التفاصيل.

## كيفية تمكين GPU في Aspose OCR

حمّل محرك OCR، فعّل وضع GPU، واختياريًا اختر فهرس الجهاز.  

`OcrEngine` هي الفئة الأساسية لـ Aspose OCR التي تقوم بتحليل الصور والتعرف على النص.  

تمكين GPU هو عملية من خطوتين: ضبط `UseGpu = true` وعند وجود عدة GPUs، تعيين `GpuDeviceId` المطلوب. يشرح هذا الفقرة المباشرة العملية بالكامل في 45 كلمة.

أول شيء تحتاج إخبار `OcrEngine` به لاستخدام GPU. يتم ذلك عبر خاصيتين بسيطتين: `UseGpu` واختياريًا `GpuDeviceId`. ضبط `UseGpu` إلى `true` يحول المحرك إلى وضع GPU، بينما يتيح لك `GpuDeviceId` اختيار أي GPU (إذا كان لديك أكثر من واحد) سيتولى الأعمال الثقيلة.

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

> **لماذا هذا مهم** – نسخة CPU تعالج كل بكسل بشكل متسلسل، مما قد يكون عنق زجاجة للصور عالية الدقة. نسخة GPU تشغل آلاف الخيوط بالتوازي، مما يقلل زمن كل صفحة بشكل كبير.

### نظرة بصرية  

![مخطط يوضح كيف يقوم محرك OCR بتحميل العمل إلى GPU عندما يتم تعيين “how to enable gpu”](/images/enable-gpu-diagram.png){: .center .responsive alt="كيفية تمكين gpu"}

[مخطط يوضح كيف يقوم محرك OCR بتحميل العمل إلى GPU عندما يتم تعيين “how to enable gpu”](/images/enable-gpu-diagram.png)

*(إذا لم تتمكن من رؤية الصورة، تخيل مخطط تدفق حيث يسلم محرك OCR مخزن الصورة إلى نواة CUDA.)*

## كيفية تشغيل معالجة OCR دفعة مع Aspose

طريقة `Recognize` في `OcrEngine` تعالج صورة وتعيد `OcrResult` يحتوي على النص المستخرج والبيانات الوصفية. يمكنك معالجة مجلد كامل عبر التكرار على قائمة مسارات الملفات. يقوم المحرك تلقائيًا بوضع كل صورة في طابور إلى GPU، مما يبقي خط الأنابيب مشغولًا بينما يستمر تطبيقك في إمداد ملفات جديدة. يتيح لك هذا النهج التعامل مع مئات ملفات TIFF بكفاءة، مع تولي GPU الأعمال الثقيلة بالتوازي.

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

> **نصيحة احترافية** – للدفعات الضخمة حقًا، فكر في استخدام `Parallel.ForEach` مع `ocrEngine.Clone()` لتجنب مشكلات سلامة الخيوط. طريقة `Clone` تنشئ نسخة سطحية من المحرك لا تزال تشير إلى نفس سياق GPU.

### النتيجة المتوقعة

```
C:\OCRSamples\page1.tif: 1245 characters
C:\OCRSamples\page2.tif: 1130 characters
C:\OCRSamples\page3.tif: 1389 characters
```

إذا كانت الأرقام تبدو معقولة، فإن **معالجة OCR دفعة** تعمل ويتم استخدام GPU.

## كيفية استخراج النص من الصور – الحصول على النتائج

`OcrResult` هو الكائن الذي يحمل ناتج OCR، بما في ذلك النص المعترف به، درجات الثقة، ومعلومات التخطيط. طريقة `Recognize` تُعيد كائن `OcrResult`. استخرج النص العادي من الخاصية `Text` واكتبها إلى ملف للاستخدام اللاحق. تخزين نص OCR يسمح بالمعالجة اللاحقة (فهرسة البحث، استخراج البيانات، إلخ) دون إعادة تشغيل المحرك ويعطيك سجلًا دائمًا للتصحيح.

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

> **لماذا استخراج إلى ملف؟** – تخزين نص OCR يسمح بالمعالجة اللاحقة (فهرسة البحث، استخراج البيانات، إلخ) دون إعادة تشغيل المحرك. كما يمنحك سجلًا دائمًا للتصحيح.

## كيفية تعيين جهاز GPU للأداء الأمثل

`CudaDeviceInfo` يوفر معلومات حول GPUs المتوافقة مع CUDA المثبتة على النظام. عندما تكون هناك عدة GPUs، استخدم `GpuDeviceId` لاختيار الأنسب. الفهرس يتطابق مع الترتيب الذي تُعيده `CudaDeviceInfo.GetDevices()`. اختيار الجهاز المناسب يضمن استخدام أقوى GPU وتجنب التنافس مع أحمال عمل أخرى على البطاقات الثانوية.

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

> **حالة حافة** – بعض GPUs القديمة لا تدعم نسخة CUDA المطلوبة. في هذه الحالة، `UseGpu = true` سيعود إلى CPU بصمت، لذا تحقق دائمًا من `ocrEngine.IsGpuEnabled` بعد التهيئة.

## كيفية استخدام Aspose OCR في مشروع واقعي

بجمع كل شيء معًا، إليك تطبيق كونسول مضغوط وجاهز للتنفيذ يوضح **كيفية تمكين GPU**، يشغل **معالجة OCR دفعة**، يستخرج النص، ويسمح لك باختيار جهاز GPU. العينة تنشئ `OcrEngine`، تمكّن GPU، تُعدد الأجهزة المتاحة، تعالج كل صورة، وتكتب النص المعترف به إلى ملف `.txt` بجانب الصورة الأصلية.

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

1. ثبت حزمة NuGet: `dotnet add package Aspose.OCR --version 23.10.0`  
2. استبدل المسارات في `imageFiles` بموقع ملفات `.tif` الخاصة بك.  
3. ابنِ وشغّل: `dotnet run`.  

يجب أن ترى قائمة GPUs، تليها سطر لكل صورة يُظهر عدد الأحرف ومسار ملف `.txt` المُولد.

## أسئلة شائعة ومشكلات محتملة

- **هل يعمل هذا على جهاز CPU فقط؟**  
  نعم—إذا كان `UseGpu` `true` ولكن لا يُعثر على GPU متوافق، فإن Aspose يعود إلى CPU. يمكنك التحقق من الوضع عبر `ocrEngine.IsGpuEnabled`.

- **ماذا لو حصلت على خطأ “إصدار برنامج تشغيل CUDA غير كافٍ”؟**  
  حدّث برنامج تشغيل NVIDIA إلى أحدث نسخة تتطابق مع مجموعة أدوات CUDA المرفقة مع Aspose. المكتبة تتطلب على الأقل CUDA 11.0 للميزات الحديثة للـ GPU.

- **هل يمكنني معالجة ملفات PDF مباشرة؟**  
  Aspose OCR يعمل على الصور النقطية. حوّل صفحات PDF إلى صور أولاً (مثلًا باستخدام Aspose.PDF) ثم قدمها إلى محرك OCR.

- **كيف أحسن الدقة في المسحات الضوضائية؟**  
  فعّل خيارات ما قبل المعالجة مثل `ocrEngine.Preprocess = true` أو قدم صورًا ذات دقة أعلى (300 dpi أو أكثر). لا يزال تسريع GPU ساريًا.

## الأسئلة المتكررة

**س: هل يلزم ترخيص للاستخدام في الإنتاج؟**  
ج: نعم، يلزم الحصول على ترخيص تجاري لـ Aspose.OCR للنشر في بيئات الإنتاج؛ تتوفر نسخة تجريبية مجانية للتقييم.

**س: أي نماذج GPU مدعومة رسميًا؟**  
ج: أي GPU من NVIDIA يدعم CUDA 11.0 أو أحدث، مثل RTX 2060، RTX 3070، RTX 4090، وسلسلة Tesla المقابلة.

**س: هل يمكن تشغيل هذا الكود في واجهة ويب ASP.NET Core؟**  
ج: بالتأكيد. يمكن إعادة استخدام نفس كائن `OcrEngine` عبر الطلبات؛ فقط تأكد من سلامة الخيوط عن طريق استنساخ المحرك لكل طلب.

**س: هل يدعم Aspose OCR المستندات متعددة اللغات؟**  
ج: نعم، يمكنك ضبط `ocrEngine.Language = Language.English | Language.Spanish` لتمكين التعرف المتزامن على عدة لغات.

**س: ما هو الحد الأقصى لحجم الصورة الذي يمكن للـ GPU معالجته؟**  
ج: المحرك يبث بيانات الصورة، لذا يمكنك معالجة صور تصل إلى 10,000 × 10,000 بكسل دون استنفاد ذاكرة GPU، رغم أن الأداء قد يختلف.

---

**آخر تحديث:** 2026-09-08  
**تم الاختبار مع:** Aspose.OCR 23.10 لـ .NET  
**المؤلف:** Aspose

## دروس ذات صلة

- [كيفية استخدام OCR في C لاستخراج النص من الصور مع تسريع GPU](/ocr/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/)
- [استخراج النص من الصورة باستخدام Aspose OCR GPU دليل C](/ocr/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-gpu-c-guide/)
- [إزالة خلفية OCR باستخدام Aspose OCR دليل GPU كامل](/ocr/net/ocr-optimization/remove-background-ocr-with-aspose-ocr-complete-gpu-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}