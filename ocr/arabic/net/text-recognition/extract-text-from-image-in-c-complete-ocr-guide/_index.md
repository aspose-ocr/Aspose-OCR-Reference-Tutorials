---
category: general
date: 2026-04-11
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلّم كيفية تحميل الصورة
  للتعرف الضوئي على الأحرف وتعرّف النص من ملفات TIFF بدعم وحدة معالجة الرسومات.
draft: false
keywords:
- extract text from image
- load image for OCR
- recognize text from TIFF
- Aspose OCR C#
- GPU OCR processing
- high‑resolution OCR
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR في C#. يوضح هذا الدرس كيفية
  تحميل الصورة للتعرف الضوئي على الأحرف (OCR) والتعرف على النص من ملف TIFF باستخدام
  تسريع وحدة معالجة الرسومات.
og_title: استخراج النص من الصورة في C# – دليل OCR كامل
tags:
- OCR
- C#
- Aspose
- GPU
title: استخراج النص من الصورة في C# – دليل OCR الكامل
url: /ar/net/text-recognition/extract-text-from-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة في C# – دليل OCR كامل

هل احتجت يومًا إلى **استخراج النص من الصورة** لكن لم تكن متأكدًا أي مكتبة ستتعامل مع ملف TIFF ضخم دون أن تتعطل؟ لست وحدك. في العديد من المشاريع الواقعية—مثل رقمنة الفواتير أو أرشفة الكتب الممسوحة ضوئيًا—تصبح القدرة على تحميل الصورة لـ OCR ثم التعرف على النص من TIFF بسرعة ميزة حاسمة.

في هذا الدليل سنستعرض حلًا عمليًا يفعل ذلك بالضبط باستخدام Aspose OCR لـ .NET. بحلول النهاية ستحصل على تطبيق C# Console قابل للتنفيذ يقوم بتحميل مسح عالي الدقة، ويشغل المعالجة المعجلة بالـ GPU (مع تراجع سلس)، ويُخرج النتيجة كنص عادي. لا قطع مفقودة، ولا نهايات “انظر إلى الوثائق”.

## ما ستحتاجه

- **.NET 6 أو أحدث** (الكود يُترجم مع أي SDK حديث)
- **Aspose.OCR لـ .NET** حزمة NuGet  
  `dotnet add package Aspose.OCR`
- **TIFF كبير** أو أي تنسيق صورة آخر تريد تطبيق OCR عليه  
  (المثال يستخدم `large_scan.tif`)
- (اختياري) GPU يدعم CUDA 11+ – إذا لم يكن لديك، ستتحول المكتبة تلقائيًا إلى وضع CPU.

هذا كل شيء. هيا نبدأ.

![Extract text from image using Aspose OCR in C#](image-placeholder.png "Extract text from image using Aspose OCR in C#")

## الخطوة 1: استخراج النص من الصورة – تهيئة محرك OCR

قبل أن يتم معالجة أي صورة، تحتاج إلى نسخة من `OcrEngine`. يحتفظ المحرك بجميع الإعدادات التي تتحكم في كيفية تشغيل التعرف.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine and request GPU processing.
        // ProcessingMode.Auto tells Aspose to fall back to CPU if a GPU isn’t detected.
        var ocrEngine = new OcrEngine
        {
            Settings = { ProcessingMode = ProcessingMode.Gpu }
        };

        // Optional: cap GPU memory usage to avoid OOM on shared machines.
        ocrEngine.Settings.GpuMemoryLimit = 1024; // MB
```

**لماذا هذا مهم:**  
`ProcessingMode.Gpu` يمكن أن يقلل ثوانٍ من زمن التعرف على بطاقة حديثة، لكن ضبط `ProcessingMode.Auto` (أو ترك الإعداد الافتراضي) يكون أكثر أمانًا في البيئات التي قد لا يتوفر فيها GPU. الحماية `GpuMemoryLimit` هي نصيحة عملية—بدونها قد تستهلك صورة ضخمة كل ذاكرة الـ VRAM وتسبب تعطل التطبيقات الأخرى.

## الخطوة 2: تحميل الصورة لـ OCR – جلب ملف TIFF إلى الذاكرة

الآن بعد أن أصبح المحرك جاهزًا، نحتاج إلى تزويده بالصورة التي نريد تحليلها. توفر Aspose الدالة `ImageStream.FromFile` التي تُجرد التعامل مع الصيغ.

```csharp
        // Load the high‑resolution TIFF you want to OCR.
        // Replace the path with the location of your own file.
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/large_scan.tif");
```

**ما الذي يحدث في الخلفية؟**  
`ImageStream.FromFile` يقرأ الملف إلى تدفق ويكتشف تلقائيًا تنسيق الصورة (TIFF، PNG، JPEG، إلخ). إذا كنت تتعامل مع ملفات TIFF متعددة الصفحات، ستعامل Aspose كل صفحة كإطار منفصل؛ يمكنك التكرار عليها لاحقًا إذا لزم الأمر.

## الخطوة 3: التعرف على النص من TIFF – تشغيل محرك OCR

مع تحميل الصورة، يبدأ العمل الشاق. تُعيد الدالة `Recognize` كائن `OcrResult` يحتوي على النص المستخرج وبعض حقول البيانات الوصفية المفيدة.

```csharp
        // Perform the OCR operation.
        var ocrResult = ocrEngine.Recognize(image);
```

**لماذا نستدعي `Recognize` مرة واحدة فقط؟**  
لأن المحرك يخزن هياكل داخلية مؤقتًا بعد التشغيل الأول، فإن استدعاءً واحدًا يكفي لمعظم السيناريوهات. إذا كنت بحاجة لمعالجة صفحات متعددة، أعد استخدام نفس نسخة `OcrEngine`—هذا يتجنب عبء إعادة تهيئة سياقات الـ GPU.

## الخطوة 4: عرض النتيجة – إظهار النص المستخرج

أخيرًا، نطبع السلسلة التي تم التعرف عليها إلى وحدة التحكم. في تطبيق حقيقي ربما تكتبها إلى قاعدة بيانات أو ملف.

```csharp
        // Show the extracted plain text.
        Console.WriteLine(ocrResult.Text);
    }
}
```

**الناتج المتوقع:**  
إذا كان `large_scan.tif` يحتوي على فاتورة مطبوعة، سترى شيئًا مثل:

```
Invoice #12345
Date: 2024‑03‑15
Total: $1,234.56
...
```

التنسيق الدقيق يعتمد على الصورة الأصلية، لكن النقطة الأساسية هي أنك الآن تملك نتائج **استخراج النص من الصورة** جاهزة للمعالجة اللاحقة.

## الخطوة 5: استكشاف الأخطاء وإصلاحها والحالات الخاصة

### عدم اكتشاف GPU؟

إذا شغّلت العينة على جهاز لا يحتوي على GPU متوافق، سيعود المحرك صامتًا إلى CPU عند استخدام `ProcessingMode.Auto`. لفرض وضع CPU صراحةً، استبدل السطر السابق بـ:

```csharp
ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
```

### ملفات TIFF التي تستهلك الذاكرة

المسحات الضخمة جدًا (مثلاً 10 000 × 10 000 بكسل) قد تتجاوز الحد الأقصى للـ GPU البالغ 1 GB الذي حددناه. في هذه الحالة، إما رفع قيمة `GpuMemoryLimit` (إذا كان لديك VRAM إضافي) أو تقليل حجم الصورة قبل تمريرها إلى المحرك:

```csharp
var resized = image.Resize(4000, 4000); // keep aspect ratio as needed
var ocrResult = ocrEngine.Recognize(resized);
```

### مستندات متعددة الصفحات

إذا كان ملف TIFF يحتوي على صفحات متعددة، قم بالتكرار عليها:

```csharp
for (int i = 0; i < image.PageCount; i++)
{
    var pageStream = image.GetPage(i);
    var result = ocrEngine.Recognize(pageStream);
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(result.Text);
}
```

### دعم اللغات والخطوط

تكتشف Aspose OCR النصوص اللاتينية تلقائيًا، لكن للخطوط السيريالية أو العربية أو الخطوط المخصصة قد تحتاج إلى توفير حزمة لغة:

```csharp
ocrEngine.Settings.Language = Language.Russian; // example
```

## نصائح احترافية وأفضل الممارسات

- **إعادة استخدام المحرك**: إنشاء `OcrEngine` جديد لكل صورة يضيف تأخيرًا ملحوظًا.
- **المعالجة الدفعية**: عند التعامل مع عشرات ملفات TIFF، ضعها في طابور وعالجها في خيوط متوازية—مع مراعاة تنافسية ذاكرة الـ GPU.
- **التحقق من المخرجات**: OCR ليس مثاليًا؛ نفّذ تدقيق إملائي بسيط أو تحقق regex على `ocrResult.Text` لاكتشاف الأخطاء الواضحة.
- **تسجيل الأداء**: قس وقت `Stopwatch` المستغرق قبل وبعد `Recognize` لتحديد ما إذا كان تسريع الـ GPU يستحق الإعداد الإضافي في بيئتك.

## الخلاصة

أصبح لديك الآن مثال كامل من البداية إلى النهاية ي **استخراج النص من ملفات الصورة** باستخدام Aspose OCR في C#. من خلال تحميل الصورة لـ OCR، واستدعاء المحرك للتعرف على النص من TIFF، ومعالجة سيناريوهات GPU مقابل CPU، يوفر لك هذا الدليل أساسًا جاهزًا للإنتاج يمكنك تكييفه مع الفواتير أو جوازات السفر أو أي مستند ممسوح.

ما الخطوة التالية؟ جرّب استبدال TIFF بملف PDF متعدد الصفحات، جرب حزم لغات مخصصة، أو صلّ النتيجة إلى خط أنابيب معالجة لغة طبيعية لاستخراج البيانات تلقائيًا. السماء هي الحد—برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}