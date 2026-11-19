---
category: general
date: 2026-05-06
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية تحويل JPG
  إلى نص، وتعيين لغة OCR، وقراءة النص من JPG بكفاءة.
draft: false
keywords:
- extract text from image
- convert jpg to text
- image to text c#
- read text from jpg
- set OCR language
language: ar
og_description: استخراج النص من الصورة في C# باستخدام Aspose OCR. يوضح هذا الدليل
  كيفية تحويل JPG إلى نص، وتعيين لغة OCR، وقراءة النص من JPG.
og_title: استخراج النص من الصورة في C# – دليل كامل
tags:
- OCR
- C#
- Aspose
title: استخراج النص من الصورة في C# – دليل خطوة بخطوة
url: /ar/net/text-recognition/extract-text-from-image-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة في C# – دليل برمجة كامل

هل احتجت يومًا إلى **استخراج النص من الصورة** لكن لم تكن متأكدًا أي مكتبة تختار؟ لست وحدك—المطورون يسألون باستمرار، “كيف أحول JPG إلى نص دون إرسال البيانات إلى السحابة؟” الخبر السار هو أن Aspose OCR يوفر لك حلاً كاملاً دون اتصال يعمل مباشرة داخل تطبيق .NET الخاص بك.

في هذا الدرس سنستعرض كل ما تحتاج إلى معرفته: من تثبيت حزمة Aspose OCR NuGet، إلى **تعيين لغة OCR** للنص الروسي، وأخيرًا **قراءة النص من ملفات JPG**. في النهاية ستحصل على مقطع شفرة قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع C# والبدء في استخراج النص من الصور فورًا.

> **ما ستحصل عليه**  
> • مثال واضح وقابل للتنفيذ **يستخرج النص من ملفات الصورة**.  
> • معرفة كيفية **تحويل JPG إلى نص** باستخدام محرك Aspose OCR.  
> • نصائح حول تكوين **تعيين لغة OCR** لسيناريوهات متعددة اللغات.  
> • معالجة الحالات الخاصة للصور غير القابلة للقراءة وحزم اللغة المفقودة.

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6.0 أو أحدث (أي بيئة تشغيل .NET حديثة) | Aspose OCR تستهدف .NET Standard 2.0+، لذا فإن البيئات الأحدث تمنحك أفضل أداء. |
| Visual Studio 2022 (أو VS Code مع امتدادات C#) | بيئة تطوير متكاملة صديقة تساعدك على تصحيح تدفق OCR بسرعة. |
| الوصول إلى الإنترنت **مرة واحدة** لتحميل حزمة Aspose OCR NuGet | بعد التثبيت الأول يمكنك تمكين **الموارد غير المتصلة** لتجنب أي تنزيلات إضافية. |
| صورة JPG نموذجية (`input.jpg`) تحتوي على نص روسي (أو أي لغة تخطط لاستخدامها) | يستخدم الدرس مثالًا روسيًا، لكن يمكنك استبداله بأي حزمة لغة قمت بتثبيتها. |

## نظرة عامة على الحل

على مستوى عالٍ، تبدو العملية هكذا:

1. **إنشاء** `OcrEngine` مع موارد غير متصلة بحيث لا تحاول المكتبة تنزيل بيانات اللغة أثناء التشغيل.  
2. **تعيين** اللغة المطلوبة (مثلاً الروسية) باستخدام تعداد `OcrLanguage`.  
3. **استدعاء** `RecognizeImage` على ملف JPG محلي.  
4. **طباعة** السلسلة المستخرجة إلى وحدة التحكم أو توجيهها إلى سير عملك الخاص.

![استخراج النص من الصورة باستخدام Aspose OCR في C#](https://example.com/placeholder-image.png){.align-center alt="استخراج النص من الصورة باستخدام Aspose OCR في C#"}

*المخطط توضيحي فقط؛ الشيفرة تقوم بالعمل الشاق.*

## استخراج النص من الصورة – المفاهيم الأساسية

قبل أن نبدأ بكتابة الشيفرة، دعونا نستعرض بعض المفاهيم التي غالبًا ما تُربك المطورين:

- **OfflineResources** – عندما تكون `true`، يبحث Aspose OCR عن حزم اللغة التي قمت بتحميلها مسبقًا. هذا يلغي خطوة “التحميل التلقائي” التي قد تبطئ بدء التشغيل في بيئات الإنتاج.  
- **OcrLanguage** – يحتوي التعداد على عشرات معرفات اللغة (`English`, `Russian`, `Japanese`, …). اختيار اللغة الصحيحة يحسن الدقة بشكل كبير لأن المحرك يمكنه تطبيق خوارزميات خاصة باللغة.  
- **جودة الصورة** – يعمل OCR بأفضل شكل على صور ذات تباين عالي وخالية من الضوضاء. إذا حصلت على نتائج مشوشة، فكر في ما قبل المعالجة (مثل التثنائي) قبل تمرير الصورة إلى المحرك.

فهم هذه النقاط سيساعدك على تحديد متى يجب **تعيين لغة OCR** يدويًا مقابل الاعتماد على الاكتشاف التلقائي، ولماذا **تحويل JPG إلى نص** ليس مجرد سطر واحد.

## الخطوة 1: تثبيت حزمة Aspose OCR NuGet

افتح طرفية في مجلد مشروعك وشغّل:

```bash
dotnet add package Aspose.OCR
```

*نصيحة احترافية:* بعد التثبيت الأول، أضف `-v latest` لتضمن حصولك دائمًا على أحدث نسخة مستقرة. حجم الحزمة حوالي 15 ميغابايت، وهو معقول لمعظم عمليات النشر على سطح المكتب أو الخادم.

## الخطوة 2: تحويل JPG إلى نص – تهيئة المحرك

الآن بعد أن أصبحت المكتبة على جهازك، دعنا ننشئ `OcrEngine` يعمل دون اتصال.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 2.1: Create an OCR engine with offline resources.
        // This prevents the SDK from trying to download language data at runtime.
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            OfflineResources = true   // <-- crucial for production stability
        });

        // Step 2.2: Choose the language pack you need.
        // Here we use Russian; replace with OcrLanguage.English for English text.
        ocrEngine.Language = OcrLanguage.Russian;

        // Step 2.3: Perform OCR on a local JPG file.
        // The file path can be absolute or relative to the executable.
        var result = ocrEngine.RecognizeImage("YOUR_DIRECTORY/input.jpg");

        // Step 2.4: Output the extracted text.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(result.Text);
    }
}
```

### لماذا هذا مهم

- **وضع غير متصل** يضمن أوقات بدء تشغيل حتمية—بدون مكالمات شبكة مفاجئة عند نشرك على خادم مقفل.  
- **تعيين اللغة** (`OcrLanguage.Russian`) يخبر المحرك باستخدام مجموعة الأحرف الروسية، مما يزيد دقة التعرف من ~70 % إلى >95 % للصور النظيفة.  
- طريقة `RecognizeImage` تقبل أي تنسيق صورة يدعمه Aspose (`.jpg`, `.png`, `.tiff`, …). لهذا يمكننا **قراءة النص من JPG** دون خطوات تحويل إضافية.

## الخطوة 3: تعيين لغة OCR – معالجة لغات متعددة

أحيانًا تحتاج إلى معالجة مستندات تحتوي على لغات مختلطة (مثل الروسية والإنجليزية). يتيح لك Aspose OCR تحديد مصفوفة لغات *احتياطية*:

```csharp
// Example: Russian primary, English secondary
ocrEngine.Language = OcrLanguage.Russian;
ocrEngine.AdditionalLanguages = new[] { OcrLanguage.English };
```

> **ملاحظة:** يجب أن تكون حزم اللغة موجودة في مجلد `Resources` الخاص بمشروعك. إذا حصلت على استثناء `FileNotFoundException`، قم بتحميل الحزمة المفقودة من بوابة Aspose وضعها بجانب الملف التنفيذي.

## الخطوة 4: قراءة النص من JPG – المشكلات الشائعة والحلول

حتى مع حزمة اللغة الصحيحة، قد تواجه:

| المشكلة | العَرَض النموذجي | الحل السريع |
|-------|-----------------|-----------|
| انخفاض التباين | نص مشوش أو فارغ | تطبيق مرشح تمدد التباين البسيط باستخدام `System.Drawing` قبل OCR. |
| صورة مائلة | النص يظهر بشكل جانبي | استخدم `ocrEngine.ImageRotation = OcrRotation.Rotate90;` (أو 180/270) قبل استدعاء `RecognizeImage`. |
| حجم ملف كبير | التعرف بطيء، استهلاك عالي للذاكرة | إعادة تحجيم الصورة إلى حد أقصى 2000 بكسل على الجانب الأطول؛ تظل جودة OCR عالية. |

```csharp
using System.Drawing;
using System.Drawing.Imaging;

static string PreprocessAndRead(string jpgPath)
{
    // Load the original image
    using var original = new Bitmap(jpgPath);

    // Resize while preserving aspect ratio (max 2000px)
    int maxDim = 2000;
    int newWidth, newHeight;
    if (original.Width > original.Height)
    {
        newWidth = maxDim;
        newHeight = original.Height * maxDim / original.Width;
    }
    else
    {
        newHeight = maxDim;
        newWidth = original.Width * maxDim / original.Height;
    }

    using var resized = new Bitmap(original, new Size(newWidth, newHeight));

    // Optional: increase contrast (simple linear stretch)
    var contrast = new ImageAttributes();
    float[][] matrix = {
        new float[] {1.2f, 0, 0, 0, 0},
        new float[] {0, 1.2f, 0, 0, 0},
        new float[] {0, 0, 1.2f, 0, 0},
        new float[] {0, 0, 0, 1, 0},
        new float[] {0, 0, 0, 0, 1}
    };
    contrast.SetColorMatrix(new ColorMatrix(matrix));

    using var graphics = Graphics.FromImage(resized);
    graphics.DrawImage(resized, new Rectangle(0, 0, newWidth, newHeight), 0, 0, newWidth, newHeight, GraphicsUnit.Pixel, contrast);

    // Save to a temporary file (Aspose OCR works with file paths)
    string tempPath = Path.GetTempFileName() + ".jpg";
    resized.Save(tempPath, ImageFormat.Jpeg);

    // Run OCR
    var engine = new OcrEngine(new OcrEngineSettings { OfflineResources = true });
    engine.Language = OcrLanguage.Russian;
    var res = engine.RecognizeImage(tempPath);
    File.Delete(tempPath); // clean up
    return res.Text;
}
```

يمكنك الآن استدعاء `Console.WriteLine(PreprocessAndRead("YOUR_DIRECTORY/input.jpg"));` والحصول على نتيجة أنظف.

## مثال كامل يعمل – جميع الخطوات في ملف واحد

فيما يلي البرنامج *الكامل* الذي يمكنك نسخه ولصقه في `Program.cs`. يتضمن ملاحظات التثبيت، تكوين اللغة، ما قبل المعالجة، ومعالجة الأخطاء.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        string imagePath = "YOUR_DIRECTORY/input.jpg";

        try
        {

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}