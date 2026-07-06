---
category: general
date: 2026-02-11
description: إنشاء ملف PDF قابل للبحث من صورة عربية باستخدام C#. تعلم كيفية تحويل
  الصورة إلى PDF، استخراج النص العربي، وإضافة نص مخفي باستخدام Aspose OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract arabic text
- pdf with hidden text
- ocr arabic image
language: ar
og_description: إنشاء ملف PDF قابل للبحث من صورة عربية باستخدام Aspose OCR في C#.
  اتبع هذا الدليل لتحويل الصورة إلى PDF، واستخراج النص العربي، وإدراج النص المخفي.
og_title: إنشاء ملف PDF قابل للبحث من صورة عربية – خطوة بخطوة
tags:
- Aspose
- OCR
- PDF
- C#
- Arabic
title: إنشاء ملف PDF قابل للبحث من صورة عربية – دليل كامل
url: /ar/net/text-recognition/create-searchable-pdf-from-arabic-image-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ملف PDF قابل للبحث من صورة عربية – دليل كامل

هل احتجت يوماً إلى **إنشاء PDF قابل للبحث** من فاتورة عربية ممسوحة ضوئياً لكنك لم تكن متأكدًا من كيفية الحفاظ على المظهر الأصلي مع إمكانية تحديد النص؟ لست وحدك. في العديد من مشاريع أتمتة المستندات التحدي ليس مجرد تحويل الصورة إلى PDF، بل أيضًا الحفاظ على التخطيط البصري وإضافة طبقة نص مخفية يمكن لمحركات البحث فهرستها.

في هذا الدرس سنستعرض العملية بالكامل: **تحويل الصورة إلى PDF**، **استخراج النص العربي** باستخدام Aspose OCR، وأخيرًا دمج هذا النص كـ **PDF بنص مخفي** بحيث يكون الملف الناتج قابلًا للبحث بالكامل. في النهاية ستحصل على مقتطف C# جاهز يمكنك وضعه في أي حل .NET. لا خدمات خارجية، فقط مكتبات Aspose التي لديك بالفعل.

## ما الذي ستحتاجه

- .NET 6 أو أحدث (الكود يعمل أيضًا مع .NET Core)  
- حزم NuGet **Aspose.OCR** و **Aspose.Pdf** (أحدث الإصدارات حتى فبراير 2026)  
- ملف صورة عربية (مثال: `arabic_invoice.jpg`) تريد تحويله إلى PDF قابل للبحث  
- قليل من معرفة C# – المفاهيم بسيطة، لكننا سنشرح “السبب” وراء كل سطر.

> **نصيحة احترافية:** إذا لم تقم بعد بإضافة حزم NuGet، نفّذ  
> `dotnet add package Aspose.OCR` و  
> `dotnet add package Aspose.Pdf` من مجلد المشروع الخاص بك.

بعد الانتهاء من المتطلبات المسبقة، دعنا نغوص في تنفيذ الخطوات خطوة بخطوة.

## الخطوة 1 – إعداد محرك OCR للنص العربي

أول شيء علينا فعله هو تكوين Aspose OCR للتعرف على الأحرف العربية. العربية لغة من اليمين إلى اليسار، لذا يجب إخبار المحرك بأي لغة يجب تحميلها وتمكين تنزيل الموارد تلقائيًا في حال لم تكن بيانات اللغة موجودة على الجهاز.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Configure OCR for Arabic and let Aspose fetch the language pack if needed
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Arabic,
    AutomaticResourceDownload = true
};
```

**لماذا هذا مهم:**  
إذا تخطيت إعداد `Language = OcrLanguage.Arabic`، سيفترض المحرك اللغة الإنجليزية وستحصل على أحرف مشوشة. تمكين `AutomaticResourceDownload` يحفظك من وضع ملفات اللغة يدويًا على الخادم.

## الخطوة 2 – تحميل صورة المصدر

بعد ذلك نقوم بتحميل الصورة التي تحتوي على النص العربي. استخدام `Image.FromFile` يضمن قراءة الصورة إلى كائن GDI+ `Image`، وهو ما يتوقعه Aspose OCR.

```csharp
using System.Drawing;          // For Image
using System.IO;                // For MemoryStream

// Replace with the actual path to your Arabic invoice
string imagePath = @"YOUR_DIRECTORY/arabic_invoice.jpg";

using (var inputImage = Image.FromFile(imagePath))
{
    // The rest of the workflow lives inside this using block
```

**حالة حافة:** إذا كانت الصورة ضخمة (مثلاً صفحة A3 ممسوحة)، فكر في تقليل حجمها أولاً لتحسين الأداء. يستطيع محرك OCR التعامل مع ملفات كبيرة، لكن استهلاك الذاكرة يرتفع بسرعة.

## الخطوة 3 – التعرف على النص العربي والتقاط النتيجة

الآن نقوم فعليًا بتشغيل OCR. طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على النص المكتشف، درجات الثقة، ومربعات الحدود (إذا احتجت إليها لاحقًا لتحليل تخطيط متقدم).

```csharp
    // Perform OCR on the loaded image
    OcrResult ocrResult = ocrEngine.Recognize(inputImage);
    string extractedText = ocrResult.Text;

    // Quick sanity check: print the first 200 characters to the console
    Console.WriteLine("Extracted Arabic text (preview):");
    Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**لماذا نحتفظ بمعاينة؟**  
رؤية مقتطف من النص المستخرج يساعدك على التحقق من تحميل حزمة اللغة بشكل صحيح قبل إضاعة الوقت في إنشاء PDF.

## الخطوة 4 – إنشاء مستند PDF جديد وإضافة صفحة فارغة

مع النص في يدنا يمكننا البدء في بناء PDF. Aspose PDF يزودنا بكائن `Document` يمثل الملف بالكامل. إضافة صفحة تمنحنا مساحة لوضع كل من الصورة الأصلية وطبقة النص المخفية.

```csharp
    // Initialize a new PDF document
    var pdfDocument = new Aspose.Pdf.Document();

    // Add a blank page – this will become the background for our image
    var pdfPage = pdfDocument.Pages.Add();
```

**ملاحظة:** يمكنك إضافة صفحات متعددة إذا كنت تعالج ملف TIFF أو PDF متعدد الصفحات، لكن في سيناريو صورة واحدة صفحة واحدة تكفي.

## الخطوة 5 – إدراج الصورة الأصلية كعنصر خلفية

نريد أن يبدو PDF النهائي مطابقة تمامًا للفاتورة الممسوحة، لذا ندمج الصورة كخلفية مرئية. فئة `Image` من Aspose PDF تتوقع تدفقًا (stream)، لذا نقرأ الملف إلى `MemoryStream`.

```csharp
    // Load the same image bytes for the PDF background
    var backgroundImage = new Aspose.Pdf.Image
    {
        ImageStream = new MemoryStream(File.ReadAllBytes(imagePath))
    };

    // Add the image to the page's paragraph collection
    pdfPage.Paragraphs.Add(backgroundImage);
```

**لماذا نستخدم صورة خلفية؟**  
وضع الصورة مباشرة على الصفحة يحافظ على التخطيط الأصلي، الألوان، وأي طوابع أو شعارات قد يتجاهلها محرك OCR.

## الخطوة 6 – إضافة نص OCR كطبقة مخفية

السر لإنتاج **PDF قابل للبحث** هو طبقة نص مخفية توضع فوق الصورة. بتعيين حجم الخط إلى `0` نجعل النص غير مرئي للعين البشرية مع بقائه قابلًا للتحديد والبحث.

```csharp
    // Create a TextFragment with the extracted Arabic text
    var searchableText = new Aspose.Pdf.Text.TextFragment(extractedText)
    {
        // Hide the visible text; only the text layer remains searchable
        TextState = { FontSize = 0 }
    };

    // Add the hidden text fragment to the same page
    pdfPage.Paragraphs.Add(searchableText);
```

**تفصيل مهم:**  
إذا كنت بحاجة إلى محاذاة النص المخفي بدقة مع الصورة (مثلاً عندما تُعيد OCR إحداثيات)، يمكنك استخدام `TextFragmentAbsorber` وتحديد موضع كل جزء يدويًا. بالنسبة لمعظم الفواتير، تغطية الصفحة بالكامل بنص بسيط كافية.

## الخطوة 7 – حفظ PDF القابل للبحث

أخيرًا نكتب ملف PDF إلى القرص. سيحتوي الملف الناتج على كل من الصورة المرئية والنص العربي المخفي، مما يجعله قابلًا للبحث بالكامل في Adobe Reader، Google Drive، أو أي عارض يدعم OCR.

```csharp
    // Define the output path
    string outputPath = @"YOUR_DIRECTORY/arabic_invoice_searchable.pdf";

    // Save the document
    pdfDocument.Save(outputPath);

    Console.WriteLine($"Searchable PDF created at: {outputPath}");
}
```

### مثال كامل يعمل

بجمع كل القطع معًا، إليك البرنامج الكامل الجاهز للتنفيذ:

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure OCR for Arabic
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Arabic,
            AutomaticResourceDownload = true
        };

        // 2️⃣ Load the source image
        string imagePath = @"YOUR_DIRECTORY/arabic_invoice.jpg";
        using (var inputImage = Image.FromFile(imagePath))
        {
            // 3️⃣ Run OCR and get the text
            OcrResult ocrResult = ocrEngine.Recognize(inputImage);
            string extractedText = ocrResult.Text;

            // Optional preview
            Console.WriteLine("Extracted Arabic text (preview):");
            Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));

            // 4️⃣ Create PDF document
            var pdfDocument = new Document();
            var pdfPage = pdfDocument.Pages.Add();

            // 5️⃣ Add original image as background
            var backgroundImage = new Aspose.Pdf.Image
            {
                ImageStream = new MemoryStream(File.ReadAllBytes(imagePath))
            };
            pdfPage.Paragraphs.Add(backgroundImage);

            // 6️⃣ Add hidden searchable text
            var searchableText = new TextFragment(extractedText)
            {
                TextState = { FontSize = 0 }
            };
            pdfPage.Paragraphs.Add(searchableText);

            // 7️⃣ Save the searchable PDF
            string outputPath = @"YOUR_DIRECTORY/arabic_invoice_searchable.pdf";
            pdfDocument.Save(outputPath);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**النتيجة المتوقعة:** افتح الملف `arabic_invoice_searchable.pdf` في أي عارض PDF، اضغط **Ctrl + F** واكتب كلمة عربية تظهر في الفاتورة الأصلية. سيقوم العارض بتحديد الكلمة رغم أنك لا ترى أي طبقة نصية.

## أسئلة شائعة ومشكلات محتملة

- **هل يعمل مع لغات أخرى؟**  
  بالتأكيد. فقط غيّر `Language = OcrLanguage.YourLanguage` وتأكد من توفر حزمة اللغة. باقي الخطوات تبقى كما هي.

- **ماذا لو كانت ثقة OCR منخفضة؟**  
  يمكنك فحص `ocrResult.Confidence` (قيمة بين 0 و 1). إذا كانت أقل من عتبة معينة (مثلاً 0.75)، فكر في معالجة الصورة مسبقًا—إزالة الميل، زيادة التباين، أو التحويل إلى تدرج رمادي—قبل تمريرها إلى المحرك.

- **هل يمكن إضافة صور متعددة إلى PDF واحد؟**  
  نعم. كرّر عبر مجموعة مسارات الصور، أضف صفحة جديدة لكل صورة، وكرر الخطوات 5‑6. فقط تذكّر إبقاء كتلة `using` لكل صورة لتحرير موارد GDI.

- **هل النص المخفي غير مرئي تمامًا؟**  
  تعيين `FontSize = 0` يجعل النص غير مرئي في معظم العارضين. إذا ظل عارض ما يظهر رموزًا خفيفة، يمكنك أيضًا تعيين لون النص إلى شفاف تمامًا (`TextState.FillColor = Color.Transparent`).

## الخطوات التالية

الآن بعد أن عرفت كيفية **إنشاء PDF قابل للبحث** من صورة عربية، قد ترغب في استكشاف:

- **المعالجة الدفعية** – قراءة جميع الصور في مجلد وإنشاء PDF قابل للبحث لكل ملف.  
- **إضافة إحداثيات OCR** – استخدام `OcrResult.Regions` لتحديد موضع كل جزء نصي بدقة، مما يحسن دقة البحث في التخطيطات المعقدة.  
- **تشفير PDF** – Aspose PDF يتيح لك إضافة كلمات مرور أو توقيعات رقمية إذا كنت تحتاج إلى أمان إضافي.  
- **التكامل مع Azure Blob Storage** – تخزين ملفات PDF المولدة مباشرةً في السحابة لتدفقات عمل لاحقة.

كل من هذه المواضيع يتضمن بطبيعة الحال الكلمات المفتاحية الثانوية **convert image to pdf**, **extract

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}