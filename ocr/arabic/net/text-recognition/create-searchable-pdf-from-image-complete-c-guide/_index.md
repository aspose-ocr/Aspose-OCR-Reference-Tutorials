---
category: general
date: 2026-03-23
description: إنشاء ملف PDF قابل للبحث من صورة باستخدام Aspose OCR. تعلّم كيفية تحويل
  TIFF إلى PDF بضغط عالي والتعرف على نص الصورة في دقائق.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- high compression pdf
- recognize image text
- searchable pdf from image
language: ar
og_description: إنشاء ملف PDF قابل للبحث من صورة باستخدام Aspose OCR. يوضح هذا الدليل
  كيفية تحويل TIFF إلى PDF، وإضافة طبقة نصية قابلة للبحث، وتطبيق ضغط عالي.
og_title: إنشاء ملف PDF قابل للبحث من صورة – دليل C# الكامل
tags:
- Aspose OCR
- C#
- PDF generation
title: إنشاء PDF قابل للبحث من صورة – دليل C# الكامل
url: /ar/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث من صورة – دليل C# كامل

هل احتجت يوماً إلى **إنشاء PDF قابل للبحث** من مستند ممسوح ضوئياً لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك—العديد من المطورين يواجهون نفس المشكلة عند تحويل مسحات TIFF إلى ملفات PDF قابلة للبحث. الخبر السار؟ باستخدام Aspose OCR يمكنك **تحويل tiff إلى pdf**، إضافة طبقة نص مخفية فوق الصورة، وحتى تقليل حجم الملف باستخدام خيارات **high compression pdf**، كل ذلك في بضع أسطر من C#.

في هذا البرنامج التعليمي سنستعرض العملية بالكامل: من تثبيت حزم NuGet المناسبة، تحميل صورة TIFF، التعرف على نصها، وأخيرًا تصدير PDF قابل للبحث. في النهاية ستحصل على تطبيق console قابل للتنفيذ **يتعرف على نص الصورة** وينتج PDF مضغوط وقابل للبحث جاهز للفهرسة. لا أدوات إضافية، لا خطوات OCR يدوية—فقط كود نظيف وقليل من الشرح.

## المتطلبات المسبقة وما ستحتاجه

- **.NET 6+** (أو .NET Framework 4.6+). تعمل الواجهة البرمجية على كلاهما، لكن .NET 6 يمنحك أحدث تحسينات وقت التشغيل.  
- **Visual Studio 2022** أو أي بيئة تطوير تفضلها.  
- حزم NuGet **Aspose.OCR** و **Aspose.OCR.Gpu** (حزمة GPU اختيارية لكنها تسرع عملية التعرف على الأجهزة المدعومة).  
- ملف TIFF تجريبي (مثال: `invoice.tif`) موجود في مجلد يمكنك التحكم فيه.  

إذا كان لديك كل هذه العناصر، ممتاز—تقدم إلى الخطوة التالية. إذا لم يكن كذلك، ستغطي خطوة التثبيت أدناه كل ما تحتاجه.

## الخطوة 1: تثبيت حزم Aspose OCR

لبدء العمل، افتح مجلد المشروع في الطرفية ونفّذ:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

هذه الأوامر تجلب كل من محرك OCR الأساسي ومكتبة تسريع GPU. الأخيرة ليست إلزامية؛ سيعود المحرك إلى وضع CPU إذا لم يجد GPU متوافق.  

> **نصيحة احترافية:** عند استهداف بيئة إنتاج، قم بتثبيت إصدارات الحزم في ملف `csproj` لتجنب التغييرات غير المتوقعة.

## الخطوة 2: إعداد هيكل المشروع

أنشئ تطبيق console جديد (إذا لم يكن لديك واحد):

```bash
dotnet new console -n PdfExportDemo
cd PdfExportDemo
```

استبدل ملف `Program.cs` الذي تم إنشاؤه تلقائيًا بالكود الكامل الموضح لاحقًا. سيقوم البرنامج بـ:

1. تهيئة `OcrEngine` مع دعم GPU.  
2. تحميل صورة TIFF.  
3. تشغيل OCR وإنهاء العملية بأناقة عند الفشل.  
4. تكوين **PdfExportOptions** لإضافة طبقة نص قابلة للبحث و**high compression**.  
5. كتابة ملف الإخراج.

## الخطوة 3: كتابة الكود الكامل (مثال كامل)

فيما يلي ملف المصدر **كامل**. انسخه‑الصقه في `Program.cs`. التعليقات توضح “السبب” وراء كل سطر، وليس فقط “ما هو”.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;

class PdfExport
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Initialise OCR engine with GPU acceleration.
        //    GpuMode.Enabled tells Aspose to use the GPU if one is present.
        //    If no compatible GPU exists, the engine automatically falls back
        //    to CPU mode—no extra code required.
        // ------------------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine(GpuMode.Enabled))
        {
            // ------------------------------------------------------------
            // 2️⃣ Load the source image.
            //    ImageStream.FromFile supports many formats; here we use TIFF.
            // ------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\invoice.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // ------------------------------------------------------------
            // 3️⃣ Perform OCR recognition.
            //    Recognize() returns false if the engine cannot read the image.
            //    Exiting early prevents us from creating an empty PDF.
            // ------------------------------------------------------------
            if (!ocrEngine.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return;
            }

            // ------------------------------------------------------------
            // 4️⃣ Configure PDF export options.
            //    IncludeTextLayer = true adds an invisible, searchable text layer.
            //    CompressionLevel = High reduces file size dramatically.
            // ------------------------------------------------------------
            PdfExportOptions pdfExportOptions = new PdfExportOptions
            {
                IncludeTextLayer = true,
                CompressionLevel = PdfCompression.High
            };

            // ------------------------------------------------------------
            // 5️⃣ Save the searchable PDF.
            //    The output will be a compact, searchable PDF ready for indexing.
            // ------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\invoice.pdf";
            ocrEngine.Save(outputPath, pdfExportOptions);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");
        }
    }
}
```

### لماذا يعمل هذا

- **تسريع GPU** يمكنه تقليل زمن التعرف من ثوانٍ إلى مللي ثانية على البطاقات الحديثة—مفيد للمعالجة الجماعية.  
- **IncludeTextLayer** يدمج النص المستخرج من OCR بصورة غير مرئية، مما يسمح لعارضات PDF بالبحث في المستند دون تغيير مظهره البصري.  
- **High compression** يستخدم ضغط Flate (ZIP) على تدفق الصورة، وهو ضغط غير فقدان لكنه يقلل حجم الملف بشكل كبير—مثالي لأرشفة آلاف الفواتير.

## الخطوة 4: تشغيل التطبيق والتحقق من النتيجة

افتح طرفية داخل مجلد المشروع ونفّذ:

```bash
dotnet run
```

إذا تم إعداد كل شيء بشكل صحيح، سترى:

```
Searchable PDF saved to: YOUR_DIRECTORY\invoice.pdf
```

افتح `invoice.pdf` في أي قارئ PDF (Adobe Acrobat، Edge، أو حتى المتصفح). جرّب البحث عن كلمة تعرف أنها موجودة في ملف TIFF الأصلي—مثلاً “Total”. يجب أن يبرز العارض الكلمة رغم أنها جزء من الصورة. هذا هو ما يميز **searchable pdf**.

### حجم الملف المتوقع

عادةً ما ينخفض حجم فاتورة ممسوحة ضوئياً (≈300 KB TIFF) إلى **≈80 KB** بعد تطبيق `PdfCompression.High`. الحجم الدقيق يعتمد على تعقيد الصورة، لكنك ستلاحظ انخفاضًا واضحًا.

## الخطوة 5: التعديلات الشائعة والحالات الخاصة

| الحالة | ما الذي يجب تعديله | السبب |
|-----------|----------------|-----|
| **لا يوجد GPU** | غيّر `new OcrEngine(GpuMode.Enabled)` إلى `new OcrEngine(GpuMode.Disabled)` | يمنع المحرك من محاولة تهيئة GPU، ما قد يسبب تأخيرًا بسيطًا. |
| **ملفات متعددة الصفحات (TIFF متعدد الصفحات)** | اضبط `ocrEngine.Image = ImageStream.FromFile("multi.tif", PageRange.All);` | يحمل جميع الإطارات؛ Aspose سيعالج كل صفحة وينتج PDF متعدد الصفحات. |
| **تحتاج لغة OCR غير الإنجليزية** | `ocrEngine.Language = Language.French;` (أو أي لغة مدعومة) | يحسن الدقة للمستندات غير الإنجليزية. |
| **تريد طبقة نص مرئية بدلاً من المخفية** | `pdfExportOptions.IncludeTextLayer = false;` ثم أضف كائنات `TextFragment` يدويًا. | مفيد عندما تريد أن يظهر نص OCR كنص قابل للتحديد فوق الصورة. |
| **PDFات صغيرة جدًا** | اجمع بين `PdfCompression.High` و `ImageResolution = 150` DPI قبل التعرف. | تقليل DPI يقلل بيانات الصورة، مما يصغر حجم PDF أكثر على حساب جودة الصورة. |

> **ملاحظة:** اختبر الحالات الخاصة على عينة صغيرة قبل توسيعها إلى الإنتاج. قد تختلف دقة OCR بناءً على جودة الصورة، الضوضاء، واللغة.

## الخطوة 6: نصائح لتطبيقات جاهزة للإنتاج

1. **تسجيل الأخطاء** – استبدل `Console.WriteLine` بإطار تسجيل مناسب (Serilog، NLog) لتسهيل التشخيص.  
2. **معالجة دفعات** – ضع المنطق الأساسي في طريقة تقبل مسارات الإدخال/الإخراج، ثم كرّرها على مجلد يحتوي على ملفات TIFF.  
3. **I/O غير متزامن** – رغم أن Aspose OCR نفسه متزامن، يمكن جعل تحميل وحفظ الملفات غير متزامن للحفاظ على استجابة واجهات المستخدم.  
4. **الأمان** – إذا قدمت هذه الوظيفة عبر واجهة ويب API، تحقق من مسارات الملفات وحدد حجم الملفات لتجنب الاستغلال.  
5. **تثبيت الإصدارات** – استخدم أرقام إصدارات محددة (`<PackageReference Include="Aspose.OCR" Version="23.12.0" />`) لضمان سلوك ثابت عبر عمليات البناء.

## الخاتمة

لقد بنينا الآن **حلًا كاملاً من البداية إلى النهاية** يتيح لك **إنشاء PDF قابل للبحث** من صور ممسوحة، **تحويل tiff إلى pdf**، واستخدام إعدادات **high compression pdf** مع **التعرف على نص الصورة** بدقة. الناتج هو **searchable pdf from image** خفيف الوزن، قابل للبحث، وجاهز لتدفقات العمل اللاحقة مثل الفهرسة، الأرشفة، أو e‑discovery.

هل لديك مجموعة من الفواتير؟ ضع الطريقة داخل حلقة، وجهها إلى مجلد، ودع Aspose OCR يتولى العمل الشاق. تريد تجربة مستويات ضغط مختلفة أو حزم لغات أخرى؟ الكود مرن بما يكفي لتبديل هذه الخيارات في ثوانٍ.

---

*هل تريد الارتقاء بالمستوى؟* جرّب إضافة علامة مائية، تضمين بيانات تعريفية، أو حتى دمج عدة ملفات PDF معالجة بـ OCR معًا. مجموعة Aspose توفر العديد من الامتدادات—استكشف الوثائق واستمر في التقدم. برمجة سعيدة!

![Create searchable PDF from image example screenshot](https://example.com/images/create-searchable-pdf.png "create searchable pdf example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}