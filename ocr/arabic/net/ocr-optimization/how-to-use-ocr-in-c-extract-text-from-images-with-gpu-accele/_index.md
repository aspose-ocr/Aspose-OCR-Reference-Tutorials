---
category: general
date: 2025-12-29
description: كيفية استخدام OCR في C# لاستخراج النص من الصور، وعرض عدد الأحرف، وتعزيز
  الأداء باستخدام تسريع GPU عبر Aspose OCR.
draft: false
keywords:
- how to use OCR
- extract text image
- display character count
- gpu acceleration ocr
- c# ocr aspose
language: ar
og_description: كيفية استخدام OCR في C# لاستخراج النص من الصور، وعرض عدد الأحرف، وتسريع
  المعالجة باستخدام GPU مع Aspose OCR.
og_title: كيفية استخدام OCR في C# – استخراج النص بسرعة باستخدام وحدة معالجة الرسومات
tags:
- OCR
- C#
- Aspose
- GPU
title: كيفية استخدام OCR في C# – استخراج النص من الصور باستخدام تسريع GPU
url: /ar/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيف تستخدم OCR في C# – دليل كامل

هل تساءلت يومًا **كيف تستخدم OCR** في مشروع .NET دون كتابة آلاف الأسطر من الشيفرة؟ ربما قمت بمسح ملف TIFF ضخم وتحتاج إلى النص بسرعة، أو تريد فقط عد الأحرف لواجهة تقارير. في أي حال، أنت في المكان الصحيح. في هذا البرنامج التعليمي سنستعرض استخراج النص من صورة، عرض عدد الأحرف، وتعزيز العملية باستخدام **GPU acceleration OCR** – كل ذلك باستخدام مكتبة **C# Aspose OCR**.

سنضيف أيضًا المواضيع الثانوية التي قد تبحث عنها: **extract text image**, **display character count**, و**c# ocr aspose**. في النهاية ستحصل على تطبيق console جاهز للتشغيل يمكنه معالجة المسحات الكبيرة في لمح البصر.

---

## ما ستتعلمه

- إعداد Aspose OCR في مشروع C# (بدون أسرار NuGet).
- تمكين **GPU acceleration OCR** للملفات الضخمة.
- تحميل صورة و**extract text from the image**.
- **Display character count** ووقت المعالجة.
- التعامل مع المشكلات الشائعة مثل نقص تعريفات GPU أو صيغ الصور غير المدعومة.

> **المتطلبات المسبقة:** .NET 6+ (أو .NET Framework 4.7.2) وGPU متوافق. إذا لم يكن لديك GPU، سيتحول الكود بسلاسة إلى وضع CPU.

---

![How to use OCR with GPU acceleration in C#](ocr-gpu.png "how to use OCR example showing GPU usage")
*نص بديل للصورة: توضيح كيفية استخدام OCR مع تسريع GPU*

---

## الخطوة 1: تثبيت Aspose OCR وتحضير المشروع

### لماذا هذا مهم

قبل أن تتمكن من **use OCR**، يجب الإشارة إلى المكتبة. Aspose OCR يأتي كحزمة NuGet واحدة تضم الثنائيات الأصلية لكل من CPU وGPU، لذا لن تحتاج إلى البحث عن DLLs يدويًا.

```csharp
// In your terminal or Package Manager Console
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت تستهدف .NET Framework، استخدم واجهة NuGet في Visual Studio لتجنب تعارض الإصدارات.

### هيكل المشروع الكامل

أنشئ تطبيق console جديد والصق الكود التالي في `Program.cs`. يتضمن جميع عبارات `using` المطلوبة، لذا لن تحتاج إلى التخمين بشأن ما يجب استيراده.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.ImageProcessing; // optional, for advanced pre‑processing

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Call the helper that does the heavy lifting
            RunOcr(@"YOUR_DIRECTORY/large_scanned_page.tif");
        }

        static void RunOcr(string imagePath)
        {
            // Step 2: Create and configure the OCR engine (see next section)
        }
    }
}
```

احفظ الملف، استعد الحزم، وستكون جاهزًا للخطوة التالية.

---

## الخطوة 2: كيفية استخدام محرك OCR مع تسريع GPU

### لماذا تمكين GPU؟

معالجة ملف TIFF متعدد الميجابكسل على CPU قد تستغرق ثوانٍ أو حتى دقائق. مسار **GPU acceleration OCR** يرفع عمليات البكسل إلى بطاقة الرسومات، مما يقلل الوقت بشكل كبير—غالبًا إلى جزء صغير من الوقت الأصلي.

```csharp
static void RunOcr(string imagePath)
{
    // Create an OCR engine instance
    var ocrEngine = new OcrEngine();

    // Enable GPU acceleration – if a compatible device is found
    ocrEngine.UseGpu = true;
    ocrEngine.GpuDeviceId = 0; // 0 = first GPU; change if you have multiple

    // Optional sanity check – fall back to CPU if GPU init fails
    try
    {
        // This call forces the engine to initialize GPU resources
        ocrEngine.InitializeGpu();
        Console.WriteLine("✅ GPU acceleration enabled.");
    }
    catch (Exception ex)
    {
        Console.WriteLine($"⚠️ GPU init failed ({ex.Message}), switching to CPU.");
        ocrEngine.UseGpu = false;
    }

    // Load the image (this also validates format)
    var inputImage = Image.Load(imagePath);
    
    // Perform OCR – the heavy lifting happens here
    var ocrResult = ocrEngine.Recognize(inputImage);

    // Step 3: Display results (character count & processing time)
    DisplayResult(ocrResult);
}
```

> **لماذا يعمل ذلك:** `UseGpu` يبدّل خط الأنابيب الداخلي. `InitializeGpu()` يجري التحقق المبكر حتى يمكنك اكتشاف مشاكل التعريف قبل استدعاء `Recognize` الطويل.

---

## الخطوة 3: استخراج النص من الصورة وعرض عدد الأحرف

الآن بعد أن المحرك يعمل بسلاسة، دعنا **extract text from the image** ونظهر عدد الأحرف التي تم التعرف عليها. هذه هي الخطوة التي يتخطاها معظم المطورين، لكنها أساسية للتحقق والتحليلات اللاحقة.

```csharp
static void DisplayResult(OcrResult ocrResult)
{
    // The raw OCR text
    string extractedText = ocrResult.Text;

    // Character count – includes spaces and line breaks
    int charCount = extractedText.Length;

    // Processing time in milliseconds (provided by Aspose)
    long processingMs = ocrResult.ProcessingTime;

    // Output to console – easy to pipe to a file or logger
    Console.WriteLine($"🖋️ Extracted {charCount} characters in {processingMs} ms");
    Console.WriteLine("----- Begin OCR Text -----");
    Console.WriteLine(extractedText);
    Console.WriteLine("------ End OCR Text ------");
}
```

**الناتج المتوقع** (مثال لمسح من صفحتين):

```
✅ GPU acceleration enabled.
🖋️ Extracted 12,345 characters in 842 ms
----- Begin OCR Text -----
Lorem ipsum dolor sit amet, consectetur...
... (rest of the page) ...
------ End OCR Text ------
```

إذا لم يتوفر GPU، ستظهر لك تحذير وستحصل على نفس النتيجة، ولكن ببطء أكبر.

---

## الخطوة 4: معالجة الملفات الكبيرة والحالات الخاصة

### ماذا لو كانت الصورة ضخمة؟

Aspose OCR يمكنه بث الصفحات، لكن لا يزال يتطلب ذاكرة RAM كافية. من الممارسات الجيدة تقليل DPI غير الضروري قبل التعرف:

```csharp
// Optional pre‑processing: downscale to 300 DPI if original > 600 DPI
if (inputImage.DpiX > 600 || inputImage.DpiY > 600)
{
    inputImage = inputImage.Resize(0.5, 0.5); // 50% reduction
    Console.WriteLine("🔎 Image downscaled for faster OCR.");
}
```

### نقص تعريفات GPU؟

كتلة `try/catch` حول `InitializeGpu()` تلتقط معظم المشكلات، لكن يمكنك أيضًا الاستعلام عن الأجهزة المتاحة:

```csharp
var gpuInfo = GpuDeviceManager.GetDevices();
if (gpuInfo.Count == 0)
{
    Console.WriteLine("⚡ No GPU detected – defaulting to CPU.");
    ocrEngine.UseGpu = false;
}
```

### صيغ الصور غير المدعومة؟

Aspose يدعم TIFF، PNG، JPEG، BMP، وبعض الصيغ النادرة. إذا حصلت على `UnsupportedFormatException`، حوّل الملف أولًا باستخدام أداة مثل ImageMagick أو الطريقة المدمجة `Image.Save` إلى PNG.

---

## الخطوة 5: الخاتمة – مثال كامل يعمل

انسخ‑الصق البرنامج الكامل أدناه إلى `Program.cs`. إنه عرض توضيحي مستقل يمكنك تشغيله فورًا (فقط استبدل المسار).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.ImageProcessing;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust the path to point at your scanned TIFF or JPEG
            RunOcr(@"YOUR_DIRECTORY/large_scanned_page.tif");
        }

        static void RunOcr(string imagePath)
        {
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,
                GpuDeviceId = 0
            };

            try
            {
                ocrEngine.InitializeGpu();
                Console.WriteLine("✅ GPU acceleration enabled.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ GPU init failed ({ex.Message}), switching to CPU.");
                ocrEngine.UseGpu = false;
            }

            var inputImage = Image.Load(imagePath);

            // Optional downscale for gigantic files
            if (inputImage.DpiX > 600 || inputImage.DpiY > 600)
            {
                inputImage = inputImage.Resize(0.5, 0.5);
                Console.WriteLine("🔎 Image downscaled for faster OCR.");
            }

            var ocrResult = ocrEngine.Recognize(inputImage);
            DisplayResult(ocrResult);
        }

        static void DisplayResult(OcrResult ocrResult)
        {
            string extractedText = ocrResult.Text;
            int charCount = extractedText.Length;
            long processingMs = ocrResult.ProcessingTime;

            Console.WriteLine($"🖋️ Extracted {charCount} characters in {processingMs} ms");
            Console.WriteLine("----- Begin OCR Text -----");
            Console.WriteLine(extractedText);
            Console.WriteLine("------ End OCR Text ------");
        }
    }
}
```

شغّله باستخدام `dotnet run` وسترى في وحدة التحكم **character count** ونص OCR. هذه هي دورة **how to use OCR** من البداية إلى النهاية.

---

## الخلاصة

لقد غطينا **how to use OCR** في C# لـ **extract text from images**, **display character count**, وتسريع الخط الأنابيب بالكامل باستخدام **GPU acceleration OCR** عبر مكتبة **c# ocr aspose**. النقاط الأساسية:

1. تثبيت Aspose OCR عبر NuGet وإضافة المساحات الاسمية الصحيحة.  
2. تفعيل GPU، مع وجود fallback إلى CPU دائمًا.  
3. تحميل الصورة، تقليل الدقة إذا لزم، ثم استدعاء `Recognize`.  
4. استخراج `ocrResult.Text` و`ocrResult.ProcessingTime` لعرض عدد الأحرف ومقاييس الأداء.  

من هنا يمكنك التوسع—تخزين النص في قاعدة بيانات، إرساله إلى فهرس بحث، أو تشغيل كشف لغة على السلسلة المستخرجة. إذا احتجت لمعالجة PDFs، ما عليك سوى تحويل كل صفحة إلى صورة؛ نفس الكود سيعمل.

**الخطوات التالية** التي قد تستكشفها:

- استخدام **extract text image** من ملفات PDF متعددة الصفحات عبر `PdfConverter`.  
- تعديل إعدادات OCR (حزم اللغات، تقليل الضوضاء) لتحسين الدقة.  
- توسيع الحل في Azure Functions أو AWS Lambda باستخدام مثيلات مدعومة بـ GPU.  

جرّبه، اكسره، ثم حسّنه. هكذا تُبنى مشاريع OCR الواقعية. برمجة سعيدة، ولتكن مسحاتك دائمًا قابلة للقراءة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}