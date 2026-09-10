---
category: general
date: 2025-12-30
description: إنشاء ملف PDF قابل للبحث من صورة باستخدام C# – تعلم كيفية تحويل TIFF
  إلى PDF، استخراج النص من الصورة، وأتمتة إنشاء ملفات PDF.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- convert tiff to pdf
- extract text from image
- how to create pdf
language: ar
og_description: إنشاء ملف PDF قابل للبحث من صورة باستخدام Aspose OCR في C#. يوضح هذا
  الدليل كيفية تحويل TIFF إلى PDF، واستخراج النص، وضمان توافق PDF/A‑1b.
og_title: إنشاء ملف PDF قابل للبحث من TIFF – دليل C# خطوة بخطوة
tags:
- Aspose OCR
- C#
- PDF generation
title: إنشاء ملف PDF قابل للبحث من TIFF – دليل C# الكامل
url: /ar/net/text-recognition/create-searchable-pdf-from-tiff-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث من TIFF – دليل C# كامل

هل احتجت يوماً إلى **إنشاء PDF قابل للبحث** من ملف TIFF ممسوح ضوئياً ولكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك. يواجه العديد من المطورين هذه العقبة عندما يحتاجون إلى ملفات PDF قابلة للبحث لأغراض الأرشفة أو الامتثال، والخبر السار هو أن الحل بسيط بشكل مفاجئ باستخدام Aspose OCR.

في هذا الدرس سنستعرض تحويل صورة إلى PDF، استخراج النص من الصورة، وتحسين الناتج ليتوافق مع معايير PDF/A‑1b. في النهاية ستتمكن من **تحويل tiff إلى pdf**، **استخراج النص من الصورة**، وستعرف بالضبط **كيفية إنشاء pdf** ملفات تكون قابلة للبحث وجاهزة للأرشفة.

## ما ستحتاجه

- .NET 6 (أو أي نسخة حديثة من .NET) – الكود يعمل على .NET Core و .NET Framework على حد سواء.  
- حزمة NuGet Aspose.OCR – قم بتثبيتها باستخدام `dotnet add package Aspose.OCR`.  
- ملف TIFF تجريبي (`input.tif`) تريد تحويله إلى PDF قابل للبحث.  
- بيئة تطوير (Visual Studio، VS Code، Rider… أي منها يناسب).  

هذا كل شيء. لا حزم SDK إضافية، لا خدمات خارجية، ولا خطوات تكوين مخفية.

![Create searchable PDF example](image-placeholder.png "Create searchable PDF preview")

## الخطوة 1 – تهيئة محرك OCR وتحميل نموذج اللغة الإنجليزية

قبل أن نتمكن من تحويل صورة إلى نص قابل للبحث، يحتاج محرك OCR إلى معرفة اللغة التي يجب البحث عنها. يأتي Aspose OCR مع حزم لغات يمكنك تحميلها عند الحاجة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Load the English language model (you can swap this for other languages)
ocrEngine.LoadLanguage(LanguageModel.English);
```

**لماذا هذا مهم:** تحميل نموذج اللغة الصحيح يحسن دقة التعرف بشكل كبير. إذا تخطيت هذه الخطوة سيعود المحرك إلى نموذج عام، مما ينتج نصًا مشوشًا—خاصةً في ملفات TIFF منخفضة الدقة.

## الخطوة 2 – التعرف على النص من الصورة المصدر (اختياري لكن مفيد)

تشغيل OCR يمنحك كائن `OcrResult` يمكنك فحصه، تسجيله، أو حتى حفظه كنص عادي. هذه الخطوة اختيارية إذا كنت تهتم فقط بالـ PDF النهائي، لكنها مفيدة للتصحيح.

```csharp
// Perform OCR on the input TIFF
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/input.tif");

// Dump the raw text to the console (useful for validation)
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

**نصيحة احترافية:** إذا كان النص المستخرج يبدو غير صحيح، فكر في معالجة الصورة مسبقًا (إزالة الميل، إزالة الضجيج) قبل تمريرها إلى المحرك. يقدم Aspose OCR أيضًا أدوات تحسين الصورة يمكنك ربطها هنا.

## الخطوة 3 – إعداد مُصدّر PDF القابل للبحث

الآن نخبر Aspose كيف نريد أن يبدو الـ PDF النهائي. يتيح لك `SearchablePdfExporter` تحديد مسار الإخراج، توافق PDF/A، وبعض الإعدادات الإضافية.

```csharp
var pdfExporter = new SearchablePdfExporter
{
    // Where the searchable PDF will be saved
    OutputPath = "YOUR_DIRECTORY/output.pdf",

    // Enforce PDF/A‑1b compliance – ideal for long‑term archiving
    PdfACompliance = PdfACompliance.PdfA1b
};
```

**لماذا PDF/A‑1b؟** تتطلب العديد من الصناعات (القانونية، الطبية، المالية) ملفات PDF تتوافق مع معايير الأرشفة. يضمن ضبط `PdfACompliance` تضمين الخطوط، أن تكون الألوان مستقلة عن الجهاز، وأن يجتاز الملف أدوات التحقق.

## الخطوة 4 – تصدير نتيجة OCR مباشرة إلى PDF قابل للبحث

مع جاهزية المحرك والمصدّر، يصبح العمل الشاق سطرًا واحدًا. يبني المصدّر داخليًا صفحة PDF، يضع النص المعترف به كطبقة غير مرئية، ويكتب الملف.

```csharp
// Export the OCR result to a searchable PDF
pdfExporter.Export(ocrEngine, "YOUR_DIRECTORY/input.tif");

// Confirmation message
Console.WriteLine("Searchable PDF created at YOUR_DIRECTORY/output.pdf");
```

**ما الذي يحدث في الخلفية؟**  
1. يتم تضمين ملف TIFF الأصلي كصورة نقطية.  
2. يتم وضع النص المستخرج من OCR فوقه، مخفيًا ولكنه قابل للتحديد.  
3. يتم إضافة بيانات التعريف (مثل اللغة) حتى يتمكن قارئ PDF من فهرسة النص.

## الخطوة 5 – التحقق من الناتج (فحص يدوي + تحقق برمجي)

من الممارسات الجيدة دائمًا التأكد من أن الـ PDF قابل للبحث فعليًا.

```csharp
// Quick sanity check: open the PDF and try to extract its text
using var pdfReader = new Aspose.Pdf.Facades.PdfConverter();
pdfReader.BindPdf("YOUR_DIRECTORY/output.pdf");
var extracted = pdfReader.ExtractText();
Console.WriteLine("Text extracted from the PDF:");
Console.WriteLine(extracted);
```

إذا استطعت نسخ النص من عارض PDF أو رؤيته في مخرجات الكونسول أعلاه، فقد نجحت.

## حالات الحافة والاختلافات الشائعة

### تحويل صيغ صور أخرى

نفس الكود يعمل مع PNG، JPEG، BMP—فقط غيّر امتداد الملف في استدعاءات `Recognize` و `Export`. لا حاجة لتكوين إضافي.

### ملفات TIFF متعددة الصفحات

يقوم Aspose OCR تلقائيًا بمعالجة كل صفحة من TIFF متعدد الصفحات ويجمعها في PDF متعدد الصفحات. إذا احتجت لتخطي صفحة، قم بفلترة `ocrResult.Pages` قبل التصدير.

### لغات غير الإنجليزية

استبدل `LanguageModel.English` بـ `LanguageModel.Spanish`، `LanguageModel.French`، إلخ، أو حمّل حزمة لغة مخصصة. تذكر تعديل بيانات تعريف PDF إذا كنت تستهدف لغة معينة.

### تقليل حجم PDF

إذا كانت ملفات TIFF ذات دقة عالية، قد يصبح الـ PDF الناتج كبيرًا. يمكنك تقليل دقة الصورة قبل OCR:

```csharp
ocrEngine.ImageProcessingOptions = new ImageProcessingOptions
{
    Dpi = 150 // Lower DPI reduces size, but test for acceptable quality
};
```

### التعامل مع PDFs محمية بكلمة مرور

إذا كنت بحاجة لحماية الناتج، غلف `SearchablePdfExporter` بواجهة تشفير Aspose.Pdf بعد التصدير:

```csharp
var pdfDoc = new Aspose.Pdf.Document("YOUR_DIRECTORY/output.pdf");
pdfDoc.Encrypt("userPassword", "ownerPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save("YOUR_DIRECTORY/output_protected.pdf");
```

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للنسخ واللصق والذي يدمج جميع الخطوات والتعديلات الاختيارية التي نوقشت أعلاه.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Export;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Initialize OCR engine and load language model
        // -----------------------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.LoadLanguage(LanguageModel.English);

        // Optional: lower DPI to shrink output size (adjust as needed)
        // ocrEngine.ImageProcessingOptions = new ImageProcessingOptions { Dpi = 150 };

        // -----------------------------------------------------------------
        // 2️⃣ Recognize text from the source TIFF
        // -----------------------------------------------------------------
        const string inputPath = @"YOUR_DIRECTORY/input.tif";
        var ocrResult = ocrEngine.Recognize(inputPath);
        Console.WriteLine("Extracted text from image:");
        Console.WriteLine(ocrResult.Text);

        // -----------------------------------------------------------------
        // 3️⃣ Configure the searchable PDF exporter
        // -----------------------------------------------------------------
        var pdfExporter = new SearchablePdfExporter
        {
            OutputPath = @"YOUR_DIRECTORY/output.pdf",
            PdfACompliance = PdfACompliance.PdfA1b // archival compliance
        };

        // -----------------------------------------------------------------
        // 4️⃣ Export OCR result to searchable PDF
        // -----------------------------------------------------------------
        pdfExporter.Export(ocrEngine, inputPath);
        Console.WriteLine("Searchable PDF created successfully.");

        // -----------------------------------------------------------------
        // 5️⃣ Verify by extracting text from the generated PDF
        // -----------------------------------------------------------------
        using var converter = new PdfConverter();
        converter.BindPdf(@"YOUR_DIRECTORY/output.pdf");
        var extractedFromPdf = converter.ExtractText();
        Console.WriteLine("Text extracted from the PDF:");
        Console.WriteLine(extractedFromPdf);
    }
}
```

**الناتج المتوقع:**  
- يطبع الـ Console النص الأصلي المستخرج من OCR للـ TIFF.  
- يظهر ملف `output.pdf` في `YOUR_DIRECTORY`.  
- فتح `output.pdf` في Adobe Reader يتيح لك تحديد النص ونسخه، مما يؤكد أنه قابل للبحث.

## ملخص

غطينا كل ما تحتاجه **لإنشاء PDF قابل للبحث** من صور TIFF باستخدام Aspose OCR في C#. من تهيئة محرك OCR، استخراج النص، ضبط توافق PDF/A، إلى التحقق من المستند النهائي، تم شرح كل خطوة بوضوح. الآن تعرف أيضًا كيف **تحول صورة إلى pdf**، **تحول tiff إلى pdf**، **استخراج النص من الصورة**، والسؤال الأوسع **كيفية إنشاء pdf** بطبقات قابلة للبحث.

## ما الذي يمكنك استكشافه لاحقًا

- **معالجة دفعات:** ضع المنطق داخل حلقة لمعالجة العشرات من الصور تلقائيًا.  
- **خطوط مخصصة:** تضمين خطوط الشركة للتماسك في العلامة التجارية.  
- **تكامل سحابي:** احفظ ملفات PDF مباشرةً في Azure Blob Storage أو AWS S3 بعد الإنشاء.  
- **واجهة مستخدم:** بناء تطبيق WinForms/WPF بسيط يتيح للمستخدمين سحب وإفلات الصور للتحويل الفوري.

لا تتردد في تجربة نماذج لغات مختلفة، إعدادات DPI، ومستويات PDF/A. الـ API مرن بما يكفي ليتكيف مع أي سير عمل يمكنك تخيله.

---

*برمجة سعيدة، ولتكن ملفات PDF الخاصة بك دائمًا قابلة للبحث!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}