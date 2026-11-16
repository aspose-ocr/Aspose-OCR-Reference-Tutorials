---
category: general
date: 2026-03-13
description: كيفية استخدام OCR في C# لاستخراج النص من المسحات الضوئية. تعلم تحويل
  ملفات TIFF إلى نص باستخدام Aspose OCR، تسريع GPU، وكود خطوة بخطوة.
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: ar
og_description: كيفية استخدام OCR في C# لاستخراج النص من المسحات الضوئية. يوضح هذا
  الدليل كيفية تحويل TIFF إلى نص باستخدام Aspose OCR وتسريع GPU.
og_title: كيفية استخدام OCR في C# – استخراج النص من المسح الضوئي بسرعة
tags:
- OCR
- C#
- Aspose
- Image Processing
title: كيفية استخدام OCR في C# – استخراج النص من المسح الضوئي بسرعة
url: /ar/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# – استخراج النص من المسح الضوئي بسرعة

هل تساءلت يومًا **كيفية استخدام OCR** لاستخراج نص قابل للقراءة من مجموعة من ملفات TIFF الممسوحة ضوئيًا؟ لست الوحيد. في العديد من المشاريع الواقعية—مثل رقمنة الفواتير، أرشفة الوثائق التاريخية، أو ببساطة جعل ملفات PDF قابلة للبحث—يحتاج المطورون إلى طريقة موثوقة **لاستخراج النص من المسح الضوئي** دون عناء.

الخبر السار؟ باستخدام Aspose OCR وبضع أسطر من C# يمكنك تحويل TIFF إلى نص في غضون ثوانٍ، حتى على محطة عمل متواضعة. أدناه ستحصل على مثال كامل جاهز للتنفيذ، بالإضافة إلى شرح السبب وراء كل اختيار حتى تتمكن من تكييفه مع سير عملك.

## ما ستحتاجه

| المتطلب | لماذا يهم |
|--------------|----------------|
| .NET 6+ (or .NET Framework 4.7+) | حزمة Aspose OCR NuGet تستهدف بيئات .NET الحديثة. |
| Visual Studio 2022 (or any IDE you like) | توفر لك IntelliSense وتصحيح الأخطاء بسهولة. |
| CUDA‑compatible GPU & driver (optional) | يتيح `ocrEngine.UseGpu = true` تحسينًا ملحوظًا في السرعة على الدفعات الكبيرة. |
| A folder of TIFF images you want to process | يستخدم هذا الدرس ملفات `*.tif`، لكن يمكنك تعديل النمط. |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | المكتبة الأساسية التي تقوم بالمعالجة الثقيلة. |

إذا كان أيٌ من هذه غير متوفر لديك، احصل عليه الآن—لا فائدة من المتابعة فقط لتصادف نقصًا في الاعتماديات لاحقًا.

## نظرة عامة على الحل

على مستوى عالٍ، يقوم البرنامج بثلاثة أشياء:

1. **إنشاء محرك OCR** وتفعيل تسريع GPU اختياريًا.  
2. **التكرار على كل ملف TIFF** في دليل، تشغيل التعرف، والتقاط النص الناتج.  
3. **كتابة النص** إلى ملف `.txt` بجوار الصورة الأصلية.

هذا كل شيء. الكود صغير عمدًا، لكنه يوضح أفضل الممارسات مثل اختيار اللغة صراحةً، التخلص السليم من الموارد، ومعالجة الأخطاء لأكثر الحالات شيوعًا.

![مثال على كيفية استخدام OCR في C#](/images/how-to-use-ocr-csharp.png "رسم توضيحي لكيفية استخدام OCR في C# لاستخراج النص من المسح الضوئي")

## الخطوة 1: تهيئة محرك OCR (كيفية استخدام OCR)

أول شيء تحتاجه هو نسخة من `OcrEngine`. هذا الكائن هو البوابة إلى جميع وظائف Aspose OCR. بشكل افتراضي يعمل على وحدة المعالجة المركزية، لكن ضبط `UseGpu = true` يوجه المكتبة لتحميل حسابات المصفوفات الثقيلة إلى بطاقة الرسوميات الخاصة بك— بشرط أن يكون لديك برنامج تشغيل متوافق مع CUDA مثبت.

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**لماذا هذا مهم:**  
- **تسريع GPU** يمكن أن يقلل وقت المعالجة حتى 70 % للماسحات عالية الدقة.  
- **اختيار اللغة صراحةً** يمنع المحرك من التخمين ويحسن الدقة، خاصةً للخطوط غير اللاتينية.

## الخطوة 2: توجيه المحرك إلى ملفات المسح (تحويل TIFF إلى نص)

بعد ذلك نخبر البرنامج بمكان البحث عن الصور. استخدام `Directory.GetFiles` مع مرشح `*.tif` يبقي المنطق بسيطًا ويتجنب جلب ملفات غير ذات صلة مثل `.jpg` أو `.png`.

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**ملاحظة حالة الحافة:** إذا كان الدليل فارغًا، فإن الحلقة أدناه ببساطة لا تُنفّذ أبداً، وهذا مقبول تمامًا. سترى رسالة ودية “No files found” لاحقًا.

## الخطوة 3: معالجة كل ملف TIFF (استخراج النص من المسح الضوئي)

الآن قلب البرنامج: تحميل كل صورة، تشغيل OCR، وحفظ الناتج. المساعد `ImageStream.FromFile` يرسل الملف مباشرة إلى الذاكرة، وهو أكثر كفاءة من تحميل `Bitmap` أولاً.

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**لماذا نغلف كل تكرار بـ `try/catch`:**  
مسح دفعة من المستندات قد يكون فوضويًا؛ ملف TIFF تالف أو انقطاع الذاكرة لا ينبغي أن يوقف التنفيذ بالكامل. كتلة الـ catch تسجل المشكلة وتستمر، مما يحافظ على استقرار الخط.

### النتيجة المتوقعة

لكل ملف `example.tif` ستجد ملفًا شقيقًا `example.txt` يحتوي على شيء مشابه:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

إذا لم يتمكن محرك OCR من قراءة سطر، سيترك سطرًا فارغًا أو حرفًا مشوشًا— ولا يحدث أي تعطل.

## الخطوة 4: التنظيف والتخلص (أفضل ممارسة)

`OcrEngine` يطبق `IDisposable`، لذا من الأدب تحرير الموارد الأصلية عند الانتهاء. في تطبيق كونسول قصير يمكنك الاعتماد على الـ GC، لكن التحرير الصريح عادة تستحق تبنيها.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل الذي يمكنك لصقه في مشروع تطبيق كونسول جديد. يترجم كما هو، بشرط أن تكون قد أضفت حزمة Aspose.OCR NuGet.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### قائمة التحقق السريعة

- **علامة GPU** – احذفها أو اضبطها على `false` إذا لم يكن لديك برنامج تشغيل CUDA.  
- **اللغة** – استبدل `Language.English` بأي لغة مدعومة أخرى.  
- **نمط الملف** – غيّر `"*.tif"` إلى `"*.png"` أو `"*.*"` إذا كانت مسحاتك بصيغة أخرى.  

## الأخطاء الشائعة والنصائح الاحترافية (دروس OCR في C#)

| المشكلة | كيفية تجنبها |
|---------|-----------------|
| **أخطاء نفاد الذاكرة** في دفعات ضخمة | معالجة الملفات على دفعات أصغر أو استدعاء `GC.Collect()` بعد كل 50 ملفًا (نادراً ما يكون ضروريًا). |
| **GPU غير مكتشف** رغم ضبط `UseGpu = true` | المحرك يعود صامتًا إلى CPU، لكن يمكنك التحقق من `ocrEngine.IsGpuAvailable` بعد الإنشاء. |
| **حزمة اللغة الخاطئة** تؤدي إلى مخرجات مشوشة | دائمًا اضبط `ocrEngine.Language` صراحةً؛ الافتراضي قد يكون `Language.Unknown`. |
| **مسار الملف يحتوي على أحرف Unicode** | استخدم `Path.GetFullPath` للتطبيع، أو أضف البادئة `@"\\?\"` على Windows إذا تجاوزت المسارات |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}