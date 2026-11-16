---
category: general
date: 2026-03-05
description: تحويل ملفات TIFF إلى نص في C# باستخدام Aspose OCR — استخراج النص من ملفات
  الصور الممسوحة ضوئياً بسرعة وتعلم كيفية تحميل ملف الصورة في C# لمعالجة OCR.
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: ar
og_description: تحويل ملفات TIFF إلى نص في C# باستخدام Aspose OCR. تعلّم سير العمل
  الكامل لاستخراج النص من الصور الممسوحة ضوئياً وتحميل ملفات الصور بكفاءة.
og_title: تحويل TIFF إلى نص في C# – استخراج نص الصورة الممسوحة ضوئياً
tags:
- OCR
- C#
- Aspose
title: تحويل TIFF إلى نص في C# – استخراج نص الصورة الممسوحة ضوئياً
url: /ar/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل TIFF إلى نص في C# – استخراج نص الصورة الممسوحة ضوئياً

هل تحتاج إلى **تحويل TIFF إلى نص في C#**؟ لست الوحيد الذي يكافح مع صور ممسوحة ضوئياً متعددة الصفحات ترفض بشدة أن تتحول إلى سلاسل قابلة للبحث.  
في هذا الدليل سنستعرض حلاً كاملاً وجاهزًا للتنفيذ يأخذ ملف TIFF، يمرره إلى Aspose OCR، ويُخرج نصًا عاديًا — دون خدمات إضافية، دون سحر خفي.

> **نصيحة محترف:** إذا كنت تتعامل مع مسحات عالية الدقة، فإن تمكين معالجة GPU يمكن أن يوفر بضع ثوانٍ لكل صفحة.

سنُظهر لك أيضًا كيفية **استخراج نص من ملفات الصور الممسوحة** وأفضل طريقة لـ **تحميل ملف الصورة C#** إلى محرك OCR، حتى تتمكن من دمج هذه المنطق في أي مشروع .NET اليوم.

---

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي على جهازك:

| المتطلبات | السبب |
|-------------|--------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | بيئة تشغيل حديثة، تدعم `Span<T>` و I/O غير المتزامن |
| Aspose.OCR for .NET (NuGet package `Aspose.OCR`) | محرك OCR الذي سنستخدمه |
| A valid Aspose OCR license file (`Aspose.OCR.lic`) | بدونها ستواجه حدود التقييم |
| A TIFF file (single‑ or multi‑page) to test | المثال المستخدم: `scanned_multi_page.tif` |
| GPU with CUDA 11+ (optional) | يسرّع التعرف عندما يكون `EngineMode = Gpu` |

إذا كنت تفتقد أيًا من هذه العناصر، احصل على حزمة NuGet الآن:

```bash
dotnet add package Aspose.OCR
```

---

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أنشئ تطبيقًا سطريًا جديدًا (أو أضف الكود إلى مشروع موجود). أول شيء نفعله هو استيراد الفئات التي سنحتاجها.

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **لماذا هذا مهم:** استيراد `Aspose.OCR.Image` يمنحنا مصنع `ImageStream`، الذي يمكنه قراءة ملفات TIFF مباشرة من القرص أو من تدفق. تخطي هذه الخطوة سيسبب خطأً في وقت التجميع.

---

## الخطوة 2: تهيئة محرك OCR واختيار وضع المعالجة

يجب تكوين محرك OCR **قبل** تعيين أي صورة. هنا نقرر ما إذا كنا سنعمل على وحدة المعالجة المركزية أو نستفيد من وحدة معالجة الرسوميات.

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*إذا كنت على خادم بدون بطاقة رسومية، غيّر `Gpu` إلى `Cpu` أو `Auto`.*  
وضع المحرك يؤثر على تخصيص الذاكرة والسرعة؛ وضع GPU يمكن أن يكون أسرع بـ 2‑3× على ملفات TIFF الكبيرة وعالية الدقة.

---

## الخطوة 3: تطبيق ترخيص Aspose OCR الخاص بك

التشغيل بدون ترخيص يحدّك إلى عدد قليل من الصفحات وعلامات مائية. حمّل ترخيصك مبكرًا حتى تكون كل العملية اللاحقة غير مقيدة.

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **مشكلة شائعة:** وضع `SetLicense` بعد `Recognize()` سيجعل المحرك يعود إلى وضع التجربة لتلك العملية.

---

## الخطوة 4: تحميل ملف TIFF – معالجة الصور الفردية والمتعددة الصفحات

يمكن لـ Aspose OCR قراءة ملفات TIFF متعددة الصفحات مباشرةً، لكن عليك تمرير التدفق الصحيح. إليك نمطًا قويًا يعمل في كلا السيناريوهين.

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### لماذا نستخدم `ImageStream.FromFile`؟

- ي抽象 `FileStream` الأساسي، ويتعامل مع تعداد صفحات TIFF داخليًا.  
- يعمل مع `MemoryStream` أيضًا، لذا يمكنك تحميل الصور من قاعدة بيانات أو واجهة ويب دون لمس نظام الملفات.

### حالة الحافة: ملفات TIFF ضخمة جدًا

إذا تجاوز حجم TIFF الخاص بك 200 MB، فكر في تحميله صفحة بصفحة لتجنب استثناءات نفاد الذاكرة:

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

---

## الخطوة 5: التحقق من النتيجة

عند تشغيل البرنامج، يجب أن ترى شيئًا مشابهًا لهذا:

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

إذا كان النص مشوّهًا، تحقق من التالي:

1. **الدقة** – يعمل OCR بأفضل صورة مع 300 dpi أو أعلى.  
2. **EngineMode** – غيّر إلى `Cpu` إذا كان برنامج تشغيل GPU قديمًا.  
3. **الترخيص** – تأكد من صحة مسار ملف الترخيص وأن الملف قابل للقراءة.

---

## الأسئلة المتكررة (FAQ)

### هل يعمل هذا مع صيغ صور أخرى؟

بالتأكيد. `ImageStream.FromFile` يدعم JPEG، PNG، BMP، وحتى PDF (عبر Aspose.PDF). فقط استبدل امتداد الملف.

### ماذا لو احتجت لمعالجة صور مخزنة في قاعدة بيانات؟

اقرأ الـ BLOB إلى `MemoryStream` ومرره إلى `ImageStream.FromStream(memoryStream)`. يعامل محرك OCR ذلك كأنه تدفق مستند إلى ملف.

### هل يمكن تشغيله على لينكس؟

نعم — Aspose OCR متعدد المنصات. ثبّت بيئة تشغيل .NET المناسبة وتأكد من توفر المكتبات الأصلية المطلوبة لـ GPU (إن استخدمت).

---

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج بالكامل، جاهزًا للترجمة. استبدل `YOUR_DIRECTORY` ومسار ملف الترخيص بالمواقع الفعلية لديك.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

احفظ هذا كـ `Program.cs`، شغّل `dotnet run`، وشاهد النص

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}