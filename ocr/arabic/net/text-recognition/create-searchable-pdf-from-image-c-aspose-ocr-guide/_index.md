---
category: general
date: 2026-05-06
description: إنشاء ملف PDF قابل للبحث من صورة باستخدام Aspose OCR في C#. تعلم كيفية
  تحويل PNG إلى PDF، استخراج النص من الصورة وإنشاء ملف PDF قابل للبحث.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- convert png to pdf
- ocr image to pdf
language: ar
og_description: إنشاء ملف PDF قابل للبحث من صورة باستخدام Aspose OCR في C#. يوضح هذا
  الدليل خطوة بخطوة كيفية تحويل PNG إلى PDF، واستخراج النص من الصورة، وإنتاج ملف PDF
  قابل للبحث.
og_title: إنشاء ملف PDF قابل للبحث من صورة – دليل Aspose OCR بلغة C#
tags:
- Aspose
- C#
- OCR
- PDF
title: إنشاء ملف PDF قابل للبحث من صورة – دليل Aspose OCR بلغة C#
url: /ar/net/text-recognition/create-searchable-pdf-from-image-c-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث من صورة – دليل C# Aspose OCR

هل احتجت يومًا إلى **إنشاء PDF قابل للبحث** من صورة ممسوحة ضوئيًا لكن لم تكن متأكدًا من أين تبدأ؟ ربما لديك إيصال بصيغة PNG، أو صورة JPEG لعقد، أو أي صورة نقطية تريد تحويلها إلى PDF يمكنك فعلاً البحث فيه. هذه مشكلة شائعة، خاصةً عندما تتعامل مع مسحات قديمة تجلس غير مستخدمة في مجلد.

الخبر السار هو أنه باستخدام Aspose OCR يمكنك **تحويل الصورة إلى PDF**، استخراج النص المخفي، والحصول على مستند قابل للبحث بالكامل—كل ذلك في بضع أسطر من C#. في هذا الدليل سنوضح لك أيضًا كيفية **تحويل PNG إلى PDF**، **استخراج النص من الصورة**، وحتى معالجة حالة ملفات TIFF متعددة الصفحات. في النهاية، ستحصل على حل مستقل يمكنك إدراجه في أي مشروع .NET.

## ما ستحتاجه

- **.NET 6+** (الكود يعمل أيضًا على .NET Framework 4.6+)
- **Visual Studio 2022** أو أي بيئة تطوير تفضلها
- حزمة NuGet **Aspose.OCR** (ستجلب Aspose.PDF تلقائيًا)
- ملف صورة (PNG، JPEG، BMP، TIFF) تريد تحويله إلى PDF قابل للبحث

لا حاجة لأي حيل ترخيص إضافية، ولا خدمات خارجية—مجرد إشارة NuGet واحدة وبضع دقائق من البرمجة.

## الخطوة 1: تثبيت حزمة NuGet Aspose.OCR

أولًا، أضف المكتبة إلى مشروعك. افتح وحدة تحكم مدير الحزم واكتب:

```powershell
Install-Package Aspose.OCR
```

هذا الأمر الواحد يجلب كلًا من **Aspose.OCR** وملف التجميع **Aspose.Pdf** الذي يعتمد عليه، لذا ستكون جاهزًا لقراءة الصورة وكتابة الـ PDF.

> **نصيحة احترافية:** إذا كنت تستخدم .NET CLI، فالأمر المكافئ هو `dotnet add package Aspose.OCR`.

## الخطوة 2: تهيئة محرك OCR

إنشاء نسخة من `OcrEngine` هو البوابة لكل عمليات OCR. فكر فيه كالعقل الذي سيُنظر إلى صورتك ويبدأ "قراءة" الأحرف.

```csharp
using Aspose.OCR;
using Aspose.Pdf;   // pulled in by the OCR package

// Create an OCR engine instance – this object holds configuration and state
var ocrEngine = new OcrEngine();
```

قد تتساءل، *لماذا لا نستدعي طريقة ثابتة مباشرة؟* النهج الكائني يسمح لك بتعديل الإعدادات لاحقًا (اللغة، الدقة، إلخ) دون تغيير سير العمل العام.

## الخطوة 3: تحميل الصورة التي تريد تحويلها

هنا نبدأ **تحويل الصورة إلى PDF** من حيث الفكرة—عن طريق إمداد الـ OCR بالصورة. استبدل `"YOUR_DIRECTORY/input.png"` بالمسار الفعلي لملفك.

```csharp
// Load the source image (PNG, JPEG, BMP, or multi‑page TIFF)
ocrEngine.SetImage("YOUR_DIRECTORY/input.png");
```

إذا كان لديك سيناريو **تحويل PNG إلى PDF**، فقط أشِر إلى ملف PNG. بالنسبة لملفات TIFF متعددة الصفحات، سيقوم Aspose.OCR تلقائيًا بمعالجة كل إطار كصفحة منفصلة.

## الخطوة 4: تشغيل OCR واستخراج النص اختياريًا

تشغيل `Recognize()` يقوم بالعمل الشاق: يحلل الصورة، يكتشف الأحرف، ويعيد نتيجة منظمة. يمكنك الاحتفاظ بالنص للتسجيل، فهرسة البحث، أو العرض.

```csharp
// Perform OCR – this extracts the textual content from the image
var ocrResult = ocrEngine.Recognize();

// Optional: show the extracted text in the console
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

> **لماذا استخراج النص؟** على الرغم من أننا سندمجه في الـ PDF النهائي، فإن وجود السلسلة الخام قد يكون مفيدًا للتحقق أو التحليل.

## الخطوة 5: ضبط خيارات PDF لإنشاء مستند قابل للبحث

يقدم Aspose.PDF وضعًا خاصًا من `PdfSaveOptions` يُدعى **CreateSearchablePdf**. يخبر المكتبة بدمج نص OCR كطبقة غير مرئية خلف الصورة، مما يجعل الـ PDF قابلًا للبحث.

```csharp
// Prepare PDF save options – this tells Aspose to embed OCR text
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();
```

إذا احتجت يومًا إلى PDF يحتوي على الصورة فقط (بدون نص مخفي)، يمكنك التحول إلى `PdfSaveOptions.CreatePdf()` بدلاً من ذلك. لكن هدفنا—**إنشاء PDF قابل للبحث**—هو الوضع المميز هنا.

## الخطوة 6: حفظ الـ PDF القابل للبحث على القرص

الآن نجمع كل شيء معًا. طريقة `SavePdf` تكتب الصورة والنص المخفي في ملف واحد.

```csharp
// Save the searchable PDF file
ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

Console.WriteLine("Searchable PDF created successfully.");
```

في هذه المرحلة ستحصل على **PDF قابل للبحث** يمكنك فتحه في Adobe Reader، كتابة كلمة في مربع البحث، والقفز فورًا إلى الموقع المطابق—على الرغم من أن الصفحة الظاهرة لا تزال مجرد الصورة الأصلية.

## مثال عملي كامل

بجمع جميع القطع معًا، إليك تطبيق كونسول جاهز للتنفيذ. انسخه إلى مشروع C# جديد، عدل مسارات الملفات، واضغط **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf; // included automatically with Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image that contains the scanned document
        // Replace with your actual image path
        ocrEngine.SetImage("YOUR_DIRECTORY/input.png");

        // Step 3: Run the OCR process to extract text (optional but useful)
        var ocrResult = ocrEngine.Recognize();

        // Show extracted text – helpful for debugging
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("======================");

        // Step 4: Prepare to export the recognized content as a searchable PDF
        var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

        // Step 5: Save the searchable PDF to disk
        // Replace with your desired output path
        ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created successfully.");
    }
}
```

### النتيجة المتوقعة

عند تشغيل البرنامج، سيعرض الكونسول شيئًا مثل:

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑04‑30
Total: $1,250.00
...
======================
Searchable PDF created successfully.
```

وفي `YOUR_DIRECTORY` ستجد `output.pdf`. افتحه، اضغط **Ctrl F**، اكتب “Invoice”، وستنتقل مباشرة إلى الكلمة—على الرغم من أن الصفحة تبدو كمسح ضوئي مسطح.

## التعامل مع التغييرات الشائعة

### تحويل عدة صور مرة واحدة

إذا كان لديك مجلد مليء بملفات PNG وتريد PDF قابل للبحث واحد، يمكنك التكرار على الملفات وإضافة كل واحدة كصفحة منفصلة:

```csharp
var allImages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
var ocrEngine = new OcrEngine();
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

foreach (var imgPath in allImages)
{
    ocrEngine.SetImage(imgPath);
    ocrEngine.Recognize(); // extracts text for the current page
    ocrEngine.SavePdf("temp_page.pdf", pdfOptions);

    // Merge temp_page.pdf into the final document (omitted for brevity)
}
```

يمكنك أيضًا استخدام `PdfFileEditor` من Aspose.PDF لدمج ملفات PDF المؤقتة في ملف نهائي واحد.

### التعامل مع مسحات منخفضة الدقة

تنخفض دقة OCR عندما تكون DPI الصورة أقل من 150. قبل إمداد الصورة للمحرك، يمكنك تكبيرها:

```csharp
ocrEngine.ImageProcessingOptions.Dpi = 300; // forces 300 DPI for better recognition
```

### اختيار لغة محددة

إذا لم يكن مستندك باللغة الإنجليزية، عيّن اللغة قبل استدعاء `Recognize()`:

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, etc.
```

هذه التعديلات تضمن أن **استخراج النص من الصورة** يعمل بثبات عبر مختلف السيناريوهات.

## النتيجة البصرية

![Searchable PDF created with Aspose OCR – create searchable PDF](https://example.com/images/searchable-pdf.png)

*تُظهر اللقطة أعلاه PDF حيث الصورة مرئية، لكن طبقة النص يمكن البحث فيها.*

## الخلاصة

أصبح لديك الآن وصفة كاملة وجاهزة للإنتاج **لإنشاء PDF قابل للبحث** من أي صورة باستخدام Aspose OCR وC#. غطينا كيفية **تحويل الصورة إلى PDF**، **استخراج النص من الصورة**، وحتى تناولنا حالات **تحويل PNG إلى PDF** و**OCR صورة إلى PDF**. الكود مستقل تمامًا، يعمل على أي بيئة تشغيل .NET، ويمكن توسيعه لمعالجة دفعات أو دعم لغات مخصصة.

ما الخطوة التالية؟ جرّب إضافة علامة مائية، تشفير الـ PDF، أو إمداد النص المستخرج إلى فهرس بحث مثل Elasticsearch. الاحتمالات لا حصر لها، والنمط نفسه—تحميل → التعرف → حفظ—سيخدمك في أي سير عمل يعتمد على OCR.

إذا واجهت أي صعوبات أو لديك حالة استخدام مميزة تريد مشاركتها، اترك تعليقًا أدناه. برمجة سعيدة، واستمتع بتحويل تلك المسحات العنيدة إلى ذهب قابل للبحث!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}