---
category: general
date: 2026-05-06
description: تعلم كيفية تنفيذ OCR دفعيًا في C# واستخراج النص من المسحات بسرعة باستخدام
  Aspose OCR Batch. اتبع دليلًا كاملاً خطوة بخطوة يتضمن الشيفرة والنصائح ومعالجة الحالات
  الخاصة.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: ar
og_description: كيف تقوم بعملية OCR دفعةً في C#؟ يوضح لك هذا الدليل كيفية استخراج
  النص من المسحات الضوئية بكفاءة باستخدام Aspose OCR، ودعم GPU، والمعالجة المتوازية.
og_title: كيفية تنفيذ OCR دفعي في C# – استخراج النص من المسحات الضوئية
tags:
- C#
- OCR
- Aspose
title: كيفية تنفيذ OCR دفعيًا في C# – استخراج النص من المسحات الضوئية
url: /ar/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعيًا في C# – استخراج النص من المستندات الممسوحة

هل تساءلت يومًا **كيف تقوم بعمل OCR دفعي** عندما يكون لديك مجلد مليء بملفات PDF أو JPEG الممسوحة؟ لست وحدك الذي يواجه جبلًا من الصور ويفكر، “يجب أن تكون هناك طريقة أسرع لاستخراج النص.” في هذا الدرس سنستعرض حلًا عمليًا لا يتيح لك **استخراج النص من المستندات الممسوحة** فحسب، بل يسرّع العملية باستخدام تسريع GPU والتوازي.

الأمر واضح: تنفيذ OCR ملفًا بملف هو استهلاك كبير للوقت، خاصةً إذا كنت تتعامل مع عشرات أو مئات الصفحات. بنهاية هذا الدليل ستحصل على تطبيق C# Console جاهز للتنفيذ يعالج دليلًا كاملًا بأمر واحد، ويعطيك ملفات نصية نظيفة جاهزة للفهرسة أو البحث أو أي خطوة تالية.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- **.NET 6.0 أو أحدث** (الكود يستخدم ميزات C# الحديثة).
- **رخصة Aspose.OCR** (الإصدار التجريبي المجاني يكفي للاختبار).
- جهاز متوافق مع **GPU** إذا أردت تفعيل `UseGpu`؛ وإلا سيعود المكتبة إلى المعالج المركزي.
- إلمام أساسي بـ **تطبيقات C# Console**.

لا توجد خدمات خارجية، ولا ملفات إعداد مخفية—فقط الـ SDK ومجلد الصور.

## الخطوة 1: تثبيت حزمة NuGet الخاصة بـ Aspose.OCR

أولًا، أضف مكتبة Aspose OCR إلى مشروعك. افتح الطرفية في مجلد الحل وشغّل الأمر التالي:

```bash
dotnet add package Aspose.OCR
```

سيتم جلب `Aspose.OCR` والمساحة الاسمية الخاصة بالدفعات، والتي سنستخدمها لاحقًا لـ **OCR دفعي**.

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، يمكنك أيضًا إضافة الحزمة عبر واجهة NuGet Package Manager.

## الخطوة 2: إنشاء هيكل تطبيق Console

لنقم بإعداد تطبيق Console بسيط سيستضيف معالج الدفعات. أنشئ ملفًا جديدًا باسم `Program.cs` والصق الهيكل التالي:

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll configure and run the OCR batch processor here.
        }
    }
}
```

لماذا نضع المنطق داخل `Main`؟ لأن تطبيق Console يمنحنا تغذية راجعة فورية عبر `Console.WriteLine`، وهو مثالي للتحقق السريع من أن مهمة **OCR الدفعي** انتهت فعلاً.

## الخطوة 3: تكوين OcrBatchProcessor

الآن الجزء الأساسي من الحل. سننشئ كائن `OcrBatchProcessor`، نحدده إلى مجلد الإدخال، نحدد مكان حفظ النتائج، ونضبط بعض إعدادات الأداء.

```csharp
// Step 3: Configure the OCR batch processor
var batch = new OcrBatchProcessor
{
    // Folder that contains the source images to be processed
    InputFolder = @"YOUR_DIRECTORY/Scans",

    // Folder where the OCR results will be saved
    OutputFolder = @"YOUR_DIRECTORY/OcrResults",

    // Specify the language of the documents (Spanish in this example)
    Language = OcrLanguage.Spanish,

    // Enable GPU acceleration for faster processing (if available)
    UseGpu = true,

    // Limit the number of concurrent OCR operations
    MaxDegreeOfParallelism = 4
};
```

### لماذا هذه الإعدادات مهمة

| الإعداد | ما يفعله | متى قد تحتاج لتغييره |
|---------|----------|----------------------|
| `InputFolder` | مسار المجلد الذي يحتوي على المستندات الممسوحة. | استخدم مسارًا نسبيًا لسهولة النقل. |
| `OutputFolder` | المكان الذي سيتم حفظ النص المستخرج لكل صورة كملف `.txt`. | وجهه إلى مشاركة شبكة إذا كنت تحتاج تخزينًا مركزيًا. |
| `Language` | نموذج لغة OCR؛ اخترنا الإسبانية لتوضيح الدعم متعدد اللغات. | غيّره إلى `OcrLanguage.English` أو أي لغة مدعومة. |
| `UseGpu` | يرسل الحسابات المكثفة إلى الـ GPU. | اضبطه على `false` في الخوادم بدون GPU. |
| `MaxDegreeOfParallelism` | يتحكم في عدد الصور التي تُعالج في آن واحد. | قلّ القيمة على الأجهزة ذات المعالج الضعيف لتجنب الإبطاء. |

## الخطوة 4: تنفيذ عملية الدفعة مع معالجة الأخطاء

تشغيل الدفعة بسيط كاستدعاء `Execute()`، لكننا سنغلفه بكتلة `try‑catch` لتظهر لك رسالة مفيدة إذا حدث خطأ (مثل عدم وجود المجلد أو تنسيق صورة غير مدعوم).

```csharp
try
{
    // Step 4: Run the batch OCR operation
    batch.Execute();

    // Step 5: Inform the user that processing has finished
    Console.WriteLine("Batch completed.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
}
```

عند انتهاء المعالج، ستظهر لك **Batch completed.** في الطرفية، وسيكون لكل صورة مصدر ملف `.txt` مطابق داخل `OcrResults`. أسماء الملفات تحاكي الأصل، مما يسهل ربط النص بالمسح الأصلي.

## الخطوة 5: التحقق من الناتج – ما الذي تتوقعه

بعد تشغيل البرنامج، افتح أي ملف داخل `YOUR_DIRECTORY/OcrResults`. يجب أن ترى محتوى نصي عادي مستخرج من الصورة المقابلة، على سبيل المثال:

```
Este es un documento de prueba.
Contiene varias líneas de texto.
```

إذا كان الناتج مشوشًا، تأكد من أن `Language` يتطابق مع لغة المستندات الممسوحة. يدعم Aspose OCR أكثر من 100 لغة، لذا يمكنك استبدال `OcrLanguage.Spanish` بأي لغة تحتاجها.

## معالجة الحالات الخاصة والمشكلات الشائعة

### 1. عدم توفر GPU

إذا كان جهازك يفتقر إلى GPU متوافق، فإن `UseGpu = true` سيعود صامتًا إلى وضع المعالج المركزي، لكنك ستفقد تسريع السرعة. لتكون صريحًا، يمكنك اكتشاف قدرة الـ GPU:

```csharp
if (!OcrBatchProcessor.IsGpuSupported)
{
    batch.UseGpu = false;
    Console.WriteLine("GPU not detected – falling back to CPU processing.");
}
```

### 2. ملفات كبيرة تتجاوز الذاكرة

عند التعامل مع ملفات TIFF أو PDF ضخمة، فكر في تقسيمها إلى صور أصغر مسبقًا. يمكن لـ Aspose OCR معالجة ملفات PDF متعددة الصفحات، لكن استهلاك الذاكرة يزداد مع عدد الصفحات. خطوة ما قبل المعالجة باستخدام `Aspose.Imaging` يمكنها تقطيع المستند إلى قطع يمكن التحكم فيها.

### 3. ملفات غير صور في مجلد الإدخال

يتجاهل معالج الدفعة الملفات التي لا يستطيع解析ها، لكن من الأفضل الحفاظ على نظافة المجلد. يمكنك الفلترة حسب الامتداد:

```csharp
batch.InputFolder = @"YOUR_DIRECTORY/Scans";
batch.FileFilter = file => file.EndsWith(".png", StringComparison.OrdinalIgnoreCase)
                         || file.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase);
```

*(ملاحظة: `FileFilter` خاصية افتراضية؛ استبدلها بالـ API الفعلي إذا كان متاحًا.)*

## مثال كامل جاهز للتنفيذ

فيما يلي البرنامج الكامل جاهز للنسخ واللصق. استبدل `YOUR_DIRECTORY` بالمسار الكامل على جهازك.

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Configure the batch processor
            var batch = new OcrBatchProcessor
            {
                InputFolder = @"C:\MyScans",          // <-- change this
                OutputFolder = @"C:\OcrResults",     // <-- change this
                Language = OcrLanguage.Spanish,
                UseGpu = true,
                MaxDegreeOfParallelism = 4
            };

            // Optional: fall back to CPU if no GPU is found
            if (!OcrBatchProcessor.IsGpuSupported)
            {
                batch.UseGpu = false;
                Console.WriteLine("GPU not detected – using CPU.");
            }

            try
            {
                // Run the batch job
                batch.Execute();

                Console.WriteLine("Batch completed.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### ناتج الطرفية المتوقع

```
Batch completed.
```

وفي `C:\OcrResults` ستجد ملف `.txt` لكل صورة موجودة في `C:\MyScans`.

## الخلاصة

أصبح لديك الآن طريقة قوية وجاهزة للإنتاج **كيفية تنفيذ OCR دفعي** في C# و**استخراج النص من المستندات الممسوحة** دون الحاجة لفتح كل ملف يدويًا. من خلال الاستفادة من API الدفعات في Aspose، وتسريع GPU، وتوازي قابل للتكوين، يمكن لهذا الحل أن يتعامل مع عدد قليل من الصفحات أو آلافها.

ما الخطوة التالية؟ جرّب الأفكار التالية:

- **دمج مع فهرس بحث** (مثل Elasticsearch) لجعل النص المستخرج قابلًا للبحث.
- **إضافة معالجة لاحقة** مثل تدقيق إملائي أو كشف لغة.
- **تحويل تطبيق Console إلى خدمة Windows** لمراقبة مجلد الإدخال باستمرار.

لا تتردد في التجربة، تعديل مستوى التوازي، أو تغيير نموذج اللغة. إذا واجهت أي صعوبات، اترك تعليقًا أدناه—نتمنى لك تجربة OCR موفقة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}