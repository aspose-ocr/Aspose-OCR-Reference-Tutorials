---
category: general
date: 2026-04-06
description: تعلم كيفية إجراء التعرف الضوئي على الأحرف (OCR) على ملفات الصور، استخراج
  النص من ملفات TIF، تحميل الصورة للتعرف الضوئي على الأحرف وتحويل النتيجة إلى ملف
  EPUB باستخدام Aspose OCR في C#.
draft: false
keywords:
- perform OCR on image
- convert image to EPUB
- how to generate EPUB
- extract text from TIF
- load image for OCR
language: ar
og_description: قم بتنفيذ التعرف الضوئي على الأحرف (OCR) على صورة باستخدام C#، استخراج
  النص من ملف TIF، تحميل الصورة للتعرف الضوئي على الأحرف وتحويل النتيجة إلى ملف EPUB.
  دليل خطوة بخطوة مع الكود الكامل.
og_title: إجراء التعرف الضوئي على الحروف في الصورة → EPUB – دليل C# الكامل
tags:
- C#
- Aspose OCR
- EPUB conversion
- Image processing
title: تنفيذ التعرف الضوئي على الأحرف في الصورة وتحويلها إلى EPUB – دليل C# الكامل
url: /ar/net/text-recognition/perform-ocr-on-image-and-convert-to-epub-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء OCR على الصورة وتحويلها إلى EPUB – دليل C# كامل

هل احتجت يومًا إلى **إجراء OCR على صورة** ولكنك لم تكن متأكدًا من كيفية الحصول على النص بصيغة كتاب إلكتروني قابل للقراءة؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يكون لديهم صفحة ممسوحة ضوئيًا (غالبًا ملف .TIF) ويرغبون في تحويلها إلى EPUB نظيف دون الحاجة إلى النسخ واللصق يدويًا.  

في هذا الدليل سنستعرض كامل سير العمل: **تحميل الصورة للـ OCR**، استخراج النص، وأخيرًا **تحويل الصورة إلى EPUB** باستخدام مكتبة Aspose OCR. في النهاية ستحصل على برنامج مستقل يمكنه أخذ صفحة ممسوحة وإنتاج ملف EPUB منظم تمامًا—دون الحاجة إلى أدوات إضافية.

## ما ستتعلمه

- كيفية **تحميل الصورة للـ OCR** في C# (مع معالجة ملفات TIF الكبيرة).  
- الخطوات الدقيقة **لإجراء OCR على صورة** باستخدام Aspose OCR ولماذا كل استدعاء مهم.  
- تقنيات **استخراج النص من TIF** وتنظيفه للنشر ككتاب إلكتروني.  
- أبسط طريقة **لتحويل الصورة إلى EPUB** وما الخيارات المتاحة للتخصيص.  
- الأخطاء الشائعة—مثل الضغط على الذاكرة في المسحات الكبيرة—والحلول السريعة.

### المتطلبات المسبقة

| المتطلبات | لماذا يهم |
|-------------|----------------|
| .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.8) | يوفر بيئة تشغيل لصياغة C# 10 المستخدمة أدناه. |
| حزمة NuGet Aspose.OCR (`Aspose.OCR` و `Aspose.OCR.Export`) | المحرك الذي يتعرف فعليًا على الأحرف ويكتب ملف EPUB. |
| صورة TIF (`book_page.tif`) تريد معالجتها | مثالنا يستخدم مسحًا بصفحة واحدة، لكن المنطق نفسه يعمل مع ملفات TIFF متعددة الصفحات. |
| Visual Studio 2022 (أو أي بيئة تطوير تفضلها) | يجعل عملية تصحيح الأخطاء وإدارة الحزم سهلة وسلسة. |

إذا كان لديك كل ذلك، احضر فنجانًا من القهوة ولنغص في الموضوع.

![مخطط سير العمل يوضح كيفية إجراء OCR على الصورة، استخراج النص، وإنشاء ملف EPUB](perform-ocr-on-image-workflow.png "سير عمل إجراء OCR على الصورة")

## الخطوة 1: تحميل الصورة للـ OCR

قبل أن يتمكن المحرك من التعرف على أي شيء، يحتاج إلى كائن `System.Drawing.Image` صالح. طريقة `Image.FromFile` تعمل لمعظم صيغ الرسوم النقطية، لكن مع TIF قد تواجه مشاكل الإطارات المتعددة. وضع الاستدعاء داخل كتلة `using` يضمن تحرير مقبض الملف بسرعة—وهو أمر مهم عندما تعالج عشرات الصفحات في دفعة واحدة.

```csharp
using System.Drawing;

// Path to your source scan – change this to your actual file location
string sourcePath = @"C:\Scans\book_page.tif";

// Load the image safely
using (Image sourceImage = Image.FromFile(sourcePath))
{
    // The image is now ready for OCR
    // (We’ll hand it off to the engine in the next step)
}
```

**لماذا يهم ذلك:**  
- **أمان الذاكرة:** `using` يضمن التخلص من موارد GDI+، مما يمنع التسريبات التي قد تتسبب في تعطل الخدمات طويلة التشغيل.  
- **مرونة الصيغ:** `Image.FromFile` يكتشف تلقائيًا TIFF، PNG، JPEG، إلخ، لذا لا تحتاج إلى محملات منفصلة لكل نوع ملف.

> **نصيحة احترافية:** إذا صادفت أخطاء “الوسيط غير صالح” على بعض ملفات TIFF، فكر في استخدام `Image.FromStream` مع `FileStream` مفتوح بوضع القراءة فقط. هذا يتجاوز بعض عيوب GDI+.

## الخطوة 2: إجراء OCR على الصورة

الآن بعد أن أصبحت الصورة في الذاكرة، نقوم بإنشاء محرك Aspose OCR. فئة `OcrEngine` خفيفة؛ يمكنك إعادة استخدام نسخة واحدة لعدة صفحات، مما يقلل الحمل.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

// Create the OCR engine – you can pass a license object here if you have one
OcrEngine ocrEngine = new OcrEngine();

// Inside the using block from Step 1
using (Image sourceImage = Image.FromFile(sourcePath))
{
    // Run the recognition process
    OcrResult ocrResult = ocrEngine.Recognize(sourceImage);

    // The Result property holds the extracted plain text
    string extractedText = ocrResult.Text;

    // Optional: Write the raw text to console for quick verification
    Console.WriteLine("=== Extracted Text ===");
    Console.WriteLine(extractedText);
}
```

**لماذا يهم ذلك:**  
- `Recognize` يقوم بكل الأعمال الثقيلة (التنقيط، تحليل التخطيط، تصنيف الأحرف).  
- النتيجة `OcrResult` تُعيد لك النص العادي، وإذا لزم الأمر، إحداثيات كل كلمة—مفيد للمعالجة اللاحقة.

### حالات خاصة وتعديلات

| الحالة | التعديل المقترح |
|-----------|-----------------|
| مسحات منخفضة التباين | عيّن `ocrEngine.Settings.ImagePreprocessing` إلى `ImagePreprocessingMode.Auto` للحصول على تنقيط أفضل. |
| مستندات متعددة اللغات | استخدم `ocrEngine.Settings.Language = Language.English | Language.French;` لتمكين خلط اللغات. |
| ملف TIFF ضخم (> 200 MB) | عالج الصفحة بصفحة باستخدام `Image.GetFrameCount` و `SelectActiveFrame` للحفاظ على استهلاك الذاكرة منخفضًا. |

## الخطوة 3: تحويل الصورة إلى EPUB

مع النص الخام في يدك، الخطوة التالية هي تجميعه في ملف EPUB. Aspose OCR يأتي بمساعد `EpupExport` مريح (نعم، المكتبة تكتب “Epup”، لكن الناتج هو ملف `.epub` قياسي). يمكنك تمرير `OcrResult` مباشرة؛ المكتبة ستنشئ EPUB بفصل واحد يحتوي على النص المعترف به.

```csharp
// Destination path for the EPUB file
string epubPath = @"C:\Outputs\book_page.epub";

// Inside the same using block after OCR
using (Image sourceImage = Image.FromFile(sourcePath))
{
    OcrResult ocrResult = ocrEngine.Recognize(sourceImage);

    // Export to EPUB – this writes the file to disk
    EpupExport.ToEpup(ocrResult, epubPath);

    Console.WriteLine($"EPUB created at: {epubPath}");
}
```

**لماذا يهم ذلك:**  
- المساعد يتولى تعبئة حزمة EPUB (المانيفست، السّبين، البيانات الوصفية) بحيث لا تحتاج إلى بناء بنية XML يدويًا.  
- يحافظ على ترتيب القراءة الأصلي الذي اكتشفه محرك OCR، مما يعني أن العناوين والفقرات تبقى بالترتيب الصحيح.

### تخصيص EPUB

إذا كنت تحتاج إلى صورة غلاف، بيانات وصفية مخصصة، أو فصول متعددة، يمكنك بناء `EpubDocument` يدويًا:

```csharp
using Aspose.OCR.Export.Epub;

// Create a new EPUB document
EpubDocument epubDoc = new EpubDocument();

// Add a title metadata entry
epubDoc.Metadata.Title = "Scanned Book – Chapter 1";

// Optionally add a cover (must be a JPEG or PNG)
epubDoc.CoverImage = Image.FromFile(@"C:\Assets\cover.jpg");

// Insert the OCR text as a chapter
epubDoc.AddChapter("Chapter 1", ocrResult.Text);

// Save the custom EPUB
epubDoc.Save(epubPath);
```

> **ملاحظة:** استدعاء `EpupExport.ToEpup` البسيط مثالي للسكربتات السريعة، بينما يبرز النهج اليدوي عندما تحتاج إلى تحكم كامل.

## الخطوة 4: التحقق من النتيجة

فحص سريع يوفر ساعات من التصحيح لاحقًا. افتح ملف `.epub` المُولد في أي قارئ (Calibre، Adobe Digital Editions، أو حتى متصفح ويب) وتأكد من وجود:

1. تدفق نص صحيح—بدون كلمات مفقودة.  
2. عنوان الفصل صحيح (إذا قمت بتعيين البيانات الوصفية).  
3. ظهور صورة الغلاف إذا تم إضافتها.

إذا لاحظت أحرفًا مشوهة، عد إلى **الخطوة 2** وجرب تعديل `Settings` للمحرك (مثلاً، فعّل اكتشاف `Language` أو اضبط `Resolution`).

```csharp
// Quick verification snippet
if (File.Exists(epubPath))
{
    Console.WriteLine("✅ EPUB file exists and is ready for reading.");
}
else
{
    Console.WriteLine("❌ Something went wrong – the EPUB wasn't created.");
}
```

## مثال عملي كامل

فيما يلي البرنامج الكامل الجاهز للتنفيذ الذي يجمع كل شيء معًا. الصقه في مشروع Console جديد، استعد حزم NuGet الخاصة بـ Aspose OCR، ثم اضغط **F5**.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Export;
using Aspose.OCR.Export.Epub;   // Only needed for custom EPUB handling

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // Configuration – adjust these paths for your environment
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Scans\book_page.tif";
        string epubPath   = @"C:\Outputs\book_page.epub";

        // -----------------------------------------------------------------
        // Step 1: Load image for OCR (handles TIFF, JPEG, PNG, etc.)
        // -----------------------------------------------------------------
        using (Image sourceImage = Image.FromFile(sourcePath))
        {
            // -----------------------------------------------------------------
            // Step 2: Perform OCR on image
            // -----------------------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // Optional: tweak settings for low‑quality scans
            // ocrEngine.Settings.ImagePreprocessing = ImagePreprocessingMode.Auto;
            // ocrEngine.Settings.Language = Language.English;

            OcrResult ocrResult = ocrEngine.Recognize(sourceImage);

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);

            // -----------------------------------------------------------------
            // Step 3: Convert image to EPUB (simple one‑chapter book)
            // -----------------------------------------------------------------
            EpupExport.ToEpup(ocrResult, epubPath);

            // For a richer EPUB, uncomment the block below:
            /*
            EpubDocument epubDoc = new EpubDocument();
            epubDoc.Metadata.Title = "Scanned Book – Chapter 1";
            epubDoc.AddChapter("Chapter 1", ocrResult.Text);
            // epubDoc.CoverImage = Image.FromFile(@"C:\Assets\cover.jpg");
            epubDoc.Save(epubPath);
            */

            // -----------------------------------------------------------------
            // Step 4: Verify output
            // -----------------------------------------------------------------
            if (System.IO.File.Exists(epubPath))
                Console.WriteLine($"✅ EPUB created successfully at: {epubPath}");
            else
                Console.WriteLine("❌ EPUB creation failed.");
        }
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج يطبع النص المعترف به في وحدة التحكم وينشئ ملف `book_page.epub`. فتح ملف EPUB يظهر فصلًا واحدًا يحتوي على النص نفسه الذي ظهر في مخرجات وحدة التحكم. لا حاجة للنسخ واللصق يدويًا.

## الخلاصة

غطينا كل ما تحتاجه **لإجراء OCR على صورة**، **استخراج النص من TIF**، و**تحويل الصورة إلى EPUB** باستخدام Aspose OCR في C#. سير العمل بسيط:

1. **تحميل الصورة للـ OCR** باستخدام كتلة `using` الآمنة.  
2. **إجراء OCR على الصورة** عبر `OcrEngine.Recognize`.  
3. **تحويل النتيجة إلى EPUB** باستخدام `EpupExport.ToEpup` (أو `EpubDocument` مخصص).  
4. **التحقق** من النتيجة وتعديل الإعدادات إذا لزم الأمر.

من هنا يمكنك توسيع الحل لمعالجة دفعات من الكتب بالكامل، إضافة غلاف، دمج خطوط، أو حتى دمجه في واجهة برمجة تطبيقات ويب. جميع اللبنات الأساسية موجودة الآن، ولديك مرجع موثوق يمكنك الإشارة إليه للمساعدات الذكية.

**ما التالي؟** جرّب إضافة حلقة تمر عبر مجلد من ملفات TIFF، تجمع نتائج OCR في فصول EPUB متعددة، أو تجربة

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}