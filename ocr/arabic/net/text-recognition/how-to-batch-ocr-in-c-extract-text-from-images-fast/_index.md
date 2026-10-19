---
category: general
date: 2026-03-21
description: كيفية تنفيذ OCR دفعي في C# بسهولة—تعلم استخراج النص من الصور، تحويل الصور
  إلى نص، وحفظ OCR كنص مع إعدادات اللغة.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert images to text
- save OCR as text
- set OCR language
language: ar
og_description: كيف تقوم بعملية OCR دفعة واحدة في C# يتيح لك استخراج النص من الصور،
  تحويل الصور إلى نص، وحفظ OCR كنص مع تعيين لغة OCR بسهولة.
og_title: كيفية تنفيذ OCR دفعيًا في C# – دليل سريع
tags:
- OCR
- C#
- Aspose
title: كيفية تنفيذ OCR دفعيًا في C# – استخراج النص من الصور بسرعة
url: /ar/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعيًا في C# – استخراج النص من الصور بسرعة

هل تساءلت يومًا **كيف تقوم بعملية OCR دفعيًا** عندما يكون لديك مئات الصور مخزنة في مجلد؟ لست وحدك—المطورون يسألون باستمرار كيف يمكن استخراج النص من الصور دون كتابة حلقة لكل ملف. الخبر السار هو أن Aspose.OCR يزودك بطريقة نظيفة وجاهزة للتوازي **لتحويل الصور إلى نص** في بضع أسطر فقط من C#.

في هذا الدرس سنستعرض مثالًا كاملًا وجاهزًا للتنفيذ يوضح لك كيفية **حفظ OCR كنص**، اختيار اللغة المناسبة، وتفعيل المعالجة المتوازية للسرعة. في النهاية ستحصل على حل مستقل يمكنك إدراجه في أي مشروع .NET.

## ما ستحتاجه

- .NET 6 أو أحدث (واجهة برمجة التطبيقات تعمل مع .NET Core و .NET Framework)
- Aspose.OCR لـ .NET (حزمة NuGet `Aspose.OCR`)
- مجلد يحتوي على الصور التي تريد معالجتها (PNG، JPEG، TIFF، إلخ)
- قليل من الفضول حول البرمجة المتوازية (اختياري، لكنه مفيد)

لا خدمات إضافية، لا مفاتيح سحابية—فقط كود C# نقي يعمل محليًا.

---

![تدفق عمل OCR دفعي](placeholder.png){alt="مخطط تدفق عمل OCR دفعي"}

## الخطوة 1: إعداد المشروع وتثبيت Aspose.OCR

أولًا، أنشئ تطبيقًا من نوع console (أو استخدم تطبيقًا موجودًا) وأضف حزمة Aspose.OCR:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

**نصيحة احترافية:** إذا كنت تستخدم Visual Studio، انقر بزر الماوس الأيمن على المشروع → *Manage NuGet Packages* → ابحث عن *Aspose.OCR* وقم بتثبيت أحدث نسخة مستقرة.

هذا يمنحك الوصول إلى `OcrBatchProcessor` و `OcrEngineSettings` والعدد `Language`.

## الخطوة 2: تعريف مجلدات الإدخال والإخراج

يحتاج معالج الدفعة إلى معرفة مكان وجود الصور المصدر وأين يجب كتابة ملفات النص المستخرجة. احتفظ بالمسارات مطلقة أو نسبية إلى جذر المشروع—فقط تأكد من وجود المجلدات قبل تشغيل الكود.

```csharp
var inputPath  = @"C:\MyImages\BatchInput";
var outputPath = @"C:\MyImages\BatchResults";

// Ensure the output directory exists
if (!Directory.Exists(outputPath))
    Directory.CreateDirectory(outputPath);
```

**لماذا هذا مهم:** إذا كان مجلد الإخراج غير موجود سيتسبب المعالج في رمي استثناء، مما يقطع الدفعة بأكملها. إن إنشائه مسبقًا يضمن تشغيلًا سلسًا.

## الخطوة 3: تكوين إعدادات OCR (بما في ذلك اللغة)

هنا تقوم **بتحديد لغة OCR** للدفعة بأكملها. يدعم Aspose.OCR عشرات اللغات؛ اللغة الإنجليزية هي الافتراضية، لكن يمكنك التبديل إلى الفرنسية أو الإسبانية، إلخ، عن طريق تغيير قيمة العدد `Language`.

```csharp
var ocrSettings = new OcrEngineSettings
{
    Language = Language.English   // Change to Language.French, Language.Spanish, etc.
};
```

إذا احتجت يومًا إلى معالجة لغات مختلفة لكل صورة، يمكنك لاحقًا تجاوز هذا الإعداد لكل ملف—سنتحدث عن ذلك لاحقًا.

## الخطوة 4: بناء كائن `OcrBatchProcessor`

الآن نجمع كل شيء معًا. يتيح لك `OcrBatchProcessor` تحديد مجلد الإدخال، مجلد الإخراج، تنسيق الإخراج، خيارات التوازي، والإعدادات المشتركة التي أنشأناها للتو.

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System.Threading.Tasks;

var batch = new OcrBatchProcessor
{
    InputFolder   = inputPath,
    OutputFolder  = outputPath,
    OutputFormat  = OcrOutputFormat.PlainText, // **save OCR as text** in .txt files
    ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 }, // up to 4 threads
    Settings = ocrSettings
};
```

**لماذا التوازي؟** عندما يكون لديك عشرات أو مئات الصور، يمكن أن يكون معالجتها واحدةً تلو الأخرى بطيئًا جدًا. ضبط `MaxDegreeOfParallelism` إلى 4 يسمح للوقت التشغيل باستخدام أربعة أنوية CPU في آنٍ واحد، مما يقلل الوقت الكلي بشكل كبير على محطة عمل عادية.

## الخطوة 5: تشغيل عملية الدفعة

مع تكوين المعالج، يصبح التنفيذ استدعاءً واحدًا للطريقة. تتولى المكتبة عد الملفات، OCR، وكتابة النتائج تلقائيًا.

```csharp
batch.Execute();
Console.WriteLine("Batch OCR completed.");
```

عند طباعة وحدة التحكم *“Batch OCR completed.”* ستجد ملفًا `.txt` بجوار كل صورة أصلية داخل `BatchResults`. يحتوي كل ملف نصي على الأحرف الخام المستخرجة من صورته المصدر—وهو بالضبط ما تحتاجه **لاستخراج النص من الصور** للمعالجة اللاحقة.

### النتيجة المتوقعة

```
C:\MyImages\BatchResults\image1.txt
C:\MyImages\BatchResults\image2.txt
...
```

افتح أيًا من هذه الملفات وسترى تمثيل النص العادي لمحتوى الصورة.

## الخطوة 6: التحقق من النتائج (اختياري)

من العادات الجيدة التحقق مرتين من بعض الملفات للتأكد من أن OCR تم كما هو متوقع. طريقة سريعة هي قراءة السطر الأول من كل ملف تم إنشاؤه وطباعةه إلى وحدة التحكم:

```csharp
foreach (var txtFile in Directory.GetFiles(outputPath, "*.txt"))
{
    var firstLine = File.ReadLines(txtFile).FirstOrDefault();
    Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
}
```

إذا لاحظت أحرفًا مشوشة، فكر في تغيير إعداد `Language` أو تعديل جودة الصورة (مثلاً، زيادة DPI، التحويل إلى تدرج الرمادي).

## تنويعات متقدمة وحالات حافة

### 1. تجاوز اللغة لكل ملف

أحيانًا تحتوي الدفعة على مستندات متعددة اللغات. يمكنك فحص اسم كل صورة وتعيين لغة في الوقت الفعلي:

```csharp
batch.Settings = new OcrEngineSettings(); // default settings

batch.FileProcessing += (sender, args) =>
{
    if (args.FileName.Contains("_fr"))
        args.Settings.Language = Language.French;
    else if (args.FileName.Contains("_es"))
        args.Settings.Language = Language.Spanish;
    // otherwise keep the default (English)
};
```

### 2. تنسيقات إخراج مختلفة

إذا كنت تحتاج إلى ملفات PDF قابلة للبحث بدلاً من النص العادي، غيّر `OutputFormat`:

```csharp
batch.OutputFormat = OcrOutputFormat.SearchablePdf;
```

سيؤدي ذلك إلى **تحويل الصور إلى نص** داخل حاوية PDF، مع الحفاظ على التخطيط الأصلي.

### 3. معالجة الصور الكبيرة

الصور ذات الدقة العالية جدًا قد تستهلك الذاكرة. للحفاظ على خفة العملية، فعّل تقليل دقة الصورة:

```csharp
batch.Settings.Dpi = 300; // lowers internal processing DPI
```

### 4. تسجيل الأخطاء

المعالج يرمي استثناءات للملفات غير القابلة للقراءة. غلف `Execute` بكتلة try/catch وسجّل أسماء الملفات التي تواجه مشكلة:

```csharp
try
{
    batch.Execute();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {ex.Data["FileName"]}: {ex.Message}");
}
```

## مثال كامل يعمل

بجمع كل شيء معًا، إليك البرنامج الكامل الجاهز للنسخ واللصق:

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System;
using System.IO;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 1️⃣ Input & output locations
        var inputFolder  = @"C:\MyImages\BatchInput";
        var outputFolder = @"C:\MyImages\BatchResults";

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ OCR settings – set OCR language
        var ocrSettings = new OcrEngineSettings
        {
            Language = Language.English // change as needed
        };

        // 3️⃣ Configure the batch processor
        var batch = new OcrBatchProcessor
        {
            InputFolder    = inputFolder,
            OutputFolder   = outputFolder,
            OutputFormat   = OcrOutputFormat.PlainText, // **save OCR as text**
            ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 },
            Settings       = ocrSettings
        };

        // 4️⃣ Run the batch job
        batch.Execute();

        // 5️⃣ Confirmation message
        Console.WriteLine("Batch OCR completed.");

        // 6️⃣ (Optional) Quick verification of a few results
        foreach (var txtFile in Directory.GetFiles(outputFolder, "*.txt").Take(5))
        {
            var firstLine = File.ReadLines(txtFile).FirstOrDefault();
            Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
        }
    }
}
```

احفظ هذا كـ `Program.cs`، ابنِ المشروع، وشغّل `dotnet run`. سترى مخرجات وحدة التحكم التي تؤكد الانتهاء، تليها معاينة قصيرة للنص المستخرج.

## الخلاصة

لقد غطينا للتو **كيفية تنفيذ OCR دفعيًا** في C# باستخدام Aspose.OCR، موضحين لك كيفية **استخراج النص من الصور**، **تحويل الصور إلى نص**، و**حفظ OCR كنص** مع **تحديد لغة OCR** لتتناسب مع محتواك. المثال يعمل بالكامل، يتضمن معالجة متوازية للسرعة، ويوفر نقاط توصيل لسيناريوهات متقدمة مثل تجاوز اللغة لكل ملف أو إخراج PDF.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال `OcrOutputFormat.PlainText` بـ `SearchablePdf` وشاهد مدى سهولة إنشاء ملفات PDF قابلة للبحث. أو جرّب قيمًا مختلفة لـ `MaxDegreeOfParallelism` لاستخراج كل مللي ثانية على جهاز متعدد النوى.

إذا واجهت أي مشاكل، تحقق مرة أخرى من مسارات المجلدات، تأكد من أن الصور قابلة للقراءة، وتأكد من أن عدد اللغة يتطابق مع النص في صورك. برمجة سعيدة، ولتكن دفعات OCR سريعة ودقيقة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}