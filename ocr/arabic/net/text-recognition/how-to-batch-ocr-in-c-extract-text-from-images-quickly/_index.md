---
category: general
date: 2026-02-19
description: تعلم كيفية تنفيذ التعرف الضوئي على الأحرف (OCR) على دفعات باستخدام Aspose.OCR
  في لغة C#. يوضح لك هذا الدليل كيفية استخراج النص من الصور وتحويل الصور إلى ملفات
  txt بكفاءة.
draft: false
keywords:
- how to batch ocr
- extract text from images
- convert images to txt
- Aspose OCR batch processing
- C# image to text conversion
language: ar
og_description: كيفية تنفيذ التعرف الضوئي على الحروف (OCR) على دفعات باستخدام Aspose.OCR
  في C#. استخراج النص من الصور وتحويل الصور إلى ملف txt في بضع خطوات سهلة.
og_title: كيفية تنفيذ OCR دفعيًا في C# – تحويل سريع من الصورة إلى النص
tags:
- OCR
- C#
- Aspose
title: كيفية تنفيذ OCR دفعيًا في C# – استخراج النص من الصور بسرعة
url: /ar/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعةً في C# – دليل كامل خطوة بخطوة

هل تساءلت يومًا **how to batch OCR** لمجلد كامل من الصور دون كتابة برنامج منفصل لكل ملف؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى استخراج النص من العشرات — أو حتى آلاف — من الصفحات الممسوحة ضوئيًا، الإيصالات، أو لقطات الشاشة. الخبر السار؟ باستخدام Aspose.OCR يمكنك أتمتة العملية بأكملها، **extract text from images**، و **convert images to txt** ببضع أسطر فقط.

في هذا الدرس سنستعرض مثالًا كاملًا وجاهزًا للتنفيذ يوضح بالضبط كيفية إعداد معالج OCR دفعةً، تعديل ما قبل المعالجة، التعامل مع التوازي، وكتابة كل نتيجة إلى ملف `.txt`. في النهاية ستحصل على تطبيق console مستقل يمكنك إدراجه في أي مشروع .NET.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل على .NET Core و .NET Framework أيضًا)
- Aspose.OCR for .NET حزمة NuGet (`Aspose.OCR`)  
- مجلد مليء بملفات الصور (`.png`, `.jpg`, إلخ) التي تريد معالجتها
- كمية معتدلة من الذاكرة RAM؛ العرض التجريبي يستخدم 4 خيوط متوازية لكن يمكنك تعديل ذلك

لا خدمات خارجية، ولا ملفات تكوين مخفية — مجرد كود C# نقي يمكنك تجميعه وتشغيله اليوم.

![Diagram illustrating how to batch ocr processing flow](/images/how-to-batch-ocr-flow.png "how to batch ocr flow diagram")

## الخطوة 1: تثبيت Aspose.OCR وإعداد المشروع

أولاً، أضف حزمة Aspose.OCR إلى مشروعك:

```bash
dotnet add package Aspose.OCR
```

لماذا هذا مهم: Aspose.OCR يجمع محرك OCR، بيانات اللغات، وأدوات ما قبل المعالجة، لذا لن تحتاج إلى أي ملفات ثنائية من طرف ثالث. بمجرد تثبيت الحزمة، أنشئ تطبيق console جديد (أو أضف الكود إلى تطبيق موجود) واستورد المساحات الاسمية المطلوبة:

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
```

تمنحك هذه العبارات `using` إمكانية الوصول إلى فئات معالج الدفعات ومساعدي الإدخال/الإخراج المفيدين.

## الخطوة 2: تكوين معالج OCR الدفعي

الآن سننشئ كائن `OcrBatchProcessor` ونخبره بأي لغة يبحث عنها، وكيفية تنظيف الصور، وعدد الخيوط التي سيعمل بها بالتوازي. هذا هو جوهر **how to batch ocr** بكفاءة.

```csharp
// Step 2: Create and configure the OCR batch processor
var ocrBatch = new OcrBatchProcessor
{
    // Language selection – English is the most common, but you can change it
    Language = Language.English,

    // Preprocessing improves accuracy; Deskew removes rotation
    Preprocessing = new PreprocessingOptions
    {
        Deskew = DeskewAdvanced.Enable()
    },

    // Parallelism – adjust based on your CPU/GPU capabilities
    MaxDegreeOfParallelism = 4
};
```

**لماذا تمكين Deskew؟** العديد من المستندات الممسوحة ليست محاذية بشكل مثالي؛ خوارزمية Deskew تقوم بتدويرها إلى خط أساس مستقيم، مما يزيد غالبًا من معدلات التعرف بنسبة 10‑15 %.

## الخطوة 3: ربط رد نداء النتيجة لحفظ ملفات النص

معالج الدفعة يطلق حدثًا لكل صورة ينجزها. سنشترك في `ResultProcessed` حتى نتمكن من كتابة كل نتيجة OCR إلى ملف `.txt` — وبالتالي **convert images to txt** مباشرةً.

```csharp
// Step 3: Register a callback to save each OCR result as a text file
ocrBatch.ResultProcessed += (sender, args) =>
{
    // Change the original file extension to .txt
    string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");

    // Write the recognized text to the new file
    File.WriteAllText(txtPath, args.Result.Text);

    // Inform the console for debugging / progress monitoring
    Console.WriteLine($"Processed: {args.ImagePath}");
};
```

نصيحة سريعة: إذا كنت بحاجة للحفاظ على هيكل المجلد الأصلي، يمكنك تعديل `txtPath` لتضمين المجلدات الفرعية أو دليل إخراج منفصل.

## الخطوة 4: تشغيل الدفعة على مجلد الصور الخاص بك

كل ما تبقى هو توجيه المعالج إلى المجلد الذي يحتوي على الصور التي تريد **extract text from images**. طريقة `ProcessFolder` تقوم بمسح المجلدات الفرعية بشكل متكرر، لذا يمكنك إلقاء شجرة كاملة من المسحات ودع المكتبة تتعامل مع البقية.

```csharp
// Step 4: Run the batch on all image files in the target folder
ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
```

عند تشغيل البرنامج، سترى مخرجات console مثل:

```
Processed: C:\Path\To\Your\Images\invoice1.png
Processed: C:\Path\To\Your\Images\receipt_2024.jpg
...
```

كل صورة الآن لديها ملف `.txt` شقيق يحتوي على النص المستخرج.

## مثال كامل يعمل

بجمع كل شيء معًا، إليك البرنامج الكامل الذي يمكنك نسخه‑ولصقه في `Program.cs`:

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR batch processor
        var ocrBatch = new OcrBatchProcessor
        {
            Language = Language.English,
            Preprocessing = new PreprocessingOptions
            {
                Deskew = DeskewAdvanced.Enable()
            },
            // Step 2: Define the level of parallelism (adjust for your CPU/GPU)
            MaxDegreeOfParallelism = 4
        };

        // Step 3: Register a callback to save each OCR result as a text file
        ocrBatch.ResultProcessed += (sender, args) =>
        {
            string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");
            File.WriteAllText(txtPath, args.Result.Text);
            Console.WriteLine($"Processed: {args.ImagePath}");
        };

        // Step 4: Run the batch on all image files in the target folder
        ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
    }
}
```

### النتيجة المتوقعة

- لكل `*.png` أو `*.jpg` في دليل المصدر، يظهر ملف `*.txt` المقابل بجانبه.
- تطبع console سطرًا لكل ملف، مما يمنحك تغذية راجعة مباشرة.
- إذا تعذر قراءة صورة (ملف تالف، صيغة غير مدعومة)، يسجل Aspose.OCR خطأً لكنه يواصل معالجة البقية — بفضل المتانة المدمجة في محرك الدفعة.

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت لمعالجة ملفات PDF بدلاً من الصور؟

يمكن لـ Aspose.OCR قبول صفحات PDF كصور داخليًا، لكن سيتعين عليك تحويل PDF إلى صور نقطية أولاً (مثلاً باستخدام Aspose.PDF). بمجرد حصولك على PNGs، يعمل نفس كود الدفعة دون تغيير.

### هل يمكنني تغيير اللغة أثناء التشغيل؟

نعم. خاصية `Language` تقبل أي قيمة من تعداد `Language` (Spanish, French, Chinese، إلخ). إذا كان لديك مستندات متعددة اللغات، فكر في تشغيل تمريرين — واحد لكل لغة — أو استخدم `Language.AutoDetect`.

### كيف يمكنني تحديد الدفعة لأنواع ملفات معينة؟

`ProcessFolder` تقبل خيارًا اختياريًا `SearchOption` ومصفوفة `string[] extensions`. مثال:

```csharp
ocrBatch.ProcessFolder(@"C:\Images", new[] { ".png", ".tif" });
```

### ماذا عن تسريع GPU؟

يدعم Aspose.OCR GPU عبر إعدادات `OcrEngine`، لكن `MaxDegreeOfParallelism` في معالج الدفعة لا يزال المفتاح الأساسي للتوازي. إذا كان لديك GPU متوافق، فعّله في إعدادات المحرك قبل إنشاء `OcrBatchProcessor`.

### كيف تتعامل مع مجلدات ضخمة (عشرات الآلاف من الملفات)؟

- قم بزيادة `MaxDegreeOfParallelism` بحذر؛ عدد كبير جدًا من الخيوط قد يستهلك الذاكرة.
- استخدم مجلد إخراج مخصص لتجنب الفوضى.
- قم بتفريغ السجلات إلى القرص بشكل دوري لمنع تراكم الذاكرة.

## نصائح احترافية للحصول على OCR عالي الجودة

- **DPI Matters**: الصور بدقة 300 DPI أو أعلى تعطي أفضل دقة. إذا كانت مسحاتك أقل، فكر في تكبيرها باستخدام مرشح بيكوبك قبل المعالجة.
- **Noise Reduction**: فعل `Preprocessing.NoiseRemoval` إذا كانت الصور المصدرية مليئة بالضوضاء.
- **File Naming**: حافظ على أسماء الملفات قصيرة وألفبائية رقمية؛ الأحرف الخاصة قد تربك منطق مسار رد النداء.
- **Logging**: استبدل `Console.WriteLine` بمسجل مناسب (مثلاً `Serilog`) لأعباء العمل الإنتاجية.

## الخطوات التالية

الآن بعد أن أتقنت **how to batch OCR**، قد ترغب في:

- **Extract text from images** وإدخال الناتج في فهرس بحث (مثلاً Elasticsearch) للبحث النصي الكامل.
- **Convert images to txt** ثم تشغيل معالجة اللغة الطبيعية (NLP) لتصنيف المستندات تلقائيًا.
- جرّب **different language packs** أو قواميس مخصصة للمصطلحات الخاصة بالصناعة.

إذا كنت مهتمًا بالمعالجة اللاحقة، تفقد الدروس حول “تحليل مخرجات OCR باستخدام التعابير النمطية” أو “تخزين نتائج OCR في قاعدة بيانات SQL”.

---

**برمجة سعيدة!** لا تتردد في تعديل التوازي، إضافة خطوات ما قبل معالجة إضافية، أو تغليف كل ذلك في خدمة Windows للمراقبة المستمرة. السماء هي الحد عندما تجمع بين قدرات Aspose.OCR الدفعية وقليل من إبداع .NET.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}