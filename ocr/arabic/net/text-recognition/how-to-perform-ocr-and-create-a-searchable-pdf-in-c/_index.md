---
category: general
date: 2026-02-14
description: تعلم كيفية إجراء التعرف الضوئي على الأحرف (OCR) على ملف TIFF أو صورة
  وتحويل PDF باستخدام OCR لإنشاء PDF قابل للبحث — دليل خطوة بخطوة بلغة C#.
draft: false
keywords:
- how to perform OCR
- convert pdf using OCR
- make searchable pdf
- tiff to searchable pdf
- searchable pdf from image
language: ar
og_description: اكتشف كيفية إجراء OCR على الصور، وتحويل ملفات PDF باستخدام OCR، وإنشاء
  PDF قابل للبحث باستخدام Aspose OCR في دليل مختصر بلغة C#.
og_title: كيفية تنفيذ OCR وإنشاء ملف PDF قابل للبحث باستخدام C#
tags:
- OCR
- C#
- Aspose
- PDF conversion
title: كيفية تنفيذ OCR وإنشاء PDF قابل للبحث باستخدام C#
url: /ar/net/text-recognition/how-to-perform-ocr-and-create-a-searchable-pdf-in-c/
---

end.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR وإنشاء PDF قابل للبحث في C#

هل احتجت إلى **تنفيذ OCR** على مستند ممسوح ضوئياً لكن لم تكن متأكدًا من كيفية تحويل النتيجة إلى PDF قابل للبحث؟ لست وحدك—العديد من المطورين يواجهون هذه العقبة عند التعامل مع أرشيفات TIFF القديمة أو ملفات PDF التي تحتوي على صور فقط. الخبر السار؟ ببضع أسطر من C# ومكتبة Aspose.OCR، يمكنك تحويل TIFF أو أي صورة إلى PDF قابل للبحث بالكامل في ثوانٍ معدودة.

في هذا البرنامج التعليمي سنستعرض كل ما تحتاج معرفته: من تثبيت المكتبة، تحميل TIFF متعدد الصفحات، إلى استدعاء `RecognizeToPdf` حتى تتمكن من **تحويل PDF باستخدام OCR** و**إنشاء ملفات PDF قابلة للبحث** يمكن لمستخدميك البحث فيها فعليًا. في النهاية، ستحصل على تطبيق Console جاهز للتنفيذ ينتج PDF قابل للبحث من مصدر صورة.

## المتطلبات المسبقة

- **.NET 6.0** أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+).
- رخصة **Aspose.OCR** صالحة أو مفتاح تقييم مؤقت (الإصدار التجريبي المجاني يكفي للاختبار).
- Visual Studio 2022 (أو أي محرر تفضله) مع مدير الحزم **NuGet**.
- ملف إدخال باسم `input.tif` موجود في مجلد تتحكم به—ملفات TIFF متعددة الصفحات تعمل مباشرةً.

> **نصيحة احترافية:** إذا كنت على نظام Windows، انسخ ملف TIFF إلى نفس المجلد الذي يحتوي على ملف `.exe` المُجمع لتجنب مشاكل المسارات.

## الخطوة 1: تثبيت حزمة Aspose.OCR عبر NuGet

افتح مجلد المشروع في الطرفية وشغّل الأمر التالي:

```bash
dotnet add package Aspose.OCR
```

يقوم هذا بجلب أحدث نسخة مستقرة (حتى فبراير 2026 الإصدار 23.10) ويضيف جميع الاعتمادات المطلوبة. بعد انتهاء الاستعادة، سترى `Aspose.OCR` مدرجًا تحت **Dependencies** في مستكشف الحلول.

## الخطوة 2: إنشاء تطبيق Console بسيط

أنشئ مشروع console جديد إذا لم يكن لديك واحد بالفعل:

```bash
dotnet new console -n OcrSearchablePdfDemo
cd OcrSearchablePdfDemo
```

استبدل ملف `Program.cs` الذي تم إنشاؤه تلقائيًا بالكود الكامل الموجود في **الخطوة 3**. سيقوم البرنامج بـ:

1. إنشاء محرك OCR.
2. تحميل صورة المصدر (أو TIFF متعدد الصفحات).
3. تشغيل OCR وكتابة النتيجة مباشرةً إلى PDF قابل للبحث.
4. إبلاغ المستخدم بأن العملية نجحت.

## الخطوة 3: الكود الكامل – من صورة إلى PDF قابل للبحث

فيما يلي ملف المصدر **كامل**. انسخه والصقه في `Program.cs`. تم تضمين التعليقات لتوضيح الأجزاء غير الواضحة.

```csharp
using System;
using Aspose.OCR;          // Core OCR namespace
using Aspose.OCR.Image;   // Provides ImageStream helpers

namespace OcrSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialise the OCR engine.
            // -------------------------------------------------
            // The Engine class is the entry point for all OCR operations.
            // You can optionally pass a license object here if you have one.
            var ocrEngine = new Engine();

            // -------------------------------------------------
            // 2️⃣ Load the source image.
            // -------------------------------------------------
            // ImageStream.FromFile supports TIFF, PDF, JPEG, PNG, etc.
            // For multi‑page TIFFs the stream automatically contains all pages.
            string inputPath = "YOUR_DIRECTORY/input.tif";
            var imageStream = ImageStream.FromFile(inputPath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR and write a searchable PDF.
            // -------------------------------------------------
            // RecognizeToPdf does the heavy lifting:
            // • It runs the OCR engine on every page.
            // • It embeds the extracted text as an invisible layer.
            // • The visual appearance of the original image is preserved.
            string outputPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.RecognizeToPdf(imageStream, outputPath);

            // -------------------------------------------------
            // 4️⃣ Inform the user.
            // -------------------------------------------------
            Console.WriteLine("Searchable PDF created at: " + outputPath);
        }
    }
}
```

**ما ستلاحظه:** بعد تشغيل البرنامج، سيظهر ملف باسم `searchable.pdf` في المجلد المستهدف. افتحه في Adobe Reader أو أي عارض PDF وجرب البحث عن كلمة موجودة في TIFF الأصلي. يجب أن يتم العثور على النص فورًا، مما يثبت أنك نجحت في **إنشاء PDF قابل للبحث** من صورة.

### تشغيل التطبيق

```bash
dotnet run
```

إذا تم إعداد كل شيء بشكل صحيح ستحصل على:

```
Searchable PDF created at: YOUR_DIRECTORY/searchable.pdf
```

افتح ملف PDF، اضغط `Ctrl+F`، اكتب كلمة من المصدر، وسترى التحديد ينتقل إلى الموقع الصحيح.

## الخطوة 4: التغييرات الشائعة وحالات الحافة

### تحويل PDF عادي (صورة‑فقط) إلى PDF قابل للبحث

إذا كان المصدر PDF يحتوي على صور ممسوحة ضوئيًا بدلاً من نص، يمكنك استخدام نفس الطريقة—فقط غيّر مصدر `ImageStream` إلى:

```csharp
var pdfStream = ImageStream.FromFile("YOUR_DIRECTORY/input.pdf");
ocrEngine.RecognizeToPdf(pdfStream, "YOUR_DIRECTORY/searchable_from_pdf.pdf");
```

هذا يلبي سيناريو **تحويل PDF باستخدام OCR** دون أي كود إضافي.

### معالجة مستندات متعددة الصفحات كبيرة الحجم

للمستندات التي تتجاوز بضع مئات صفحة، ضع في اعتبارك:

- **زيادة حدود الذاكرة** (`Engine.MemoryLimit = 2_000; // MB`).
- **المعالجة على دفعات**: حمّل مجموعة فرعية من الصفحات، اكتب ملفات PDF وسيطة، ثم دمجها باستخدام مكتبة PDF (مثل Aspose.PDF).

### التعامل مع لغات غير الإنجليزية

تدعم Aspose.OCR العديد من اللغات مباشرة. اضبط اللغة قبل التعرف:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

إذا كنت تحتاج إلى **tiff إلى pdf قابل للبحث** بلغة غير لاتينية، تأكد من تثبيت حزمة اللغة المناسبة.

### ماذا لو كان PDF الناتج فارغًا؟

- تحقق من أن ملف الإدخال غير تالف.
- تأكد من أن محرك OCR يحمل رخصة صالحة—وضع التقييم قد يفرض حدودًا على عدد الصفحات.
- تحقق من أن دقة الصورة لا تقل عن 300 dpi؛ الدقة الأقل قد تؤدي إلى ضعف التعرف.

## الخطوة 5: التحقق من النتيجة برمجيًا (اختياري)

أحيانًا تريد التأكد من أن PDF يحتوي فعلاً على طبقة نصية. يمكنك استخدام Aspose.PDF لاستخراج النص:

```csharp
using Aspose.Pdf;

var pdfDoc = new Document("YOUR_DIRECTORY/searchable.pdf");
string extracted = pdfDoc.Pages[1].ExtractText();
Console.WriteLine("First page text snippet: " + extracted.Substring(0, 100));
```

إذا كان المتغير `extracted` غير فارغ، فقد نجحت في **إنشاء pdf قابل للبحث**.

## الخلاصة

غطينا **كيفية تنفيذ OCR** على TIFF (أو أي صورة) و**تحويل PDF باستخدام OCR** بسلاسة لإنشاء **PDF قابل للبحث** يتصرف كوثيقة أصلية. الخطوات الأساسية هي:

1. تثبيت Aspose.OCR.  
2. تهيئة `Engine`.  
3. تحميل الصورة عبر `ImageStream`.  
4. استدعاء `RecognizeToPdf`.  

من هنا يمكنك تجربة إعدادات اللغة، المعالجة الدفعية الكبيرة، أو دمج النتيجة مع مهام أخرى لمعالجة PDF. نفس النمط يعمل لـ **tiff إلى pdf قابل للبحث**، **pdf قابل للبحث من صورة**، وحتى ملفات PDF الممسوحة ضوئيًا.

هل أنت مستعد للتحدي التالي؟ جرّب دمج OCR في واجهة ويب API بحيث يمكن للمستخدمين رفع مسحات والحصول على PDFs قابلة للبحث فورًا، أو استكشف OCR على الملاحظات المكتوبة بخط اليد باستخدام إعدادات `OcrEngine` المتقدمة. الاحتمالات لا حصر لها—برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}