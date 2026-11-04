---
category: general
date: 2026-03-07
description: كيفية إنشاء ePub من الصور الممسوحة ضوئياً باستخدام Aspose OCR – تعلم
  تحويل الصورة إلى ePub، استخراج النص من الصورة، إضافة المؤلف إلى ePub، وتحميل الصورة
  للتعرف الضوئي على الأحرف.
draft: false
keywords:
- how to create epub
- convert image to epub
- extract text from image
- add author to epub
- load image for ocr
language: ar
og_description: كيفية إنشاء ePub من الصور الممسوحة ضوئياً في C#. يوضح هذا الدرس كيفية
  تحويل الصورة إلى ePub، استخراج النص من الصورة، إضافة المؤلف إلى ePub، وتحميل الصورة
  للتعرف الضوئي على الأحرف.
og_title: كيفية إنشاء ePub من الصور في C# – دليل كامل
tags:
- C#
- Aspose OCR
- ePub
- Document Conversion
title: كيفية إنشاء ملف ePub من الصور باستخدام C# – دليل خطوة بخطوة
url: /ar/net/text-recognition/how-to-create-epub-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء ePub من الصور في C# – دليل كامل

هل تساءلت يومًا **how to create ePub** من مجموعة من الصفحات الممسوحة ضوئيًا؟ ربما لديك مجموعة من ملفات PNG لرواية كلاسيكية وتود تحويلها إلى ePub مرتب يمكنك قراءته على أي جهاز. الخبر السار هو أنه باستخدام Aspose OCR يمكنك **load image for OCR**، استخراج النص، ثم **convert image to ePub** ببضع أسطر فقط من C#.

في هذا الدرس سنستعرض كامل سير العمل: تحميل الصورة، استخراج النص، إضافة بعض البيانات الوصفية (نعم، سنقوم بـ **add author to epub**)، وأخيرًا كتابة ملف ePub متوافق مع المعايير. في النهاية ستحصل على ePub جاهز للنشر وفهم عميق لكل خطوة، لتتمكن من تعديل الكود للكتب متعددة الصفحات، الخطوط المخصصة، أو حتى التوزيع بدون DRM.

## ما ستحتاجه

- **.NET 6** أو أحدث (تعمل الواجهة البرمجية أيضًا مع .NET Standard 2.0+)
- **Aspose.OCR for .NET** – يمكنك الحصول على نسخة تجريبية مجانية من موقع Aspose.
- صورة ممسوحة ضوئيًا مثل `book_page.png` موجودة في مكان ما على القرص.
- بيئة تطوير مفضلة (Visual Studio، Rider، أو VS Code – سأستخدم Visual Studio في لقطات الشاشة).

لا توجد حزم NuGet إضافية مطلوبة؛ فـ Aspose.OCR يتضمن كل ما تحتاجه لتصدير ePub.

---

![كيفية إنشاء ePub من صورة ممسوحة ضوئيًا](/images/how-to-create-epub.png "كيفية إنشاء ePub من صورة ممسوحة ضوئيًا باستخدام Aspose OCR")

## الخطوة 1 – إعداد المشروع وتثبيت Aspose.OCR

أولًا وقبل كل شيء. أنشئ تطبيق console جديد:

```bash
dotnet new console -n OcrToEpubDemo
cd OcrToEpubDemo
```

أضف حزمة Aspose.OCR:

```bash
dotnet add package Aspose.OCR
```

هذا كل شيء – المكتبة تتضمن كل من OCR وتصدير ePub، لذا لن تحتاج إلى أي تبعيات إضافية.

## الخطوة 2 – تحميل الصورة لـ OCR

قبل أن نتمكن من **extract text from image**، علينا أن نوفر لمحرك OCR ما يقرأه. المساعد `ImageStream.FromFile` يجعل ذلك سهلًا:

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Load the PNG (or JPG, TIFF, etc.) you want to process
// This is the “load image for OCR” step.
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book_page.png");
```

> **نصيحة احترافية:** إذا كانت صورتك موجودة كـ resource مدمج، استخدم `ImageStream.FromResource` بدلاً من `FromFile`.

## الخطوة 3 – استخراج النص من الصورة

الآن يقوم المحرك بقراءة البكسلات وتحويلها إلى سلاسل Unicode. طريقة `Recognize` تقوم بالعمل الشاق.

```csharp
// Run the OCR process – this will fill ocrEngine.RecognitionResult
ocrEngine.Recognize();

// Optional: inspect the raw text
string rawText = ocrEngine.RecognitionResult.Text;
Console.WriteLine("Extracted text (first 200 chars):");
Console.WriteLine(rawText.Substring(0, Math.Min(200, rawText.Length)));
```

لماذا نستدعي `Recognize` بشكل منفصل؟ يتيح لك فحص ناتج OCR الخام، تعديل إعدادات اللغة، أو حتى إجراء تدقيق إملائي قبل الانتقال إلى إنشاء ePub.

## الخطوة 4 – إعداد خيارات تصدير ePub (Add Author to ePub)

إنشاء ePub مصقول ليس مجرد إلقاء النص؛ تحتاج أيضًا إلى بيانات وصفية صحيحة. فئة `EpubExportOptions` توفر لك طريقة نظيفة لـ **add author to ePub**، تعيين العنوان، وتحديد ما إذا كنت تريد تضمين الصور الأصلية.

```csharp
var epubExportOptions = new EpubExportOptions
{
    Title = "Scanned Book",          // Title shown in eReader libraries
    Author = "Unknown",              // This is where we “add author to epub”
    IncludeImages = true             // Embeds the original PNGs for visual fidelity
};
```

إذا كان لديك عدة صفحات، يمكنك الاستمرار في استدعاء `ocrEngine.Image = …` و `ocrEngine.Recognize()` داخل حلقة؛ كل استدعاء يضيف محتوى الصفحة الجديدة إلى نفس مستند ePub.

## الخطوة 5 – تحويل الصورة إلى ePub وتصديره

مع استخراج النص وتعيين البيانات الوصفية، الخطوة الأخيرة هي سطر واحد يكتب ملف ePub إلى القرص:

```csharp
// Export the recognized content to an ePub file
ocrEngine.ExportToEpub("YOUR_DIRECTORY/book.epub", epubExportOptions);

// Confirmation for the user
Console.WriteLine("ePub created.");
```

يمكن فتح `book.epub` الناتج في Calibre، Apple Books، أو أي قارئ يدعم EPUB. وبما أننا عيّننا `IncludeImages = true`، ستظهر صورة PNG الأصلية كصفحة صورة، مما يحافظ على مظهر المصدر الممسوح.

## مثال كامل يعمل

نجمع كل ما سبق في برنامج جاهز للتنفيذ:

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // This is the “load image for OCR” step.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book_page.png");

        // Step 3: Run the OCR recognition – we now “extract text from image”
        ocrEngine.Recognize();

        // (Optional) Print a snippet of the extracted text
        string snippet = ocrEngine.RecognitionResult.Text.Substring(0,
            Math.Min(200, ocrEngine.RecognitionResult.Text.Length));
        Console.WriteLine("Extracted text preview:");
        Console.WriteLine(snippet);
        Console.WriteLine();

        // Step 4: Set up ePub export options – we “add author to epub” here
        var epubExportOptions = new EpubExportOptions
        {
            Title = "Scanned Book",
            Author = "Unknown",
            IncludeImages = true   // embed the original images in the ePub
        };

        // Step 5: Export the recognized content – this is how we “convert image to epub”
        ocrEngine.ExportToEpub("YOUR_DIRECTORY/book.epub", epubExportOptions);

        // Step 6: Inform the user that the ePub has been created
        Console.WriteLine("ePub created.");
    }
}
```

### المخرجات المتوقعة

```
Extracted text preview:
Chapter 1
It was a bright cold day in April, and the...
 
ePub created.
```

افتح `book.epub` في القارئ المفضل لديك وسترى صفحة عنوان، سطر المؤلف (حتى وإن كان “Unknown”)، والصورة الممسوحة مع النص القابل للتحديد.

## أسئلة شائعة وحالات خاصة

### ماذا لو لم تكن لغة OCR هي الإنجليزية؟

يدعم Aspose.OCR أكثر من 70 لغة. فقط عيّن خاصية `Language` قبل استدعاء `Recognize`:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

### كيف أتعامل مع الكتب متعددة الصفحات؟

ضع منطق التحميل/التعرف داخل حلقة `foreach`:

```csharp
string[] pages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
foreach (var pagePath in pages)
{
    ocrEngine.Image = ImageStream.FromFile(pagePath);
    ocrEngine.Recognize();
}
ocrEngine.ExportToEpub("YOUR_DIRECTORY/full_book.epub", epubExportOptions);
```

كل تكرار يضيف النص المعترف به حديثًا إلى نفس ePub، مع الحفاظ على ترتيب الصفحات.

### هل يمكنني استبعاد الصور الأصلية؟

بالتأكيد – عيّن `IncludeImages = false` في `EpubExportOptions`. سيصبح ePub الناتج نصًا قابلًا لإعادة التدفق فقط، مما يقلل حجم الملف بشكل كبير.

### ماذا عن الخطوط أو الأنماط المخصصة؟

يتيح مُصدر ePub في Aspose.OCR لك توفير ورقة أنماط CSS عبر خاصية `Css` في `EpubExportOptions`. بهذه الطريقة يمكنك فرض عائلة خطوط معينة، ارتفاع سطر، أو هوامش محددة.

## الخلاصة

أنت الآن تعرف **how to create ePub** من صورة ممسوحة ضوئيًا باستخدام Aspose OCR في C#. غطى الدرس كل شيء من **load image for OCR**، مرورًا بـ **extract text from image**، إلى **add author to epub**، وأخيرًا **convert image to epub** باستدعاء تصدير واحد. مع عينة الكود الكاملة، يمكنك توسيع الحل لمعالجة دفعات من المكتبات، إضافة غلاف مخصص، أو دمج سير العمل في واجهة ويب API.

هل أنت مستعد للتحدي التالي؟ جرّب تحويل PDF إلى ePub، أو جرب ضبط عتبات ثقة OCR لتحسين الدقة على المسحات الضوضائية. السماء هي الحد عندما تجمع بين OCR قوي وتوليد ePub مرن.

برمجة سعيدة، واستمتع بقراءة ePub الجديد الخاص بك!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}