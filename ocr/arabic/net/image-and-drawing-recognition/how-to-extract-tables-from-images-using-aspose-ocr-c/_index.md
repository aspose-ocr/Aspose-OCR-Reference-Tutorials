---
category: general
date: 2026-03-28
description: تعلم كيفية استخراج الجداول من الصور باستخدام Aspose OCR في C#. يغطي هذا
  الدليل كيفية اكتشاف الجداول في الصورة، تحميل الصورة للتعرف الضوئي على الأحرف، واستخراج
  الجداول من ملفات PNG.
draft: false
keywords:
- how to extract tables
- extract table from image
- detect tables in image
- load image for ocr
- extract tables from png
language: ar
og_description: دليل خطوة بخطوة حول كيفية استخراج الجداول من الصور باستخدام Aspose
  OCR في C#. يتضمن الشيفرة، الشروحات والنصائح لاكتشاف الجداول في ملفات الصور.
og_title: كيفية استخراج الجداول من الصور باستخدام Aspose OCR (C#)
tags:
- Aspose OCR
- C#
- Table Extraction
title: كيفية استخراج الجداول من الصور باستخدام Aspose OCR (C#)
url: /ar/net/image-and-drawing-recognition/how-to-extract-tables-from-images-using-aspose-ocr-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج الجداول من الصور باستخدام Aspose OCR (C#)

هل تساءلت يومًا **كيفية استخراج الجداول** من فاتورة ممسوحة ضوئيًا أو لقطة شاشة لجدول بيانات؟ لست وحدك. في العديد من المشاريع الواقعية نحتاج إلى تحويل صورة جدول إلى شيء يمكننا الاستعلام عنه—عادةً ملف CSV أو DataTable. الخبر السار؟ Aspose OCR يجعل ذلك سهلًا للغاية، ويمكنك القيام به ببضع أسطر من C# فقط.

في هذا الشرح سنستعرض العملية بالكامل: من **تحميل الصورة للـ OCR**، إلى **اكتشاف الجداول في الصورة**، وأخيرًا **استخراج الجدول من الصورة** وحفظه كملف CSV. في النهاية ستحصل على تطبيق Console جاهز للتنفيذ يمكنه **استخراج الجداول من ملفات PNG** (أو أي صورة bitmap مدعومة) دون أي عناء.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- .NET 6.0 SDK أو أحدث (الكود يعمل أيضًا مع .NET Framework)
- Visual Studio 2022 (أو أي بيئة تطوير تفضلها)
- ملف ترخيص Aspose.OCR for .NET (يمكنك البدء بنسخة تجريبية مجانية)
- صورة نموذجية تحتوي على جدول (مثال: `invoice_table.png`)

إذا كان أي من هذه غير مألوف لك، لا تقلق—فقط قم بتثبيت .NET SDK واحصل على حزمة NuGet، وستكون جاهزًا للانطلاق.

## نظرة عامة على الحل

على مستوى عالٍ، يبدو سير العمل هكذا:

1. **تحميل الصورة** التي تريد معالجتها.
2. **تشغيل التعرف الضوئي على الحروف (OCR)** حتى يعرف المحرك مكان النص.
3. **إنشاء TableExtractor** الذي يمسح نتائج OCR للبحث عن هياكل شبيهة بالشبكة.
4. **استخراج جميع الجداول المكتشفة** واختيار الجدول الذي تحتاجه.
5. **حفظ الجدول** كملف CSV (أو أي تنسيق آخر تفضله).

سيتم شرح كل خطوة بالتفصيل أدناه، مع مقتطفات الكود الكاملة التي يمكنك نسخها ولصقها.

<img src="table_extraction_example.png" alt="مثال على كيفية استخراج الجداول من صورة" width="600">

*(الصورة أعلاه تُظهر جدول فاتورة نموذجي سنقوم باستخراجه.)*

## الخطوة 1 – تحميل الصورة للـ OCR

أول شيء عليك فعله هو إخبار Aspose OCR بأي ملف يجب قراءته. المكتبة تدعم PNG، JPEG، BMP، TIFF، وبعض الصيغ الأخرى. إليك الحد الأدنى من الكود:

```csharp
using Aspose.OCR;
using System.Drawing;   // Required for Image.FromFile

// ...

// Load the image that contains the table
var ocrEngine = new OcrEngine
{
    Image = Image.FromFile(@"C:\Images\invoice_table.png") // <-- adjust the path
};
```

**لماذا هذا مهم:**  
`Image.FromFile` يقوم بالعمل الشاق لتحويل PNG (أو أي bitmap آخر) إلى صيغة يستطيع محرك OCR فهمها. إذا تخطيت هذه الخطوة أو مررت بملف تالف، فإن استدعاء `Recognize()` التالي سيلقي استثناءً.

> **نصيحة احترافية:** إذا كنت تتعامل مع ملفات PDF كبيرة، استخرج كل صفحة كصورة أولًا—وإلا سيفقد محرك OCR الذاكرة.

## الخطوة 2 – التعرف على الصفحة (مطلوب قبل اكتشاف الجداول)

يقوم التعرف بتحويل بيانات البكسل الخام إلى تخطيط نصي قابل للبحث. بدون هذه الخطوة لا يملك `TableExtractor` ما يعمل عليه.

```csharp
// Perform OCR recognition – this populates internal structures
ocrEngine.Recognize();
```

**ما الذي يحدث خلف الكواليس؟**  
Aspose OCR يشغل كاشف نصوص قائم على الشبكات العصبية، ثم يُنشئ هيكلًا هرميًا من كائنات `Page` و`Paragraph` و`Word`. لاحقًا، يقوم كاشف الجداول بفحص العلاقات المكانية بين هذه الكلمات.

إذا كنت تعالج العديد من الصور داخل حلقة، فكر في إعادة استخدام نفس كائن `OcrEngine` وتبديل خاصية `Image` فقط—هذا يقلل من استهلاك الذاكرة.

## الخطوة 3 – إنشاء TableExtractor واكتشاف الجداول في الصورة

الآن بعد أن أصبحت بيانات OCR موجودة، يمكننا طلب من Aspose العثور على الجداول. فئة `TableExtractor` تقوم بذلك بالضبط.

```csharp
using Aspose.OCR.Table;

// ...

// Initialize the TableExtractor with the recognized engine
var tableExtractor = new TableExtractor(ocrEngine);

// Extract all tables detected on the page
List<Table> extractedTables = tableExtractor.ExtractAll();
```

**لماذا نستخدم `ExtractAll()`؟**  
الصورة الواحدة قد تحتوي على جداول متعددة (مثل تقرير متعدد الأقسام). `ExtractAll()` تُعيد `List<Table>` بحيث يمكنك التكرار، اختيار الجدول المناسب، أو حتى دمجها لاحقًا.

إذا كنت تحتاج فقط إلى أول جدول، يمكنك بأمان استخدام `extractedTables[0]`، لكن احرص دائمًا على التحقق من أن القائمة غير فارغة لتجنب `IndexOutOfRangeException`.

```csharp
if (extractedTables.Count == 0)
{
    Console.WriteLine("No tables were detected. Check the image quality or try adjusting OCR settings.");
    return;
}
```

## الخطوة 4 – حفظ الجدول المستخرج كملف CSV (أو أي تنسيق آخر)

Aspose يجعل عملية التصدير بسيطة. فئة `Table` تحتوي على طرق مدمجة `SaveCsv`، `SaveXls`، و`SaveJson`. إليك كيفية كتابة ملف CSV:

```csharp
// Save the first detected table to CSV
string outputPath = @"C:\Output\invoice_table.csv";
extractedTables[0].SaveCsv(outputPath);

Console.WriteLine($"Table extraction completed. CSV saved to {outputPath}");
```

**كيف يبدو ملف CSV؟**  
باستخدام مثال صورة يحتوي على شبكة 4 × 3، قد يظهر CSV كالتالي:

```
Item,Quantity,Price
Widget A,2,19.99
Widget B,5,9.50
Service C,1,150.00
```

يمكنك فتح هذا الملف في Excel أو Power BI أو تمريره مباشرة إلى خط أنابيب البيانات الخاص بك.

## مثال كامل من البداية إلى النهاية

فيما يلي البرنامج الكامل المستقل. انسخه إلى مشروع Console جديد (`dotnet new console`) وشغّله. تأكد من تثبيت حزمة NuGet `Aspose.OCR` (`dotnet add package Aspose.OCR`).

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;          // For Image
using Aspose.OCR;
using Aspose.OCR.Table;

namespace TableExtractTutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the image that contains the table
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                Image = Image.FromFile(@"C:\Images\invoice_table.png")
            };

            // -------------------------------------------------
            // Step 2: Recognize the page (required before table detection)
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 3: Create a TableExtractor and detect tables
            // -------------------------------------------------
            var tableExtractor = new TableExtractor(ocrEngine);
            List<Table> extractedTables = tableExtractor.ExtractAll();

            // Guard against no tables found
            if (extractedTables.Count == 0)
            {
                Console.WriteLine("No tables detected. Verify image quality or OCR settings.");
                return;
            }

            // -------------------------------------------------
            // Step 4: Save the first extracted table as CSV
            // -------------------------------------------------
            string csvPath = @"C:\Output\invoice_table.csv";
            extractedTables[0].SaveCsv(csvPath);

            Console.WriteLine($"Table extraction completed. CSV saved at: {csvPath}");
        }
    }
}
```

### النتيجة المتوقعة

عند تشغيل البرنامج يجب أن ترى شيئًا مشابهًا لـ:

```
Table extraction completed. CSV saved at: C:\Output\invoice_table.csv
```

افتح `invoice_table.csv` وستجد الصفوف والأعمدة مطابقة للصورة الأصلية.

## أسئلة شائعة وحالات خاصة

### ماذا لو كانت الصورة بصيغة JPEG بدلاً من PNG؟

الكود نفسه يعمل—فقط غيّر امتداد الملف في `Image.FromFile`. Aspose OCR يكتشف الصيغة تلقائيًا، لذا **استخراج الجداول من png** ليس شرطًا صارمًا؛ فهو يعمل مع أي bitmap مدعوم.

### جدولي يحتوي على خلايا مدمجة. هل سيتم الحفاظ عليها؟

الخلايا المدمجة تُعامل كأعمدة منفصلة في مخرجات CSV لأن CSV لا يدعم الدمج. إذا كنت تحتاج تنسيقًا أغنى (مثل Excel مع خلايا مدمجة)، استخدم `SaveXls` بدلاً من ذلك:

```csharp
extractedTables[0].SaveXls(@"C:\Output\invoice_table.xls");
```

### اكتشف الكاشف عمودًا مفقودًا. كيف يمكن تحسين الدقة؟

- زيادة دقة الصورة (≥300 dpi هو المثالي).
- معالجة مسبقة للصورة: تحويلها إلى تدرج رمادي، زيادة التباين، أو تطبيق فلتر تصحيح الميل.
- تعديل إعدادات Aspose OCR مثل `PageSegMode` أو `Language` إذا كان الجدول يحتوي على أحرف غير لاتينية.

### هل يمكن استخراج الجداول مباشرة من PDF؟

نعم. حوّل كل صفحة PDF إلى صورة أولًا (باستخدام `Aspose.PDF` أو أي مكتبة تحويل PDF إلى صورة)، ثم مرّر تلك الصور إلى نفس سير العمل.

## نصائح لتطبيقات جاهزة للإنتاج

1. **غلف OCR بكتلة try/catch** – بيئات الترخيص الشبكي قد تلقي استثناءات ترخيص.
2. **تحرير كائنات `Image`** – ضعها داخل كتل `using` لتحرير الموارد الأصلية.
3. **سجّل درجات الثقة** – `TableExtractor` يُظهر `Table.Confidence` يمكنك تخزينه لمراقبة الجودة.
4. **معالجة دفعات** – عند التعامل مع مئات الفواتير، يمكن تنفيذ OCR بشكل متوازي لكن احترس من إرشادات أمان الترخيص المتعلقة بالخيوط.

## الخطوات التالية

الآن بعد أن عرفت **كيفية استخراج الجداول** من الصور، قد ترغب في استكشاف:

- **اكتشاف الجداول في الفيديو** (باستخدام `TableExtractor` من Aspose على كل إطار).
- **تحميل الصورة للـ OCR** من واجهة برمجة تطبيقات ويب، لتمكين خدمات استخراج الجداول السحابية.
- **استخراج الجداول من ملفات PNG** المخزنة في Azure Blob Storage، مع دمجها في Azure Functions للمعالجة بدون خادم.

لا تتردد في تجربة صيغ ملفات مختلفة، تعديل إعدادات OCR، أو توجيه مخرجات CSV مباشرة إلى قاعدة بيانات. السماء هي الحد.

---

*برمجة سعيدة! إذا واجهت أي صعوبات أو لديك أفكار لتحسين الشرح، اترك تعليقًا أدناه. سنحلها معًا.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}