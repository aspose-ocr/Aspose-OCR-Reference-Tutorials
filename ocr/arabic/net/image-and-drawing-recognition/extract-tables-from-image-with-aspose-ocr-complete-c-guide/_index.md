---
category: general
date: 2026-05-31
description: استخراج الجداول من الصورة باستخدام Aspose OCR في C#. تعلم كيفية تحويل
  الصورة إلى جدول، وتفعيل اكتشاف الجداول، وإخراج النتائج بكفاءة.
draft: false
keywords:
- extract tables from image
- convert image to table
- OCR table extraction
- Aspose OCR C#
- image to spreadsheet conversion
- table detection in OCR
language: ar
og_description: استخراج الجداول من الصورة باستخدام Aspose OCR. يوضح هذا الدليل كيفية
  تحويل الصورة إلى جدول، وتمكين اكتشاف الجداول، ومعالجة النتائج في C#.
og_title: استخراج الجداول من الصورة – دليل C# خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  headline: Extract Tables from Image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  name: Extract Tables from Image with Aspose OCR – Complete C# Guide
  steps:
  - name: Expected Output
    text: 'Assuming the source image contains a 3 × 4 table of invoice line items,
      you might see something like:'
  - name: Low‑Resolution Images
    text: 'When your source picture is under 150 dpi, the table detection algorithm
      may miss cell boundaries. A quick fix is to upscale the image using `System.Drawing`
      before feeding it to Aspose:'
  - name: Skewed Tables
    text: 'If the table is rotated even a few degrees, enable auto‑deskew:'
  - name: Multiple Tables on One Page
    text: Aspose OCR returns each table as a separate object in `result.Tables`. You
      can treat them individually, or merge them into a single DataTable if you need
      a unified view.
  - name: Exporting to Excel
    text: 'Once you have a `DataTable`, exporting to an `.xlsx` file is a breeze with
      `ClosedXML`:'
  type: HowTo
- questions:
  - answer: Yes. Convert each PDF page to an image first (`PdfRenderer` or `Ghostscript`),
      then feed the bitmap to Aspose OCR.
    question: Does this work with PDFs?
  - answer: Absolutely. The `ImageStream.FromFile` method accepts JPEG, PNG, BMP,
      and TIFF out of the box.
    question: Can I extract tables from a JPG?
  - answer: Aspose OCR treats merged cells as separate logical cells; you may need
      to post‑process the output to combine them based on confidence or content patterns.
    question: What if my table has merged cells?
  - answer: Practically, the engine handles tables up to several hundred rows. Performance
      degrades linearly, so consider chunking very large scans.
    question: Is there a limit on table size?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- Data Extraction
title: استخراج الجداول من الصورة باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/image-and-drawing-recognition/extract-tables-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج الجداول من الصورة – دليل C# الكامل

هل احتجت يومًا إلى **استخراج الجداول من الصورة** لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك؛ العديد من المطورين يواجهون هذه المشكلة عند محاولة تحويل الفواتير أو الإيصالات الممسوحة ضوئيًا إلى بيانات قابلة للاستخدام. الخبر السار؟ باستخدام Aspose OCR يمكنك **تحويل الصورة إلى جدول** في بضع أسطر فقط من كود C#.

في هذا البرنامج التعليمي سنستعرض مثالًا واقعيًا: تحميل ملف PNG يحتوي على جدول، تحويل هذا التخطيط البصري إلى شبكة منظمة، وطباعة محتوى كل خلية مع درجات الثقة. في النهاية ستحصل على مقطع كود يعمل بالكامل يمكنك إدراجه في أي مشروع .NET، بالإضافة إلى نصائح للتعامل مع الحالات الخاصة وتوسيع الحل.

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي:

- **.NET 6.0** أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+)
- حزمة NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`)
- ملف صورة يحتوي فعليًا على جدول (مثال: `invoice_with_table.png`)
- بيئة تطوير C# أساسية (Visual Studio، Rider، أو VS Code مع ملحق C#)

هذا كل شيء—لا محركات OCR إضافية، ولا تبعيات ثقيلة. جاهز؟ لننطلق.

## الخطوة 1: تهيئة محرك OCR **استخراج الجداول من الصورة**

أولًا، نقوم بإنشاء كائن `OcrEngine` ونشير به إلى صورة المصدر. فكر في المحرك كالعقل الذي سيقرأ كل بكسل ويحاول فهم التخطيط.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Initialize the OCR engine with the input image
OcrEngine engine = new OcrEngine
{
    // ImageStream.FromFile loads the image from disk
    Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
};
```

> **لماذا هذا مهم:** بدون تهيئة المحرك بشكل صحيح، لن يكون لدى محرك OCR ما يحلله، ولن تحصل على أي جداول من الصورة. استدعاء `ImageStream.FromFile` يعتني أيضًا بمشكلات الصيغ الشائعة (PNG، JPEG، BMP) لذا لا تحتاج إلى خطوات تحويل إضافية.

## الخطوة 2: تمكين اكتشاف الجداول – المفتاح لـ **تحويل الصورة إلى جدول**

يمكن لـ Aspose OCR قراءة النص العادي من الصورة، لكنه لن يفهم الصفوف والأعمدة إلا إذا أخبرته بالبحث عن الجداول. هنا يأتي دور علم `DetectTables`.

```csharp
// Turn on table detection in the OCR options
engine.Options = new OcrOptions
{
    DetectTables = true   // This activates the table extraction algorithm
};
```

> **نصيحة احترافية:** إذا كنت تحتاج فقط إلى النص الخام، اترك `DetectTables` على `false`. تمكينه يضيف عبءً بسيطًا، لكن النتيجة تكون منظمة ويمكنك إرسالها مباشرة إلى جدول بيانات أو قاعدة بيانات.

## الخطوة 3: تنفيذ التعرف على OCR – لحظة الحقيقة

الآن نطلب من المحرك قراءة الصورة فعليًا. تُعيد طريقة `Recognize` كائن `OcrResult` يحتوي على النص العادي وأي جداول مكتشفة.

```csharp
// Execute the OCR process
OcrResult result = engine.Recognize();
```

> **ماذا يحدث خلف الكواليس؟** تقوم Aspose بسلسلة من خطوات ما قبل معالجة الصورة (تصحيح الميل، التحويل إلى ثنائي) قبل تطبيق مُعرف النص القائم على الشبكات العصبية. عندما تكون `DetectTables` مفعلة، يتم تشغيل تمريرة تحليل تخطيط تُجَمّع الأحرف في صفوف وأعمدة.

## الخطوة 4: التجاوز عبر الجداول المكتشفة – **استخراج الجداول من الصورة** عمليًا

إذا وجد المحرك أي جداول، ستظهر في `result.Tables`. سنقوم بالتكرار عبر كل جدول، ثم عبر كل صف وعمود، مطبعين نص الخلية ونسبة الثقة.

```csharp
// Loop over every detected table
foreach (var table in result.Tables)
{
    Console.WriteLine("Table found:");
    for (int r = 0; r < table.Rows; r++)
    {
        for (int c = 0; c < table.Columns; c++)
        {
            var cell = table[r, c];
            // Show cell text and its confidence level
            Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
        }
        Console.WriteLine(); // New line after each row
    }
}
```

> **لماذا نتحقق من الثقة؟** OCR ليس مثاليًا، خاصةً مع المسحات منخفضة الدقة. قيمة `Confidence` (0‑100) تتيح لك اتخاذ قرار بقبول الخلية كما هي أو وضع علامة للمراجعة اليدوية. عادةً ما يكون العتبة 80 % للبيانات الحرجة.

### النتيجة المتوقعة

بافتراض أن صورة المصدر تحتوي على جدول 3 × 4 من بنود الفاتورة، قد ترى ما يلي:

```
Table found:
Item (conf:96%)   Qty (conf:94%)   Price (conf:97%)   Total (conf:95%)
Pen (conf:99%)    10 (conf:98%)    1.20 (conf:97%)    12.00 (conf:96%)
Notebook (conf:95%) 5 (conf:93%)  3.50 (conf:94%)    17.50 (conf:92%)
...
```

إذا لم يتم اكتشاف أي جداول، سيكون `result.Tables` فارغًا—لا شيء للطباعة، لكن البرنامج سيخرج بأمان.

## الخطوة 5: التعامل مع الحالات الخاصة والمشكلات الشائعة

### صور منخفضة الدقة

عندما تكون صورة المصدر أقل من 150 dpi، قد يتخطى خوارزمية اكتشاف الجداول حدود الخلايا. حل سريع هو تكبير الصورة باستخدام `System.Drawing` قبل تمريرها إلى Aspose:

```csharp
using System.Drawing;
using System.Drawing.Imaging;

// Load and upscale
Bitmap bmp = new Bitmap(@"YOUR_DIRECTORY/invoice_with_table.png");
Bitmap resized = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
engine.Image = ImageStream.FromBitmap(resized);
```

### جداول مائلة

إذا كان الجدول مائلًا بضع درجات، فعّل تصحيح الميل التلقائي:

```csharp
engine.Options.Deskew = true; // Turns on automatic deskewing
```

### جداول متعددة في صفحة واحدة

تُعيد Aspose OCR كل جدول ككائن منفصل في `result.Tables`. يمكنك معالجتها بشكل فردي، أو دمجها في `DataTable` واحد إذا كنت تحتاج إلى عرض موحد.

```csharp
// Example: Merge all tables into one DataTable
var merged = new System.Data.DataTable();
foreach (var tbl in result.Tables)
{
    // Simple merge logic – assumes same column count
    // Add rows from each table
    for (int r = 0; r < tbl.Rows; r++)
    {
        var row = merged.NewRow();
        for (int c = 0; c < tbl.Columns; c++)
        {
            row[c] = tbl[r, c].Text;
        }
        merged.Rows.Add(row);
    }
}
```

### تصدير إلى Excel

بمجرد حصولك على `DataTable`، يصبح تصديرها إلى ملف `.xlsx` سهلًا باستخدام `ClosedXML`:

```csharp
using ClosedXML.Excel;

var workbook = new XLWorkbook();
var worksheet = workbook.Worksheets.Add(merged, "ExtractedTable");
workbook.SaveAs("ExtractedTable.xlsx");
```

الآن لقد **حولت الصورة إلى جدول** فعليًا ويمكنك تسليم ملف الجدول إلى عمليات المعالجة اللاحقة.

## مثال كامل يعمل – من البداية إلى النهاية

فيما يلي البرنامج الكامل الجاهز للتنفيذ الذي يجمع كل الخطوات. الصقه في مشروع Console جديد، عدل مسار الملف، واضغط **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;
using System.Data;
using ClosedXML.Excel;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine with the image
        OcrEngine engine = new OcrEngine
        {
            Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
        };

        // 2️⃣ Enable table detection (key to convert image to table)
        engine.Options = new OcrOptions
        {
            DetectTables = true,
            Deskew = true // Helps with slightly rotated scans
        };

        // 3️⃣ Perform recognition
        OcrResult result = engine.Recognize();

        // 4️⃣ Process each detected table
        DataTable merged = new DataTable();
        bool firstTable = true;

        foreach (var table in result.Tables)
        {
            Console.WriteLine("Table found:");
            for (int r = 0; r < table.Rows; r++)
            {
                // Ensure DataTable has enough columns
                if (firstTable && merged.Columns.Count < table.Columns)
                {
                    for (int i = merged.Columns.Count; i < table.Columns; i++)
                        merged.Columns.Add($"Col{i + 1}");
                }

                DataRow dr = merged.NewRow();
                for (int c = 0; c < table.Columns; c++)
                {
                    var cell = table[r, c];
                    Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
                    dr[c] = cell.Text; // Populate DataTable for Excel export
                }
                Console.WriteLine();
                merged.Rows.Add(dr);
            }
            firstTable = false;
            Console.WriteLine(); // Blank line between tables
        }

        // 5️⃣ Optional: Export merged result to Excel
        if (merged.Rows.Count > 0)
        {
            using var wb = new XLWorkbook();
            wb.Worksheets.Add(merged, "ExtractedTables");
            wb.SaveAs("ExtractedTables.xlsx");
            Console.WriteLine("\nExcel file 'ExtractedTables.xlsx' created successfully.");
        }
        else
        {
            Console.WriteLine("\nNo tables were detected in the image.");
        }
    }
}
```

**شرح التدفق**

1. **إعداد المحرك** – يحمل الصورة ويخبر Aspose بالبحث عن الجداول.
2. **ضبط الخيارات** – `DetectTables` يقوم بالعمل الشاق؛ `Deskew` يحسن الدقة في المسحات المائلة.
3. **التعرف** – يُعيد كلًا من النص العادي ومجموعة كائنات `Table`.
4. **التكرار** – يطبع كل خلية مع الثقة، وفي الوقت نفسه يبني `DataTable` للتصدير لاحقًا.
5. **التصدير** – يستخدم `ClosedXML` (مكتبة خفيفة لا تحتاج إلى interop) لكتابة ملف `.xlsx`—مثالي للتحليلات أو التقارير اللاحقة.

## الأسئلة المتكررة

- **هل يعمل هذا مع ملفات PDF؟**  
  نعم. قم أولاً بتحويل كل صفحة PDF إلى صورة (`PdfRenderer` أو `Ghostscript`)، ثم مرر البت ماب إلى Aspose OCR.

- **هل يمكنني استخراج الجداول من ملف JPG؟**  
  بالتأكيد. طريقة `ImageStream.FromFile` تدعم JPEG، PNG، BMP، وTIFF مباشرةً.

- **ماذا لو كان جدولي يحتوي على خلايا مدمجة؟**  
  يتعامل Aspose OCR مع الخلايا المدمجة كخلايا منطقية منفصلة؛ قد تحتاج إلى معالجة لاحقة للجمع بينها بناءً على الثقة أو نمط المحتوى.

- **هل هناك حد لحجم الجدول؟**  
  عمليًا، يدعم المحرك جداول تصل إلى عدة مئات من الصفوف. الأداء يتدهور بصورة خطية، لذا يُفضَّل تقسيم المسحات الكبيرة إلى أجزاء أصغر.

## الخاتمة

لقد أظهرنا لك الآن كيفية 

## ماذا يجب أن تتعلم بعد ذلك؟

- [كيفية استخراج جدول من صورة باستخدام Aspose.OCR لـ .NET](/ocr/english/net/text-recognition/recognize-table/)
- [استخراج النص من الصورة – تحسين OCR باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)
- [كيفية استخراج النص من الصورة عن طريق إعداد المستطيلات في OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}