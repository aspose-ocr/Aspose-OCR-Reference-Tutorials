---
category: general
date: 2026-03-21
description: 'دورة تعليمية عن OCR في C#: تعلم كيفية استخراج النص من الصورة، مسح الفواتير
  وتحميل الصورة في C# باستخدام Aspose OCR مع تسريع GPU.'
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- ocr invoice scanning
- how to ocr image
- load image in c#
language: ar
og_description: 'دورة تعليمية عن OCR بلغة C#: دليل خطوة بخطوة لاستخراج النص من الصورة،
  إجراء مسح الفواتير باستخدام OCR وتعلم كيفية تنفيذ OCR للصور في C# باستخدام تسريع
  GPU.'
og_title: دليل C# للتعرف الضوئي على الأحرف – استخراج النص من الصور باستخدام Aspose
  OCR
tags:
- OCR
- C#
- Image Processing
title: دورة C# OCR – استخراج النص من الصور باستخدام Aspose OCR
url: /ar/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل c# OCR – استخراج النص من الصور باستخدام Aspose OCR

هل تساءلت يومًا كيف يمكنك تطبيق **c# OCR tutorial** على مشكلة واقعية مثل تحويل فاتورة ممسوحة ضوئيًا إلى نص قابل للتحرير؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى *extract text from image* ملفات وينتهي بهم الأمر بكتابة محللات هشة تتعطل عند أول مسح ضوضائي.

الأمر ببساطة—Aspose.OCR يجعل العملية بأكملها سهلة للغاية، خاصةً عندما تقوم بتمكين تسريع GPU. في هذا الدليل ستشاهد بالضبط **how to ocr image** ملفات في C#، وكيفية تحميل الصورة في c# بشكل صحيح، وحتى التعامل مع عيوب مسح الفواتير الشائعة دون أن تشعر بالإحباط.

بنهاية هذا الدرس ستحصل على تطبيق كونسول قابل للتشغيل يقرأ فاتورة بصيغة TIFF، ويجري OCR على الـ GPU، ويطبع ناتج نصي نظيف. لا سحر، فقط كود ثابت يمكنك نسخه ولصقه وتعديله.

---

## ما ستحتاجه

- **.NET 6.0** (أو أحدث) – الإصدار الحالي LTS، لذا ستكون مستقبليًا.
- **Aspose.OCR for .NET** حزمة NuGet – الإصدار 23.10 (الأحدث وقت كتابة هذا الدليل).
- **GPU‑enabled machine** (اختياري لكن يُنصح به) – الكود يعود إلى CPU إذا لم يتم العثور على GPU متوافق.
- صورة مثال، مثل `large_invoice.tif`. أي صيغة مدعومة (PNG, JPEG, TIFF, PDF) تعمل.

إذا لم تقم بتثبيت حزمة NuGet بعد، نفّذ:

```bash
dotnet add package Aspose.OCR
```

الآن بعد أن غطينا المتطلبات المسبقة، دعنا ننتقل إلى الخطوات الفعلية.

---

## الخطوة 1: إنشاء مشروع كونسول جديد وإضافة Aspose.OCR

أولاً، أنشئ تطبيق كونسول جديد حتى نتمكن من إبقاء الدرس مستقلاً.

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** استخدم العلامة `-n` لإعطاء مشروعك اسمًا ذا معنى؛ فهذا يحافظ على تنظيم الحل عندما تبدأ بإضافة المزيد من الوحدات لاحقًا.

ملف `Program.cs` الذي ينشئه Visual Studio سيكون ملعبنا. افتحه واحذف سطر `Console.WriteLine` الافتراضي – سنستبدله بمنطق OCR.

---

## الخطوة 2: تحميل الصورة في C# – الطريقة الصحيحة

قد يبدو تحميل الصورة أمرًا بسيطًا، لكن القيام به بشكل خاطئ قد يسبب تسربات للذاكرة أو قفل الملف. فئة `System.Drawing.Image` تعمل جيدًا في معظم السيناريوهات، لكن يجب تغليفها داخل كتلة `using` لضمان تحرير الموارد.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrInvoiceDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 👉 Step 2: Load the image you want to OCR.
            // Replace the path with the actual location of your invoice file.
            const string imagePath = @"C:\Invoices\large_invoice.tif";

            // The using statement ensures the image gets disposed automatically.
            using var inputImage = Image.FromFile(imagePath);
            
            // Continue to the OCR engine setup…
        }
    }
}
```

لاحظ التعليق `// 👉 Step 2:` – فهو يعكس ترقيم الخطوات في دليلنا ويساعد أي شخص يراجع الكود لاحقًا.

---

## الخطوة 3: تهيئة محرك OCR مع تسريع GPU

يتيح لك Aspose.OCR اختيار وضع المعالجة عند الإنشاء. `OcrEngineMode.Gpu` يخبر المكتبة باستخدام بطاقة الرسوميات إذا تم اكتشافها؛ وإلا فإنها تعود صامتًا إلى CPU، لذا لا تحتاج إلى كتابة منطق احتياطي إضافي.

```csharp
// 👉 Step 3: Create the OCR engine.
// The constructor argument selects GPU mode; it's the fastest option for large invoices.
var ocrEngine = new OcrEngine(OcrEngineMode.Gpu);
```

> **لماذا GPU؟**  
> يمكن أن يكون OCR على الفواتير عالية الدقة مستهلكًا للمعالج. نقل العملية إلى GPU يقلل زمن التنفيذ من عدة ثوانٍ إلى جزء صغير، خاصةً عند معالجة دفعات.

---

## الخطوة 4: تشغيل OCR واستخراج النص من الصورة

الآن يحدث السحر. استدعِ `Recognize` واحصل على النص العادي. تُعيد Aspose كائن `OcrResult` يحتوي على النص الخام، درجات الثقة، وحتى إطارات حدود كل حرف إذا احتجت إليها لاحقًا.

```csharp
// 👉 Step 4: Perform the OCR operation.
OcrResult ocrResult = ocrEngine.Recognize(inputImage);

// Display the extracted text.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مشابهًا لـ:

```
=== OCR Output ===
Invoice #12345
Date: 03/15/2026
Total: $1,234.56
...
```

إذا كان الناتج مشوشًا، تحقق مرة أخرى من أن الصورة ذات تباين عالي وأن لغة OCR مضبوطة بشكل صحيح (الإنجليزية هي الافتراضية). يمكنك أيضًا تعديل `ocrEngine.Settings` لتحسين الدقة، لكن الإعدادات الافتراضية تعمل جيدًا لمعظم الفواتير المطبوعة.

---

## الخطوة 5: معالجة حالات حافة مسح الفواتير باستخدام OCR

تأتي الفواتير بأشكال متعددة—بعضها متعدد الصفحات، وبعضها يحتوي على جداول أو ملاحظات مكتوبة يدويًا. إليك بعض التعديلات السريعة التي يمكنك إجراؤها دون إعادة كتابة كامل خط الأنابيب.

### 5.1 ملفات PDF أو TIFF متعددة الصفحات

إذا كان ملف المصدر يحتوي على عدة صفحات، ستحتاج إلى التكرار عبر كل صفحة وربط النتائج معًا.

```csharp
using var multiPageImage = Image.FromFile(@"C:\Invoices\multi_page_invoice.tif");

// Aspose can split multi‑page TIFFs into separate images.
for (int i = 0; i < multiPageImage.GetFrameCount(FrameDimension.Page); i++)
{
    multiPageImage.SelectActiveFrame(FrameDimension.Page, i);
    using var page = (Image)multiPageImage.Clone();
    var pageResult = ocrEngine.Recognize(page);
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

### 5.2 مسح منخفض الدقة

إذا كان DPI أقل من 150، قم بزيادة حجم الصورة قبل إرسالها إلى المحرك. هذا يحسن التعرف على الأحرف بشكل كبير.

```csharp
// Simple nearest‑neighbor scaling – replace with a better algorithm if needed.
var highRes = new Bitmap(inputImage, new Size(inputImage.Width * 2, inputImage.Height * 2));
var highResResult = ocrEngine.Recognize(highRes);
Console.WriteLine(highResResult.Text);
```

### 5.3 حزم لغات مخصصة

بشكل افتراضي يستخدم Aspose اللغة الإنجليزية. للغات أخرى، قم بتنزيل حزمة اللغة المناسبة من موقع Aspose وسجّلها:

```csharp
ocrEngine.Settings.Language = OcrLanguage.Spanish; // example for Spanish invoices
```

هذه التعديلات تجعل حل **ocr invoice scanning** الخاص بك قويًا بما يكفي لأحمال العمل الإنتاجية.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ والذي يدمج جميع الخطوات السابقة. انسخه إلى `Program.cs`، عدّل مسار الملف، واضغط **F5**.

```csharp
// ---------------------------------------------------------------
// Complete c# OCR tutorial – Aspose OCR with GPU acceleration
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrInvoiceDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialize the OCR engine (GPU mode)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine(OcrEngineMode.Gpu);

            // -----------------------------------------------------------------
            // Step 2: Load the image you want to process
            // -----------------------------------------------------------------
            const string imagePath = @"C:\Invoices\large_invoice.tif";

            // Using ensures the image is disposed properly.
            using var inputImage = Image.FromFile(imagePath);

            // -----------------------------------------------------------------
            // Step 3: Run OCR and extract plain text
            // -----------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(inputImage);

            // -----------------------------------------------------------------
            // Step 4: Output the result
            // -----------------------------------------------------------------
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);

            // -----------------------------------------------------------------
            // Optional: Demonstrate handling a multi‑page TIFF (comment out if not needed)
            // -----------------------------------------------------------------
            // HandleMultiPageTiff(@"C:\Invoices\multi_page_invoice.tif", ocrEngine);
        }

        // ---------------------------------------------------------------
        // Helper for multi‑page TIFFs – shows how to iterate pages
        // ---------------------------------------------------------------
        static void HandleMultiPageTiff(string path, OcrEngine engine)
        {
            using var multiPage = Image.FromFile(path);
            int pageCount = multiPage.GetFrameCount(FrameDimension.Page);

            for (int i = 0; i < pageCount; i++)
            {
                multiPage.SelectActiveFrame(FrameDimension.Page, i);
                using var page = (Image)multiPage.Clone();
                var result = engine.Recognize(page);
                Console.WriteLine($"\n--- Page {i + 1} ---");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

**الناتج المتوقع** (مقتطع للتقليل):

```
=== OCR Output ===
Invoice #98765
Date: 02/28/2026
Bill To: Acme Corp.
Subtotal: $2,500.00
Tax (8%): $200.00
Total: $2,700.00
...
```

شغّل البرنامج وتأكد من أن الكونسول يطبع النص الموجود على الفاتورة. إذا حصلت على سلاسل فارغة، تحقق مرة أخرى من صحة مسار الصورة وأن الملف غير معطوب.

---

## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا على لينكس؟**  
ج: نعم. Aspose.OCR متعدد المنصات. ما عليك سوى تثبيت بيئة تشغيل .NET للينكس وتعمل نفس حزمة NuGet. يتطلب تسريع GPU وجود GPU متوافق مع CUDA والسائق المناسب.

**س: ماذا لو لم يكن لدي GPU؟**  
ج: مُنشئ `OcrEngineMode.Gpu` يعود تلقائيًا إلى CPU عندما لا يتم اكتشاف GPU متوافق. ستحصل على نتائج دقيقة؛ فقط سيستغرق وقتًا أطول قليلاً.

**س: هل يمكنني إجراء OCR على الملاحظات المكتوبة يدويًا؟**  
ج: نماذج Aspose الافتراضية تركز على النص المطبوع. للكتابة اليدوية تحتاج إلى نموذج متخصص أو خدمة مختلفة (مثل Azure Form Recognizer). ومع ذلك، يمكنك تجربة نفس الكود—لكن توقع درجات ثقة أقل.

---

## الخلاصة

لقد أكملت للتو **c# OCR tutorial** الذي يوضح كيفية *extract text from image* الملفات، وإجراء **ocr invoice scanning**، وفهم **how to o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}