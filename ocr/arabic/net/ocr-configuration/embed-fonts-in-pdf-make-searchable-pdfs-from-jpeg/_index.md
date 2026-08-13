---
category: general
date: 2026-03-05
description: تضمين الخطوط في ملف PDF أثناء تحويل صورة JPEG إلى PDF قابل للبحث باستخدام
  Aspose OCR. تعلّم كيفية التعرف على النص من JPEG وتضمين الخطوط للامتثال لمعيار PDF/A‑2b.
draft: false
keywords:
- embed fonts in pdf
- recognize text from jpeg
- how to create searchable pdf
- convert image to searchable pdf
- perform ocr on image
language: ar
og_description: تضمين الخطوط في ملف PDF أثناء تحويل صورة JPEG إلى PDF قابل للبحث.
  يوضح هذا الدليل خطوة بخطوة كيفية التعرف على النص من JPEG وإنشاء ملفات متوافقة مع
  معيار PDF/A‑2b.
og_title: تضمين الخطوط في PDF – إنشاء ملفات PDF قابلة للبحث من JPEG
tags:
- Aspose OCR
- PDF generation
- C#
- .NET
title: تضمين الخطوط في PDF – إنشاء ملفات PDF قابلة للبحث من JPEG
url: /ar/net/ocr-configuration/embed-fonts-in-pdf-make-searchable-pdfs-from-jpeg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تضمين الخطوط في PDF – إنشاء ملفات PDF قابلة للبحث من JPEG

هل احتجت يومًا إلى **embed fonts in PDF** للملفات التي تم إنشاؤها من صور ممسوحة ضوئيًا؟ لست وحدك. يواجه معظم المطورين المشكلة حيث يبدو ملف PDF الناتج جيدًا على جهازهم ولكنه يظهر نصًا مفقودًا عند فتحه في مكان آخر لأن الخطوط لم تُضمّن.  

الخبر السار؟ مع Aspose OCR يمكنك **recognize text from JPEG**، تضمين الخطوط اللازمة، وإنتاج مستند PDF/A‑2b قابل للبحث بالكامل في بضع أسطر فقط من C#. في هذا الدرس سنستعرض كل خطوة — لماذا كل إعداد مهم، كيف نتجنب المشكلات الشائعة، وما الشكل المتوقع للملف PDF النهائي.

بنهاية هذا الدليل ستكون قادرًا على **convert image to searchable PDF**، تضمين الخطوط بشكل صحيح، وفهم كيفية **perform OCR on image** للملفات برمجيًا.

---

## ما ستحتاجه

- **Aspose.OCR for .NET** (الإصدار الأخير، مثال: 23.10) – المكتبة التي تقوم بالعمل الشاق.
- ملف ترخيص **Aspose OCR** صالح (`Aspose.OCR.lic`). النسخة التجريبية المجانية تعمل، لكن النسخة المرخصة تزيل العلامات المائية للتقييم.
- صورة JPEG (`input.jpg`) تحتوي على نص مطبوع أو مكتوب.
- بيئة تطوير .NET (Visual Studio، Rider، أو VS Code مع إضافة C#).

لا توجد حزم NuGet إضافية مطلوبة؛ محرك OCR يضم بالفعل أدوات إنشاء PDF.

## الخطوة 1: إعداد محرك OCR وتطبيق الترخيص *(Embed Fonts in PDF)*

قبل أن تتمكن من تشغيل أي عملية التعرف، يجب إنشاء مثيل `OcrEngine` وإبلاغه بالترخيص الذي سيستخدمه. تخطي خطوة الترخيص سيجعل المحرك يعمل في وضع التقييم، مما يضيف تراكبًا “Powered by Aspose” على كل صفحة.

```csharp
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;
using Aspose.OCR.Saving;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Apply your license – replace the path with the actual location of your .lic file
ocrEngine.SetLicense("Aspose.OCR.lic");
```

**Why this matters:** الترخيص لا يزيل العلامات المائية فحسب، بل يفتح أيضًا خيارات التوافق مع PDF/A التي سنحتاجها لاحقًا لتضمين الخطوط.

## الخطوة 2: تحميل صورة JPEG التي تريد معالجتها *(Recognize Text from JPEG)*

يعمل محرك OCR مع خاصية `Image` التي تقبل `ImageStream`. وجهها إلى صورة JPEG التي ترغب في تحويلها.

```csharp
// Load the source JPEG image
ocrEngine.Image = ImageStream.FromFile(@"C:\MyImages\input.jpg");
```

**Tip:** إذا كانت صورتك موجودة في تدفق (مثلاً تم تحميلها عبر API)، يمكنك استخدام `ImageStream.FromStream(yourStream)` بدلاً من `FromFile`.

## الخطوة 3: تكوين خيارات حفظ PDF لإنشاء PDF قابل للبحث

هذا هو جوهر متطلب “embed fonts in PDF”. سنستخدم `PdfSaveOptions` لـ:

1. استهداف **PDF/A‑2b** (معيار أرشيفي مقبول على نطاق واسع).
2. **Embed all used fonts** بحيث يُظهر PDF بنفس الشكل في كل مكان.
3. تطبيق **lossless Flate compression** للحفاظ على حجم الملف معقولًا.
4. الاحتفاظ بصورة JPEG الأصلية كطبقة خلفية، مما يحافظ على الدقة البصرية.

```csharp
// Set up PDF export options
var pdfSaveOptions = new PdfSaveOptions
{
    // Produce a PDF/A‑2b compliant document
    PdfAStandard = PdfAStandard.PdfA2b,

    // Ensure every font used by the OCR text is embedded
    EmbedFonts = true,

    // Use lossless compression for the text and graphics streams
    Compression = PdfCompression.Flate,

    // Keep the original image behind the OCR layer (makes the PDF searchable)
    RenderOriginalImage = true
};
```

**لماذا هذه الإعدادات؟**  
- **PdfAStandard.PdfA2b** يضمن الحفظ طويل الأمد ويفرض تضمين الخطوط.  
- **EmbedFonts = true** هو العلامة الصريحة التي تلبي هدف الكلمة المفتاحية الأساسي.  
- **Compression.Flate** يقلل الحجم دون التضحية بالجودة.  
- **RenderOriginalImage** يحافظ على المظهر البصري للصفحة الممسوحة بينما توفر طبقة OCR المخفية نصًا قابلًا للبحث.

## الخطوة 4: تشغيل التعرف الضوئي على الصورة *(Perform OCR on Image)*

مع إعداد كل شيء، قم بتشغيل عملية التعرف. سيقوم المحرك بتحليل صورة JPEG، استخراج الأحرف، وإنشاء طبقة نص داخلية.

```csharp
// Execute OCR – this populates the internal text layer
ocrEngine.Recognize();
```

**سؤال شائع:** *هل أحتاج إلى تحديد اللغة أو القاموس؟*  
إذا لم يكن مستندك باللغة الإنجليزية، قم بتعيين `ocrEngine.Language = OcrLanguage.French;` (أو أي لغة مدعومة) قبل استدعاء `Recognize()`. الافتراضي هو الإنجليزية.

## الخطوة 5: حفظ الناتج كملف PDF قابل للبحث مع تضمين الخطوط

أخيرًا، احفظ النتيجة على القرص. طريقة `Save` تأخذ مسار الهدف و`PdfSaveOptions` التي عرّفناها سابقًا.

```csharp
// Save the searchable PDF with embedded fonts
ocrEngine.Save(@"C:\MyImages\output.pdf", pdfSaveOptions);
```

عند فتح `output.pdf` في Adobe Acrobat أو أي عارض PDF، يجب أن تكون قادرًا على:

- **Search** لأي كلمة ظهرت في JPEG الأصلي.
- رؤية **no missing font warnings** (بفضل `EmbedFonts = true`).
- التحقق من أن الملف يتوافق مع **PDF/A‑2b** (ملف → خصائص → PDF/A).

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه والصقه في مشروع تطبيق Console جديد، عدل مسارات الملفات، واضغط **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;
using Aspose.OCR.Saving;

namespace ImageToSearchablePdf
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine and apply license
            var ocrEngine = new OcrEngine();
            ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

            // 2️⃣ Load JPEG image
            ocrEngine.Image = ImageStream.FromFile(@"C:\MyImages\input.jpg");

            // 3️⃣ Configure PDF save options (embed fonts, PDF/A‑2b, etc.)
            var pdfSaveOptions = new PdfSaveOptions
            {
                PdfAStandard = PdfAStandard.PdfA2b,
                EmbedFonts = true,
                Compression = PdfCompression.Flate,
                RenderOriginalImage = true
            };

            // 4️⃣ Run OCR recognition
            ocrEngine.Recognize();

            // 5️⃣ Save searchable PDF with embedded fonts
            string outputPath = @"C:\MyImages\output.pdf";
            ocrEngine.Save(outputPath, pdfSaveOptions);

            Console.WriteLine($"✅ PDF created at: {outputPath}");
            Console.WriteLine("Open it in any PDF viewer and try searching for words from the original JPEG.");
        }
    }
}
```

**الناتج المتوقع:**  
يطبع وحدة التحكم رسالة نجاح، وتظهر `output.pdf` في المجلد المستهدف. فتح الـ PDF واستخدام مربع البحث في العارض يجب أن يجد أي كلمة كانت موجودة في `input.jpg`.

## الأسئلة المتكررة وحالات الحافة

### 1. “ماذا لو كان JPEG الخاص بي ملف TIFF متعدد الصفحات؟”

يتعامل Aspose OCR مع كل صفحة على حدة. قم بتحويل TIFF إلى سلسلة من ملفات JPEG (أو استخدم `ImageStream.FromFile` على كل صفحة) وكرر عملية OCR، مع إلحاق كل نتيجة إلى نفس PDF باستخدام نفس مثيل `OcrEngine`.

### 2. “هل يمكنني التحكم في DPI أو معالجة الصورة المسبقة؟”

نعم. قبل استدعاء `Recognize()`, يمكنك تعديل دقة الصورة:

```csharp
ocrEngine.Image.DpiX = 300;
ocrEngine.Image.DpiY = 300;
ocrEngine.Image.AutoRotate = true; // auto‑rotate for landscape scans
```

عادةً ما يؤدي DPI أعلى إلى دقة تعرّف أفضل، خاصةً للخطوط الصغيرة.

### 3. “ما زال PDF يظهر خطوطًا مفقودة في Adobe Reader—ما المشكلة؟”

تأكد من أنك تستهدف **PDF/A‑2b** وأن `EmbedFonts` مضبوط على `true`. إذا قمت بتغيير `PdfAStandard` يدويًا إلى `None`, يتم تخطي خطوة التحقق من PDF/A، وقد تظل بعض الخطوط غير مضمنة.

### 4. “هل طبقة OCR قابلة للبحث على الأجهزة المحمولة؟”

بالطبع. طبقة النص المخفية هي جزء من مواصفات PDF، لذا أي عارض PDF يدعم استخراج النص (بما في ذلك iOS Files، Android PDF Viewer، إلخ) سيسمح للمستخدمين بالبحث.

### 5. “كيف أتعامل مع اللغات من اليمين إلى اليسار مثل العربية؟”

قم بتعيين اللغة قبل التعرف:

```csharp
ocrEngine.Language = OcrLanguage.Arabic;
ocrEngine.Recognize();
```

يقوم Aspose OCR تلقائيًا بتبديل اتجاه النص وتضمين الخطوط المناسبة عندما تكون `EmbedFonts` true.

## نصائح احترافية ومخاطر شائعة

- **Pro tip:** إذا كانت صورك المصدرية صورًا ملونة، فكر في تحويلها إلى تدرج الرمادي أولاً (`ocrEngine.Image.ConvertToGrayscale();`). هذا يقلل حجم الملف دون الإضرار بدقة OCR.
- **Watch out for:** استخدام ترخيص التجربة المجانية مع صورة **كبيرة** قد يتسبب في قطع نص OCR. قم بالترقية إلى ترخيص كامل لأعباء العمل الإنتاجية.
- **Performance tip:** إعادة استخدام نفس مثيل `OcrEngine` عبر صور متعددة يتجنب العبء الزائد لتحميل مكتبات OCR DLLs مرارًا.
- **Security note:** ملفات PDF/A‑2b هي **للقراءة فقط** حسب التصميم، مما يساعد على منع حقن السكريبتات عن طريق الخطأ—ميزة إضافية للبيئات التي تتطلب امتثالًا عاليًا.

## الخلاصة

لقد غطينا كامل سير العمل لـ **embed fonts in PDF** مع **recognize text from JPEG** وإنتاج **searchable PDF** يتوافق مع معايير PDF/A‑2b. العملية تختصر إلى:

1. تهيئة `OcrEngine` وتطبيق الترخيص الخاص بك.  
2. تحميل صورة JPEG.  
3. تكوين `PdfSaveOptions` (تضمين الخطوط، PDF/A‑2b، الضغط).  
4. تشغيل `Recognize()`.  
5. حفظ باستخدام الخيارات المكوّنة.

الآن يمكنك دمج هذا التدفق في خدمات الويب، أدوات سطح المكتب، أو وظائف الدُفعات التي تحتاج إلى **convert image to searchable PDF** مباشرة. الخطوة التالية قد تستكشف **how to create searchable PDF** من ملفات PDF متعددة الصفحات أو PDFs مُولدة

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}