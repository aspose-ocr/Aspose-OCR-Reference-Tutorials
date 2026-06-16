---
category: general
date: 2026-02-22
description: التعرف على النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية تحميل
  صورة TIFF، إنشاء محرك OCR، واستخراج النص من الصورة بكفاءة.
draft: false
keywords:
- recognize text from image
- load tiff image
- extract text from image
- create OCR engine
language: ar
og_description: التعرف على النص من الصورة خطوة بخطوة. تعلم كيفية تحميل صورة TIFF،
  إنشاء محرك OCR، واستخراج النص من الصورة باستخدام Aspose OCR في C#.
og_title: التعرف على النص من الصورة – دليل Aspose OCR كامل بلغة C#
tags:
- C#
- Aspose OCR
- Image Processing
title: التعرف على النص من الصورة باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة – دليل كامل C# Aspose OCR

هل احتجت يومًا إلى **التعرف على النص من الصورة** لكن شعرت بأنك عالق عند السطر الأول من الشيفرة؟ لست وحدك. في العديد من المشاريع—مسح الفواتير، رقمنة الأرشيفات، أو بناء مكتبة PDF قابلة للبحث—الحصول على نص نظيف من صورة هو العائق الأول.

خبر سار: باستخدام Aspose OCR يمكنك تحميل صورة TIFF، تشغيل محرك OCR، و**استخراج النص من الصورة** في بضع أسطر فقط. في هذا الدليل سنستعرض كامل العملية، من تحميل ملف TIFF عالي الدقة إلى طباعة النص المعترف به ووقت المعالجة.

سنغطي أيضًا بعض سيناريوهات “ماذا لو”، مثل تعطيل تسريع GPU أو معالجة ملفات TIFF متعددة الصفحات، حتى لا تتفاجأ عندما تبدو بياناتك الواقعية مختلفة قليلاً. في النهاية، ستحصل على تطبيق كونسول جاهز للتشغيل يستطيع **التعرف على النص من الصورة** بشكل موثوق.

## المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضًا)
- حزمة NuGet Aspose.OCR (`dotnet add package Aspose.OCR`)
- ملف TIFF تريد معالجته (العينة تستخدم `high_res_page.tif`)
- أي بيئة تطوير تفضلها—Visual Studio أو Rider أو VS Code ستكفي

لا توجد مكتبات أصلية إضافية مطلوبة؛ Aspose يتعامل مع كل شيء داخليًا، بما في ذلك دعم GPU الاختياري.

## الخطوة 1: تحميل صورة TIFF

أول شيء عليك فعله هو جلب بيانات الصورة إلى الذاكرة. توفر Aspose طريقة ثابتة `Image.Load` تعمل مع معظم الصيغ الشائعة، بما في ذلك TIFF.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Load the TIFF file – replace the path with your own image location
var inputImage = Image.Load(@"YOUR_DIRECTORY/high_res_page.tif");
```

**لماذا هذا مهم:** غالبًا ما تحتوي ملفات TIFF على صفحات متعددة أو بيانات عالية الدقة التي تتعطل أمامها المكتبات الأخرى. يقوم محمل Aspose بقراءة الملف بشكل صحيح ويحافظ على عمق البكسل، وهو أمر حاسم للحصول على OCR دقيق لاحقًا.

*نصيحة احترافية:* إذا كنت تتعامل مع TIFF متعدد الصفحات، يمكنك التكرار عبر `inputImage.Frames` ومعالجة كل إطار على حدة. بهذه الطريقة لن تفوت أي نص مخفي في الصفحات اللاحقة.

## الخطوة 2: إنشاء محرك OCR

الآن بعد أن أصبحت الصورة في الذاكرة، تحتاج إلى محرك يعرف كيفية قراءة الأحرف. فئة `OcrEngine` هي المكان الذي تقوم فيه بضبط اللغة، واستخدام GPU، وغيرها من الخيارات.

```csharp
// Initialize the OCR engine with desired settings
var ocrEngine = new OcrEngine
{
    // Enable GPU acceleration for faster processing (optional, requires compatible hardware)
    UseGpu = true,
    // Set the language to English – you can change this to Language.French, etc.
    Language = Language.English
};
```

**لماذا هذا مهم:** تمكين GPU (`UseGpu = true`) يمكن أن يقلل وقت المعالجة بشكل كبير على الأجهزة الداعمة، لكن من الآمن تركه معطلاً إذا كنت تعمل على خادم CI أو حاسوب محمول منخفض المواصفات. أيضًا، اختيار اللغة الصحيحة يحسن من التعرف على الأحرف لأن المحرك يحمل قواميس مخصصة للغة.

*احذر:* إذا نسيت ضبط `Language`، فإن المحرك يفرض اللغة الإنجليزية افتراضيًا، مما قد ينتج عنه نتائج غريبة على النصوص غير اللاتينية.

## الخطوة 3: التعرف على النص من الصورة

مع جاهزية المحرك، استدعاء OCR الفعلي هو طريقة واحدة: `Recognize`. تُعيد كائن `OcrResult` يحتوي على النص المستخرج ومقاييس الأداء.

```csharp
// Perform OCR on the loaded image
var ocrResult = ocrEngine.Recognize(inputImage);
```

يقدم لك `OcrResult` خاصيتين مفيدتين:

- `Text` – تمثيل النص العادي لكل ما استطاع المحرك قراءته.
- `ProcessingTime` – مدة استغراق OCR، مقاسة بالميليثانية.

## الخطوة 4: مراجعة النتائج

أخيرًا، لنطبع ما حصلنا عليه. في تطبيق حقيقي قد تكتب النص إلى قاعدة بيانات، لكن لأغراض العرض يكون إخراج الكونسول كافيًا.

```csharp
// Show how long the OCR took and the recognized text
Console.WriteLine($"Recognized in {ocrResult.ProcessingTime} ms");
Console.WriteLine("=== Extracted Text Start ===");
Console.WriteLine(ocrResult.Text);
Console.WriteLine("=== Extracted Text End ===");
```

**الناتج المتوقع** (نصك سيختلف بالطبع):

```
Recognized in 842 ms
=== Extracted Text Start ===
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
...
=== Extracted Text End ===
```

إذا كان الناتج مشوشًا، تحقق مرة أخرى من وضوح الصورة وأنك اخترت اللغة الصحيحة. يمكنك أيضًا تعديل خصائص `ocrEngine` مثل `PreprocessOptions` لتقليل الضوضاء.

## معالجة الحالات الحدية

### 1. لا GPU؟ لا مشكلة.

```csharp
ocrEngine.UseGpu = false; // fallback to CPU‑only processing
```

معالجة الـ CPU أبطأ (غالبًا 2‑3 مرات)، لكنها تعمل على كل جهاز Windows أو Linux أو macOS.

### 2. ملفات TIFF متعددة الصفحات

```csharp
foreach (var frame in inputImage.Frames)
{
    var pageResult = ocrEngine.Recognize(frame);
    Console.WriteLine(pageResult.Text);
}
```

يُعامل كل إطار كصورة منفصلة، لذا ستحصل على قطعة نصية لكل صفحة.

### 3. لغات مختلفة

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, Language.German, etc.
```

تبديل اللغات يحمل مجموعة الأحرف والقاموس المناسب، مما يحسن الدقة بشكل كبير للمستندات غير الإنجليزية.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع كونسول جديد (`dotnet new console`). يتضمن جميع الأجزاء التي ناقشناها، بالإضافة إلى بعض فحوصات الأمان.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the TIFF image you want to process
        // -------------------------------------------------
        const string imagePath = @"YOUR_DIRECTORY/high_res_page.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"Error: File not found at {imagePath}");
            return;
        }

        var inputImage = Image.Load(imagePath);

        // -------------------------------------------------
        // Step 2: Create and configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,                 // optional – set to false if GPU not available
            Language = Language.English    // change if you need another language
        };

        // -------------------------------------------------
        // Step 3: Perform OCR on the loaded image
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 4: Display processing time and extracted text
        // -------------------------------------------------
        Console.WriteLine($"Recognized in {ocrResult.ProcessingTime} ms");
        Console.WriteLine("=== Extracted Text Start ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("=== Extracted Text End ===");

        // Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

احفظ الملف، شغّل `dotnet run`، وشاهد الكونسول يطبع النص المعترف به. هذا كل شيء—خط أنابيب **التعرف على النص من الصورة** جاهز ويعمل.

## الأسئلة المتكررة

**س: هل يعمل هذا مع PNG أو JPEG؟**  
ج: بالتأكيد. `Image.Load` يكتشف الصيغة تلقائيًا، لذا يمكنك استبدال امتداد `.tif` بـ `.png` أو `.jpg` أو حتى `.bmp`. يتعامل محرك OCR معها بنفس الطريقة.

**س: ناتجي يحتوي على الكثير من الرموز العشوائية.**  
ج: جرّب تمكين المعالجة المسبقة: `ocrEngine.PreprocessOptions = new PreprocessOptions { RemoveNoise = true, Deskew = true };`. هذا ينظف الصورة قبل التعرف.

**س: هل يمكنني الحصول على إطارات الحدود لكل كلمة؟**  
ج: نعم. `ocrResult.Regions` يحتوي على كائنات `OcrRegion` مع الإحداثيات. قم بالتكرار عبرها إذا كنت بحاجة لتسليط الضوء على الكلمات في واجهة المستخدم.

## الخلاصة

لقد أظهرنا لك الآن كيفية **التعرف على النص من الصورة** باستخدام Aspose OCR في C#. بدءًا من تحميل ملف TIFF، ثم **إنشاء محرك OCR**، تشغيل عملية التعرف، وأخيرًا عرض النتائج—كل خطوة مختصرة، مشروحة بالكامل، وجاهزة للنسخ إلى مشروعك الخاص.

من هنا قد تستكشف معالجة دفعات من المجلدات، تخزين النتائج في فهرس قابل للبحث، أو دمج OCR مع واجهات برمجة تطبيقات الترجمة. مهما كان اختيارك، يبقى النمط الأساسي هو نفسه: تحميل الصورة، ضبط المحرك، التعرف، ومعالجة الناتج.

هل لديك المزيد من الأسئلة حول تحميل صور TIFF، استخراج النص من الصورة، أو تعديل محرك OCR؟ اترك تعليقًا أدناه، وبرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}