---
category: general
date: 2026-03-21
description: إنشاء ملف PDF قابل للبحث من الصور الممسوحة ضوئياً باستخدام C#. تعلم كيفية
  تحويل الصورة إلى PDF، استخراج النص من المسح، وإجراء التعرف الضوئي على الأحرف (OCR)
  على الصورة باستخدام Aspose OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from scan
- convert scanned document
- perform ocr on image
language: ar
og_description: إنشاء ملف PDF قابل للبحث من الصور الممسوحة ضوئياً في C#. تعلم خطوة
  بخطوة كيفية تحويل الصورة إلى PDF، استخراج النص من المسح، وإجراء OCR على الصورة.
og_title: إنشاء ملف PDF قابل للبحث من صورة في C# – دليل كامل
tags:
- OCR
- C#
- PDF
- Aspose
title: إنشاء ملف PDF قابل للبحث من صورة في C# – دليل كامل
url: /ar/net/text-recognition/create-searchable-pdf-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ملف PDF قابل للبحث من صورة في C# – دليل كامل

هل احتجت يوماً إلى **إنشاء ملفات PDF قابلة للبحث** من مجموعة من الصور الممسوحة ضوئياً؟ لست وحدك—ففرق القانونية، والمحاسبين، والمطورين يواجهون هذه المشكلة عندما يحاولون تحويل العقود الورقية إلى شيء يمكنك البحث فيه باستخدام Ctrl‑F.  

في هذا الدرس، ستكتشف كيفية **تحويل الصورة إلى PDF**، **استخراج النص من المسح**، و**إجراء OCR على الصورة** باستخدام مكتبة Aspose OCR. في النهاية، ستحصل على مقتطف C# جاهز للاستخدام ينتج ملف PDF قابل للبحث ببضع أسطر من الشيفرة فقط.

## ما يغطيه هذا الدليل

سنستعرض كل ما تحتاج إلى معرفته:

* إعداد حزمة Aspose OCR عبر NuGet.  
* تحميل صورة PNG أو JPEG ممسوحة ضوئياً إلى `OcrEngine`.  
* تحويل تلك الصورة إلى PDF قابل للبحث باستخدام استدعاء طريقة واحد.  
* حفظ النتيجة والتحقق من أن طبقة النص تعمل فعلياً.  

لا توجد إشارات غامضة إلى وثائق خارجية—كل ما تحتاجه موجود هنا. فهم أساسي لـ C# و .NET Core/Framework يكفي؛ إذا كتبت برنامج “Hello World” من قبل، فستكون بخير.

---

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | يدعم Aspose OCR كلاهما، لكن أحدث بيئة تشغيل تمنحك أداءً أفضل. |
| Visual Studio 2022 or VS Code | بيئة التطوير المتكاملة تجعل إدارة حزم NuGet وتشغيل العرض التجريبي أسهل. |
| Aspose.OCR NuGet package (`Aspose.OCR` v23.12 or later) | هذه المكتبة توفر فئة `OcrEngine` التي سنستخدمها. |
| A scanned image (`contract_scan.png` in this example) | ملف المصدر الذي تريد تحويله إلى PDF قابل للبحث. |

إذا كان أي من هذه مفقوداً، افتح الطرفية الخاصة بك وشغّل:

```bash
dotnet add package Aspose.OCR --version 23.12
```

هذا السطر الواحد يجلب كل ما تحتاجه.

---

## الخطوة 1: تهيئة محرك OCR – إنشاء نواة PDF قابل للبحث

أول شيء نفعله هو إنشاء نسخة من `OcrEngine`. فكر فيها كالعقل الذي سيقرأ البكسلات ويخرج النص.

```csharp
using System;
using System.Drawing;               // For Image handling
using Aspose.OCR;                  // Core OCR namespace
using Aspose.OCR.Output;           // PDFResult lives here

class Program
{
    static void Main()
    {
        // Step 1: Create the OCR engine
        var ocrEngine = new OcrEngine();

        // The rest of the steps follow...
```

**لماذا هذا مهم:**  
إنشاء المحرك مرة واحدة وإعادة استخدامه لعدة صور أكثر كفاءة من إنشاءه داخل حلقة. يحتفظ المحرك بموارد داخلية (مثل حزم اللغات) التي لا تريد إعادة تحميلها في كل مرة.

---

## الخطوة 2: تحميل الصورة المصدر – تحويل الصورة إلى PDF

بعد ذلك، نوجه المحرك إلى الملف الذي نريد معالجته. يدعم Aspose OCR أي `System.Drawing.Image`، لذا PNG، JPEG، BMP، وحتى TIFF تعمل.

```csharp
        // Step 2: Load the scanned image
        string inputPath = @"YOUR_DIRECTORY/contract_scan.png";
        ocrEngine.Image = Image.FromFile(inputPath);
```

**نصيحة احترافية:** إذا كانت صورتك ضخمة (أكثر من 10 MP)، فكر في تصغيرها أولاً للحفاظ على استهلاك الذاكرة معقولاً. عادةً ما تظل جودة OCR ثابتة عند 300 DPI.

```csharp
        // Optional: downscale large images (maintains aspect ratio)
        // ocrEngine.Image = ImageHelper.Resize(ocrEngine.Image, 2000, 2000);
```

---

## الخطوة 3: إجراء OCR وإنشاء PDF قابل للبحث – استخراج النص من المسح

الآن يحدث السحر. طريقة `RecognizePdf()` تقوم بشيئين في آن واحد: تجري OCR على الصورة **وتدمج** طبقة النص الناتجة داخل حاوية PDF.

```csharp
        // Step 3: Run OCR and get a searchable PDF result
        PdfResult searchablePdf = ocrEngine.RecognizePdf();
```

**ما الذي يحتويه `PdfResult`؟**  
إنه غلاف خفيف الوزن يحتفظ ببايتات PDF في الذاكرة. يمكنك بثه مباشرةً إلى استجابة في واجهة برمجة تطبيقات ويب، أو—كما سنفعل لاحقاً—حفظه على القرص.

---

## الخطوة 4: حفظ PDF على القرص – تحويل المستند الممسوح إلى PDF قابل للبحث

أخيراً، اكتب بايتات PDF إلى ملف. امتداد الملف `.pdf` يخبر أي عارض PDF أن المستند قابل للبحث.

```csharp
        // Step 4: Save the searchable PDF
        string outputPath = @"YOUR_DIRECTORY/contract_searchable.pdf";
        searchablePdf.Save(outputPath);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

شغّل البرنامج (`dotnet run`) وافتح `contract_searchable.pdf` في Adobe Reader. جرّب تحديد بعض النصوص ونسخها—سترى الطبقة المخفية تعمل.

---

## التحقق من النتيجة – هل يعمل OCR فعلاً؟

فحص سريع للمنطق يوفر عليك ساعات لاحقاً. افتح PDF، اضغط **Ctrl + F**، وابحث عن كلمة تعرف أنها موجودة في المسح الأصلي (مثال: “Agreement”). إذا وجدت البحث الكلمة، فقد نجحت في **إنشاء PDF قابل للبحث**.

إذا لم يكن النص قابلاً للتحديد، تحقق مرة أخرى من:

* جودة الصورة (المسحات الضبابية تنتج OCR ضعيف).  
* أنك استخدمت `RecognizePdf()` وليس فقط `Recognize()` (الأخيرة تُعيد نصًا عاديًا فقط).  
* أن اللغة الصحيحة مضبوطة—`ocrEngine.Language = Language.English;` يمكن أن يحسن الدقة.

---

## معالجة صفحات متعددة – تحويل مستند ممسوح يحتوي على عدة صور

غالباً ما يمتد العقد على عدة صفحات. بدلاً من معالجة كل صورة على حدة، يمكنك التكرار عبر مجلد ودمج النتائج:

```csharp
        var pdfPages = new System.Collections.Generic.List<PdfResult>();

        foreach (var file in System.IO.Directory.GetFiles(@"YOUR_DIRECTORY/Scans", "*.png"))
        {
            ocrEngine.Image = Image.FromFile(file);
            pdfPages.Add(ocrEngine.RecognizePdf());
        }

        // Merge all pages into one PDF
        var mergedPdf = PdfResult.Merge(pdfPages);
        mergedPdf.Save(@"YOUR_DIRECTORY/contract_full_searchable.pdf");
```

**لماذا الدمج؟**  
ملف PDF واحد أسهل للمشاركة والفهرسة. أداة `Merge` تعتني بدمج الصفحات مع الحفاظ على طبقة النص لكل صفحة.

---

## المشكلات الشائعة والنصائح – إجراء OCR على الصورة كمحترف

| المشكلة | الحل |
|-------|----------|
| **دقة منخفضة (أقل من 150)** | أعد أخذ عينة الصورة إلى 300 DPI قبل OCR. |
| **لغة غير صحيحة** | اضبط `ocrEngine.Language = Language.Spanish;` (أو أي لغة مدعومة). |
| **استهلاك ذاكرة كبير** | قم بتحرير كائنات `Image` بعد كل تكرار: `ocrEngine.Image.Dispose();` |
| **خطوط مفقودة في PDF** | يقوم Aspose تلقائياً بدمج الخطوط القياسية؛ للخطوط المخصصة، أضفها عبر `PdfSaveOptions`. |

---

## مثال كامل يعمل – كل الشيفرة في مكان واحد

فيما يلي البرنامج الكامل الجاهز للنسخ واللصق الذي **ينشئ PDF قابل للبحث** من صورة واحدة. لا توجد أجزاء مفقودة.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Load image (replace with your actual path)
        string inputPath = @"YOUR_DIRECTORY/contract_scan.png";
        ocrEngine.Image = Image.FromFile(inputPath);

        // Optional: improve accuracy by setting language
        // ocrEngine.Language = Language.English;

        // Perform OCR and get searchable PDF
        PdfResult searchablePdf = ocrEngine.RecognizePdf();

        // Save PDF to disk
        string outputPath = @"YOUR_DIRECTORY/contract_searchable.pdf";
        searchablePdf.Save(outputPath);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

شغّله، افتح الناتج، وقد قمت للتو **بتحويل الصورة إلى PDF** مع الحفاظ على النص القابل للبحث—بالضبط ما يتطلبه سير عمل المستندات الحديث.

---

## الخطوات التالية – توسيع خط أنابيب OCR الخاص بك

الآن بعد أن يمكنك **إنشاء PDF قابل للبحث**، فكر في هذه التحسينات:

* **معالجة دفعات** – استخدم حلقة الصفحات المتعددة أعلاه لمعالجة المجلدات بالكامل.  
* **إعدادات OCR مخصصة** – اضبط `ocrEngine.RecognizeArea` للتركيز على منطقة معينة، أو عدّل `ocrEngine.PageSegmentationMode`.  
* **التكامل مع واجهة برمجة تطبيقات ويب** – أعد بايتات PDF مباشرةً من نقطة نهاية ASP.NET Core للتحويل الفوري.  
* **معالجة لاحقة** – نفّذ تدقيق إملائي أو مرشح regex على النص المستخرج للحصول على دقة أعلى.  

كل من هذه المواضيع يتضمن بطبيعة الحال **استخراج النص من المسح** أو **إجراء OCR على الصورة**، لذا فأنت بالفعل تستخدم نفس الكلمات المفتاحية التي تحبها محركات البحث.

---

## الخاتمة

لقد غطينا كل ما تحتاجه **لإنشاء ملفات PDF قابلة للبحث** من صور ممسوحة ضوئياً باستخدام Aspose OCR في C#. من تهيئة المحرك، تحميل الصورة، إجراء OCR، إلى حفظ PDF القابل للبحث النهائي، العملية بسيطة ومتكاملة بالكامل.  

جرّبه مع عقودك، فواتيرك، أو أي مستند ممسوح. بمجرد إتقانك لهذه العملية، ستجد أنه من السهل **تحويل دفعات المستندات الممسوحة**، **استخراج النص من المسح**، و**إجراء OCR على الصورة** لأي مهمة معالجة بيانات لاحقة.  

إذا واجهت مشكلة أو كان لديك أفكار لأتمتة إضافية، اترك تعليقاً أدناه. برمجة سعيدة، واستمتع بتحويل أكوام الورق إلى أصول رقمية قابلة للبحث!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}