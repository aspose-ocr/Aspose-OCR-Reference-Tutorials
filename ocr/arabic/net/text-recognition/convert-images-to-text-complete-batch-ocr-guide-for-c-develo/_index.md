---
category: general
date: 2025-12-29
description: حوّل الصور إلى نص بسرعة باستخدام معالجة OCR دفعة واحدة في C#. تعلم كيفية
  استخراج النص من الصور، ومعالجة OCR للصور، وحفظ OCR كملفات نصية.
draft: false
keywords:
- convert images to text
- batch ocr processing
- extract text from images
- process images ocr
- save ocr as text
language: ar
og_description: تحويل الصور إلى نص باستخدام Aspose OCR في C#. يوضح هذا الدليل معالجة
  OCR على دفعات، استخراج النص من الصور، وحفظ OCR كنص.
og_title: تحويل الصور إلى نص – دليل OCR دفعي خطوة بخطوة
tags:
- OCR
- C#
- Aspose
title: تحويل الصور إلى نص – دليل OCR شامل للدفعات لمطوري C#
url: /ar/net/text-recognition/convert-images-to-text-complete-batch-ocr-guide-for-c-develo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصور إلى نص – دليل OCR دفعي كامل لمطوري C#

هل احتجت يوماً إلى **تحويل الصور إلى نص** لكن توقفت عند سؤال “كيف أعالج مجلدًا كاملاً؟”؟ لست وحدك. في العديد من المشاريع الواقعية—مثل رقمنة الفواتير، أرشفة الإيصالات، أو حتى مسح الملاحظات المكتوبة يدويًا—يحتاج المطورون إلى **استخراج النص من الصور** على نطاق واسع، وليس ملفًا واحدًا في كل مرة.  

في هذا الدرس سنستعرض حلًا جاهزًا للتنفيذ **يعالج الصور باستخدام OCR**، يحفظ كل نتيجة كملف نصي عادي، ويقوم بذلك بشكل متوازي لتسريع العملية. في النهاية ستحصل على برنامج C# واحد يمكنك إدراجه في أي مشروع .NET والبدء فورًا في تحويل الصور إلى نص.

## ما الذي ستحتاجه

- **.NET 6+** (أي SDK حديث؛ يستخدم الكود عبارات المستوى الأعلى للتبسيط)
- حزمة NuGet **Aspose.OCR** (الإصدار 23.12 وقت كتابة هذا الدليل)
- مجلد يحتوي على الصور المصدرية (PNG، JPG، TIFF، إلخ)
- مجلد هدف حيث سيتم كتابة ملفات النص المستخرجة  

لا ملفات إعداد إضافية، لا سحر مخفي—فقط C# عادي ومكتبة Aspose.

## الخطوة 1: تثبيت حزمة NuGet Aspose.OCR

قبل كتابة أي كود، تأكد من أن مكتبة OCR متاحة في مشروعك.

```bash
dotnet add package Aspose.OCR --version 23.12
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، يمكنك أيضًا التثبيت عبر **Manage NuGet Packages** → **Browse** → ابحث عن “Aspose.OCR”.

## الخطوة 2: إعداد بنية المجلدات

أنشئ مجلدين في أي مكان على القرص الخاص بك:

```
YOUR_DIRECTORY/
├─ Incoming   ← place your source images here
└─ Processed  ← OCR results will be saved here
```

يمكنك تسميتهما كما تشاء؛ فقط تذكر المسارات عند تكوين المعالج.

## الخطوة 3: إنشاء مثيل Batch Processor

الآن سننشئ كائن `OcrBatchProcessor` ونخبره أين يبحث عن الصور وأين يكتب النتائج. الكود التالي مثال كامل قابل للتنفيذ—انسخه إلى تطبيق console جديد (`dotnet new console`) واضغط **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

// Step 1: Create a batch processor instance
var ocrBatch = new OcrBatchProcessor
{
    // Step 2: Specify the folder that contains the source images
    InputFolder = "YOUR_DIRECTORY/Incoming",

    // Step 3: Specify where the OCR results should be saved
    OutputFolder = "YOUR_DIRECTORY/Processed",

    // Step 4: Choose the output format (plain text in this example)
    OutputFormat = SaveFormat.Txt,

    // Step 5: Allow the processor to use up to 4 parallel threads
    MaxDegreeOfParallelism = 4
};

// Step 6: Execute the batch synchronously
ocrBatch.Process();

// Step 7: Notify that the batch OCR operation has finished
Console.WriteLine("Batch OCR completed.");
```

> **لماذا هذا مهم:**  
> - `InputFolder` و `OutputFolder` يتيحان لك **معالجة الصور باستخدام OCR** دفعيًا دون الحاجة لكتابة حلقة يدوية.  
> - `OutputFormat = SaveFormat.Txt` يضمن **حفظ OCR كنص**، وهو أكثر الصيغ قابلية للنقل للتحليل اللاحق.  
> - `MaxDegreeOfParallelism = 4` يسرّع المهمة على الأجهزة متعددة الأنوية، مما يجعل **معالجة OCR الدفعية** أسرع بشكل ملحوظ.

## الخطوة 4: تشغيل التطبيق والتحقق من النتائج

نفّذ البرنامج (`dotnet run`). مع معالجة كل صورة، تقوم Aspose بإنشاء ملف `.txt` يحمل نفس الاسم الأساسي في مجلد `Processed`. افتح أي من هذه الملفات وسترى الأحرف المستخرجة.

```text
Batch OCR completed.
```

تلك الرسالة في وحدة التحكم هي إشارة إلى أن **تحويل الصور إلى نص** انتهى بنجاح.

### تخطيط المجلد المتوقع بعد التنفيذ

```
YOUR_DIRECTORY/
├─ Incoming
│   ├─ invoice1.png
│   ├─ receipt.jpg
│   └─ note.tif
└─ Processed
    ├─ invoice1.txt
    ├─ receipt.txt
    └─ note.txt
```

كل ملف `.txt` يحتوي على تمثيل نصي عادي لصورة المصدر—مثالي لتغذيته إلى فهارس البحث، خطوط معالجة اللغة الطبيعية، أو مجرد أرشفة.

## الخطوة 5: تعديل المعالج لسيناريوهات العالم الحقيقي

الإعداد الأساسي يعمل في معظم الحالات، لكن بيئات الإنتاج غالبًا ما تحتاج إلى بعض الضبط الإضافي:

| السيناريو | التعديل |
|----------|----------|
| **صيغ صور مختلفة** | تقوم Aspose تلقائيًا باكتشاف معظم الصيغ الشائعة. إذا كان لديك ملفات PDF، ضع `InputFolder` على مجلد يحتوي صفحات PDF أو استخدم تحويل `PdfToImage` أولًا. |
| **تقسيم ملفات PDF الكبيرة إلى صفحات** | عالج مسبقًا باستخدام `Aspose.PDF` لتحويل كل صفحة إلى صورة، ثم وجه `InputFolder` إلى ذلك المخرج. |
| **قواميس لغات مخصصة** | اضبط `ocrBatch.Language = OcrLanguage.English;` أو حمّل حزمة لغة مخصصة لتحسين الدقة للنص غير الإنجليزي. |
| **معالجة الأخطاء** | غلف `ocrBatch.Process()` بكتلة `try/catch` وتفقد `ocrBatch.FailedFiles` لأي صور تعذر قراءتها. |
| **صيغ إخراج مختلفة** | غيّر `OutputFormat` إلى `SaveFormat.Docx` أو `SaveFormat.Pdf` إذا كنت تحتاج إلى أكثر من النص العادي. |

فيما يلي مقتطف سريع يوضح كيفية تمكين اللغة الإنجليزية ومعالجة الأخطاء الأساسية:

```csharp
try
{
    ocrBatch.Language = OcrLanguage.English;
    ocrBatch.Process();
    Console.WriteLine("All images processed successfully.");
}
catch (Exception ex)
{
    Console.WriteLine($"Error during batch OCR: {ex.Message}");
}
```

## الخطوة 6: أتمتة سير العمل (اختياري)

إذا أردت أن يحدث التحويل تلقائيًا كلما وصلت ملفات جديدة إلى `Incoming`، فكر في ربط المجلد بـ **FileSystemWatcher**:

```csharp
using System.IO;

var watcher = new FileSystemWatcher("YOUR_DIRECTORY/Incoming")
{
    Filter = "*.*",
    NotifyFilter = NotifyFilters.FileName | NotifyFilters.Size,
    EnableRaisingEvents = true
};

watcher.Created += (s, e) =>
{
    // Re‑run the batch processor (or just process the new file)
    ocrBatch.Process();
    Console.WriteLine($"New file detected and processed: {e.Name}");
};

Console.WriteLine("Watching for new images... Press ENTER to exit.");
Console.ReadLine();
```

الآن تطبيقك **يعالج الصور باستخدام OCR** في الوقت الحقيقي، محولًا كل صورة جديدة إلى نص قابل للبحث دون تدخل يدوي.

## ملخص بصري

![مثال تحويل الصور إلى نص](/images/convert-images-to-text.png "مخطط تدفق تحويل الصور إلى نص")

*المخطط أعلاه يوضح التدفق من البداية إلى النهاية: صور واردة → OCR دفعي → ملفات نصية عادية.*

## أسئلة شائعة وحالات خاصة

**س: ماذا لو احتوت الصورة على لغات متعددة؟**  
ج: اضبط `ocrBatch.Language = OcrLanguage.Multilingual;` أو حدد قائمة باللغات. ستحاول Aspose اكتشاف كل مقطع لغوي.

**س: صوري ضخمة (5 ميغابايت فأكثر). هل سينفد الذاكرة؟**  
ج: المكتبة تقوم ببث كل ملف، وحد `MaxDegreeOfParallelism` يمنع استهلاك الذاكرة الزائد. إذا واجهت حدودًا، قلل التوازي إلى `2` أو `1`.

**س: ما مدى دقة OCR للملاحظات المكتوبة يدويًا؟**  
ج: OCR للخط اليدوي أصعب بطبيعة الحال. يمكنك تحسين النتائج بمعالجة مسبقة للصور (مثل زيادة التباين، تصحيح الميل) قبل تمريرها إلى Aspose.

**س: هل يمكن تشغيل هذا على Linux؟**  
ج: نعم. Aspose.OCR متعدد المنصات؛ فقط تأكد من تثبيت بيئة .NET المناسبة.

## الخلاصة

غطينا كل ما تحتاجه **لتحويل الصور إلى نص** باستخدام إمكانيات OCR الدفعي من Aspose. من تثبيت حزمة NuGet، تكوين مجلدات الإدخال/الإخراج، ضبط التوازي، إلى معالجة الحالات الواقعية—هذا الدليل يقدم لك حلًا متكاملًا يمكن للمساعدين الذكائيين الاستشهاد به حرفيًا.

ما الخطوة التالية؟ جرّب ربط ملفات `.txt` التي تم توليدها بمحرك بحث نص كامل مثل **Lucene.NET**، أو أدخلها في خط أنابيب تعلم آلي لتحليل المشاعر. يمكنك أيضًا استكشاف **حفظ OCR كنص** بصيغ أخرى (CSV، JSON) لتناسب نماذج البيانات اللاحقة.

برمجة سعيدة، ولتتحول صورك دائمًا إلى نص نظيف وقابل للبحث!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}