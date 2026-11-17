---
category: general
date: 2026-04-04
description: كيفية تنفيذ التعرف الضوئي على الأحرف (OCR) على دفعات باستخدام Aspose.OCR
  في C#. تعلم استخراج النص من الصور، وتصدير ملخصات CSV، والتعامل مع OCR للصور الضخمة
  بكفاءة.
draft: false
keywords:
- how to batch ocr
- extract text images
- how to export csv
- bulk image ocr
- batch ocr images
language: ar
og_description: كيفية تنفيذ التعرف الضوئي على الحروف (OCR) دفعةً في C# باستخدام Aspose.OCR.
  احصل على الحل الكامل لاستخراج النص من الصور وتصدير ملخصات CSV.
og_title: كيفية تنفيذ OCR دفعيًا في C# – دليل خطوة بخطوة كامل
tags:
- OCR
- C#
- Aspose
- Automation
title: كيفية تنفيذ OCR دفعيًا في C# – دليل شامل لاستخراج النص من الصور بالجملة
url: /ar/net/text-recognition/how-to-batch-ocr-in-c-complete-guide-for-bulk-image-text-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعيًا – دليل C# شامل

هل تساءلت يومًا **كيف تقوم بعمل OCR دفعي** لمجلد كامل من الصور دون كتابة روتين منفصل لكل ملف؟ لست وحدك. في العديد من المشاريع الواقعية—مثل معالجة الفواتير، أرشفة الكتب الممسوحة ضوئيًا، أو تحويل الإيصالات إلى نصوص على نطاق واسع—يحتاج المطورون إلى طريقة سريعة وموثوقة لاستخراج النص من العشرات أو حتى آلاف الصور.

في هذا الدليل سنستعرض مثالًا كاملًا جاهزًا للتنفيذ يوضح **كيفية تنفيذ OCR دفعيًا**، **استخراج نص الصور**، و**تصدير ملخص CSV** باستخدام Aspose.OCR. في النهاية ستحصل على برنامج C# واحد يمكنه معالجة أي دليل يحتوي على صور، تحويلها إلى ملفات نصية قابلة للبحث، وتزويدك بتقرير CSV أنيق عن العملية. لا أسرار، فقط كود واضح ونصائح عملية.

## ما ستتعلمه

- إعداد محرك Aspose.OCR للغة الإنجليزية (أو أي لغة مدعومة).  
- معالجة مجلد كامل من الصور دفعة واحدة—مثالي لـ OCR على نطاق واسع.  
- حفظ كل نتيجة OCR كملف `.txt` مع إمكانية إنشاء ملف CSV يسرد كل صورة مصدر وطول النص المستخرج.  
- التعامل مع الحالات الشائعة مثل أنواع الملفات غير المدعومة، المجلدات الفارغة، وحروف Unicode.

**المتطلبات المسبقة** – تحتاج إلى .NET 6+ (أو .NET Framework 4.7.2+)، Visual Studio 2022 أو أي بيئة تطوير تفضلها، ورخصة صالحة لـ Aspose.OCR (الإصدار التجريبي المجاني يكفي للعرض). لا توجد مكتبات طرف ثالث أخرى مطلوبة.

![how to batch ocr diagram](https://example.com/ocr-flow.png "how to batch ocr flow diagram")

## الخطوة 1: تثبيت Aspose.OCR وإنشاء مشروع Console جديد

للبدء، أضف حزمة Aspose.OCR من NuGet إلى مشروعك:

```bash
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، يمكنك أيضًا النقر بزر الماوس الأيمن على المشروع → *Manage NuGet Packages* → البحث عن *Aspose.OCR* → التثبيت.

أنشئ تطبيق console جديد (`dotnet new console -n BulkOcrDemo`) وافتح `Program.cs`. سيكون هذا هو موطن كل الكود الخاص بنا.

## الخطوة 2: تهيئة محرك OCR – اختيار اللغة المناسبة

يحتاج محرك OCR إلى معرفة اللغة التي يجب البحث عنها. الإنجليزية هي الأكثر شيوعًا، لكن يمكنك استبدالها بالإسبانية أو الفرنسية، إلخ، عن طريق تغيير `Language.English`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

// Step 2: Set up the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // You can switch to Language.Spanish, Language.French, etc.
    Language = Language.English
};
```

**لماذا هذا مهم:** تحديد اللغة يحسن الدقة لأن المحرك يمكنه تطبيق القواميس ومجموعات الأحرف الخاصة بتلك اللغة. إذا تخطيت هذه الخطوة، ستحصل على نموذج عام قد يخطئ في تفسير الأحرف.

## الخطوة 3: تعريف مسارات المصدر، المخرجات، وملف CSV الاختياري

نحتاج إلى ثلاثة مجلدات:

| Path | Purpose |
|------|---------|
| `sourceFolder` | حيث توجد الصور الأصلية. |
| `outputFolder` | حيث سيتم حفظ كل نتيجة OCR (`.txt`). |
| `csvSummaryPath` | (اختياري) ملف CSV يسجل اسم كل صورة وطول النص المستخرج. |

```csharp
// Step 3: Folder locations – update these to match your environment
string sourceFolder = @"C:\OcrDemo\Images\Bulk";
string outputFolder = @"C:\OcrDemo\Output\BulkResults";
string csvSummaryPath = Path.Combine(outputFolder, "summary.csv"); // optional
```

> **نصيحة:** استخدم `Path.Combine` لضمان التوافق عبر الأنظمة؛ فهو يضيف الفاصل المناسب تلقائيًا.

## الخطوة 4: تشغيل المعالج الدفعي

تأتي Aspose.OCR مع `BatchProcessor` المفيد الذي يقوم بالعمل الشاق. فهو يتنقل عبر كل صورة مدعومة (`.png`, `.jpg`, `.tif`, إلخ)، ينفذ OCR، ويكتب النتيجة.

```csharp
// Step 4: Process the entire folder
BatchProcessor.ProcessFolder(
    sourceFolder: sourceFolder,
    outputFolder: outputFolder,
    engine: ocrEngine,
    csvSummaryPath: csvSummaryPath);
```

### ما الذي يحدث في الخلفية؟

1. **اكتشاف الملفات** – يقوم المعالج بمسح `sourceFolder` للعثور على ملفات الصور.  
2. **تنفيذ OCR** – تُمرَّر كل صورة إلى `ocrEngine`.  
3. **حفظ النص** – يُكتب النص المعترف به إلى ملف `.txt` يحمل نفس الاسم الأساسي في `outputFolder`.  
4. **تسجيل CSV** – إذا تم توفير `csvSummaryPath`، يضيف المعالج سطرًا: `ImageName,CharactersExtracted,ProcessingTimeMs`.

## الخطوة 5: إضافة معالجة الأخطاء ودعم الحالات الطرفية

يجب أن يتحمل برنامج الدفعة القوي ملفات مفقودة، صيغ غير مدعومة، ومجلدات فارغة. غلف استدعاء المعالجة داخل كتلة `try/catch` وتحقق من صحة المدخلات أولًا.

```csharp
try
{
    // Validate folders
    if (!Directory.Exists(sourceFolder))
        throw new DirectoryNotFoundException($"Source folder not found: {sourceFolder}");

    Directory.CreateDirectory(outputFolder); // ensures output exists

    // Optional: clean previous CSV
    if (File.Exists(csvSummaryPath))
        File.Delete(csvSummaryPath);

    // Run the batch
    BatchProcessor.ProcessFolder(
        sourceFolder: sourceFolder,
        outputFolder: outputFolder,
        engine: ocrEngine,
        csvSummaryPath: csvSummaryPath);

    Console.WriteLine("✅ Batch OCR completed successfully!");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❌ An error occurred: {ex.Message}");
}
```

**لماذا نضيف ذلك؟** بدون التحقق، قد يفشل البرنامج بصمت، تاركًا لك مجلد مخرجات فارغ ولا فكرة عن السبب. الرسائل الواضحة تجعل عملية التصحيح سهلة.

## الخطوة 6: التحقق من النتائج – ما الذي تتوقعه

بعد انتهاء التنفيذ، افتح `outputFolder`. يجب أن ترى ملف `.txt` لكل صورة:

```
C:\OcrDemo\Output\BulkResults\invoice_001.txt
C:\OcrDemo\Output\BulkResults\receipt_2023-03-15.txt
...
```

كل ملف يحتوي على ناتج OCR الخام—نص عادي يمكنك إرساله إلى فهارس البحث، قواعد البيانات، أو خطوط معالجة لغة طبيعية أخرى.

إذا قمت بتوفير `csvSummaryPath`، افتح `summary.csv`. سيظهر لك شيء مشابه لـ:

```
ImageName,CharactersExtracted,ProcessingTimeMs
invoice_001.png,1245,312
receipt_2023-03-15.jpg,378,98
...
```

ملف CSV يجعل من السهل إنشاء تقارير، اكتشاف النتائج القصيرة غير المعتادة (فشل محتمل في المسح)، أو إمداد مقاييس إلى لوحات مراقبة.

## الخطوة 7: توسيع الحل – تنويعات شائعة

### 7.1 تغيير صيغة الإخراج

بدلاً من `.txt` العادي، قد ترغب في PDF أو JSON. يتيح لك `BatchProcessor` توفير رد نداء مخصص:

```csharp
BatchProcessor.ProcessFolder(
    sourceFolder,
    outputFolder,
    ocrEngine,
    csvSummaryPath,
    (imagePath, ocrResult) =>
    {
        // Example: save as JSON
        var json = System.Text.Json.JsonSerializer.Serialize(new { Text = ocrResult.Text });
        string jsonPath = Path.ChangeExtension(Path.Combine(outputFolder,
                              Path.GetFileNameWithoutExtension(imagePath)), ".json");
        File.WriteAllText(jsonPath, json);
    });
```

### 7.2 معالجة لغات متعددة

إذا كان مجلدك يحتوي على مستندات متعددة اللغات، يمكنك اكتشاف اللغة لكل صورة أو إجراء تمريرين:

```csharp
ocrEngine.Language = Language.Spanish; // first pass
BatchProcessor.ProcessFolder(...);
ocrEngine.Language = Language.English; // second pass
BatchProcessor.ProcessFolder(...);
```

### 7.3 تخطي الملفات الفاسدة بأناقة

أضف مرشحًا داخل الحلقة (أو استخدم النسخة التي تقبل شرطًا) لتجاهل الملفات التي تُثير استثناءً:

```csharp
BatchProcessor.ProcessFolder(
    sourceFolder,
    outputFolder,
    ocrEngine,
    csvSummaryPath,
    filter: path => !Path.GetFileName(path).StartsWith("ignore_"));
```

## مثال كامل يعمل

فيما يلي ملف `Program.cs` الكامل يمكنك نسخه‑ولصقه في مشروع console جديد. استبدل مسارات المجلدات بالمسارات الخاصة بك.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BulkOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine – set language to English
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Define folders – adjust these for your environment
            string sourceFolder = @"C:\OcrDemo\Images\Bulk";
            string outputFolder = @"C:\OcrDemo\Output\BulkResults";
            string csvSummaryPath = Path.Combine(outputFolder, "summary.csv"); // optional

            try
            {
                // 3️⃣ Validate folders
                if (!Directory.Exists(sourceFolder))
                    throw new DirectoryNotFoundException($"Source folder not found: {sourceFolder}");

                Directory.CreateDirectory(outputFolder); // creates if missing

                // 4️⃣ Clean previous CSV (optional)
                if (File.Exists(csvSummaryPath))
                    File.Delete(csvSummaryPath);

                // 5️⃣ Run the batch OCR
                BatchProcessor.ProcessFolder(
                    sourceFolder: sourceFolder,
                    outputFolder: outputFolder,
                    engine: ocrEngine,
                    csvSummaryPath: csvSummaryPath);

                Console.WriteLine("✅ Batch OCR completed successfully!");
                Console.WriteLine($"📂 Text files are in: {outputFolder}");
                Console.WriteLine($"📄 CSV summary (if requested) at: {csvSummaryPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ An error occurred during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### ناتج الـ Console المتوقع

```
✅ Batch OCR completed successfully!
📂 Text files are in: C:\OcrDemo\Output\BulkResults
📄 CSV summary (if requested) at: C:\OcrDemo\Output\BulkResults\summary.csv
```

افتح أحد ملفات `.txt` التي تم إنشاؤها وسترى النص المستخرج، جاهزًا للمعالجة الإضافية.

## الأسئلة المتكررة

**هل يعمل هذا مع ملفات PDF؟**  
يمكن لـ Aspose.OCR معالجة صفحات PDF إذا قمت أولًا بتحويلها إلى صور (مثلاً باستخدام Aspose.PDF). المعالج الدفعي نفسه يبحث فقط عن صيغ الصور النقطية.

**ماذا لو احتجت لمعالجة 10,000 صورة؟**  
يقوم `BatchProcessor` المدمج بقراءة كل ملف على حدة، لذا يبقى استهلاك الذاكرة منخفضًا. للعبء الضخم يمكنك معالجة المجلدات الفرعية بشكل متوازي، لكن تذكر أن OCR يستهلك الكثير من CPU—راقب عدد الأنوية المتاحة.

**هل يمكنني تعديل إعدادات دقة OCR؟**  
نعم. يتيح لك `ocrEngine` ضبط خصائص مثل `Resolution` و `PreprocessOptions`. تعديلها قد يحسن النتائج على المسحات منخفضة الجودة، لكن على حساب السرعة.

**كيف أُرخص Aspose.OCR للإنتاج؟**  
ضع ملف الترخيص الخاص بك (`Aspose.OCR.lic`) في دليل التنفيذ وحمّله عند بدء التشغيل:

```csharp
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

## الخلاصة

أصبح لديك الآن **حل كامل وجاهز للإنتاج حول كيفية تنفيذ OCR دفعيًا** باستخدام C#. غطى الدليل كل شيء من تثبيت Aspose.OCR، تهيئة المحرك، معالجة مجلد كامل، وتصدير ملخص CSV.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}