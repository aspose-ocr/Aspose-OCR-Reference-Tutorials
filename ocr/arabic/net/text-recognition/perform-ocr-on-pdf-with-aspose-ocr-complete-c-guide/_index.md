---
category: general
date: 2026-06-03
description: قم بتنفيذ OCR على ملفات PDF وتحويل PDF الممسوح ضوئياً إلى PDF قابل للبحث
  باستخدام Aspose.OCR. تعلم كيفية التعرف على النص من PDF وإنشاء ملفات PDF قابلة للبحث
  في دقائق.
draft: false
keywords:
- perform OCR on PDF
- recognize text from PDF
- how to create searchable PDF
- convert scanned PDF to searchable PDF
- convert image to searchable PDF
language: ar
og_description: قم بإجراء التعرف الضوئي على الحروف (OCR) على ملف PDF وإنشاء ملف PDF
  قابل للبحث على الفور. يوضح هذا الدرس خطوة بخطوة كيفية التعرف على النص من ملف PDF
  باستخدام Aspose.OCR.
og_title: إجراء OCR على PDF – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Perform OCR on PDF and convert scanned PDF to searchable PDF using
    Aspose.OCR. Learn how to recognize text from PDF and create searchable PDFs in
    minutes.
  headline: Perform OCR on PDF with Aspose.OCR – Complete C# Guide
  type: TechArticle
- description: Perform OCR on PDF and convert scanned PDF to searchable PDF using
    Aspose.OCR. Learn how to recognize text from PDF and create searchable PDFs in
    minutes.
  name: Perform OCR on PDF with Aspose.OCR – Complete C# Guide
  steps:
  - name: 1. Large Files & Memory Management
    text: If you’re processing PDFs larger than 100 MB, consider using `OcrEngineSettings.MemoryLimit`
      to cap memory usage. Additionally, process pages in batches to avoid `OutOfMemoryException`.
  - name: 2. Language Support
    text: 'By default Aspose.OCR assumes English. To recognize other languages, set
      the `Language` property:'
  - name: 3. Multi‑Threaded Scenarios
    text: '`OcrEngine` is **not** thread‑safe. If you need parallel processing, create
      a separate engine per thread.'
  - name: 4. Debugging OCR Accuracy
    text: 'You can extract the plain text from `ocrResult` for debugging:'
  - name: 5. Licensing Gotchas
    text: 'When you run the evaluation version, Aspose adds a watermark to the output
      PDF. Register your license early in the application:'
  type: HowTo
- questions:
  - answer: Absolutely. Replace `OcrImage.FromFile("input.pdf")` with the path to
      your image file. The engine will rasterize the image and embed the OCR layer
      just the same.
    question: Can I use this to convert a single image (PNG/JPEG) to a searchable
      PDF?
  - answer: The engine will overlay the OCR text on top of existing content, so native
      text stays selectable while scanned pages become searchable.
    question: What if my PDF has both scanned pages and native text?
  - answer: 'Accuracy hinges on source quality. Clean, high‑resolution scans (>300
      dpi) give >95 % accuracy. For noisy documents, enable `PreprocessSettings` (deskew,
      despeckle) before calling `Recognize`. --- ## Next Steps – Extending Your OCR
      Toolkit Now that you can **recognize text from PDF** and **convert s'
    question: How accurate is the OCR?
  type: FAQPage
tags:
- Aspose
- OCR
- C#
- PDF
title: إجراء التعرف الضوئي على الأحرف (OCR) على ملفات PDF باستخدام Aspose.OCR – دليل
  C# الكامل
url: /ar/net/text-recognition/perform-ocr-on-pdf-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء OCR على PDF باستخدام Aspose.OCR – دليل C# كامل

هل تساءلت يومًا **كيف تقوم بإجراء OCR على ملفات PDF** دون التعامل مع العشرات من أدوات سطر الأوامر؟ أنت لست وحدك. سواءً كنت تقوم برقمنة الفواتير، أو أرشفة التقارير القديمة، أو تحتاج فقط إلى نسخة قابلة للبحث من عقد ممسوح ضوئيًا، فإن تحويل PDF ثابت إلى شيء يمكنك البحث فيه فعليًا يُغيّر قواعد اللعبة.

في هذا الدليل سنستعرض **كيفية إنشاء ملفات PDF قابلة للبحث** من ملفات PDF الممسوحة (وحتى الصور العادية) باستخدام Aspose.OCR لـ .NET. بحلول النهاية ستتمكن من **التعرف على النص من PDF** ببضع أسطر من كود C#، وستفهم سبب كل خطوة حتى تتمكن من تكييف الحل مع مشاريعك الخاصة.

> **ملخص سريع:** العملية بأكملها تختصر في ثلاث خطوات—تهيئة محرك OCR، تزويده بالمصدر (PDF أو صورة)، وحفظ ناتج PDF القابل للبحث. لنبدأ.

---

## ما ستحتاجه

| المتطلب | لماذا يهم |
|--------------|----------------|
| **.NET 6.0+** (or .NET Framework 4.6+) | Aspose.OCR يستهدف بيئات تشغيل حديثة؛ قد تفقد الإصدارات القديمة تحديثات API. |
| **Aspose.OCR for .NET** NuGet package | يوفر فئة `OcrEngine` وأدوات معالجة PDF. |
| **A valid Aspose license** (or use the free evaluation) | بدون ترخيص ستواجه حد التقييم لمدة 30 يومًا وعلامات مائية. |
| **A scanned PDF** (or an image file) you want to make searchable | هذا هو المستند المصدر لعملية OCR. |
| **Visual Studio 2022** (or any C# editor) | يسهل عملية التصحيح، لكن أي بيئة تطوير متكاملة تعمل. |

يمكنك تثبيت المكتبة باستخدام أمر NuGet التالي:

```bash
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت تعمل على خط أنابيب CI، أضف ملف الترخيص إلى مخرجات البناء وحمّله أثناء وقت التشغيل لتجنب كتابة المسارات بشكل ثابت.

## إجراء OCR على PDF – إعداد Aspose.OCR

أول شيء نحتاجه هو نسخة جديدة من `OcrEngine`. فكر فيها كالعقل الذي سيقرأ مستندك.

```csharp
// Step 1: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

لماذا نسخة جديدة في كل مرة؟ يحتفظ المحرك بالإعدادات (مثل إعدادات اللغة) التي قد تختلف بين المستندات. إنشاء نسخة لكل تشغيل يضمن بداية نظيفة ويتجنب التداخل بين المهام.

## كيفية إنشاء PDF قابل للبحث – تكوين كلمات المرور (اختياري)

إذا كان ملف PDF محميًا، عليك إخبار المحرك بكلمة المرور قبل أن يتمكن من قراءة الصفحات:

```csharp
// Step 2: (Optional) Provide the password if the PDF is protected
ocrEngine.Settings.PdfPassword = "mySecret";
```

تخطي هذه الخطوة على ملف محمي سيؤدي إلى رفع استثناء `PdfPasswordException`. احرص دائمًا على وضعه داخل كتلة try‑catch إذا لم تكن متأكدًا من حالة الحماية.

## تحويل PDF ممسوح إلى PDF قابل للبحث – تحميل المصدر

يعمل Aspose.OCR مع تجريد `OcrImage`، الذي يمكنه تغليف ملفات PDF، TIFF، JPEG، وغيرها. إليك كيفية تحميل PDF ممسوح إلى الذاكرة:

```csharp
// Step 3: Load the scanned PDF that will be converted to a searchable PDF
var sourcePdf = OcrImage.FromFile("YOUR_DIRECTORY/input.pdf");
```

في الخلفية، تقوم `FromFile` بتحليل كل صفحة إلى صور نقطية يمكن لمحرك OCR معالجتها. إذا كان لديك PDF متعدد الصفحات، سيقوم المحرك تلقائيًا بالتنقل عبر كل صفحة.

## التعرف على النص من PDF – تنفيذ OCR

الآن جوهر الدرس: اطلب من المحرك التعرف على النص وإنتاج PDF قابل للبحث.

```csharp
// Step 4: Perform OCR and request a searchable PDF as the output format
var ocrResult = ocrEngine.Recognize(sourcePdf, OutputFormat.SearchablePdf);
```

`OutputFormat.SearchablePdf` يخبر المحرك بدمج طبقة نص غير مرئية فوق الصور الممسوحة الأصلية. يحتفظ PDF الناتج بجودة الصورة الأصلية بينما يصبح قابلًا للبحث بالكامل—وهو بالضبط ما تحتاجه لتدقيق الامتثال.

## تحويل صورة إلى PDF قابل للبحث – حفظ النتيجة

أخيرًا، اكتب البيانات الثنائية إلى القرص:

```csharp
// Step 5: Save the resulting searchable PDF to disk
File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", ocrResult.Binary);
Console.WriteLine("Searchable PDF created.");
```

خاصية `Binary` تحتفظ ببايتات PDF الخام. يمكنك أيضًا بثها مباشرةً إلى استجابة ويب إذا كنت تبني API.

![مخطط يوضح تدفق تحويل OCR لإنشاء PDF قابل للبحث](https://example.com/ocr-flow.png "مخطط تدفق إجراء OCR على PDF")

*Image alt text: Perform OCR on PDF flow diagram illustrating how a scanned PDF is turned into a searchable PDF.*

## حالات الحافة والنصائح العملية

### 1. الملفات الكبيرة وإدارة الذاكرة
إذا كنت تعالج ملفات PDF أكبر من 100 ميغابايت، فكر في استخدام `OcrEngineSettings.MemoryLimit` لتحديد حد لاستخدام الذاكرة. بالإضافة إلى ذلك، عالج الصفحات على دفعات لتجنب استثناء `OutOfMemoryException`.

```csharp
ocrEngine.Settings.MemoryLimit = 512; // MB
```

### 2. دعم اللغات
بشكل افتراضي، يفترض Aspose.OCR اللغة الإنجليزية. للتعرف على لغات أخرى، اضبط خاصية `Language`:

```csharp
ocrEngine.Settings.Language = Language.French; // or Language.Multilingual
```

### 3. السيناريوهات متعددة الخيوط
`OcrEngine` **ليس** آمنًا للاستخدام المتعدد الخيوط. إذا كنت تحتاج إلى معالجة متوازية، أنشئ محركًا منفصلًا لكل خيط.

### 4. تصحيح دقة OCR
يمكنك استخراج النص العادي من `ocrResult` للتصحيح:

```csharp
string plainText = ocrResult.Text;
Console.WriteLine(plainText);
```

إذا كان الناتج غير واضح، جرب تعديل `PreprocessSettings` (مثل تصحيح الميل، إزالة الضوضاء) لتحسين الجودة.

### 5. مشكلات الترخيص
عند تشغيل النسخة التجريبية، يضيف Aspose علامة مائية إلى PDF الناتج. سجّل ترخيصك مبكرًا في التطبيق:

```csharp
var license = new License();
license.SetLicense("Aspose.OCR.lic");
```

## مثال عملي كامل – من البداية إلى النهاية

فيما يلي البرنامج الكامل الجاهز للتنفيذ والذي يدمج جميع النصائح السابقة. لا تتردد في نسخه ولصقه في مشروع وحدة تحكم جديد.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;
using System;
using System.IO;

class PdfOcrDemo
{
    static void Main()
    {
        // Load license (replace with your actual license file)
        var license = new License();
        license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Optional: set PDF password if needed
        // ocrEngine.Settings.PdfPassword = "mySecret";

        // Optional: tweak memory usage for large files
        ocrEngine.Settings.MemoryLimit = 1024; // MB

        // 2️⃣ Load scanned PDF (or image) – adjust path as required
        var source = OcrImage.FromFile("YOUR_DIRECTORY/input.pdf");

        // 3️⃣ Perform OCR – ask for a searchable PDF output
        var result = ocrEngine.Recognize(source, OutputFormat.SearchablePdf);

        // 4️⃣ Save the searchable PDF
        string outputPath = Path.Combine("YOUR_DIRECTORY", "output.pdf");
        File.WriteAllBytes(outputPath, result.Binary);

        Console.WriteLine($"Searchable PDF created at: {outputPath}");
    }
}
```

**الناتج المتوقع:** بعد التشغيل، سترى سطرًا في وحدة التحكم يؤكد موقع الملف. افتح `output.pdf` في أي عارض PDF؛ حاول كتابة كلمة تعرف أنها موجودة في المسح الأصلي. إذا تم تظليل النص، فقد نجحت في **إجراء OCR على PDF** وإنشاء مستند قابل للبحث.

## الأسئلة المتكررة

**س: هل يمكنني استخدام هذا لتحويل صورة واحدة (PNG/JPEG) إلى PDF قابل للبحث؟**  
ج: بالتأكيد. استبدل `OcrImage.FromFile("input.pdf")` بمسار ملف الصورة الخاص بك. سيقوم المحرك بتحويل الصورة إلى نقطية ودمج طبقة OCR بنفس الطريقة.

**س: ماذا لو كان PDF يحتوي على صفحات ممسوحة ونص أصلي؟**  
ج: سيضيف المحرك نص OCR فوق المحتوى الموجود، لذا يبقى النص الأصلي قابلًا للتحديد بينما تصبح الصفحات الممسوحة قابلة للبحث.

**س: ما مدى دقة OCR؟**  
ج: الدقة تعتمد على جودة المصدر. المسحات النظيفة وعالية الدقة (>300 dpi) تعطي دقة >95 %. بالنسبة للوثائق الضوضائية، فعّل `PreprocessSettings` (تصحيح الميل، إزالة الضوضاء) قبل استدعاء `Recognize`.

## الخطوات التالية – توسيع مجموعة أدوات OCR الخاصة بك

الآن بعد أن يمكنك **التعرف على النص من PDF** و**تحويل PDF ممسوح إلى PDF قابل للبحث**، فكر في المواضيع التالية:

- **معالجة دفعات**: تكرار عبر مجلد من ملفات PDF وإنشاء نسخ قابلة للبحث تلقائيًا.  
- **استخراج النص**: استخدم `ocrResult.Text` لتغذية فهرس بحث (مثل Elasticsearch).  
- **حزم لغات مخصصة**: حمّل بيانات لغات إضافية من Aspose لدعم النصوص الآسيوية.  
- **امتثال PDF/A**: دمج Aspose.PDF مع ناتج OCR لإنشاء ملفات PDF جاهزة للأرشفة.  

كل من هذه يبني على الخطوات الأساسية التي غطيناها، لذا أنت في موقع جيد لتوسيع حلك.

## الخلاصة

لقد أظهرنا لك للتو **كيفية إجراء OCR على ملفات PDF** باستخدام Aspose.OCR، وحولنا ملفات PDF الممسوحة إلى ملفات PDF قابلة للبحث بالكامل، وحتى تناولنا تحويل الصور العادية إلى ملفات PDF قابلة للبحث. الكود

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [التعرف على نص PDF – عمليات OCR باستخدام Aspose.OCR للـ Java](/ocr/english/java/ocr-operations/)
- [كيفية إجراء OCR على PDF في .NET باستخدام Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [تحويل الصور إلى PDF C# – حفظ نتيجة OCR متعددة الصفحات](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}