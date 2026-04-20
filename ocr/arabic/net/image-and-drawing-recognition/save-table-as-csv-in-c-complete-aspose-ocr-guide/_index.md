---
category: general
date: 2026-03-02
description: احفظ الجدول كملف CSV باستخدام Aspose OCR في C#. تعلّم كيفية استخراج الجدول
  من صورة، وكيفية استخراج بيانات الجدول، وتحويل الجدول إلى CSV في دقائق.
draft: false
keywords:
- save table as csv
- how to extract table
- ocr table extraction
- convert table to csv
- image table to csv
language: ar
og_description: احفظ الجدول كملف CSV باستخدام Aspose OCR. يوضح هذا الدليل خطوة بخطوة
  كيفية استخراج جدول من صورة وتحويله إلى CSV بسهولة.
og_title: حفظ الجدول كملف CSV في C# – دليل Aspose OCR الكامل
tags:
- OCR
- C#
- CSV
- Aspose
title: حفظ الجدول كملف CSV في C# – دليل Aspose OCR الكامل
url: /ar/net/image-and-drawing-recognition/save-table-as-csv-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حفظ الجدول كملف CSV في C# – دليل Aspose OCR الكامل

هل تساءلت يومًا كيف **تحفظ الجدول كملف CSV** عندما يكون لديك فقط فاتورة ممسوحة ضوئيًا أو لقطة شاشة لجدول بيانات؟ لست وحدك. في العديد من المشاريع الواقعية، تكون بيانات المصدر مخزنة في صور، وتحويل تلك البيانات إلى صيغة قابلة للقراءة آليًا يبدو كعملية صعبة.  

الأخبار السارة؟ باستخدام Aspose.OCR يمكنك **استخراج الجدول**، تحويله إلى `DataTable`، ثم **تحويل الجدول إلى CSV** ببضع أسطر فقط. في هذا الدليل سنستعرض العملية بالكامل، نجيب على أسئلة *كيفية استخراج الجدول*، ونظهر لك مثالًا جاهزًا للتنفيذ يمكنك وضعه في أي مشروع .NET.

## ما ستحصل عليه

- صورة واضحة عن **استخراج جدول OCR** باستخدام Aspose.OCR.  
- مقتطف C# كامل وقابل للتنفيذ يحمل صورة، يستخرج الجدول، ويكتب ملف CSV.  
- نصائح للتعامل مع الحالات الخاصة مثل الخلايا الفارغة، المسح متعدد الصفحات، والفواصل المختلفة.  
- أفكار للخطوات التالية، مثل إدخال CSV في قاعدة بيانات أو توصيله بمحرك تقارير.

### المتطلبات المسبقة (نعم، تحتاج إلى بعض الأشياء)

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6.0 أو أحدث | ميزات لغة حديثة وأداء أفضل |
| حزمة NuGet الخاصة بـ Aspose.OCR (`Aspose.OCR`) | توفر `OcrEngine` واكتشاف الجداول |
| ملف صورة يحتوي على جدول واضح (PNG, JPG, إلخ) | مصدر البيانات التي سنستخرجها |
| معرفة أساسية بـ C# | لتعديل المثال وفقًا لسيناريوك الخاص |

إذا كان أي من هذه غير مألوف لك، فقط احصل على أحدث .NET SDK من Microsoft وقم بتثبيت حزمة NuGet باستخدام `dotnet add package Aspose.OCR`. لا توجد مكتبات خارجية أخرى مطلوبة.

![Diagram showing how to save table as csv using Aspose OCR](image-placeholder.png "save table as csv diagram")

## الخطوة 1: تحميل الصورة التي تحتوي على الجدول

أولاً وقبل كل شيء—نحتاج إلى `Bitmap` يشير إلى الملف على القرص. فئة `Bitmap` موجودة في `System.Drawing`، وهي جزء من بيئة تشغيل .NET.

```csharp
using System.Drawing;

// Replace with the actual path to your image
string imagePath = @"C:\Invoices\invoice_table.png";
Bitmap bitmapImage = new Bitmap(imagePath);
```

**لماذا هذه الخطوة؟**  
محرك OCR يعمل على بيانات البكسل الخام، وليس على مسارات الملفات. بإنشاء `Bitmap` نعطي Aspose تمثيلًا نظيفًا للصور في الذاكرة. إذا كانت الصورة تالفة أو المسار غير صحيح، ستظهر استثناء هنا—لذا تحقق من الموقع جيدًا.

## الخطوة 2: تكوين محرك OCR لاكتشاف الجداول

يمكن لـ Aspose.OCR التعرف على النص العادي، لكننا نريد منه البحث عن الجداول. ضبط `DetectTables = true` يخبر المحرك بالبحث عن خطوط الشبكة وحدود الخلايا.

```csharp
using Aspose.OCR;

// Create the OCR engine with table detection enabled
OcrEngine ocrEngine = new OcrEngine
{
    DetectTables = true,
    Language = OcrLanguage.English   // Change if your table is in another language
};
```

**لماذا تمكين `DetectTables`؟**  
عند إيقاف هذا العلم، يعيد المحرك سلسلة نصية طويلة تفقد هيكل الصف/العمود. عندما يكون مفعلاً، يبني المحرك `DataTable` داخليًا، محافظًا على التخطيط الدقيق للصورة المصدر.

## الخطوة 3: استخراج الجدول إلى DataTable

الآن يحدث السحر. `ExtractTable` تُعيد `System.Data.DataTable` يمكنك التعامل معها كأي جدول آخر في .NET.

```csharp
using System.Data;

// Extract the table from the bitmap
DataTable extractedTable = ocrEngine.ExtractTable(bitmapImage);
```

**ما ستحصل عليه:**  
- رؤوس الأعمدة (إذا تعرف OCR عليها).  
- صفوف مملوءة بقيم نصية.  
- الخلايا الفارغة تصبح `DBNull.Value`، وسنتعامل معها لاحقًا.

> **نصيحة احترافية:** إذا احتوت الصورة على جداول متعددة، فإن `ExtractTable` سيعيد الجدول الأول فقط. لمعالجة البقية، سيتعين عليك قص الـ bitmap وتشغيل المحرك مرة أخرى.

## الخطوة 4: كتابة DataTable إلى ملف CSV

CSV هو مجرد نص عادي مع فواصل (أو فاصل آخر) تفصل الحقول. سنقوم ببث الصفوف إلى ملف، مع معالجة القيم `null` بلطف.

```csharp
using System.IO;

// Destination CSV path
string csvPath = @"C:\Invoices\invoice.csv";

using (var writer = new StreamWriter(csvPath))
{
    // Optional: write a header line if you want column names
    writer.WriteLine(string.Join(",", extractedTable.Columns
                                            .Cast<DataColumn>()
                                            .Select(col => EscapeCsv(col.ColumnName))));

    // Write each row
    foreach (DataRow row in extractedTable.Rows)
    {
        var fields = row.ItemArray.Select(item => EscapeCsv(item?.ToString() ?? string.Empty));
        writer.WriteLine(string.Join(",", fields));
    }
}

// Helper to escape commas, quotes, and newlines per CSV spec
static string EscapeCsv(string field)
{
    if (field.Contains(',') || field.Contains('\"') || field.Contains('\n'))
    {
        field = $"\"{field.Replace("\"", "\"\"")}\"";
    }
    return field;
}
```

**لماذا أداة المساعدة `EscapeCsv`؟**  
إذا احتوت خلية على فاصلة أو سطر جديد، فإن الجمع البسيط سيكسر بنية CSV. تغليف هذه الحقول بعلامات اقتباس مزدوجة (وتعقيم الاقتباسات الداخلية) يحافظ على صحة الملف.

## الخطوة 5: التحقق من النتيجة

بعد انتهاء البرنامج، افتح `invoice.csv` في أي محرر جداول. يجب أن ترى صفوفًا وأعمدة تعكس الصورة الأصلية.

```text
Item,Quantity,Price
Widget A,10,9.99
Widget B,5,19.95
Total,,149.85
```

إذا كان الناتج يبدو متعرجًا أو بعض الخلايا فارغة، فكر في هذه التعديلات:

- **زيادة دقة الصورة** قبل تمريرها إلى OCR (مثلاً، `bitmapImage.SetResolution(300, 300)`).  
- **معالجة مسبقة للصورة** (تحويل إلى ثنائي، تصحيح الميل) باستخدام System.Drawing أو مكتبة صور مخصصة.  
- **ضبط إعدادات اللغة** إذا كان الجدول يحتوي على أحرف غير إنجليزية.

## أسئلة شائعة وحالات خاصة

### كيف تستخرج الجدول عندما تحتوي الصورة على صفحات متعددة؟

> **الإجابة:** كرر العملية عبر كل صفحة من ملف PDF أو TIFF متعدد الصفحات، حوّل كل صفحة إلى `Bitmap`، ثم نفّذ خطوات الاستخراج بشكل منفصل. أضف كل `DataTable` ناتج إلى جدول رئيسي قبل كتابة CSV.

### ماذا لو احتجت إلى فاصل مختلف (مثلاً؛)؟

ما عليك سوى استبدال `","` في استدعاءات `string.Join` بـ `";"` وتعديل منطق `EscapeCsv` وفقًا لذلك. بعض المناطق تفضّل `;` لأن الفاصل العشري هو الفاصلة.

### هل يمكنني تخطي صف العنوان؟

إذا لم تتضمن الصورة المصدر رؤوسًا، علق كتلة كتابة العنوان:

```csharp
// writer.WriteLine(...); // Skip this line to omit column names
```

### هل يعمل هذا مع صور PDF؟

يمكن لـ Aspose.OCR قبول `Bitmap` مشتق من صفحة PDF. استخدم `Aspose.Pdf` لتحويل صفحة PDF إلى bitmap أولًا، ثم مرّرها إلى محرك OCR.

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

فيما يلي البرنامج بالكامل، جاهز للترجمة إلى تطبيق Console.

```csharp
using System;
using System.Data;
using System.Drawing;
using System.IO;
using System.Linq;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the image that contains the table
        string imagePath = @"C:\Invoices\invoice_table.png";
        using Bitmap bitmapImage = new Bitmap(imagePath);

        // 2️⃣ Configure OCR for table detection
        OcrEngine ocrEngine = new OcrEngine
        {
            DetectTables = true,
            Language = OcrLanguage.English
        };

        // 3️⃣ Extract the table into a DataTable
        DataTable extractedTable = ocrEngine.ExtractTable(bitmapImage);

        // 4️⃣ Write the DataTable to CSV
        string csvPath = @"C:\Invoices\invoice.csv";
        using (var writer = new StreamWriter(csvPath))
        {
            // Write column headers
            writer.WriteLine(string.Join(",", extractedTable.Columns
                                                .Cast<DataColumn>()
                                                .Select(col => EscapeCsv(col.ColumnName))));

            // Write each row
            foreach (DataRow row in extractedTable.Rows)
            {
                var fields = row.ItemArray.Select(item => EscapeCsv(item?.ToString() ?? string.Empty));
                writer.WriteLine(string.Join(",", fields));
            }
        }

        // 5️⃣ Inform the user
        Console.WriteLine("Table extracted and saved as CSV.");
    }

    // Helper to escape CSV fields
    static string EscapeCsv(string field)
    {
        if (field.Contains(',') || field.Contains('\"') || field.Contains('\n'))
        {
            field = $"\"{field.Replace("\"", "\"\"")}\"";
        }
        return field;
    }
}
```

شغّل البرنامج (`dotnet run`)، وستظهر لك رسالة تأكيد. سيقع ملف CSV بجوار صورتك، جاهزًا للاستيراد إلى Excel أو Power BI أو أي نظام لاحق.

## الخلاصة

لقد عرضنا للتو **كيفية استخراج بيانات الجدول** من صورة، وأجرينا **استخراج جدول OCR**، وأخيرًا **تحويل الجدول إلى CSV**—كل ذلك مع الحفاظ على نظافة الكود وشرح شامل. الخلاصة الأساسية هي أن Aspose.OCR يجعل مهمة تحويل *جدول صورة إلى CSV* التي كانت صعبة سابقًا عملية تتطلب بضع أسطر فقط.

### ما الخطوات التالية؟

- **معالجة دفعات:** غلف المنطق داخل حلقة `foreach` لمعالجة عشرات الفواتير دفعة واحدة.  
- **استيراد إلى قاعدة بيانات:** استخدم `SqlBulkCopy` لدفع CSV مباشرة إلى SQL Server.  
- **تحليل متقدم:** إذا احتوت جداولك على خلايا مدمجة، فكر في معالجة `DataTable` لاحقًا لتطبيع عدد الأعمدة.

لا تتردد في التجربة—غيّر الفاصل، أضف سجلات، أو دمج مع واجهة ويب API تستقبل الصور مباشرة. السماء هي الحد، والآن لديك أساس قوي لأي سير عمل **حفظ جدول كملف CSV**.

برمجة سعيدة، ولتكن ملفات CSV دائمًا مرتبة تمامًا!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}