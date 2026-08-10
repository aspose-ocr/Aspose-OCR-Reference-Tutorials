---
category: general
date: 2026-02-14
description: إنشاء PDF قابل للبحث وتضمين الخطوط في PDF باستخدام Aspose OCR. تعلم كيفية
  تحويل الصورة إلى PDF باستخدام OCR، التعرف على النص من الصورة، وتحويل الصورة الممسوحة
  ضوئياً إلى PDF بلغة C#.
draft: false
keywords:
- create searchable pdf
- embed fonts in pdf
- ocr image to pdf
- recognize text from image
- convert scanned image to pdf
language: ar
og_description: إنشاء ملف PDF قابل للبحث باستخدام Aspose OCR في C#. يوضح هذا الدليل
  كيفية تضمين الخطوط في PDF، وتحويل الصورة إلى PDF باستخدام OCR، وتحويل الصورة الممسوحة
  ضوئياً إلى PDF مع ضمان التوافق مع معيار PDF/A‑2b.
og_title: إنشاء PDF قابل للبحث – دليل Aspose OCR الكامل
tags:
- Aspose OCR
- C#
- PDF/A‑2b
- Document Automation
title: إنشاء ملف PDF قابل للبحث باستخدام Aspose OCR – دليل خطوة بخطوة
url: /ar/net/text-recognition/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث – دليل Aspose OCR الكامل

هل احتجت يوماً إلى **إنشاء PDF قابل للبحث** من ملف TIFF ممسوح ضوئياً ولكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك. في العديد من سير عمل المكاتب، القدرة على **التعرف على النص من صورة** وإدراج الخطوط في PDF تُعد ميزة حاسمة، خاصةً عندما يتعين عليك الالتزام بمعيار PDF/A‑2b للأرشفة.

في هذا الدليل سنستعرض حلاً عمليًا يحقق ذلك بالضبط: سنأخذ صورة ممسوحة ضوئيًا، نجري عليها OCR، وننتج PDF قابل للبحث بالكامل مع تضمين الخطوط. بنهاية الدليل ستعرف كيف **تقوم بعمل OCR للصورة إلى PDF**، وكيف **تحول صورة ممسوحة ضوئيًا إلى PDF**، ولماذا يُعد تضمين الخطوط مهمًا للقراءة على المدى الطويل.

## ما ستحتاجه

- .NET 6+ (أو .NET Framework 4.7.2+) مع بيئة تطوير C# (Visual Studio، Rider، أو VS Code)
- حزمة NuGet Aspose.OCR for .NET (`Aspose.OCR` و `Aspose.OCR.Pdf`)
- صورة ممسوحة ضوئيًا تجريبية (`input.tif`) موجودة في مجلد يمكنك الإشارة إليه
- إلمام أساسي بتطبيقات C# console

> **نصيحة احترافية:** إذا كنت تستهدف PDF/A‑2b، تأكد من أنك تستخدم أحدث نسخة من Aspose.OCR؛ الإصدارات القديمة قد تفتقد تعداد `PdfAStandard`.

## الخطوة 1 – إعداد المشروع وتثبيت Aspose OCR

أنشئ مشروع console جديد وأضف حزم NuGet المطلوبة:

```bash
dotnet new console -n SearchablePdfDemo
cd SearchablePdfDemo
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Pdf
```

> **لماذا هذا مهم:** تثبيت حزمة `Aspose.OCR.Pdf` يجلب الامتدادات الخاصة بـ PDF التي تسمح لك **بتضمين الخطوط في PDF** وتطبيق توافق PDF/A دون الحاجة إلى مكتبات طرف ثالث إضافية.

## الخطوة 2 – تهيئة محرك OCR

الفئة `Engine` هي قلب Aspose OCR. تهيئتها مرة واحدة يمنحك الوصول إلى جميع ميزات OCR، بما في ذلك القدرة على **التعرف على النص من صورة**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;

// Initialize the OCR engine – this loads language data and prepares the engine.
var ocrEngine = new Engine();
```

إذا كنت تخطط لمعالجة العديد من الصور على دفعة واحدة، احتفظ بالمحرك فعالًا طوال فترة التشغيل؛ إنشاءه مرارًا يضيف عبئًا غير ضروري.

## الخطوة 3 – تحميل الصورة الممسوحة ضوئيًا

يعمل Aspose OCR مع الـ streams، لذا سنغلف ملف TIFF في `ImageStream`. هذه الخطوة هي التي سنقوم فيها لاحقًا **بتحويل الصورة الممسوحة ضوئيًا إلى PDF**.

```csharp
// Replace the path with the location of your scanned TIFF.
var imagePath = @"C:\Docs\input.tif";
var imageStream = ImageStream.FromFile(imagePath);
```

> **حالة حافة:** بعض الماسحات تنتج ملفات TIFF متعددة الصفحات. `ImageStream.FromFile` يقرأ الصفحة الأولى افتراضيًا. لمعالجة ملفات متعددة الصفحات، قم بالتكرار عبر `imageStream.Pages` وعالج كل صفحة على حدة.

## الخطوة 4 – تكوين خيارات حفظ PDF (تضمين الخطوط & PDF/A‑2b)

تضمين الخطوط يضمن أن يظهر PDF الناتج بنفس الشكل على أي جهاز، بينما يحقق توافق PDF/A‑2b متطلبات الأرشفة القانونية.

```csharp
var pdfSaveOptions = new PdfSaveOptions
{
    // PDF/A‑2b ensures long‑term preservation.
    PdfAStandard = PdfAStandard.PdfA2b,
    // Embedding fonts is crucial for searchable PDFs that render correctly everywhere.
    EmbedFonts = true
};
```

يمكنك أيضًا تعديل ضغط الصورة أو تعيين اسم مؤلف مخصص هنا، لكن الإعدادين السابقين هما الأكثر أهمية في سير عمل **إنشاء PDF قابل للبحث**.

## الخطوة 5 – تنفيذ OCR وحفظه كوثيقة PDF/A‑2b قابلة للبحث

الآن يحدث السحر. طريقة `RecognizeToPdf` تجري OCR على تدفق الصورة وتكتب PDF قابل للبحث يلتزم بمعايير PDF/A‑2b.

```csharp
// Output path for the searchable PDF.
var outputPath = @"C:\Docs\output.pdf";

// Run OCR and generate the PDF.
ocrEngine.RecognizeToPdf(imageStream, outputPath, pdfSaveOptions);

Console.WriteLine("PDF/A‑2b document created at: " + outputPath);
```

عند فتح `output.pdf` في Adobe Acrobat Reader، ستلاحظ إمكانية تحديد النص ونسخه – هذا هو علامة نتيجة **إنشاء PDF قابل للبحث**.

## الخطوة 6 – التحقق من النتيجة (اختياري لكن موصى به)

فحص سريع يساعدك على التأكد من أن الخطوط مدمجة فعلاً وأن PDF يلتزم بـ PDF/A‑2b.

```csharp
using Aspose.Pdf; // Requires Aspose.PDF NuGet if you want to inspect the file

var pdfDoc = new Document(outputPath);
bool fontsEmbedded = pdfDoc.IsFontsEmbedded; // Returns true if fonts are embedded
bool isPdfA = pdfDoc.ValidatePdfA(PdfAConformance.PdfA2b); // Validates PDF/A‑2b compliance

Console.WriteLine($"Fonts embedded: {fontsEmbedded}");
Console.WriteLine($"PDF/A‑2b compliance: {isPdfA}");
```

إذا فشل أي من الفحصين، أعد مراجعة `PdfSaveOptions` وتأكد من أنك تستخدم أحدث نسخة من Aspose OCR.

## أسئلة شائعة وملاحظات

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني إجراء OCR على PDF متعدد الصفحات مباشرة؟** | نعم. حمّل الـ PDF باستخدام `Aspose.Pdf` → حوّل كل صفحة إلى صورة → مرّر كل صورة إلى `RecognizeToPdf` داخل حلقة. |
| **ماذا لو كانت صورتي الممسوحة ضوئيًا منخفضة الدقة؟** | دقة OCR تنخفض تحت 300 dpi. يُنصح بمعالجة الصورة مسبقًا (زيادة DPI، إزالة الضوضاء) قبل تمريرها إلى المحرك. |
| **هل أحتاج إلى ترخيص لـ Aspose OCR؟** | النسخة التجريبية المجانية تعمل حتى 5 صفحات. للإنتاج، الترخيص يزيل علامة التقييم ويفتح جميع الميزات. |
| **كيف أغيّر لغة OCR؟** | اضبط `ocrEngine.Language = Language.English;` أو أي تعداد لغة مدعومة قبل استدعاء `RecognizeToPdf`. |
| **هل تضمين الخطوط إلزامي للـ PDFs القابلة للبحث؟** | ليس إلزاميًا، لكن بدون الخطوط المدمجة قد يظهر النص بشكل غير صحيح على الأنظمة التي لا تملك الخط الأصلي، مما يفسد تجربة “القابلية للبحث”. |

## مثال كامل جاهز للتنفيذ (انسخه‑الصقه)

فيما يلي البرنامج الكامل الذي يمكنك لصقه في `Program.cs`. يتضمن جميع الخطوات السابقة بالإضافة إلى كتلة التحقق.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;
using Aspose.Pdf; // For verification – add Aspose.PDF via NuGet if needed

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new Engine();

        // 2️⃣ Load the scanned image (change the path as needed)
        var imagePath = @"C:\Docs\input.tif";
        var imageStream = ImageStream.FromFile(imagePath);

        // 3️⃣ Configure PDF save options – embed fonts & PDF/A‑2b compliance
        var pdfSaveOptions = new PdfSaveOptions
        {
            PdfAStandard = PdfAStandard.PdfA2b,
            EmbedFonts = true
        };

        // 4️⃣ Recognize text and save as searchable PDF/A‑2b
        var outputPath = @"C:\Docs\output.pdf";
        ocrEngine.RecognizeToPdf(imageStream, outputPath, pdfSaveOptions);
        Console.WriteLine("PDF/A‑2b document created at: " + outputPath);

        // 5️⃣ Verify embedding and compliance (optional)
        var pdfDoc = new Document(outputPath);
        bool fontsEmbedded = pdfDoc.IsFontsEmbedded;
        bool isPdfA = pdfDoc.ValidatePdfA(PdfAConformance.PdfA2b);
        Console.WriteLine($"Fonts embedded: {fontsEmbedded}");
        Console.WriteLine($"PDF/A‑2b compliance: {isPdfA}");
    }
}
```

شغّل البرنامج باستخدام `dotnet run`. إذا تم إعداد كل شيء بشكل صحيح، ستظهر لك مخرجات في وحدة التحكم تؤكد إنشاء PDF، وتضمين الخطوط، ونجاح التحقق من PDF/A‑2b.

## الخطوات التالية – توسيع سير العمل

الآن بعد أن أصبحت قادرًا على **إنشاء PDF قابل للبحث**، فكر في التحسينات التالية:

- **معالجة دفعات** – تكرار عبر مجلد من ملفات TIFF، وإلحاق كل نتيجة OCR إلى PDF واحد.
- **بيانات تعريف مخصصة** – إضافة مؤلف، عنوان، وكلمات مفتاحية إلى PDF باستخدام `PdfSaveOptions.Metadata`.
- **معالجة مسبقة للصور** – دمج OpenCV أو ImageSharp لتحسين المسحات ذات الجودة المنخفضة قبل OCR.
- **مخرجات بديلة** – تصدير نتائج OCR إلى نص عادي، DOCX، أو HTML لتدفقات عمل لاحقة.

كل واحدة من هذه الأفكار تبني على المفاهيم الأساسية لـ **ocr image to pdf**، **recognize text from image**، و **embed fonts in pdf**، لتمنحك خط أنابيب أتمتة مستندات قوي.

---

![مخطط يوضح التدفق من الصورة الممسوحة ضوئياً → محرك OCR → PDF/A‑2b مع خطوط مدمجة](https://example.com/flow-diagram.png "سير عمل إنشاء PDF قابل للبحث")

*نص بديل للصورة: مخطط يوضح التدفق من الصورة الممسوحة ضوئياً → محرك OCR → PDF/A‑2b مع خطوط مدمجة.*

---

### TL;DR

- تهيئة `Engine`.
- تحميل ملف TIFF الممسوح باستخدام `ImageStream.FromFile`.
- ضبط `PdfSaveOptions` لتضمين الخطوط وتطبيق PDF/A‑2b.
- استدعاء `RecognizeToPdf` لـ **إنشاء PDF قابل للبحث**.
- تحقق من تضمين الخطوط والامتثال إذا لزم الأمر.

هذا هو كل ما تحتاجه. لديك الآن طريقة موثوقة وجاهزة للإنتاج **لتحويل صورة ممسوحة ضوئيًا إلى PDF**، مع ضمان قابلية البحث وثبات الوثيقة للمستقبل. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}