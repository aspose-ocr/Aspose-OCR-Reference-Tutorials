---
category: general
date: 2026-04-08
description: إنشاء PDF قابل للبحث بسرعة وتعلم كيفية ضغط صور PDF، تضمين الخطوط في PDF،
  والتعرف على النص في الصورة باستخدام C# و Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- compress pdf images
- embed fonts pdf
- image to searchable pdf
- recognize text image
language: ar
og_description: أنشئ PDF قابل للبحث بسرعة باستخدام Aspose.OCR. تعلم كيفية ضغط صور
  PDF، تضمين الخطوط في PDF، والتعرف على النص في الصورة في دليل واحد.
og_title: إنشاء ملف PDF قابل للبحث – دليل C# الكامل
tags:
- Aspose.OCR
- C#
- PDF Generation
title: إنشاء ملف PDF قابل للبحث – دليل C# الكامل لتحويل الصور إلى PDF
url: /ar/net/text-recognition/create-searchable-pdf-complete-c-guide-for-image-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث – دليل C# الكامل

هل تحتاج إلى **إنشاء PDF قابل للبحث** من صورة ممسوحة ضوئياً؟ لست الوحيد الذي حدق في صورة PNG ضخمة وتساءل كيف يمكن تحويلها إلى مستند خفيف الوزن وقابل للبحث بالنص. الخبر السار هو أنه باستخدام Aspose.OCR يمكنك القيام بذلك في بضع أسطر فقط، وستتعلم أيضاً كيفية **ضغط صور PDF**، **دمج خطوط PDF**، و**التعرف على نص الصورة** دون عناء.

في هذا الدرس سنستعرض العملية بالكامل: من تحميل الصورة، تشغيل OCR، تعديل خيارات حفظ PDF، إلى كتابة PDF قابل للبحث على القرص. في النهاية ستحصل على طريقة جاهزة للاستخدام يمكنك إدراجها في أي مشروع .NET، بالإضافة إلى مجموعة من النصائح الاحترافية للحالات الخاصة التي قد تواجهها لاحقاً.

## ما الذي ستحتاجه

- **.NET 6+** (الكود يعمل أيضاً على .NET Framework 4.7، لكننا سنستهدف .NET 6 للتركيب الحديث).  
- **Aspose.OCR for .NET** – تثبيت عبر NuGet: `Install-Package Aspose.OCR`.  
- ملف صورة (PNG، JPEG، TIFF) يحتوي على النص الذي تريد جعله قابلاً للبحث.  
- قدر بسيط من الفضول – الباقي مغطى أدناه.

> **نصيحة احترافية:** إذا كنت تخطط لمعالجة عشرات الصفحات، فكر في إعادة استخدام كائن `OcrEngine` واحد لتجنب العبء المتكرر لتحميل بيانات اللغة.

## الخطوة 1: إعداد محرك OCR – التعرف على نص الصورة

أول شيء نحتاجه هو محرك OCR يمكنه قراءة الأحرف من البت ماب المصدر. يتيح لك Aspose.OCR تحديد اللغة (English، French، إلخ) ويعيد كائن `OcrResult` يحتوي على النص الخام وبيانات الصورة.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

public static OcrResult LoadAndRecognize(string imagePath)
{
    // Initialize the OCR engine – “en” is the ISO code for English.
    var ocrEngine = new OcrEngine { Language = "en" };

    // Recognize the image and get the result.
    OcrResult result = ocrEngine.RecognizeImage(imagePath);

    // Quick sanity check – throw if nothing was detected.
    if (string.IsNullOrWhiteSpace(result.Text))
        throw new InvalidOperationException("No text was recognized in the image.");

    return result;
}
```

**لماذا هذا مهم:**  
- ضبط اللغة يحسن الدقة بشكل كبير؛ حيث يحمل المحرك القواميس الخاصة باللغة في الخلفية.  
- `OcrResult` لا يحتوي فقط على السلسلة المستخرجة بل أيضاً على البت ماب الأساسي، والذي سندمجه لاحقاً في PDF بحيث يبقى المستند بصرياً مطابقاً للمسح الأصلي.

## الخطوة 2: تكوين خيارات حفظ PDF – ضغط صور PDF ودمج الخطوط

PDF القابل للبحث هو في الأساس PDF عادي مع طبقة نصية غير مرئية فوق الصورة الممسوحة. إذا تجاهلت الضغط، قد يصبح الملف النهائي ضخماً. توفر لك فئة `PdfSaveOptions` تحكمًا دقيقًا في جودة الصورة، دمج الخطوط، وما إذا كان يجب تقليص الخطوط.

```csharp
public static PdfSaveOptions GetPdfSaveOptions()
{
    return new PdfSaveOptions
    {
        // Reduce file size by compressing the raster image.
        CompressImages = true,

        // ImageQuality ranges from 0 (worst) to 100 (best). 75 is a good balance.
        ImageQuality = 75,

        // Embedding fonts ensures the text layer looks the same on any machine.
        EmbedFonts = true,

        // Subsetting keeps only the glyphs we actually use – another size saver.
        FontSubset = true
    };
}
```

**لماذا يجب دمج خطوط PDF:**  
عند فتح PDF على نظام لا يحتوي على الخط الدقيق المستخدم في طبقة OCR، قد يظهر النص مشوّهًا. الدمج يضمن الحفاظ على المظهر البصري عبر جميع المنصات، وهو أمر حاسم للمستندات القانونية أو الأرشيفية.

## الخطوة 3: حفظ النتيجة كـ PDF قابل للبحث – من صورة إلى PDF قابل للبحث

الآن نجمع كل شيء معًا: نأخذ `OcrResult`، نطبق `PdfSaveOptions`، ونكتب الملف. تقوم طريقة `SaveAsSearchablePdf` بالعمل الشاق—إنشاء طبقة نصية مخفية تعكس ناتج OCR مع الحفاظ على الصورة الأصلية.

```csharp
public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
{
    // Step 1: Recognize the image.
    OcrResult ocrResult = LoadAndRecognize(inputImage);

    // Step 2: Prepare PDF options.
    PdfSaveOptions pdfOptions = GetPdfSaveOptions();

    // Step 3: Write the searchable PDF.
    ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);

    Console.WriteLine($"Searchable PDF created at: {outputPdf}");
}
```

### مثال كامل يعمل

فيما يلي برنامج Console مستقل يمكنك نسخه ولصقه في مشروع .NET Console جديد. يفترض أن الصورة موجودة في مجلد يسمى `YOUR_DIRECTORY` بالنسبة للملف التنفيذي.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

class Program
{
    static void Main()
    {
        string inputPath = "YOUR_DIRECTORY/input.png";
        string outputPath = "YOUR_DIRECTORY/output.pdf";

        try
        {
            CreateCompressedSearchablePdf(inputPath, outputPath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }

    // --- Methods from the previous steps -------------------------------------------------
    public static OcrResult LoadAndRecognize(string imagePath)
    {
        var ocrEngine = new OcrEngine { Language = "en" };
        OcrResult result = ocrEngine.RecognizeImage(imagePath);
        if (string.IsNullOrWhiteSpace(result.Text))
            throw new InvalidOperationException("OCR did not detect any text.");
        return result;
    }

    public static PdfSaveOptions GetPdfSaveOptions()
    {
        return new PdfSaveOptions
        {
            CompressImages = true,
            ImageQuality = 75,
            EmbedFonts = true,
            FontSubset = true
        };
    }

    public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
    {
        OcrResult ocrResult = LoadAndRecognize(inputImage);
        PdfSaveOptions pdfOptions = GetPdfSaveOptions();
        ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);
        Console.WriteLine("Searchable PDF created.");
    }
}
```

تشغيل البرنامج سينتج ملف `output.pdf` يمكنك فتحه في Adobe Reader أو Foxit أو أي عارض PDF والبحث فوراً عن الكلمات التي كانت موجودة أصلاً فقط في الصورة.

## الخطوة 4: التحقق من النتيجة – هل يعمل البحث؟

بعد إنشاء الملف، افتحه وجرب البحث المدمج (Ctrl + F). إذا تمكنت من العثور على كلمات مثل “invoice”، “date”، أو “total”، فقد نجحت في إنشاء **PDF قابل للبحث**.  

إذا لم يُظهر البحث أي نتائج:

1. **تحقق من دقة OCR** – ربما تكون الصورة المصدر منخفضة الدقة. فكر في زيادة DPI قبل OCR (Aspose يتيح لك ضبط `Resolution` على المحرك).  
2. **تأكد من دمج الخطوط** – افتح خصائص PDF وابحث تحت *Fonts*؛ يجب أن ترى الخط المدمج مدرجًا.  
3. **افحص ضغط الصورة** – جودة `ImageQuality` منخفضة جداً قد تجعل الطبقة البصرية غير قابلة للقراءة، مما يربك بعض الأدوات اللاحقة.

## الاختلافات الشائعة والحالات الخاصة

| السيناريو | ما الذي يجب تعديله | السبب |
|----------|-------------------|-------|
| **TIFF متعدد الصفحات** | تكرار الحلقة على كل إطار، استدعاء `RecognizeImage` لكل صفحة، ثم استخدام `PdfSaveOptions` مع `AppendMode = true`. | يحافظ على كل صفحة ممسوحة كصفحة قابلة للبحث مستقلة. |
| **لغة غير إنجليزية** | تغيير `Language = "fr"` (أو رمز ISO المناسب) وتوفير قاموس مخصص إذا لزم الأمر. | يحسن التعرف على الأحرف المتحركة والرموز الخاصة باللغة. |
| **صور ضخمة جداً** | تقليل حجم البت ماب قبل OCR (`ocrEngine.Image = Image.FromFile(...).GetThumbnailImage(...)`). | يقلل استهلاك الذاكرة ويسرّع OCR دون فقدان كبير في الدقة. |
| **الحاجة إلى ثقة OCR** | الوصول إلى `ocrResult.RecognizedWords` وفحص خاصية `Confidence`. | يتيح لك وضع علامة على الكلمات ذات الثقة المنخفضة للمراجعة اليدوية. |

## نصائح الأداء

- **أعد استخدام `OcrEngine`** عند معالجة دفعة من الملفات – فهو يخزن بيانات اللغة مؤقتًا.  
- **قم بالتوازي** لخطوة التعرف باستخدام `Parallel.ForEach` إذا كنت على جهاز متعدد النوى، لكن حافظ على كتابة ملفات PDF بشكل متسلسل لتجنب تعارضات الوصول إلى الملفات.  
- **اضبط `ImageQuality`**: 85‑90 يعطي صورًا شبه غير مضغوطة، بينما 60‑70 يكفي عادةً للمستندات النصية الكثيفة.

## الخلاصة

غطينا كل ما تحتاجه **لإنشاء PDF قابل للبحث** من الصور باستخدام Aspose.OCR، بالإضافة إلى تعلم كيفية **ضغط صور PDF**، **دمج خطوط PDF**، و**التعرف على نص الصورة** بفعالية. العينة الكاملة جاهزة للإدراج في أي مشروع C#، والنصائح الإضافية ستساعدك على تعديل الحل ليتناسب مع أحمال عمل أكبر أو لغات مختلفة.

هل أنت مستعد للخطوة التالية؟ جرّب إضافة علامة مائية، دمج عدة ملفات PDF قابلة للبحث، أو دمج هذه العملية في واجهة ويب API بحيث يمكن للمستخدمين رفع المسحات والحصول فوراً على ملفات PDF قابلة للبحث. الاحتمالات لا حصر لها، ومع الأساسيات في مكانها ستجد أنه من السهل توسيع سير العمل.

برمجة سعيدة، ولتظل ملفات PDF الخاصة بك صغيرة، قابلة للبحث، ومُعروضة بشكل مثالي!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}