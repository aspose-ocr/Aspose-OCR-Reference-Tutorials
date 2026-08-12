---
category: general
date: 2026-08-12
description: التعرف على النص من الصورة باستخدام Aspose OCR للغة C#. تعلم كيفية استخراج
  النص من PNG، تحويل الصورة إلى نص، ومعالجة اللغة السيريالية.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- extract text from png
- convert image to text
- c# image ocr
- aspose ocr c#
language: ar
lastmod: 2026-08-12
og_description: التعرف على النص من صورة باستخدام Aspose OCR في C#. يوضح هذا الدليل
  كيفية استخراج النص من PNG، تحويل الصورة إلى نص، والعمل مع اللغة السيريلية.
og_image_alt: Diagram showing the OCR processing flow from image file to recognized
  text output
og_title: التعرف على النص من الصورة في C# – دليل Aspose OCR الكامل
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: recognize text from image using Aspose OCR for C#. Learn how to extract
    text from PNG, convert image to text, and handle Cyrillic language.
  headline: recognize text from image in C# – step‑by‑step Aspose OCR guide
  type: TechArticle
- description: recognize text from image using Aspose OCR for C#. Learn how to extract
    text from PNG, convert image to text, and handle Cyrillic language.
  name: recognize text from image in C# – step‑by‑step Aspose OCR guide
  steps:
  - name: Expected console output
    text: '``` === Recognized Text === Привет мир! Это пример текста на кириллице.
      ```'
  - name: Recognize text from JPEG or BMP
    text: Replace the PNG file path with a JPEG or BMP file; the same `engine.Image`
      assignment works because Aspose.OCR auto‑detects the format.
  - name: Extract text from multiple pages
    text: 'If you need to **extract text from png** files that represent scanned pages,
      loop over the file list and concatenate the results:'
  - name: Convert image to text in an ASP.NET API
    text: 'Expose the OCR logic through a controller action:'
  type: HowTo
tags:
- Aspose OCR
- C#
- OCR
- Image processing
title: التعرف على النص من الصورة في C# – دليل Aspose OCR خطوة بخطوة
url: /ar/net/text-recognition/recognize-text-from-image-in-c-step-by-step-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من صورة في C# – دليل Aspose OCR خطوة بخطوة

إذا كنت بحاجة إلى **التعرف على النص من صورة** في تطبيق .NET، فإن هذا الدرس يقدم لك حلاً كاملاً وجاهزًا للتنفيذ. ستتعرف على كيفية استخراج النص من ملفات PNG، تحويل الصورة إلى نص، ومعالجة الأحرف السيريالية—كل ذلك باستخدام مكتبة Aspose.OCR للغة C#.

يغطي الدليل كل ما تحتاجه للبدء في استخدام OCR اليوم: حزم NuGet المطلوبة، إعداد اللغة، تحميل الصورة، ومعالجة الأخطاء. في النهاية ستحصل على برنامج كونسول يطبع السلسلة المعترف بها في الكونسول، وستفهم كيف تُكيّف الشيفرة لتدعم صيغ صور أو لغات أخرى.

## المتطلبات المسبقة

- .NET 6 SDK أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7.2)  
- Visual Studio 2022 أو أي محرر C# تفضله  
- اتصال بالإنترنت في المرة الأولى التي تشغل فيها البرنامج (Aspose.OCR يقوم بتحميل وحدات اللغة تلقائيًا)  
- صورة PNG تحتوي على نص قابل للقراءة (العينة تستخدم *cyrillic_sample.png*)

> **نصيحة احترافية:** احرص على أن تكون ملفات PNG أقل من 2 ميغابايت للحصول على معالجة أسرع. يمكن تقليل حجم الصور الأكبر قبل الـ OCR لتحسين الدقة.

## الخطوة 1: تثبيت حزمة Aspose.OCR عبر NuGet

افتح الطرفية في مجلد المشروع وشغّل الأمر التالي:

```bash
dotnet add package Aspose.OCR
```

تتضمن الحزمة محرك OCR الأساسي ووحدات اللغة الافتراضية. عندما تطلب لغة غير موجودة محليًا، يقوم Aspose بتحميلها تلقائيًا.

## الخطوة 2: إنشاء محرك OCR واختيار اللغة

محرك OCR هو الكائن المركزي الذي يقوم بالتحويل من الصورة إلى نص. للنص السيريالي تقوم بتعيين الخاصية `Language` إلى `Language.Cyrillic`. نفس الخاصية تعمل مع لغات أخرى مثل `Language.English`.

```csharp
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 2.1: Instantiate the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2.2: Choose the language module – Cyrillic in this example
        engine.Language = Language.Cyrillic;
```

**لماذا هذا مهم:** اختيار اللغة الصحيحة يحسّن من التعرف على الأحرف لأن المحرك يحمل القواميس والخطوط الخاصة بتلك اللغة. إذا تخطيت هذه الخطوة، سيتراجع المحرك إلى الإنجليزية وتصبح الأحرف السيريالية غير مفهومة.

## الخطوة 3: تحميل الصورة التي تريد معالجتها

يدعم Aspose.OCR صيغ صور متعددة، لكن PNG يُعد خيارًا شائعًا غير مضغوط يحافظ على حواف النص. استخدم `ImageStream.FromFile` لقراءة الملف إلى المحرك.

```csharp
        // Step 3: Load the PNG image that contains the text
        engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/cyrillic_sample.png");
```

استبدل `YOUR_DIRECTORY` بالمسار الفعلي لملف PNG الخاص بك. إذا كنت بحاجة إلى **استخراج النص من png** الموجود في مجلد مختلف، قم بتعديل المسار وفقًا لذلك.

## الخطوة 4: تنفيذ عملية OCR

استدعاء `engine.Recognize()` يشغّل خط أنابيب OCR ويعيد سلسلة نصية عادية. هذا هو جوهر وظيفة **تحويل الصورة إلى نص**.

```csharp
        // Step 4: Run OCR and get the recognized string
        string recognizedText = engine.Recognize();
```

تُطلق الطريقة استثناءً إذا تعذّر تحميل الصورة أو فشل تحميل وحدة اللغة. احرص على وضع الاستدعاء داخل كتلة try‑catch في الشيفرة الإنتاجية.

## الخطوة 5: عرض أو تخزين النتيجة المعترف بها

لعرض سريع يمكنك كتابة النتيجة إلى الكونسول. في التطبيقات الفعلية قد تحتاج لحفظها في قاعدة بيانات، ملف نصي، أو تمريرها إلى خدمة أخرى.

```csharp
        // Step 5: Output the recognized text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

### النتيجة المتوقعة في الكونسول

```
=== Recognized Text ===
Привет мир! Это пример текста на кириллице.
```

إذا احتوت الصورة على نص إنجليزي، ستكون النتيجة الجملة الإنجليزية المقابلة. نفس الشيفرة تعمل لمهام **c# image ocr** عبر لغات متعددة.

## الشيفرة الكاملة – جاهزة للنسخ

فيما يلي البرنامج الكامل، بما في ذلك توجيه `using` وجميع الخطوات في ملف واحد. انسخه إلى `Program.cs` وشغّل `dotnet run`.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        try
        {
            // Create an OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Select the Cyrillic language module (downloaded automatically if missing)
            engine.Language = Language.Cyrillic;

            // Load the image that contains Cyrillic text
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/cyrillic_sample.png");

            // Perform the OCR recognition
            string recognizedText = engine.Recognize();

            // Display the recognized text
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"OCR failed: {ex.Message}");
        }
    }
}
```

## التعامل مع المتغيّرات الشائعة

### التعرف على النص من JPEG أو BMP

استبدل مسار ملف PNG بملف JPEG أو BMP؛ تعيين `engine.Image` يبقى نفسه لأن Aspose.OCR يكتشف الصيغة تلقائيًا.

```csharp
engine.Image = ImageStream.FromFile("photo.jpg");
```

### استخراج النص من صفحات متعددة

إذا كنت بحاجة إلى **استخراج النص من png** التي تمثل صفحات ممسوحة، قم بالتكرار عبر قائمة الملفات وضم النتائج:

```csharp
string[] files = Directory.GetFiles("scans", "*.png");
var allText = new StringBuilder();

foreach (var file in files)
{
    engine.Image = ImageStream.FromFile(file);
    allText.AppendLine(engine.Recognize());
}
Console.WriteLine(allText.ToString());
```

### تحويل الصورة إلى نص في API ASP.NET

اعرض منطق OCR عبر إجراء في المتحكم:

```csharp
[HttpPost("api/ocr")]
public async Task<IActionResult> Ocr(IFormFile image)
{
    using var stream = image.OpenReadStream();
    OcrEngine engine = new OcrEngine { Language = Language.English };
    engine.Image = ImageStream.FromStream(stream);
    string text = engine.Recognize();
    return Ok(new { text });
}
```

هذا يوضح **c# image ocr** داخل خدمة ويب، مما يسمح للعملاء بتحميل أي صورة نقطية واستلام النص المستخرج بصيغة JSON.

## نصائح الأداء والحالات الخاصة

- **جودة الصورة:** تنخفض دقة OCR بشكل حاد عندما تكون الصورة غير واضحة أو ذات تباين منخفض. استخدم معالجة ما قبل الصورة (مثل الشحذ أو التحويل إلى ثنائي) قبل تمريرها إلى المحرك.  
- **الملفات الكبيرة:** بالنسبة للصور التي تتجاوز 5 MP، قم بتصغيرها إلى أقصى حد 2000 بكسل على الجانب الأطول. هذا يقلل استهلاك الذاكرة دون الإضرار بالتعرف.  
- **العودة إلى لغة افتراضية:** إذا عينت لغة غير مدعومة، يعود المحرك إلى الإنجليزية. تحقق دائمًا من `engine.Language` بعد التهيئة إذا كنت تقوم بتحميل وحدات اللغة ديناميكيًا.  
- **سلامة الخيوط:** كائنات `OcrEngine` غير آمنة للاستخدام المتعدد الخيوط. أنشئ محركًا جديدًا لكل طلب في بيئات متعددة الخيوط (مثل ASP.NET Core).

## الخلاصة

أنت الآن تعرف كيف **تتعرف على النص من صورة** في C# باستخدام Aspose.OCR. استعرض الدرس خطوات تثبيت الحزمة، إعداد اللغة، تحميل PNG، تنفيذ OCR، ومعالجة النتيجة. باستخدام هذه اللبنات يمكنك أيضًا **استخراج النص من png**، **تحويل الصورة إلى نص**، وبناء حلول **c# image ocr** قوية لسطح المكتب، الويب، أو السحابة.

بعد ذلك، استكشف وحدات لغات أخرى (مثل `Language.Spanish`) أو دمج نتائج OCR مع مكتبات معالجة اللغة الطبيعية. للحصول على تحسينات أعمق في الأداء، اطلع على وثائق Aspose.OCR حول معالجة الصور والقواميس المخصصة.

برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [استخراج النص من صورة – تحسين OCR مع Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)
- [كيفية استخراج النص من صورة باستخدام Aspose.OCR لـ .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}