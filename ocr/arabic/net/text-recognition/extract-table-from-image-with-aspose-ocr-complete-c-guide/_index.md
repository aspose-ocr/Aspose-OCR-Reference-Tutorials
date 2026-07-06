---
category: general
date: 2026-03-18
description: استخراج جدول من صورة باستخدام Aspose OCR في C#. تعلم كيفية تحويل الجدول
  إلى JSON، الحصول على JSON للجدول واستخراج النص من الصورة في دقائق.
draft: false
keywords:
- extract table from image
- convert table to json
- convert image to json
- extract text from image
- get table json
language: ar
og_description: استخراج جدول من صورة باستخدام Aspose OCR في C#. تعلم تحويل الجدول
  إلى JSON، الحصول على JSON للجدول واستخراج النص من الصورة بسرعة.
og_title: استخراج جدول من صورة باستخدام Aspose OCR – دليل كامل بلغة C#
tags:
- Aspose OCR
- C#
- Table Extraction
title: استخراج جدول من صورة باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/text-recognition/extract-table-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج جدول من صورة – دليل C# كامل

هل احتجت يومًا إلى **extract table from image** لكن لم تكن متأكدًا أي مكتبة يمكنها القيام بذلك دون جبل من التحليل اليدوي؟ لست وحدك. في العديد من مشاريع معالجة الفواتير أو مسح الإيصالات، النقطة المؤلمة الحقيقية هي تحويل صورة bitmap صاخبة إلى جدول منظم يمكن لنظامك اللاحق استهلاكه.  

الأخبار السارة؟ باستخدام Aspose OCR يمكنك **convert table to JSON** في بضع أسطر، وستحصل أيضًا على النص العادي للصورة بأكملها، لذا فإن **extract text from image** هو مكافأة. في هذا الدرس سنستعرض العملية بالكامل – من تحميل الصورة إلى الحصول على تمثيل JSON منظم للجدول المكتشف.

> **فوز سريع:** بنهاية الدرس ستحصل على تطبيق C# console قابل للتنفيذ يطبع كلًا من نص OCR الخام وسلسلة JSON يمكنك إدخالها مباشرةً إلى قاعدة بيانات أو API.

## المتطلبات المسبقة

- .NET 6.0 SDK (أو أي نسخة حديثة من .NET) مثبت.  
- رخصة Aspose OCR صالحة أو نسخة تجريبية مجانية (المكتبة تعمل بدون رخصة لكنها تضيف علامة مائية).  
- صورة تحتوي فعليًا على جدول – على سبيل المثال `invoice_table.png`.  
- Visual Studio 2022، VS Code، أو أي محرر تفضله.

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.OCR`.

## الخطوة 1: إعداد المشروع وتثبيت Aspose  OCR

أولاً، أنشئ مشروع console جديد وأدرج مكتبة OCR.

```bash
dotnet new console -n TableJsonDemo
cd TableJsonDemo
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت تستخدم بروكسي مؤسسي، أضف العلامة `--no-restore` وشغّل `dotnet restore` لاحقًا مع المتغيرات البيئية المناسبة.

## الخطوة 2: تهيئة محرك OCR وتمكين التعرف على الجداول

قلب الحل هو `OcrEngine`. من خلال تفعيل `EnableTableRecognition` نخبر Aspose  OCR بالبحث عن هياكل شبيهة بالشبكة بدلاً من معالجة كل شيء كنص عادي.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;

class TableJsonDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable table detection – this is what lets us get a JSON table later
        ocrEngine.Settings.EnableTableRecognition = true;
```

لماذا هذه الخطوة حاسمة؟ بدون التعرف على الجداول، سيقوم المحرك بدمج الصورة في سلسلة واحدة، مما يجعل من المستحيل إعادة بناء الصفوف والأعمدة لاحقًا. تفعيلها يضيف مرحلة تحليل تخطيط خفيفة الوزن لا تكلف الكثير من الأداء لكنها توفر فوائد هائلة للخطوات اللاحقة.

## الخطوة 3: تحميل صورتك وتشغيل التعرف

الآن نوجه المحرك إلى الملف الذي يحتوي على الجدول. `ImageStream.FromFile` يدعم معظم الصيغ الشائعة (PNG، JPEG، TIFF).

```csharp
        // Load the image that contains the table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Perform OCR – this returns an OcrResult object with multiple helpers
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

إذا كانت الصورة كبيرة، فكر في تغيير حجمها أولاً لتسريع المعالجة. Aspose  OCR يكتشف DPI تلقائيًا، لكن مسح بدقة 300 DPI يعتبر نقطة مثالية لمعظم الجداول.

## الخطوة 4: استخراج النص العادي – “extract text from image”

على الرغم من أن هدفنا الرئيسي هو الجدول، إلا أنك غالبًا ما تحتاج إلى النص الخام للتسجيل أو المعالجة الاحتياطية.

```csharp
        // Output the full recognized text
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);
```

خاصية `Text` تجمع كل ما يراه المحرك، مع الحفاظ على فواصل الأسطر. هذا مفيد عندما تحتاج إلى التحقق من أن OCR قرأ العناوين أو التذييلات خارج منطقة الجدول بشكل صحيح.

## الخطوة 5: الحصول على الجدول المكتشف كـ JSON – “convert table to json” & “get table json”

هنا يحدث السحر. `GetTableAsJson()` تسلسل الصفوف والأعمدة ومحتويات الخلايا المكتشفة إلى سلسلة JSON نظيفة.

```csharp
        // Retrieve the table structure as a JSON string
        string tableJson = ocrResult.GetTableAsJson();

        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);
    }
}
```

JSON الناتج يبدو شيئًا مثل هذا (منسق للقراءة):

```json
{
  "Rows": [
    {
      "Cells": [
        { "Text": "Item", "ColumnIndex": 0 },
        { "Text": "Quantity", "ColumnIndex": 1 },
        { "Text": "Price", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget A", "ColumnIndex": 0 },
        { "Text": "10", "ColumnIndex": 1 },
        { "Text": "$5.00", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget B", "ColumnIndex": 0 },
        { "Text": "7", "ColumnIndex": 1 },
        { "Text": "$8.50", "ColumnIndex": 2 }
      ]
    }
  ]
}
```

لماذا JSON هو الصيغة المفضلة؟ إنه مستقل عن اللغة، سهل التفكيك إلى كائنات، ويعمل بشكل رائع مع واجهات برمجة التطبيقات الحديثة. إذا كنت تحتاج إلى CSV بدلاً من ذلك، ما عليك سوى التكرار على الصفوف وربط نصوص الخلايا بفواصل.

## الخطوة 6: (اختياري) تحويل JSON إلى كائن .NET – “convert image to json”

إذا كنت تفضل العمل مع أنواع قوية، فقم بتفكيك JSON باستخدام `System.Text.Json`.

```csharp
using System.Text.Json;

...

        // Deserialize into a C# class (optional)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
```

ستقوم بتعريف `TableModel` و `RowModel` و `CellModel` لتطابق مخطط JSON. تُظهر هذه الخطوة كيف يمكنك الانتقال من **convert image to json** إلى كائن مُعَرَّف، مما يجعل التحقق اللاحق سهلًا.

## مثال كامل يعمل

بجمع كل شيء معًا، إليك البرنامج الكامل الجاهز للتشغيل. احفظه كـ `Program.cs` داخل مجلد المشروع الذي أنشأته مسبقًا.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;
using System.Text.Json;

class TableJsonDemo
{
    static void Main()
    {
        // Step 1: Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable table recognition
        ocrEngine.Settings.EnableTableRecognition = true;

        // Step 3: Load image containing a table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Step 4: Run OCR
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 5: Print full text (extract text from image)
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);

        // Step 6: Get table as JSON (convert table to json, get table json)
        string tableJson = ocrResult.GetTableAsJson();
        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);

        // Optional: Deserialize JSON to C# objects (convert image to json)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
    }
}

// Helper classes matching Aspose's JSON structure
public class TableModel
{
    public RowModel[] Rows { get; set; }
}
public class RowModel
{
    public CellModel[] Cells { get; set; }
}
public class CellModel
{
    public string Text { get; set; }
    public int ColumnIndex { get; set; }
}
```

### النتيجة المتوقعة

عند تشغيل `dotnet run`، يجب أن ترى شيئًا مشابهًا لـ:

```
Full text:
Item Quantity Price
Widget A 10 $5.00
Widget B 7 $8.50

Detected table (JSON):
{
  "Rows":[
    {"Cells":[{"Text":"Item","ColumnIndex":0},{"Text":"Quantity","ColumnIndex":1},{"Text":"Price","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget A","ColumnIndex":0},{"Text":"10","ColumnIndex":1},{"Text":"$5.00","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget B","ColumnIndex":0},{"Text":"7","ColumnIndex":1},{"Text":"$8.50","ColumnIndex":2}]}
  ]
}

First cell value: Item
```

إذا كان الإخراج فارغًا، تحقق مرة أخرى من أن `EnableTableRecognition` مضبوط على `true` وأن الصورة تحتوي فعليًا على خطوط شبكة واضحة.

## الأخطاء الشائعة وكيفية تجنبها

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **No JSON returned** | تم تعطيل اكتشاف الجدول أو الصورة ذات تباين منخفض جدًا. | تأكد من أن `ocrEngine.Settings.EnableTableRecognition = true` وحسّن جودة الصورة (زيادة التباين، تحويل إلى ثنائي). |
| **Partial rows** | الـ OCR ارتبك بسبب الخلايا المدمجة أو النص المدور. | قم بمعالجة مسبقة للصورة: تصحيح الميل (`ImageProcessor.Rotate`) أو تقسيم الخلايا المدمجة يدويًا. |
| **Unicode gibberish** | الخط غير معترف به (مثلاً، مكتوب يدويًا). | بدّل حزم اللغة عبر `ocrEngine.Language = Language.English;` أو استخدم محرك OCR مختلف للكتابة اليدوية. |
| **Performance slowdown** | صورة كبيرة جدًا (>5 MP). | قلل الحجم إلى عرض ~1500 بكسل مع الحفاظ على DPI. |

## الخطوات التالية: تجاوز الأساسيات

الآن بعد أن يمكنك **extract table from image** و **convert table to JSON**، فكر في هذه الإضافات:

- **Persist the JSON** إلى قاعدة بيانات باستخدام Entity Framework.  
- **Post‑process** الـ JSON لتطبيع صيغ العملات (مثلاً، إزالة `$`).  
- **Batch process** مجلد الفواتير باستخدام `Directory.GetFiles` وتوازي التنفيذ عبر `Parallel.ForEach`.  
- **Integrate** مع Azure Functions أو AWS Lambda لإنشاء خطوط معالجة OCR بدون خوادم.

كل من هذه المواضيع بطبيعتها يجلب الكلمات المفتاحية الثانوية الأخرى مثل **convert image to json** (عند إرسال نتيجة OCR بالكامل إلى نقطة سحابية) و **get table json** للتحليلات اللاحقة.

---

### الخاتمة

لقد أظهرنا لك الآن كيفية **extract table from image** باستخدام Aspose  OCR، وتحويل ذلك الجدول إلى JSON نظيف، وحتى تفكيكه إلى كائنات C#. النمط نفسه

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}