---
category: general
date: 2026-03-17
description: أنشئ ملف PDF قابل للبحث بسرعة عن طريق تحويل ملف PDF الممسوح ضوئياً باستخدام
  تقنية OCR. تعلّم كيفية تشغيل OCR، استخراج النص من PDF والمزيد.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- ocr to searchable pdf
- extract text from pdf
- how to run ocr
language: ar
og_description: إنشاء ملف PDF قابل للبحث من المستندات الممسوحة ضوئياً. يوضح هذا الدليل
  كيفية تحويل ملف PDF الممسوح، تشغيل تقنية التعرف الضوئي على الأحرف (OCR)، واستخراج
  النص باستخدام لغة C#.
og_title: إنشاء PDF قابل للبحث – دليل OCR كامل بلغة C#
tags:
- OCR
- PDF
- C#
- .NET
title: إنشاء ملف PDF قابل للبحث من الملفات الممسوحة ضوئياً – دليل C# خطوة بخطوة
url: /ar/net/text-recognition/create-searchable-pdf-from-scanned-files-step-by-step-c-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث – دليل C# الكامل

هل احتجت يوماً إلى **إنشاء PDF قابل للبحث** من مجموعة من الصفحات الممسوحة ضوئياً؟ ربما تقوم برقمنة عقود قديمة، أو تريد فقط أن تكون ملفات PDF الخاصة بك قابلة للبحث في مستكشف Windows. على أي حال، ربما تتساءل كيف **تحويل PDF الممسوح** إلى شيء يمكنك البحث فيه فعلياً.  

الأخبار السارة؟ ببضع أسطر من C# ومحرك OCR، يمكنك تحويل أي PDF يعتمد على الصور إلى PDF قابل للبحث بالكامل—دون الحاجة إلى خدمات خارجية. في هذا الدرس سنستعرض العملية بالكامل، من تثبيت المكتبة إلى استخراج النص، وسنشرح “السبب” وراء كل خطوة حتى تفهم ما يحدث في الخلفية.

> **الإجابة السريعة:** فقط اضبط `PdfConversionMode = PdfConversionMode.SearchablePdf`، قدم الملف الممسوح، استدعِ `Recognize()`، واحفظ النتيجة.  

فيما يلي كل ما تحتاجه لتجعلها تعمل اليوم.

---

## ما الذي ستحتاجه

| المتطلب المسبق | لماذا هو مهم |
|--------------|----------------|
| .NET 6 or later (or .NET Framework 4.7+) | SDK الـ OCR الذي سنستخدمه يستهدف هذه البيئات. |
| Visual Studio 2022 (or any C# IDE) | يسهل عملية تصحيح الأخطاء وإدارة NuGet. |
| A NuGet‑compatible OCR library (e.g., **Aspose.OCR** or **Tesseract.NET**) | يوفر فئة `OcrEngine` المعروضة في الشيفرة. |
| A scanned PDF file to test with | سنحول هذا إلى PDF قابل للبحث. |

إذا كان لديك مشروع بالفعل، فقط أضف حزمة OCR عبر وحدة تحكم مدير الحزم:

```powershell
Install-Package Aspose.OCR
```

*(استبدل `Aspose.OCR` بالمكتبة التي تختارها؛ الـ API الذي نعرضه عام إلى حد ما.)*

---

## تنفيذ خطوة بخطوة

أسفل كل خطوة ندرج الشيفرة C# الدقيقة التي يمكنك نسخها ولصقها، بالإضافة إلى شرح مختصر **لماذا** توجد هذه السطر.

### الخطوة 1: تهيئة محرك OCR  

إنشاء المحرك هو أول ما تقوم به لأنه يحتفظ بجميع الإعدادات والحالة لجلسة التعرف.

```csharp
using Aspose.OCR;          // <-- OCR library namespace
using System.IO;           // needed for file handling

// Step 1: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **نصيحة احترافية:** إعادة استخدام نسخة واحدة من `OcrEngine` لملفات متعددة يقلل استهلاك الذاكرة، خاصةً عند معالجة دفعات كبيرة.

### الخطوة 2: ضبط المحرك لإنشاء PDF قابل للبحث  

يمكن للمحرك إخراج نص عادي، أو صور، أو PDF قابل للبحث. ضبط الوضع الصحيح يخبر المكتبة بإدراج طبقة نص غير مرئية خلف صور الصفحات الأصلية.

```csharp
// Step 2: Tell the engine to produce a searchable PDF
ocrEngine.Config.PdfConversionMode = PdfConversionMode.SearchablePdf;
```

*لماذا؟* بدون هذا العلم ستحصل من عملية OCR على مجرد `string` من النص المعترف به، وهو غير مفيد إذا كنت لا تزال بحاجة إلى تخطيط الصفحة الأصلي.

### الخطوة 3: تحميل المستند الممسوح  

معظم SDKs للـ OCR تقبل `Image` أو `ImageStream`. هنا نستخدم أداة مساعدة تقرأ ملف PDF وتتعامل مع كل صفحة كصورة.

```csharp
// Step 3: Load the scanned PDF you want to convert
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\scanned.pdf");
```

> **حالة خاصة:** إذا كان PDF الخاص بك يحتوي على صفحات نقطية ومتجهة مختلطة، قد تتخطى بعض المحركات الصفحات المتجهة. في هذه الحالة، حوّل PDF إلى صور مسبقاً (مثلاً باستخدام Ghostscript) قبل إمداده إلى محرك OCR.

### الخطوة 4: تشغيل التعرف OCR  

استدعاء `Recognize()` يقوم بالعمل الشاق—اكتشاف النص، نمذجة اللغة، وإنشاء PDF—all يحدث في الخلفية.

```csharp
// Step 4: Run OCR; the result includes the searchable PDF object
var ocrResult = ocrEngine.Recognize();
```

إذا كنت بحاجة إلى **استخراج النص من pdf** أيضاً، يمكنك الحصول عليه من `ocrResult.Text`:

```csharp
string extractedText = ocrResult.Text;   // plain text version
```

### الخطوة 5: حفظ PDF القابل للبحث  

أخيراً، احفظ الناتج إلى القرص. خاصية `PdfDocument` تحتوي على PDF مكتمل مع طبقة نص غير مرئية.

```csharp
// Step 5: Persist the searchable PDF
ocrResult.PdfDocument.Save(@"C:\Docs\searchable.pdf");
```

عند فتح `searchable.pdf` في Adobe Reader أو Edge، ستتمكن من كتابة كلمة في مربع البحث والانتقال مباشرة إلى الموقع المطابق—تماماً مثل PDF الأصلي.

---

## التحقق من النتيجة

1. افتح الملف المُولد في أي عارض PDF.  
2. اضغط **Ctrl + F** واكتب كلمة تعلم أنها موجودة في الصفحات الممسوحة.  
3. إذا قام العارض بتمييز الكلمة، فقد نجحت في **إنشاء PDF قابل للبحث**.

إذا لم يُعثر على شيء، تحقق مرة أخرى أن PDF المصدر يحتوي فعلاً على نص قابل للقراءة (بعض المسحات منخفضة الدقة بحيث لا يستطيع OCR التعرف على أي شيء). زيادة DPI قبل OCR (مثلاً `ocrEngine.Config.Dpi = 300`) غالباً ما تساعد.

---

## الأخطاء الشائعة وكيفية إصلاحها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| PDF قابل للبحث فارغ | `PdfConversionMode` ترك على الإعداد الافتراضي (صورة فقط) | اضبط `PdfConversionMode = PdfConversionMode.SearchablePdf`. |
| حروف مشوشة | نموذج اللغة غير صحيح | `ocrEngine.Config.Language = Language.English;` (أو اللغة المناسبة). |
| معالجة بطيئة على ملفات كبيرة | المحرك يعيد التهيئة لكل صفحة | أعد استخدام نفس نسخة `OcrEngine`، أو فعّل المعالجة المتعددة الخيوط إذا كانت المكتبة تدعم ذلك. |
| لا نص قابل للبحث بعد التحويل | PDF الإدخال يحتوي على متجهات فقط (لا صور نقطية) | احول صفحات PDF إلى صور أولاً (مثلاً `PdfRenderer` من Aspose.PDF). |

---

## مكافأة: استخراج النص مباشرةً من PDF القابل للبحث  

أحياناً تحتاج النص الخام للفهرسة أو التحليل. بما أن `ocrResult` يزودك بالفعل بـ `Text`، يمكنك تخطي فتح PDF مرة أخرى. ومع ذلك، إذا كان لديك ملف PDF فقط لاحقاً، استخدم مستخرج نص PDF:

```csharp
using Aspose.Pdf;   // PDF library for reading

var pdfDoc = new Document(@"C:\Docs\searchable.pdf");
var textAbsorber = new TextAbsorber();
pdfDoc.Pages.Accept(textAbsorber);
string fullText = textAbsorber.Text;
```

الآن لديك **استخراج النص من pdf** دون إعادة تشغيل OCR—اختصار مفيد عند معالجة ملفات متعددة.

---

## مثال كامل يعمل (جميع الخطوات في ملف واحد)

```csharp
// ------------------------------------------------------------
// Full C# example: Convert a scanned PDF into a searchable PDF
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.Pdf;               // For optional text extraction
using Aspose.Pdf.Text;          // TextAbsorber class

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Configure for searchable PDF output
            ocrEngine.Config.PdfConversionMode = PdfConversionMode.SearchablePdf;
            // Optional: set language and DPI for better accuracy
            ocrEngine.Config.Language = Language.English;
            ocrEngine.Config.Dpi = 300;

            // 3️⃣ Load the scanned document (replace path as needed)
            string inputPath = @"C:\Docs\scanned.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 4️⃣ Run OCR – this creates both PDF and plain‑text results
            var ocrResult = ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\searchable.pdf";
            ocrResult.PdfDocument.Save(outputPath);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");

            // 🎉 Bonus: Extract plain text without opening the PDF again
            string extractedText = ocrResult.Text;
            Console.WriteLine("\n--- Extracted Text Preview ---");
            Console.WriteLine(extractedText.Substring(0,
                Math.Min(300, extractedText.Length)) + "...");

            // Optional: Verify by re‑reading the PDF
            var pdfDoc = new Document(outputPath);
            var absorber = new TextAbsorber();
            pdfDoc.Pages.Accept(absorber);
            Console.WriteLine("\nText extracted from saved PDF:");
            Console.WriteLine(absorber.Text.Substring(0,
                Math.Min(300, absorber.Text.Length)) + "...");
        }
    }
}
```

**الناتج المتوقع** (مقتطع للاختصار):

```
Searchable PDF saved to: C:\Docs\searchable.pdf

--- Extracted Text Preview ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

Text extracted from saved PDF:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

إذا رأيت المقتطف نفسه مرتين، فإن OCR نجح والـ PDF الآن يحتوي على طبقة نص قابلة للبحث.

---

## الخطوات التالية والمواضيع ذات الصلة

- **معالجة دفعات:** تكرار عبر مجلد من ملفات PDF الممسوحة، وإعادة استخدام نفس نسخة `OcrEngine` لتحسين الإنتاجية.  
- **اكتشاف اللغة:** للأرشيفات متعددة اللغات، غيّر `ocrEngine.Config.Language` ديناميكياً بناءً على بيانات الملف.  
- **الامتثال لـ PDF/A:** بعض الصناعات تتطلب PDFs أرشيفية؛ اضبط `PdfConversionMode = PdfConversionMode.SearchablePdfA` إذا كان SDK يدعم ذلك.  
- **تحسين الأداء:** جرب `ocrEngine.Config.UseParallelProcessing = true` (إن كان متاحاً) لتسريع المهام الكبيرة.

كل هذه تبني على المفهوم الأساسي لـ **كيفية تشغيل OCR** بفعالية بينما **إنشاء PDF قابل للبحث** ملفات يمكن فهرستها فوراً.

---

## الخلاصة

أصبحت الآن تملك وصفة كاملة وجاهزة للإنتاج لتحويل أي مستند ممسوح إلى تحفة **إنشاء PDF قابل للبحث**. من خلال ضبط محرك OCR، تحميل المصدر، تشغيل التعرف، وحفظ النتيجة، غطيت كامل خط الأنابيب—من صورة خام إلى PDF قابل للبحث واستخراج النص.  

جرّبها مع ملفاتك الخاصة، عدّل إعداد DPI أو اللغة، وست

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}