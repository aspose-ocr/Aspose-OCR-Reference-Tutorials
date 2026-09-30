---
category: general
date: 2026-01-15
description: دروس C# OCR تُظهر لك كيفية التعرف على النص من الصورة، استخراج النص من
  الفاتورة، وتحويل الصورة إلى نص باستخدام Aspose OCR على وحدة معالجة الرسومات.
draft: false
keywords:
- c# ocr tutorial
- recognize text from image
- extract text from invoice
- convert image to text
- load image for ocr
language: ar
og_description: دروس C# OCR تعلمك كيفية التعرف على النص من الصورة، استخراج النص من
  الفاتورة، وتحويل الصورة إلى نص باستخدام Aspose OCR على وحدة معالجة الرسومات.
og_title: دليل c# OCR – التعرف السريع على النصوص المدعومة بالمعالج الرسومي
tags:
- OCR
- C#
- Aspose
- GPU
title: دليل C# OCR – التعرف على النص من الصورة باستخدام تسريع GPU
url: /ar/net/ocr-optimization/c-ocr-tutorial-recognize-text-from-image-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل c# ocr – التعرف على النص من الصورة مع تسريع GPU

هل احتجت إلى **c# ocr tutorial** ينجز المهمة فعلاً دون تجارب لا نهائية؟ ربما أنت تنظر إلى فاتورة عالية الدقة وتتساءل كيف **extract text from invoice** في ثوانٍ معدودة. الخبر السار هو أنك لست بحاجة إلى إعادة اختراع العجلة — Aspose.OCR يوفر لك API نظيفًا ومسرّعًا بـ GPU يقوم بالعمل الشاق نيابةً عنك.

في هذا الدليل سنستعرض مثالًا كاملاً قابلاً للتنفيذ يوضح كيفية **recognize text from image**، **convert image to text**، وكيفية التعامل مع أكثر المشكلات شيوعًا. بنهاية القراءة ستحصل على برنامج مستقل يمكنه قراءة أي صورة لوثيقة، من الإيصالات إلى العقود الممسوحة، وإنتاج نص نظيف قابل للبحث.

## ما ستتعلمه

- كيفية تثبيت وإضافة مرجع حزمة Aspose.OCR من NuGet.  
- كيفية ضبط محرك OCR للعمل على GPU للحصول على أداء فائق السرعة.  
- الطريقة الصحيحة لـ **load image for ocr** باستخدام `OcrImage.FromFile`.  
- كيفية استدعاء `Recognize` مع اللغة المطلوبة واستخراج النتيجة.  
- نصائح للتعامل مع ملفات PDF متعددة الصفحات، المسحات منخفضة التباين، ومعالجة الأخطاء.

لا تحتاج إلى أي خبرة سابقة مع Aspose؛ فقط بيئة تطوير .NET جاهزة (Visual Studio 2022 أو VS Code) وGPU بسيط (حتى GPU مدمج من Intel يكفي).

---

## الخطوة 1 – تثبيت Aspose.OCR وتحضير المشروع

أولًا: تحتاج إلى مكتبة Aspose.OCR. أسهل طريقة هي عبر NuGet.

```bash
dotnet add package Aspose.OCR
```

> **نصيحة محترف:** إذا كنت تستهدف .NET 6 أو أحدث، ستقوم الحزمة تلقائيًا بجلب الثنائيات الأصلية لـ GPU على Windows وLinux وmacOS. لا حاجة لنسخ ملفات DLL إضافية.

بعد إضافة الحزمة، افتح ملف المشروع الخاص بك (`*.csproj`) وتأكد من وجود المرجع:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.12.0" />
</ItemGroup>
```

الآن لديك كل ما تحتاجه للبدء بالبرمجة.

## الخطوة 2 – إنشاء محرك OCR مدعوم بـ GPU (c# ocr tutorial)

قلب **c# ocr tutorial** هو `OcrEngine`. بتعيين `Engine = Engine.Gpu` نخبر Aspose باستخدام بطاقة الرسوميات بدلاً من المعالج.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine with GPU acceleration.
            var ocrEngine = new OcrEngine
            {
                Engine = Engine.Gpu // GPU acceleration is selected; the library auto‑detects the device.
            };

            // The rest of the steps are broken out into separate methods for clarity.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            PerformOcr(ocrEngine, imagePath);
        }
    }
}
```

> **لماذا GPU؟** يمكن للـ GPU معالجة آلاف البكسلات بالتوازي، مما يقلل زمن الـ OCR من ثوانٍ إلى أجزاء من الثانية على الصور الكبيرة ذات الدقة العالية.

## الخطوة 3 – تحميل الصورة لـ OCR (load image for ocr)

تحميل الصورة بشكل صحيح أهم مما قد تتصور. `OcrImage.FromFile` يدعم PNG وJPEG وBMP وTIFF وحتى صفحات PDF. كما يقرأ DPI الصورة، وهو ما يؤثر على الدقة.

```csharp
static void PerformOcr(OcrEngine engine, string filePath)
{
    // Step 3: Load the image you want to recognize.
    // The FromFile method automatically detects the format.
    var image = OcrImage.FromFile(filePath);

    // Optional: Pre‑process the image for better results.
    // For example, you can increase contrast or convert to grayscale.
    image = ImagePreprocessor.AdjustContrast(image, 1.2);
    image = ImagePreprocessor.ConvertToGrayscale(image);
    
    // Continue to recognition...
    RecognizeAndDisplay(engine, image);
}
```

**ملاحظة:** إذا كنت تتعامل مع PDF، يمكنك استخراج كل صفحة كـ `OcrImage` وتمريرها واحدةً تلو الأخرى.

## الخطوة 4 – التعرف على النص من الصورة (recognize text from image)

الآن يحدث السحر. نطلب من المحرك التعرف على النص الإنجليزي، لكن يمكنك تمرير أي لغة يدعمها Aspose (الإسبانية، الألمانية، الصينية، إلخ).

```csharp
static void RecognizeAndDisplay(OcrEngine engine, OcrImage image)
{
    // Step 4: Perform OCR on the image using the desired language.
    var result = engine.Recognize(image, Language.English);

    // Step 5: Output the recognized text.
    Console.WriteLine("=== OCR RESULT ===");
    Console.WriteLine(result.Text);
}
```

خاصية `result.Text` تحتوي على السلسلة النصية البسيطة. إذا كنت تحتاج إلى درجة الثقة لكل كلمة، يمكنك فحص `result.Regions`.

### النتيجة المتوقعة

```
=== OCR RESULT ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,234.56
Thank you for your business!
```

إذا كانت الصورة غير واضحة، قد ترى أحرفًا مشوشة — هنا يأتي دور التحسين المسبق من الخطوة 3.

## الخطوة 5 – استخراج النص من الفاتورة – مثال واقعي

لنفترض أن لديك مجلدًا مليئًا بالفواتير الممسوحة وتريد استخراج المبلغ الإجمالي. أدناه توسيع سريع للكود السابق يستخدم تعبيرًا نمطيًا بسيطًا.

```csharp
using System.Text.RegularExpressions;

static void ExtractTotalAmount(string ocrText)
{
    // Look for a pattern like "$1,234.56"
    var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
    if (match.Success)
        Console.WriteLine($"Detected total: {match.Value}");
    else
        Console.WriteLine("Total amount not found.");
}
```

ستستدعي `ExtractTotalAmount(result.Text);` مباشرةً بعد طباعة نتيجة الـ OCR. هذا يوضح مدى سهولة **extract text from invoice** بمجرد حصولك على النص الخام.

## الخطوة 6 – تحويل الصورة إلى نص على نطاق واسع (convert image to text)

معالجة ملف واحد تكفي للعرض، لكن الكود الإنتاجي غالبًا ما يحتاج لمعالجة عشرات أو مئات الصور. إليك حلقة مختصرة تعالج دليلًا كاملًا:

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    foreach (var file in Directory.EnumerateFiles(folderPath, "*.*", SearchOption.TopDirectoryOnly)
                                 .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
    {
        Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
        var img = OcrImage.FromFile(file);
        var res = engine.Recognize(img, Language.English);
        Console.WriteLine(res.Text);
        ExtractTotalAmount(res.Text); // optional invoice extraction
    }
}
```

تشغيل `ProcessFolder(ocrEngine, @"C:\Invoices")` سيقوم **convert image to text** لكل ملف مدعوم في المجلد، مستفيدًا من GPU للسرعة.

## الحالات الخاصة والمشكلات الشائعة

| الحالة | لماذا يحدث | الحل السريع |
|-----------|----------------|-----------|
| **مسح منخفض التباين** | يواجه OCR صعوبة في تمييز الخلفية عن المقدمة. | زيادة التباين (`ImagePreprocessor.AdjustContrast`) أو تطبيق العتبة التكيفية. |
| **PDF متعدد الصفحات** | `OcrImage.FromFile` يقرأ الصفحة الأولى فقط. | استخدم `PdfDocument` لاستخراج كل صفحة كـ `OcrImage` وتكرار العملية. |
| **لغة غير مدعومة** | اللغة الافتراضية هي الإنجليزية. | مرر `Language.Spanish` أو أي قيمة من القيم المدعومة. |
| **GPU غير مكتشف** | نقص الثنائيات الأصلية أو برنامج تشغيل قديم. | تأكد من تحديث برنامج تشغيل الـ GPU؛ أعد تثبيت حزمة NuGet مع علم `-runtime`. |
| **نفاد الذاكرة على صور ضخمة** | ذاكرة الـ GPU محدودة. | قلل حجم الصورة (`image = ImagePreprocessor.Resize(image, 2000, 0)`). |

معالجة هذه القضايا مبكرًا سيوفر لك ساعات من التصحيح لاحقًا.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في تطبيق Console جديد. يتضمن جميع الدوال المساعدة التي تم مناقشتها أعلاه.

```csharp
using System;
using System.IO;
using System.Linq;
using System.Text.RegularExpressions;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize GPU‑accelerated OCR engine.
            var ocrEngine = new OcrEngine { Engine = Engine.Gpu };

            // 2️⃣ Define the path to a single image or a folder.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            // string folderPath = @"C:\Invoices";

            // Uncomment one of the following lines:
            PerformOcr(ocrEngine, imagePath);
            // ProcessFolder(ocrEngine, folderPath);
        }

        // -------------------------------------------------
        // Load image, preprocess, recognize, and display.
        // -------------------------------------------------
        static void PerformOcr(OcrEngine engine, string filePath)
        {
            var image = OcrImage.FromFile(filePath);
            image = ImagePreprocessor.AdjustContrast(image, 1.2);
            image = ImagePreprocessor.ConvertToGrayscale(image);

            var result = engine.Recognize(image, Language.English);
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(result.Text);

            ExtractTotalAmount(result.Text);
        }

        // -------------------------------------------------
        // Bulk processing of a folder.
        // -------------------------------------------------
        static void ProcessFolder(OcrEngine engine, string folderPath)
        {
            foreach (var file in Directory.EnumerateFiles(folderPath, "*.*")
                                          .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
            {
                Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
                var img = OcrImage.FromFile(file);
                var res = engine.Recognize(img, Language.English);
                Console.WriteLine(res.Text);
                ExtractTotalAmount(res.Text);
            }
        }

        // -------------------------------------------------
        // Simple regex to pull the total amount from an invoice.
        // -------------------------------------------------
        static void ExtractTotalAmount(string ocrText)
        {
            var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
            if (match.Success)
                Console.WriteLine($"Detected total: {match.Value}");
            else
                Console.WriteLine("Total amount not found.");
        }
    }
}
```

**شغّله** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}