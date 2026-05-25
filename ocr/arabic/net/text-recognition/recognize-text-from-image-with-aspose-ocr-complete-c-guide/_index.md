---
category: general
date: 2026-05-25
description: التعرف على النص من الصورة باستخدام Aspose OCR في C#. تعلّم كيفية تحميل
  الصورة للتعرف الضوئي على الأحرف، ضبط لغة OCR، إنشاء محرك OCR واستخراج النص من ملف
  TIFF.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- set OCR language
- create OCR engine
language: ar
og_description: التعرف على النص من الصورة باستخدام Aspose OCR في C#. يوضح هذا الدرس
  كيفية إنشاء محرك OCR، تحميل الصورة للـ OCR، تعيين لغة الـ OCR، واستخراج النص من
  ملف TIFF.
og_title: التعرف على النص من الصورة باستخدام Aspose OCR – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: recognize text from image using Aspose OCR in C#. Learn how to load
    image for OCR, set OCR language, create OCR engine and extract text from TIFF.
  headline: recognize text from image with Aspose OCR – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Remove the `GpuDevice` line; the engine will automatically switch to CPU
      mode. Performance will be slower but the results remain accurate.
    question: What if my GPU isn’t detected?
  - answer: Absolutely—`Image.FromFile` works with any format supported by System.Drawing,
      so you can **load image for OCR** regardless of extension.
    question: Can I process PNG or JPEG files?
  - answer: Increase `ocrEngine.PreprocessOptions.Dpi` before calling `Recognize`.
      Higher DPI gives the engine more pixels to work with, improving accuracy.
    question: How do I handle low‑resolution scans?
  - answer: The `GpuMemoryLimit` property caps GPU usage. If you hit the limit, the
      engine will fallback to CPU for the remaining pages.
    question: Is there a limit to the size of the TIFF?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- GPU
- Text Extraction
title: التعرف على النص من الصورة باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة باستخدام Aspose OCR – دليل C# كامل

هل احتجت يوماً إلى **التعرف على النص من الصورة** لكنك لم تكن متأكدًا أي مكتبة ستوفر لك السرعة والدقة معًا؟ لست وحدك. في العديد من مشاريع معالجة الفواتير أو الأرشفة، تكون النقطة الأكثر إزعاجًا هي استخراج نص نظيف وقابل للبحث من ملفات TIFF دون كتابة محلل مخصص.

الأمر بسيط: Aspose OCR لـ .NET يجعل هذه السلسلة بأكملها سهلة للغاية. في هذا الدليل سنستعرض كل ما تحتاجه — تثبيت الحزمة، **إنشاء محرك OCR**، تحميل ملف TIFF، ضبط لغة OCR، وأخيرًا **استخراج النص من TIFF**. في النهاية ستحصل على تطبيق كونسول جاهز للتنفيذ يمكنه **التعرف على النص من ملفات الصورة** بسرعة البرق.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضًا)
- Visual Studio 2022 (أو أي بيئة تطوير تفضلها)
- حزمة Aspose.OCR عبر NuGet (دعم GPU يتطلب الإضافة `Aspose.OCR.Gpu`)
- وحدة معالجة رسومية (GPU) تدعم CUDA إذا أردت السرعة الإضافية (اختياري لكن يُنصح به)

> **نصيحة محترف:** إذا لم يكن لديك GPU، ما عليك سوى حذف سطر `GpuDevice` وسيتحول المحرك تلقائيًا إلى المعالج المركزي (CPU).

## الخطوة 1: تثبيت Aspose OCR وإنشاء محرك OCR

أولاً، أضف الحزم الضرورية عبر NuGet:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu   # optional GPU support
```

الآن يمكننا **إنشاء محرك OCR**. هذا الكائن هو قلب العملية؛ فهو يحمل الإعدادات مثل الجهاز الذي يعمل عليه وحدود الذاكرة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU support
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine (GPU‑enabled)
        var ocrEngine = new OcrEngine
        {
            // 0 = first GPU in the system; change if you have multiple cards
            GpuDevice = new GpuDevice(0),
            // Optional: cap GPU memory usage to 1024 MB
            GpuMemoryLimit = 1024
        };
```

**لماذا هذا مهم:** بربط المحرك بوحدة GPU، تقلل بشكل كبير الوقت المستغرق لـ **التعرف على النص من الصورة**، خاصةً عند معالجة دفعات كبيرة من ملفات TIFF عالية الدقة.

## الخطوة 2: تحميل الصورة لـ OCR

بعد ذلك، نحتاج إلى **تحميل الصورة لـ OCR**. Aspose.OCR يعمل مع `System.Drawing.Image`، لذا أي تنسيق يدعمه GDI+ (بما في ذلك TIFF متعدد الصفحات) سيكون مناسبًا.

```csharp
        // Step 2: Load the image you want to process
        // Replace the path with the location of your TIFF file
        var imagePath = @"C:\Invoices\invoice_batch.tif";
        Image image = Image.FromFile(imagePath);
```

إذا كنت تتعامل مع TIFF متعدد الصفحات يمكنك التنقل بين الصفحات باستخدام `image.SelectActiveFrame`، لكن في معظم الحالات نداء واحد يكفي.

## الخطوة 3: ضبط لغة OCR

المحرك لا يعرف سحرًا أي لغة تقوم بمسحها. **ضبط لغة OCR** قبل تشغيل المعرّف؛ وإلا ستحصل على مخرجات مشوشة.

```csharp
        // Step 3: Tell the engine which language to expect
        ocrEngine.Language = OcrLanguage.English; // change to .German, .French, etc. as needed
```

> **هل تعلم؟** تبديل اللغات أثناء التشغيل تكلفة منخفضة — يمكنك حتى معالجة مستند مختلط اللغات بتغيير هذه الخاصية بين الصفحات.

## الخطوة 4: تنفيذ التعرف – التعرف على النص من الصورة

الآن الجزء الممتع: **التعرف على النص من الصورة** فعليًا. طريقة `Recognize` تُعيد سلسلة نصية عادية تحتوي جميع الأحرف المكتشفة.

```csharp
        // Step 4: Run OCR and capture the output
        string recognizedText = ocrEngine.Recognize(image);
```

إذا كنت تحتاج إلى درجات الثقة أو إطارات الحدود يمكنك استخدام النسخة التي تُعيد كائن `OcrResult`، لكن لمعظم مهام الاستخراج السلسلة النصية العادية كافية.

## الخطوة 5: استخراج النص من TIFF (وتعامل مع الملفات متعددة الصفحات)

عندما يكون المصدر TIFF يحتوي على عدة صفحات، ستحتاج إلى تكرار الخطوات 2‑4 لكل إطار. إليك حلقة سريعة **تستخرج النص من TIFF** صفحة بصفحة:

```csharp
        // Optional: process multi‑page TIFFs
        var totalFrames = image.GetFrameCount(FrameDimension.Page);
        for (int i = 0; i < totalFrames; i++)
        {
            image.SelectActiveFrame(FrameDimension.Page, i);
            string pageText = ocrEngine.Recognize(image);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
```

الكود أعلاه يطبع النص المستخرج لكل صفحة، مما يجعل من السهل توجيه النتائج إلى قاعدة بيانات أو فهرس بحث.

## الخطوة 6: عرض أو حفظ النص المستخرج

أخيرًا، لن **نعرض النص المستخرج** وربما نكتبه إلى ملف للمعالجة لاحقًا.

```csharp
        // Step 6: Output the result to console
        Console.WriteLine("=== Full OCR Result ===");
        Console.WriteLine(recognizedText);

        // Optional: Save to a .txt file
        System.IO.File.WriteAllText(@"C:\Invoices\extracted_text.txt", recognizedText);
    }
}
```

تشغيل البرنامج يجب أن يُظهر الأحرف التي تم التعرف عليها ويُنشئ ملف `extracted_text.txt` بجانب ملف TIFF المصدر.

---

## أسئلة شائعة وحالات خاصة

- **ماذا لو لم يتم اكتشاف الـ GPU؟**  
  احذف سطر `GpuDevice`؛ سيتحول المحرك تلقائيًا إلى وضع CPU. الأداء سيكون أبطأ لكن النتائج ستظل دقيقة.

- **هل يمكنني معالجة ملفات PNG أو JPEG؟**  
  بالتأكيد — `Image.FromFile` يعمل مع أي تنسيق يدعمه System.Drawing، لذا يمكنك **تحميل الصورة لـ OCR** بغض النظر عن الامتداد.

- **كيف أتعامل مع المسحات منخفضة الدقة؟**  
  زد قيمة `ocrEngine.PreprocessOptions.Dpi` قبل استدعاء `Recognize`. DPI أعلى يمنح المحرك المزيد من البكسلات للعمل معها، مما يحسن الدقة.

- **هل هناك حد لحجم ملف TIFF؟**  
  خاصية `GpuMemoryLimit` تحد من استهلاك الذاكرة على الـ GPU. إذا وصلت إلى الحد، سيتحول المحرك إلى CPU للصفحات المتبقية.

---

## الخلاصة

أصبح لديك الآن مقطع شفرة كامل وجاهز للإنتاج يمكنه **التعرف على النص من ملفات الصورة** باستخدام Aspose OCR في C#. غطى الدليل كيفية **إنشاء محرك OCR**، **تحميل الصورة لـ OCR**، **ضبط لغة OCR**، و**استخراج النص من TIFF** — كل ذلك مع الاستفادة من تسريع الـ GPU للسرعة.  

من هنا يمكنك:

- تجربة لغات مختلفة (`OcrLanguage.Spanish`, `OcrLanguage.ChineseSimplified`, إلخ).
- دمج المخرجات في فهرس ElasticSearch قابل للبحث.
- إضافة معالجة ما بعد الاستخراج (تدقيق إملائي، تنظيف regex) لتحسين جودة البيانات.

جرّبه على دفعة الفواتير الخاصة بك، عدّل حدود الذاكرة، وشاهد أداء OCR يرتفع. Happy coding!

## دروس ذات صلة

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}