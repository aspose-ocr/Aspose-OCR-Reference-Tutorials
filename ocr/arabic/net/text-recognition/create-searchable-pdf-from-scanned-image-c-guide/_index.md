---
category: general
date: 2026-04-26
description: إنشاء ملف PDF قابل للبحث من صورة ممسوحة ضوئياً باستخدام Aspose OCR في
  C#. تعلم كيفية تحويل الصورة الممسوحة، استخراج النص، وإنشاء ملف PDF قابل للبحث بسرعة.
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: ar
og_description: إنشاء ملف PDF قابل للبحث من صورة ممسوحة ضوئياً باستخدام Aspose OCR.
  كود C# خطوة بخطوة للتحويل واستخراج النص وإنشاء ملف PDF قابل للبحث.
og_title: إنشاء ملف PDF قابل للبحث من صورة ممسوحة ضوئيًا – دليل C#
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: إنشاء ملف PDF قابل للبحث من صورة ممسوحة ضوئيًا – دليل C#
url: /ar/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث من صورة ممسوحة ضوئياً – دليل C#

هل احتجت يوماً إلى **إنشاء PDF قابل للبحث** من عقود ورقية أو إيصالات أو أرشيفات قديمة؟ لست وحدك—معظم المطورين يواجهون هذه العقبة عندما يسلمهم العميل كومة من مسحات TIFF ويتوقعون ملف PDF قابل للبحث كالناتج النهائي.  

في هذا الدرس سنوضح لك بالضبط **كيفية OCR مستند** وتحويل صورة ممسوحة إلى **PDF قابل للبحث** باستخدام Aspose OCR لـ .NET. في النهاية ستتمكن من **تحويل صورة ممسوحة**، **استخراج النص من الصورة**، وحتى التعامل مع ملفات TIFF متعددة الصفحات دون عناء.

## ما ستحتاجه

* .NET 6.0 أو أحدث (API يعمل مع .NET Core، .NET Framework، و .NET 5+).  
* رخصة Aspose OCR صالحة أو إذا كنت راضيًا عن العلامة المائية للتقييم.  
* حزمة NuGet `Aspose.OCR` مثبتة (`dotnet add package Aspose.OCR`).  
* ملف TIFF تجريبي (مثال: `contract_scan.tif`) تريد تحويله إلى PDF قابل للبحث.

هذا كل شيء—لا مكتبات إضافية، ولا إعدادات معقدة. جاهز؟ هيا نبدأ.

![إنشاء مثال PDF قابل للبحث](create-searchable-pdf.png "إنشاء مثال PDF قابل للبحث")

## الخطوة 1 – تهيئة محرك OCR (إنشاء PDF قابل للبحث)

أولاً: تحتاج إلى كائن `OcrEngine`. هذا الكائن هو العامل الأساسي الذي يقرأ البت ماب، يحدد الأحرف، ويعيد لك النص.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**لماذا ضبط اللغة؟**  
إذا تركتها على الإعداد الافتراضي، سيحاول Aspose تجربة كل حزمة لغات، مما يبطئ العملية. تحديد `Language.Latin` يخبر المحرك بالتركيز على الأبجدية اللاتينية، مما يمنحك تسريعًا ودقة أعلى للوثائق الإنجليزية.

## الخطوة 2 – تحميل الصورة الممسوحة (تحويل صورة ممسوحة)

الآن نغذي المحرك بالصورة التي نريد معالجتها. يمكن لـ Aspose قراءة مسار ملف، تدفق، أو حتى `byte[]`. للتبسيط سنستخدم `ImageStream.FromFile`.  

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

إذا احتجت يوماً إلى **تحويل TIFF إلى PDF** لاحقًا، تذكر أن ملفات TIFF متعددة الصفحات تُعالج تلقائيًا—كل إطار يصبح صفحة PDF منفصلة.

## الخطوة 3 – تشغيل OCR والحصول على النص (استخراج النص من الصورة)

تشغيل OCR سهل مثل استدعاء `Recognize`. سيعيد المحرك كائن `RecognitionResult` يحتوي على النص العادي، درجات الثقة، ومعلومات التخطيط.  

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**نصيحة احترافية:** إذا كنت تحتاج النص فقط (بدون PDF)، يمكنك التوقف هنا وكتابة `extractedText` إلى ملف `.txt`. لكن غالبًا هدفنا هو PDF قابل للبحث، لذا سنستمر.

## الخطوة 4 – حفظ كـ PDF قابل للبحث (إنشاء PDF قابل للبحث)

يجعل Aspose الخطوة الأخيرة بسيطة: فقط استدعِ `Save` مع `SaveFormat.PdfSearchable`. في الخلفية، المكتبة تدمج النص المستخرج كطبقة غير مرئية مع الحفاظ على مظهر الصورة الأصلي.  

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

عند فتح `contract_searchable.pdf` في أي عارض PDF، ستتمكن من تحديد النص، نسخه، والبحث فيه—تمامًا ما يتوقعه العميل من “PDF قابل للبحث”.

## معالجة ملفات TIFF متعددة الصفحات (تحويل TIFF إلى PDF)

إذا كان ملف المصدر يحتوي على عدة صفحات، سيعامل Aspose كل إطار كصفحة منفصلة تلقائيًا. لا حاجة لحلقات إضافية. ومع ذلك، قد ترغب في التحكم في DPI أو جودة الصورة لكل صفحة:

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

بعد ضبط هذه الخيارات، كرّر **الخطوة 2** لكل إطار، أو ببساطة وجه `ImageStream.FromFile` إلى ملف TIFF متعدد الصفحات ودع Aspose يتولى العمل.

## المشكلات الشائعة وكيفية إصلاحها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| النص مشوش أو مفقود | تم ضبط لغة خاطئة | اضبط `ocrEngine.Language` إلى حزمة اللغة الصحيحة (مثال: `Language.German`). |
| حجم الـ PDF كبير (10 MB لمسح صفحة واحدة) | ضغط الصورة الافتراضي منخفض | قم بتعديل `ocrEngine.ImageProcessingOptions.Compression` إلى `Jpeg` واضبط قيمة `Quality` معقولة (0‑100). |
| تشغيل OCR ببطء شديد | استخدام الكشف التلقائي للغة الافتراضي | حدد اللغة المتوقعة صراحةً. |
| لا تظهر طبقة البحث | تم حفظه باستخدام `SaveFormat.Pdf` بدلاً من `PdfSearchable` | استخدم `PdfSearchable`. |

## مثال كامل من البداية إلى النهاية

بوضع كل شيء معًا، إليك تطبيق وحدة تحكم جاهز للتنفيذ يمكنك نسخه ولصقه في Visual Studio:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**ما ستراه:**  
* نافذة وحدة التحكم التي تطبع مقتطفًا من النص المستخرج بواسطة OCR.  
* ملف `contract_searchable.pdf` موجود بجوار ملف TIFF الأصلي. افتحه، اضغط **Ctrl + F**، وابحث عن أي كلمة ظهرت في المسح الأصلي—ها هو، يعمل.

## الخطوات التالية والمواضيع ذات الصلة

* **كيفية OCR مستندات** على دفعات – غلف الكود أعلاه داخل حلقة `foreach` ومعالجة مجلد كامل.  
* **تحويل صورة ممسوحة** إلى صيغ غير TIFF (PNG، JPEG) – نفس الـ API يعمل؛ فقط غيّر امتداد الملف.  
* **استخراج النص من الصورة** للتحليل الإضافي – مرر `result.Text` إلى خط أنابيب معالجة اللغة الطبيعية.  
* **تحسين حجم PDF** – استكشف `PdfSaveOptions` لضغط الصور أكثر أو تضمين الخطوط فقط عند الحاجة.  

جرّب هذه الأفكار، وستصبح سريعًا الشخص المرجعي لأي طلب “تحويل هذا المسح إلى PDF قابل للبحث”.

---

### TL;DR

أنت الآن تعرف كيف **إنشاء PDF قابل للبحث** من صور ممسوحة باستخدام Aspose OCR في C#. العملية هي: تهيئة المحرك، تحميل الصورة، تشغيل OCR، والحفظ باستخدام `PdfSearchable`. اضبط إعدادات اللغة، DPI، والضغط للتعامل مع الحالات الخاصة، وستكون جاهزًا **لتحويل صورة ممسوحة**, **لاستخراج النص من الصورة**, وحتى **تحويل TIFF إلى PDF** على نطاق واسع. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}