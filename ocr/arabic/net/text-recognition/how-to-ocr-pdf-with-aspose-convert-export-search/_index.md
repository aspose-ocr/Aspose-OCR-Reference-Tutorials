---
category: general
date: 2026-01-06
description: كيفية التعرف الضوئي على النص في ملفات PDF بسرعة باستخدام Aspose OCR.
  تعلم تحويل PDF إلى Excel، استخراج النص من PDF، إنشاء PDF قابل للبحث وتحويل المستند
  الممسوح إلى EPUB.
draft: false
keywords:
- how to ocr pdf
- convert pdf to excel
- extract text from pdf
- create searchable pdf
- convert scanned to epub
language: ar
og_description: كيفية التعرف الضوئي على الحروف (OCR) لملف PDF باستخدام Aspose OCR.
  يوضح هذا الدرس كيفية استخراج النص، التحويل إلى Excel، إنشاء PDF قابل للبحث وتحويل
  المستند الممسوح ضوئياً إلى EPUB.
og_title: كيفية التعرف الضوئي على النص في ملفات PDF باستخدام Aspose – دليل شامل
tags:
- Aspose OCR
- C#
- PDF processing
title: 'كيفية التعرف الضوئي على النص في ملفات PDF باستخدام Aspose: التحويل، التصدير
  والبحث'
url: /ar/net/text-recognition/how-to-ocr-pdf-with-aspose-convert-export-search/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف الضوئي على النص في ملفات PDF باستخدام Aspose: التحويل، التصدير والبحث

هل تساءلت يومًا **كيف تقوم بالتعرف الضوئي على النص في ملفات PDF** دون إنفاق مبالغ طائلة على الخدمات الخارجية؟ لست وحدك. في العديد من المشاريع—مثل أتمتة الفواتير، أرشفة المستندات القديمة، أو مجرد جعل عقد ممسوح ضوئيًا قابلًا للبحث—تحتاج إلى طريقة موثوقة لاستخراج النص من الصور المخفية داخل ملفات PDF.

الخبر السار هو أن Aspose OCR يجعل ذلك سهلًا للغاية. في هذا الدليل سنستعرض سير العمل بالكامل: من تحميل ملف PDF ممسوح ضوئيًا، استخراج نصه، تحويل البيانات إلى Excel، إنشاء PDF قابل للبحث، وحتى تحويل المستند الممسوح إلى كتاب إلكتروني بصيغة EPUB. في النهاية ستحصل على مقتطف C# قابل لإعادة الاستخدام يتعامل مع جميع السيناريوهات مثل “convert pdf to excel”، “extract text from pdf”، “create searchable pdf”، و “convert scanned to epub” التي قد تواجهها.

> **ما ستحصل عليه**  
> • برنامج C# كامل، قابل للتنفيذ، يتعرف على النص في ملف PDF.  
> • خيارات تصدير إلى Excel، JSON، EPUB، وإصدار PDF قابل للبحث.  
> • نصائح للتعامل مع المشكلات الشائعة مثل ملفات PDF متعددة الصفحات وإعدادات اللغة.  

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يُمكن تجميعه تحت .NET Core أيضًا).  
- حزمة NuGet الخاصة بـ Aspose.OCR (`Install-Package Aspose.OCR`).  
- ملف PDF ممسوح ضوئيًا (مثال: `invoice.pdf`) موجود في مجلد يمكنك الإشارة إليه.  
- إلمام أساسي بـ C# و Visual Studio (أو أي بيئة تطوير تفضلها).

لا توجد أدوات خارجية إضافية مطلوبة؛ Aspose يتولى كل الأعمال الثقيلة داخليًا.

---

## كيفية التعرف الضوئي على النص في PDF – دليل خطوة بخطوة

نقسم العملية إلى خطوات منطقية. كل خطوة تتضمن شرحًا مختصرًا، الكود C# الدقيق الذي تحتاجه، وملاحظة حول أهمية الخطوة.

### الخطوة 1: إعداد محرك OCR (الكلمة المفتاحية الأساسية)

أول شيء تقوم به عندما تريد **how to OCR PDF** هو إنشاء كائن `OcrEngine` وتكوين لغته. يدعم Aspose عشرات اللغات؛ بالنسبة لمعظم المستندات الإنجليزية يكفي `OcrLanguage.English`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

// Step 1 – Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // Choose the language that matches your source document.
    Language = OcrLanguage.English
};
```

> **لماذا؟**  
> يحتاج المحرك إلى معرفة اللغة لتطبيق مجموعة الأحرف الصحيحة وتحسين الدقة. تخطي هذه الخطوة قد يؤدي إلى مخرجات مشوشة، خاصةً للخطوط غير اللاتينية.

### الخطوة 2: تحميل ملف PDF الممسوح (الكلمة المفتاحية الثانوية: extract text from pdf)

يمكن لـ Aspose.OCR قراءة ملف PDF مباشرة، معاملة كل صفحة كصورة. تساعد الأداة المساعدة `ImageStream.FromFile` في إخفاء عملية تحويل PDF إلى صورة.

```csharp
// Step 2 – Load the PDF you want to OCR
string inputPath = Path.Combine("YOUR_DIRECTORY", "invoice.pdf");
ocrEngine.Image = ImageStream.FromFile(inputPath);
```

> **نصيحة:**  
> إذا كان ملف PDF يحتوي على العديد من الصفحات، سيقوم Aspose بمعالجتها تسلسليًا. يمكنك أيضًا تمرير تدفق (stream) إذا كان الملف مخزنًا في سحابة.

### الخطوة 3: تشغيل محرك التعرف (الكلمة المفتاحية الأساسية)

الآن نقوم فعليًا بتنفيذ عملية OCR. تُعيد طريقة `Recognize` القيمة `true` عند النجاح؛ وإلا يمكنك فحص `ErrorMessage` للتشخيص.

```csharp
// Step 3 – Perform OCR
if (!ocrEngine.Recognize())
{
    // Throw an exception with a clear message; this is helpful for debugging.
    throw new InvalidOperationException($"OCR failed: {ocrEngine.ErrorMessage}");
}
Console.WriteLine("✅ OCR completed successfully.");
```

> **مشكلة شائعة:**  
> قد تتجاوز ملفات PDF الكبيرة حدود الذاكرة الافتراضية. إذا واجهت استثناء `OutOfMemoryException`، فكر في معالجة الصفحات على دفعات (انظر قسم “المتقدم” لاحقًا).

### الخطوة 4: تصدير المحتوى المعترف به

الآن بعد أن عرفت **how to OCR PDF**، يمكنك تصدير النتائج إلى الصيغ التي تحتاجها فعليًا. فيما يلي أربعة مخرجات عملية.

#### 4a – إنشاء PDF قابل للبحث (الكلمة المفتاحية الثانوية: create searchable pdf)

PDF القابل للبحث يدمج طبقة نصية غير مرئية فوق الصورة الممسوحة، مما يتيح لك البحث في المستند دون فقدان جودة العرض.

```csharp
// 4a – Export to a searchable PDF
string searchablePdfPath = Path.Combine("YOUR_DIRECTORY", "invoice_searchable.pdf");
ocrEngine.Save(searchablePdfPath, new PdfExportOptions
{
    // Preserve the original appearance while adding a text layer.
    IncludeOriginalImage = true,
    TextLayerOnly = false
});
Console.WriteLine($"🔎 Searchable PDF saved to {searchablePdfPath}");
```

#### 4b – تحويل PDF إلى Excel (الكلمة المفتاحية الثانوية: convert pdf to excel)

تحتاج العديد من الشركات إلى بيانات جدولة من الفواتير أو الإيصالات. التصدير إلى XLSX يمنحك جدولًا جاهزًا للاستخدام.

```csharp
// 4b – Export to Excel (XLSX)
string excelPath = Path.Combine("YOUR_DIRECTORY", "invoice.xlsx");
ocrEngine.Save(excelPath, new ExcelExportOptions
{
    IncludeHeaders = true,
    WorksheetName = "Invoice"
});
Console.WriteLine($"📊 Excel file saved to {excelPath}");
```

#### 4c – استخراج النص كملف JSON (الكلمة المفتاحية الثانوية: extract text from pdf)

إذا كنت تفضل حمولة JSON منظمة—ربما لتغذية API لاحق—فعّل إطارات الحدود (bounding boxes) لكل كلمة تم التعرف عليها.

```csharp
// 4c – Export to JSON with word bounding boxes
string jsonPath = Path.Combine("YOUR_DIRECTORY", "invoice.json");
ocrEngine.Save(jsonPath, new JsonExportOptions
{
    IncludeWordBoundingBoxes = true
});
Console.WriteLine($"📄 JSON output saved to {jsonPath}");
```

#### 4d – تحويل الممسوح إلى EPUB (الكلمة المفتاحية الثانوية: convert scanned to epub)

الكتب الإلكترونية طريقة رائعة لأرشفة الأدلة الممسوحة. المقتطف التالي يوضح كيفية إنشاء ملف EPUB مباشرةً من نتيجة OCR.

```csharp
// 4d – Export to EPUB (e‑book format)
string epubPath = Path.Combine("YOUR_DIRECTORY", "invoice.epub");
ocrEngine.Save(epubPath, new EpubExportOptions
{
    Title = "Scanned Invoice",
    Author = "Acme Corp"
});
Console.WriteLine($"📚 EPUB created at {epubPath}");
```

### مثال كامل يعمل

بدمج كل ما سبق، إليك برنامج C# Console واحد يمكنك نسخه ولصقه ثم تشغيله.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Initialize OCR engine – how to OCR PDF?
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // -------------------------------------------------
            // 2️⃣ Load scanned PDF (extract text from PDF)
            // -------------------------------------------------
            string inputDir = "YOUR_DIRECTORY";
            string pdfFile = Path.Combine(inputDir, "invoice.pdf");
            ocrEngine.Image = ImageStream.FromFile(pdfFile);

            // -------------------------------------------------
            // 3️⃣ Perform recognition
            // -------------------------------------------------
            if (!ocrEngine.Recognize())
                throw new InvalidOperationException($"OCR failed: {ocrEngine.ErrorMessage}");
            Console.WriteLine("✅ OCR completed.");

            // -------------------------------------------------
            // 4️⃣ Export results (convert PDF to Excel, etc.)
            // -------------------------------------------------
            // Searchable PDF
            ocrEngine.Save(Path.Combine(inputDir, "invoice_searchable.pdf"),
                new PdfExportOptions { IncludeOriginalImage = true });

            // Excel file
            ocrEngine.Save(Path.Combine(inputDir, "invoice.xlsx"),
                new ExcelExportOptions { IncludeHeaders = true, WorksheetName = "Invoice" });

            // JSON with bounding boxes
            ocrEngine.Save(Path.Combine(inputDir, "invoice.json"),
                new JsonExportOptions { IncludeWordBoundingBoxes = true });

            // EPUB e‑book
            ocrEngine.Save(Path.Combine(inputDir, "invoice.epub"),
                new EpubExportOptions { Title = "Scanned Invoice", Author = "Acme Corp" });

            Console.WriteLine("🎉 All exports completed successfully.");
        }
    }
}
```

شغّل البرنامج، وستحصل على أربعة ملفات جديدة في `YOUR_DIRECTORY`: PDF قابل للبحث، مصنف Excel، ملف JSON، وكتاب EPUB—جميعها مُولدة من نفس المصدر الممسوح.

---

## نصائح متقدمة وحالات حافة

| الحالة | ما يجب فعله |
|-----------|------------|
| **ملفات PDF متعددة الصفحات** | يعالج Aspose كل صفحة تلقائيًا، لكن قد ترغب في الحصول على أوراق Excel منفصلة لكل صفحة. استخدم `ExcelExportOptions.StartPage` و `EndPage` لتحديد النطاق. |
| **المستندات غير الإنجليزية** | غيّر `Language = OcrLanguage.Spanish` (أو أي لغة مدعومة). للغات مختلطة، اضبط `Language = OcrLanguage.AutoDetect`. |
| **مسحات منخفضة الدقة (<150 dpi)** | تنخفض دقة OCR بشكل حاد. عالج الصورة مسبقًا باستخدام `ImageProcessor` لتكبيرها (`Resize`) قبل استدعاء `Recognize`. |
| **ملفات كبيرة (>100 MB)** | عالجها على دفعات: حمّل صفحة، تعرف عليها، صدّرها، ثم حرّر `ocrEngine.Image` قبل الانتقال إلى الصفحة التالية. |
| **خطوط مفقودة في PDF** | عند إنشاء PDF قابل للبحث، دمج الخطوط عبر `PdfExportOptions.FontEmbedding = FontEmbedding.Always` لتجنب مشاكل الأحرف المفقودة على الأجهزة الأخرى. |

---

## الأسئلة المتكررة

**س: هل يعمل هذا النهج مع ملفات PDF محمية بكلمة مرور؟**  
ج: نعم. حمّل PDF إلى `MemoryStream` بعد فك تشفيره باستخدام مكتبة مثل `PdfSharp`. ثم مرّر الـ stream إلى `ImageStream.FromStream`.

**س: هل يمكنني تنفيذ OCR على PDF مخزن في Azure Blob Storage؟**  
ج: بالتأكيد. نزّل الـ blob إلى stream (`BlobClient.OpenReadAsync`) ومرّر ذلك الـ stream إلى `ImageStream.FromStream`. باقي سير العمل يبقى كما هو.

**س: ماذا أفعل إذا ألقى محرك OCR استثناء `InvalidOperationException` رغم أن الملف يبدو سليمًا؟**  
ج: افحص `ocrEngine.ErrorMessage`. الأسباب الشائعة هي تنسيقات صور غير مدعومة داخل PDF أو صفحات تالفة. تقسيم PDF ومعالجة كل صفحة على حدة غالبًا ما يعزل المشكلة.

---

## الخلاصة

ها هي حلًا كاملًا من البداية إلى النهاية يوضح **how to OCR PDF** باستخدام Aspose OCR، ثم **convert PDF to Excel**, **extract text from PDF**, **create searchable PDF**, وحتى **convert scanned to EPUB**. الكود مستقل تمامًا، يعمل على أي منصة متوافقة مع .NET، ويمكن تكييفه لمعالجة دفعات من المستندات مع تغييرات بسيطة.

### خطوات قد ترغب في استكشافها لاحقًا:

- دمج المخرجات في قاعدة بيانات لأرشفة قابلة للبحث.  
- إضافة واجهة مستخدم بسيطة (WinForms أو Blazor) للسماح للمستخدمين بتحميل ملفات PDF مباشرة.  
- دمج OCR مع واجهات برمجة تطبيقات تلخيص الذكاء الاصطناعي لتوليد ملخصات سريعة للعقود الطويلة.

جرّبه، عدّل الخيارات لتناسب حالتك بالضبط، ودع الأتمتة تتولى الأعمال الشاقة. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}