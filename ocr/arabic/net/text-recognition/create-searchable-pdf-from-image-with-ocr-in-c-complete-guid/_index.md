---
category: general
date: 2026-05-21
description: إنشاء ملف PDF قابل للبحث من صورة باستخدام Aspose OCR في C#. تحويل الصورة
  إلى PDF، ضبط دقة PDF، وإدراج الصورة الأصلية.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- set pdf resolution
- pdf with embedded image
language: ar
og_description: إنشاء ملف PDF قابل للبحث من صورة باستخدام Aspose OCR في C#. تعلم كيفية
  تحويل الصورة إلى PDF، وضبط دقة PDF، وإدراج الصورة الأصلية.
og_title: إنشاء ملف PDF قابل للبحث من صورة باستخدام OCR في C#
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Create searchable PDF from an image using Aspose OCR in C#. Convert
    image to PDF, set PDF resolution, and embed the original image.
  headline: Create Searchable PDF from Image with OCR in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- Aspose
- C#
- PDF
title: إنشاء ملف PDF قابل للبحث من صورة باستخدام OCR في C# – دليل شامل
url: /ar/net/text-recognition/create-searchable-pdf-from-image-with-ocr-in-c-complete-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ملف PDF قابل للبحث من صورة باستخدام OCR في C# – دليل كامل

هل احتجت يوماً إلى **إنشاء ملفات PDF قابلة للبحث** من فواتير ممسوحة، إيصالات، أو ملاحظات مكتوبة يدوياً؟ لست وحدك—المطورون يواجهون هذه المشكلة باستمرار عند بناء خطوط معالجة المستندات. الخبر السار؟ باستخدام Aspose.OCR يمكنك **تحويل الصورة إلى PDF**، تضمين الصورة الأصلية، وحتى التحكم في DPI الناتج، كل ذلك في بضع أسطر من C#.

في هذا الدرس سنستعرض العملية بالكامل لتحويل صورة PNG عادية إلى **PDF قابل للبحث**. ستتعلم كيف **تقوم بعملية OCR من الصورة إلى PDF**، **تحدد دقة PDF**، وتحتفظ بالرسمة المصدر داخل الملف. في النهاية ستحصل على مقتطف شفرة جاهز يمكنك إدراجه في أي مشروع .NET.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (تعمل الواجهة البرمجية مع .NET Core و .NET Framework)
- رخصة Aspose.OCR أو مفتاح تقييم مجاني
- صورة نموذجية (مثال: `invoice.png`) موجودة في مسار يمكن لتطبيقك قراءته
- Visual Studio، Rider، أو أي محرر تفضله

لا تحتاج إلى حزم NuGet إضافية بخلاف `Aspose.OCR`—كل ما تبقى هو جزء من مكتبة الفئات الأساسية في .NET.

<img src="/images/searchable-pdf-example.png" alt="Create searchable PDF example in C#" />

## الخطوة 1: تهيئة محرك OCR – قلب العملية

أولاً وقبل كل شيء. نحتاج إلى إنشاء نسخة من `OcrEngine` ويجب أن نخبره أي لغة سيتعرف عليها. اللغة الإنجليزية تكفي لمعظم الفواتير، لكن يمكنك استبدالها بأي قيمة من تعداد `OcrLanguage`.

```csharp
using Aspose.OCR;

// Step 1 – create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English   // Change if you need another language
};
```

**لماذا هذا مهم:** المحرك هو العنصر الأساسي الذي يقرأ بيانات البكسل ويحولها إلى نص قابل للبحث. ضبط اللغة مسبقاً يحسن الدقة بشكل كبير—خاصةً للخطوط غير اللاتينية.

## الخطوة 2: تحميل الصورة المصدر – من القرص إلى الذاكرة

بعد ذلك نوجه المحرك إلى ملف الصورة الذي تريد معالجته. توفر Aspose أداة مساعدة `ImageStream.FromFile` التي تُبسط التعامل مع `FileStream` التقليدي.

```csharp
using Aspose.OCR;

// Step 2 – load the image containing the text
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");
```

**نصيحة:** إذا كانت صورتك مخزنة في سحابة أو تأتي من طلب HTTP، يمكنك أيضاً تمرير `MemoryStream` إلى `ImageStream.FromStream`. محرك OCR لا يهتم من أين تأتي البايتات.

## الخطوة 3: تكوين خيارات حفظ PDF – تضمين الصورة وتحديد الدقة

الآن نخبر Aspose كيف نريد أن يبدو ملف PDF النهائي. هناك خياران حاسمان للحصول على **PDF قابل للبحث**:

1. `EmbedOriginalImage = true` – يبقي الصورة الممسوحة داخل PDF لتحتفظ بالوضوح البصري.
2. `OutputResolution = 300` – يحدد DPI للطبقة القابلة للبحث؛ 300 DPI هو الخيار المثالي لمعظم مهام OCR.

```csharp
using Aspose.OCR.Pdf;   // PDF‑specific options

// Step 3 – define how the PDF should be saved
var pdfOptions = new PdfSaveOptions
{
    EmbedOriginalImage = true,   // Keeps the original image inside the PDF
    OutputResolution = 300       // DPI of the searchable PDF (set PDF resolution)
};
```

**لماذا هذه الإعدادات؟** تضمين الصورة الأصلية (`pdf with embedded image`) يضمن أن المستند يبدو تماماً كالمسح الضوئي، بينما طبقة النص الناتجة تجعل الملف قابلاً للبحث. يمكنك تعديل `OutputResolution` إذا أردت ملفاً أخف (150 DPI) أو دقة أعلى (600 DPI).

## الخطوة 4: حفظ النتيجة – من محرك OCR إلى PDF قابل للبحث

أخيراً، نستدعي `Save` مع مسار الملف الناتج و`PdfSaveOptions` التي أنشأناها للتو. هذا السطر الواحد يقوم بالعمل الشاق: ينفذ OCR، ينشئ طبقة نص مخفية، ويكتب PDF إلى القرص.

```csharp
// Step 4 – generate the searchable PDF
ocrEngine.Save("YOUR_DIRECTORY/invoice_searchable.pdf", pdfOptions);

Console.WriteLine("Searchable PDF created.");
```

**ما ستحصل عليه:** ملف باسم `invoice_searchable.pdf` يبدو كالصورة الأصلية `invoice.png` لكنه يمكن فهرسته عبر بحث Windows، أداة Find في Adobe Reader، أو أي محرك بحث نصي كامل.

## الخطوة 5: التحقق من النتيجة – فحوصات سريعة يمكنك إجراؤها

بعد تشغيل الشفرة، افتح PDF في Adobe Acrobat (أو أي عارض) وجرب البحث عن كلمة تعرف أنها موجودة في الفاتورة، مثل “Total”. إذا عثرت الأداة على الكلمة، فقد نجحت في **ocr image to PDF**.

يمكنك أيضاً فحص حجم الملف: لأننا **نضمّن الصورة الأصلية**، سيكون PDF أكبر من PDF يحتوي على نص فقط، لكن هذه المقايضة تستحقها للحفاظ على الجودة البصرية.

## المشكلات الشائعة والنصائح المتقدمة

| المشكلة | السبب | الحل |
|--------|-------|------|
| **PDF فارغ** | `ocrEngine.Image` غير مُعيّن أو المسار خاطئ | تحقق من مسار الملف وتأكد من تحميل الصورة دون استثناء |
| **دقة بحث منخفضة** | `OutputResolution` منخفض أو اللغة غير صحيحة | زد `OutputResolution` إلى 300‑600 DPI واضبط `OcrLanguage` المناسبة |
| **حجم الملف كبير** | `EmbedOriginalImage = true` على مسحات عالية الدقة | قلل أبعاد الصورة قبل تمريرها للمحرك، أو عيّن `EmbedOriginalImage = false` إذا كنت تحتاج النص القابل للبحث فقط |
| **استثناءات الترخيص** | استخدام النسخة التجريبية بدون مفتاح | سجّل للحصول على مفتاح ترخيص مؤقت من Aspose واستدعِ `License license = new License(); license.SetLicense("Aspose.OCR.lic");` قبل إنشاء المحرك |

## مثال كامل يعمل – انسخ، الصق، شغّل

فيما يلي تطبيق console مكتمل يمكنك تجميعه فوراً. استبدل `YOUR_DIRECTORY` بمسار حقيقي على جهازك.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑specific options

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 2️⃣ Load the source image (convert image to PDF later)
            string inputPath = @"YOUR_DIRECTORY\invoice.png";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Set PDF options – embed image & set PDF resolution
            var pdfOptions = new PdfSaveOptions
            {
                EmbedOriginalImage = true,
                OutputResolution = 300 // DPI – you can change this to set PDF resolution
            };

            // 4️⃣ Save as searchable PDF
            string outputPath = @"YOUR_DIRECTORY\invoice_searchable.pdf";
            ocrEngine.Save(outputPath, pdfOptions);

            Console.WriteLine("Searchable PDF created at:");
            Console.WriteLine(outputPath);
        }
    }
}
```

**المخرجات المتوقعة** (في وحدة التحكم):

```
Searchable PDF created at:
C:\Your\Path\YOUR_DIRECTORY\invoice_searchable.pdf
```

افتح PDF الناتج واختبر وظيفة البحث—ها قد **أنشأت ملفات PDF قابلة للبحث** من الصور.

## الخلاصة

غطينا كل ما تحتاجه **لإنشاء ملفات PDF قابلة للبحث** باستخدام Aspose OCR في C#. من تحميل الصورة وتكوين خيارات **PDF مع صورة مضمّنة**، إلى **تحديد دقة PDF** وأخيراً **حفظ نتيجة OCR**، كل ذلك يندمج في بضع أسطر فقط.

ما الخطوة التالية؟ جرّب معالجة مئات الفواتير دفعةً واحدة، جرب لغات مختلفة، أو دمج الشفرة في API ASP.NET Core يعالج التحميلات فورياً. يمكنك أيضاً استكشاف إضافة علامات مائية أو توقيعات رقمية—كلاهما مدعوم من Aspose.PDF لتعزيز أمان المستندات.

هل لديك أسئلة حول حالات حافة، الترخيص، أو تحسين الأداء؟ اترك تعليقاً أدناه، ونتمنى لك برمجة سعيدة!

## دروس ذات صلة

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}