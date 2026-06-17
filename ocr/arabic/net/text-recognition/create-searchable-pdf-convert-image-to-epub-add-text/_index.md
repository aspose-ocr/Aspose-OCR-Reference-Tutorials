---
category: general
date: 2026-03-13
description: إنشاء ملف PDF قابل للبحث من أي صورة باستخدام Aspose OCR. تعلم كيفية تحويل
  الصورة إلى EPUB، وإضافة نص قابل للبحث، وإنشاء ملف PDF قابل للبحث باستخدام C#.
draft: false
keywords:
- create searchable pdf
- convert image to epub
- ocr image to pdf
- add searchable text
- generate searchable pdf
language: ar
og_description: إنشاء ملف PDF قابل للبحث من أي صورة باستخدام Aspose OCR. يوضح هذا
  الدليل كيفية تحويل الصورة إلى EPUB، وإضافة نص قابل للبحث، وإنشاء ملف PDF قابل للبحث
  باستخدام C#.
og_title: إنشاء PDF قابل للبحث – تحويل الصورة إلى EPUB وإضافة النص
tags:
- Aspose OCR
- C#
- PDF
- EPUB
title: إنشاء ملف PDF قابل للبحث – تحويل الصورة إلى EPUB وإضافة النص
url: /ar/net/text-recognition/create-searchable-pdf-convert-image-to-epub-add-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث – تحويل الصورة إلى EPUB وإضافة نص

هل تريد **إنشاء PDF قابل للبحث** من إيصال ممسوح ضوئياً أو أي صورة؟ في هذا الدرس سنوضح لك كيفية إنشاء PDF قابل للبحث باستخدام Aspose OCR بينما **تحول الصورة إلى EPUB** و**تضيف طبقات نصية قابلة للبحث** — كل ذلك في مشروع C# واحد.  

إذا كنت قد عانيت من ملفات PDF تبدو جيدة ولكن لا يمكن البحث فيها، فأنت لست وحدك. الخبر السار هو أن طبقة نص مخفية يمكنها تحويل صورة مسطحة إلى مستند قابل للبحث بالكامل، وAspose تجعل ذلك شبه خالٍ من المتاعب.

## ما ستتعلمه

* كيفية تهيئة محرك Aspose OCR وتحديد اللغة.  
* الخطوات الدقيقة **لتحويل الصورة إلى EPUB** لتوزيع الكتب الإلكترونية.  
* كيفية تكوين كاتب PDF بحيث يحتوي الناتج على طبقة نص مخفية وقابلة للبحث.  
* نصائح للتعامل مع الحالات الخاصة مثل الإيصالات متعددة الصفحات أو اللغات غير الإنجليزية.  

كل ما تحتاجه مسبقاً هو بيئة تطوير .NET (Visual Studio 2022 أو أحدث) وحزمة Aspose OCR NuGet. لا خدمات خارجية، لا ملفات إعدادات غامضة — مجرد C# عادي يمكنك نسخه‑ولصقه وتشغيله.

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6.0+   | Aspose OCR يستهدف .NET Standard 2.0+، لذا .NET 6 يمنحك أحدث تحسينات وقت التشغيل. |
| حزمة Aspose.OCR NuGet | توفر الفئات `OcrEngine` و `EpubWriter` و `PdfWriter` المستخدمة في الكود. |
| ملف صورة (مثال، `receipt.jpg`) | المصدر الذي ستجري عليه OCR. أي صورة نقطية (PNG، JPEG، BMP) تعمل. |
| معرفة أساسية بـ C# | ستقرأ وتعدل المقاطع، وليس تعلم اللغة من الصفر. |

يمكنك تثبيت الحزمة باستخدام الأمر التالي:

```bash
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، فإن واجهة مدير الحزم NuGet تقوم بنفس المهمة — فقط ابحث عن “Aspose.OCR”.

## الخطوة 1 – إنشاء PDF قابل للبحث باستخدام Aspose OCR

أول شيء نحتاجه هو كائن `OcrEngine` يعرف أي لغة يجب التعرف عليها. الإنجليزية هي الافتراضية، لكن يمكنك استبدالها بالفرنسية أو الألمانية، إلخ، عن طريق ضبط `ocrEngine.Language`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialise the OCR engine and set the language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English          // Change this if your document isn’t English
};
```

لماذا نهيئ المحرك أولاً؟ يحتفظ المحرك بنموذج التعرف في الذاكرة، لذا إن إنشائه مرة واحدة وإعادة استخدامه عبر صور متعددة يوفر كلًا من وحدة المعالجة المركزية والذاكرة. في وظائف الدفعات الكبيرة، ستحافظ على نفس الكائن طوال فترة التشغيل.

## الخطوة 2 – تحميل الصورة وإجراء OCR

بعد ذلك نوجه المحرك إلى الملف الذي نريد معالجته. `ImageStream.FromFile` يقرأ الصورة إلى صيغة يفهمها محرك OCR.

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Run the recognition engine – this populates the internal text buffer
ocrEngine.Recognize();
```

> **ماذا لو كانت الصورة متعددة الصفحات؟**  
> Aspose OCR يمكنه معالجة ملفات TIFF متعددة الصفحات مباشرة. فقط مرّر مسار ملف TIFF؛ سيقوم المحرك بالتنقل عبر كل صفحة تلقائيًا.

## الخطوة 3 – تحويل الصورة إلى EPUB

إذا كنت تحتاج أيضًا إلى نسخة إلكترونية من المستند الممسوح، فإن Aspose يجعل ذلك بسطر واحد. `EpubWriter` يستخدم نفس كائن `OcrEngine`، مما يعني إعادة استخدام نتائج OCR دون معالجة إضافية.

```csharp
// Export the recognised content to an ePub file
EpubWriter epubWriter = new EpubWriter();
epubWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt.epub");
```

لماذا التصدير إلى EPUB؟ EPUB هو تنسيق قابل لإعادة التدفق — مثالي لقارئات الهواتف المحمولة. يصبح نص OCR قابلًا للتحديد، وتبقى الصورة الأصلية كخلفية، مما يحافظ على مظهر المسح الأصلي.

## الخطوة 4 – إضافة طبقة نصية قابلة للبحث إلى PDF

الآن يأتي الجزء الذي **ينشئ PDF قابل للبحث** فعليًا. من خلال تمكين `AddSearchableTextLayer`، يدمج كاتب PDF طبقة نصية غير مرئية تعكس مخرجات OCR. يمكن للمستخدمين البحث، النسخ، أو تمييز النص كما في PDF أصلي.

```csharp
// Configure PDF writer to include a hidden searchable text layer
PdfWriter pdfWriter = new PdfWriter
{
    AddSearchableTextLayer = true   // Enables the hidden text layer for searchability
};

// Save the OCR result as a searchable PDF
pdfWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt_searchable.pdf");
```

> **مشكلة شائعة:** نسيان ضبط `AddSearchableTextLayer` ينتج عنه PDF يبدو متطابقًا لكنه لا يحتوي على نص قابل للبحث. تأكد دائمًا من هذا الإعداد عندما تحتاج إلى مستند قابل للبحث.

## الخطوة 5 – مثال كامل يعمل

بجمع كل شيء معًا، إليك تطبيق console مستقل يمكنك وضعه في مشروع .NET جديد وتشغيله فورًا.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace OcrToPdfAndEpub
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the source image
            string imagePath = "YOUR_DIRECTORY/receipt.jpg";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            ocrEngine.Recognize();

            // 4️⃣ Convert to EPUB (optional but handy)
            EpubWriter epubWriter = new EpubWriter();
            string epubPath = "YOUR_DIRECTORY/receipt.epub";
            epubWriter.Save(ocrEngine, epubPath);
            Console.WriteLine($"EPUB saved to {epubPath}");

            // 5️⃣ Create searchable PDF
            PdfWriter pdfWriter = new PdfWriter
            {
                AddSearchableTextLayer = true
            };
            string pdfPath = "YOUR_DIRECTORY/receipt_searchable.pdf";
            pdfWriter.Save(ocrEngine, pdfPath);
            Console.WriteLine($"Searchable PDF saved to {pdfPath}");
        }
    }
}
```

### النتيجة المتوقعة

* `receipt.epub` – ملف EPUB يمكنك فتحه في Calibre أو Apple Books أو أي قارئ إلكتروني.  
* `receipt_searchable.pdf` – ملف PDF يمكنك الضغط على **Ctrl + F** للعثور على أي كلمة ظهرت في الصورة الأصلية.

إذا فتحت ملف PDF في Adobe Acrobat وعرضت **File → Properties → Description**، ستلاحظ تدفق نص مخفي تحت علامة التبويب **Fonts**، مما يؤكد وجود الطبقة القابلة للبحث.

## أسئلة شائعة وحالات خاصة

**س: هل يعمل هذا مع لغات غير الإنجليزية؟**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}