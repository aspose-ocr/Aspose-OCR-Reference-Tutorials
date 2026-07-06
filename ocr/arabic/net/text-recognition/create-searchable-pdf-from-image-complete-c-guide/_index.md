---
category: general
date: 2026-02-13
description: إنشاء ملف PDF قابل للبحث من صورة باستخدام Aspose.OCR. تعلم كيفية تحويل
  الصورة إلى PDF، استخراج النص من الصورة، تضمين الخطوط في PDF، والتعرف على النص من
  PNG.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- embed fonts in pdf
- recognize text from png
language: ar
og_description: إنشاء ملف PDF قابل للبحث من صورة باستخدام Aspose.OCR. يوضح هذا الدليل
  كيفية تحويل الصورة إلى PDF، وتضمين الخطوط، واستخراج النص من PNG بسهولة.
og_title: إنشاء ملف PDF قابل للبحث من صورة – دليل C# خطوة بخطوة
tags:
- C#
- OCR
- Aspose
- PDF generation
title: إنشاء ملف PDF قابل للبحث من صورة – دليل C# الكامل
url: /ar/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث من صورة – دليل C# الكامل

هل احتجت يوماً إلى **إنشاء PDF قابل للبحث** من صورة PNG ممسوحة ضوئياً لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك. في العديد من المشاريع—مثل رقمنة الفواتير أو أرشفة الأدلة القديمة—تحويل الصورة إلى PDF يمكنك البحث فيه يُعدّ خطوة حاسمة.  

في هذا الدرس سنستعرض الخطوات الدقيقة **لتحويل الصورة إلى PDF**، **استخراج النص من الصورة**، تضمين الخطوط اللازمة، وأخيرًا الحصول على ملف PDF قابل للبحث بالكامل. لا إشارات غامضة، مجرد مثال كامل قابل للتنفيذ يمكنك نسخه‑ولصقه في Visual Studio اليوم.

> **ما ستحصل عليه:** تطبيق C# Console يقرأ `input.png`، يُجري OCR، يضمّن الخطوط، يحتفظ بالصورة النقطية الأصلية كخلفية، ويكتب `output.pdf`. بنهاية الدرس ستفهم *لماذا* كل سطر مهم وكيفية تعديلها لتناسب سيناريوهاتك الخاصة.

---

## المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (الكود يعمل أيضاً مع .NET Framework 4.7+).  
- Aspose.OCR for .NET – يمكنك الحصول عليه من NuGet (`Install-Package Aspose.OCR`).  
- صورة PNG تجريبية (`input.png`) موجودة في مجلد تتحكم به.  
- إلمام أساسي بمشاريع C# Console (إذا لم تقم بإنشاء واحد من قبل، افتح Visual Studio → **Create a new project** → **Console App** → **C#**).

> **نصيحة:** Aspose يقدم ترخيص تجريبي مجاني؛ فقط ضع ملف `.lic` بجوار الملف التنفيذي وستعمل المكتبة بدون علامات مائية.

---

## الخطوة 1: إعداد محرك OCR – التعرف على النص من PNG

أول شيء نحتاجه هو محرك OCR يستطيع فعلاً قراءة الأحرف في ملف PNG. Aspose.OCR يجعل ذلك بسيطًا.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

// Initialize the OCR engine with English language support
OcrEngine ocrEngine = new OcrEngine
{
    // Primary language – you can add more if needed
    Language = OcrLanguage.English
};
```

**لماذا هذا مهم:**  
تحديد `Language` يخبر المحرك بمجموعة الأحرف المتوقعة. إذا تخطيت ذلك، سيستخدم المحرك الوضع العام الذي قد يخطئ في تفسير الأحرف ذات اللكنات أو الأرقام. للوثائق متعددة اللغات، يمكنك تمرير قائمة مفصولة بفواصل مثل `OcrLanguage.English | OcrLanguage.French`.

---

## الخطوة 2: تحميل الصورة والتعرف عليها – استخراج النص من الصورة

الآن بعد أن أصبح المحرك جاهزًا، نمرره إلى ملف PNG الذي نريد معالجته.

```csharp
// Path to the source image; adjust as needed
string inputPath = @"YOUR_DIRECTORY/input.png";

// Perform OCR – this populates the engine's internal text representation
ocrEngine.RecognizeImage(inputPath);
```

**ما الذي يحدث في الخلفية؟**  
`RecognizeImage` يمسح البت ماب، يحدد كتل النص، ويخزن النتيجة في `ocrEngine`. يمكنك لاحقًا الوصول إلى `ocrEngine.Text` إذا كنت تحتاج فقط إلى السلسلة الخام، لكن لإنشاء PDF قابل للبحث سنترك Aspose يتولى التحويل مباشرة.

> **حالة خاصة:** إذا كانت صورة PNG ضخمة (أكبر من 10 ميغابايت) قد تواجه نفاد الذاكرة. في هذه الحالة، فكر في تصغير الصورة أولاً أو استخدام `OcrEngine.RecognizeImage(Stream)` لبث البيانات.

---

## الخطوة 3: تكوين خيارات تصدير PDF – تضمين الخطوط في PDF

PDF قابل للبحث لا فائدة منه إذا لم تُضمّن الخطوط؛ سيتعرض المستند للتشويه على الأجهزة التي لا تملك الخطوط المطلوبة. Aspose يتيح لنا التحكم في ذلك عبر كائن خيارات بسيط.

```csharp
// Define how the searchable PDF should be built
SearchablePdfOptions pdfOptions = new SearchablePdfOptions
{
    // Guarantees the PDF renders correctly everywhere
    EmbedFonts = true,

    // Keeps the original raster image as a visual background
    KeepOriginalImage = true
};
```

**لماذا نضمّن الخطوط؟**  
عند ضبط `EmbedFonts` إلى `true`، يحمل PDF بيانات الخط داخل الملف. هذا يضمن أن أي عارض—Chrome، Adobe Reader، أو تطبيق هاتف محمول—يعرض النص كما هو مقصود، حتى إذا كان النظام المستهدف يفتقر إلى الخط.

**متى قد تضبط `KeepOriginalImage` إلى `false`؟**  
إذا كنت تحتاج فقط إلى النص المستخرج وتريد ملفًا أصغر، إيقاف هذه الخاصية يزيل الصورة الخلفية، مما ينتج PDF “نص‑فقط” نظيف.

---

## الخطوة 4: تصدير إلى PDF قابل للبحث – تحويل الصورة إلى PDF

مع نتائج OCR وخيارات PDF جاهزة، الخطوة الأخيرة هي سطر واحد يكتب PDF القابل للبحث إلى القرص.

```csharp
// Destination path for the generated PDF
string outputPath = @"YOUR_DIRECTORY/output.pdf";

// Export the OCR result as a searchable PDF
ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created.");
```

**ما الذي ستلاحظه:**  
عند فتح `output.pdf` في أي عارض، يمكنك تحديد النص، نسخه، وحتى إجراء بحث (`Ctrl + F`) لتحديد الكلمات التي كانت في الأصل بكسلات فقط داخل PNG.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك تجميعه وتشغيله فورًا. استبدل `YOUR_DIRECTORY` بالمجلد الذي يحتوي على `input.png`.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine – set language to English
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Recognize text from the PNG image
        string inputPath = @"YOUR_DIRECTORY/input.png";
        ocrEngine.RecognizeImage(inputPath);

        // 3️⃣ Prepare PDF options – embed fonts & keep raster background
        SearchablePdfOptions pdfOptions = new SearchablePdfOptions
        {
            EmbedFonts = true,
            KeepOriginalImage = true
        };

        // 4️⃣ Export to a searchable PDF file
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

        // 5️⃣ Notify the user
        Console.WriteLine("Searchable PDF created.");
    }
}
```

**الناتج المتوقع على وحدة التحكم:**

```
Searchable PDF created.
```

افتح `output.pdf` وجرب البحث عن كلمة تعلم أنها موجودة في `input.png`. إذا تم تمييزها، فقد نجحت في **إنشاء PDF قابل للبحث** من صورة.

---

## أسئلة شائعة ونصائح احترافية

### “هل يمكنني معالجة عدة صور في تشغيل واحد؟”

بالطبع. ضع منطق التعرف والتصدير داخل حلقة، ربما باستخدام `Directory.GetFiles(..., "*.png")`. فقط تأكد من إعطاء كل PDF اسمًا فريدًا، مثل `Path.GetFileNameWithoutExtension(img) + ".pdf"`.

### “ماذا لو كان مستندي يحتوي على نص إنجليزي وإسباني معًا؟”

اضبط خاصية اللغة إلى علم مركب:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

سيسعى Aspose بعد ذلك لاكتشاف الأحرف من كلا الأبجديتين.

### “ملف PDF كبير—كيف يمكنني تقليص حجمه؟”

حيلتان سريعتان:

1. اضبط `pdfOptions.KeepOriginalImage = false` لإزالة الخلفية النقطية.  
2. استخدم `pdfOptions.ImageCompression = ImageCompression.Jpeg;` (ستحتاج لإضافة الخاصية) لضغط الصورة المضمّنة.

### “هل أحتاج ترخيصًا للاستخدام في الإنتاج؟”

الترخيص التجريبي يكفي للاختبار، لكن للنشر التجاري يجب شراء ترخيص وتسجيله مبكرًا في تطبيقك:

```csharp
Aspose.OCR.License license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

---

## توسيع الحل

الآن بعد أن عرفت كيف **إنشاء PDF قابل للبحث**، قد ترغب في:

- **إضافة علامة مائية** – استخدم `PdfDocument` من Aspose.PDF لتراكب نص بعد OCR.  
- **معالجة دفعات من PDFs** – دمج عدة PDFs قابلة للبحث في ملف واحد باستخدام `PdfFileEditor`.  
- **التكامل مع Azure Blob Storage** – قراءة/كتابة تدفقات الصورة وPDF مباشرة من السحابة، متجنبًا I/O المحلي.

كل من هذه الإضافات يتبع نفس النمط: احصل على نتيجة OCR، اضبط المكتبة التالية، وربط العمليات.

---

## الخلاصة

لقد تعلمت الآن كيفية **إنشاء PDF قابل للبحث** من صورة PNG باستخدام Aspose.OCR في C#. من خلال تهيئة محرك OCR، التعرف على النص، تكوين `SearchablePdfOptions` لت **تضمين الخطوط في PDF**، وأخيرًا التصدير، ستحصل على ملف يطابق الأصل بصريًا ولكنه قابل للبحث بالكامل.  

من هنا، يمكنك تجربة التحويلات الدفعة، اللغات المختلفة، أو ضغط أقوى—حسب ما يناسب سير عملك. إذا واجهت أي صعوبات، فإن منتديات Aspose ووثائق API موارد قوية، لكن الخطوات الأساسية أعلاه تغطي 90 % من حالات الاستخدام الشائعة.

برمجة سعيدة، ولتكن ملفات PDF دائمًا قابلة للبحث!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}