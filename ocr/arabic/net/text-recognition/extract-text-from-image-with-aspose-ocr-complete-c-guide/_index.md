---
category: general
date: 2026-05-28
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلّم كيفية استخراج
  نص OCR، تحميل الصورة للـ OCR، والتعرف على النص من ملفات TIF بسرعة.
draft: false
keywords:
- extract text from image
- how to extract ocr text
- load image for ocr
- recognize text from tif
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR في C#. يوضح هذا الدرس كيفية
  استخراج نص OCR، تحميل الصورة للـ OCR، والتعرف على النص من ملفات TIF.
og_title: استخراج النص من الصورة باستخدام Aspose OCR – دليل كامل بلغة C#
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Extract text from image using Aspose OCR in C#. Learn how to extract
    OCR text, load image for OCR, and recognize text from TIF files quickly.
  headline: Extract Text from Image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract text from image using Aspose OCR in C#. Learn how to extract
    OCR text, load image for OCR, and recognize text from TIF files quickly.
  name: Extract Text from Image with Aspose OCR – Complete C# Guide
  steps:
  - name: '**Wrong file path** – A typo leads to a `FileNotFoundException`. Double‑check
      the path or use `Path.Combine` for cross‑platform safety.'
    text: '**Wrong file path** – A typo leads to a `FileNotFoundException`. Double‑check
      the path or use `Path.Combine` for cross‑platform safety.'
  - name: '**Unsupported format** – Aspose OCR supports PNG, JPEG, BMP, and TIFF.
      Trying a PDF directly will throw an `UnsupportedFormatException`. Convert first
      if needed.'
    text: '**Unsupported format** – Aspose OCR supports PNG, JPEG, BMP, and TIFF.
      Trying a PDF directly will throw an `UnsupportedFormatException`. Convert first
      if needed.'
  - name: '**Large image size** – Very high‑resolution TIFFs can consume memory. Consider
      down‑scaling with `engine.Options.Dpi = 300` before recognition.'
    text: '**Large image size** – Very high‑resolution TIFFs can consume memory. Consider
      down‑scaling with `engine.Options.Dpi = 300` before recognition.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: استخراج النص من الصورة باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة باستخدام Aspose OCR – دليل C# كامل

استخراج النص من الصورة هو عائق شائع عندما تحتاج إلى رقمنة المستندات الممسوحة ضوئياً، الإيصالات، أو حتى صورة للسبورة. إذا كنت تتساءل **كيف تستخرج نص OCR** في مشروع .NET، فأنت في المكان الصحيح—هذا الدليل يرافقك خلال العملية بأكملها، من تحميل الصورة إلى استخراج الأحرف المعترف بها من ملف TIF.

سنغطي كل ما تحتاج معرفته: إنشاء محرك OCR، تحميل الصورة للـ OCR، إجراء التعرف بشكل غير متزامن، وأخيراً طباعة النص المستخرج إلى وحدة التحكم. في النهاية ستحصل على مقتطف قابل للتنفيذ يعمل مع أي ملف TIFF (أو صيغ مدعومة أخرى) وفهم قوي لأهمية كل خطوة.

## ما ستحتاجه

- .NET 6 أو أحدث (الكود يُجمّع أيضاً على .NET Core 3.1+)
- حزمة NuGet الخاصة بـ Aspose.OCR (`Aspose.OCR`) مُثبتة في مشروعك
- صورة TIFF نموذجية (`page1.tif`) موجودة في مكان يمكنك الإشارة إليه
- محرر شفرة أو بيئة تطوير متكاملة (Visual Studio، VS Code، Rider—ما تفضله)

لا توجد ملفات إعداد إضافية، ولا محركات OCR ثقيلة تحتاج تثبيتها محلياً—Aspose يتولى كل الأعمال الصعبة نيابةً عنك.

---

## استخراج النص من الصورة – الخطوة 1: تهيئة محرك OCR

قبل أن يتم معالجة أي صورة، تحتاج إلى إنشاء نسخة من `OcrEngine`. فكر في المحرك كالعقل الذي يعرف كيف يقرأ الأحرف؛ بدون هذا المحرك، لا شيء يدفع بقية سير العمل.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static async Task Main()
    {
        // Step 1: Create an OCR engine instance
        var engine = new OcrEngine();
```

> **لماذا هذا مهم:** `OcrEngine` يضم خوارزميات التعرف وحزم اللغات. إنشاء نسخة واحدة لكل عملية يقلل من استهلاك الذاكرة ويمنحك نقطة واضحة لتعديل الإعدادات لاحقاً (مثل اللغة، DPI).

---

## كيفية استخراج نص OCR – الخطوة 2: تحميل الصورة للـ OCR

الآن بعد أن أصبح المحرك جاهزاً، يجب أن نوجهه إلى الصورة التي نريد قراءتها. توفر Aspose الدالة `ImageStream.FromFile`، التي تُبث الملف دون تحميل الصورة بالكامل إلى الذاكرة—وذلك تحسين أداء ملحوظ للملفات الكبيرة من نوع TIFF.

```csharp
        // Step 2: Load the image to be recognized
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/page1.tif");
```

> **نصيحة احترافية:** استبدل `YOUR_DIRECTORY` بالمسار المطلق أو النسبي لصورتك. إذا كنت تشغّل التطبيق من مجلد المشروع، فإن `@"./page1.tif"` يعمل بشكل جيد.  
> **حالة حافة:** ملفات TIFF يمكن أن تحتوي على صفحات متعددة. `ImageStream.FromFile` يقرأ الصفحة الأولى افتراضياً؛ إذا احتجت صفحة أخرى، استخدم `ImageStream.FromFile(path, pageNumber)`.

---

## التعرف على النص من TIF – الخطوة 3: تنفيذ OCR غير متزامن

حجب الخيط المستدعي أثناء عمل محرك OCR قد يجمد تطبيقات الواجهة أو يضيع موارد الخادم. استخدام `RecognizeAsync` يسمح للعملية بالعمل في الخلفية، مع إرجاع `Task<string>` يتحول إلى النص المستخرج عند الانتهاء.

```csharp
        // Step 3: Perform OCR asynchronously (does not block the calling thread)
        string extractedText = await engine.RecognizeAsync();
```

> **لماذا غير متزامن؟** في واجهة برمجة تطبيقات الويب أو تطبيق سطح المكتب، تريد أن يبقى تجمع الخيوط مستجيباً. `await` يعيد التحكم إلى المستدعي حتى يكتمل الـ OCR، مما يحافظ على سلاسة الواجهة أو يترك خيط الطلب حرًا لأعمال أخرى.

---

## إخراج النص المستخرج – الخطوة 4: الطباعة أو التخزين

أخيرًا، نكتب النتيجة إلى وحدة التحكم. في سيناريوهات العالم الحقيقي قد تكتب إلى قاعدة بيانات، ملف، أو تمرّر السلسلة إلى خدمة أخرى.

```csharp
        // Step 4: Output the recognized text
        Console.WriteLine(extractedText);
    }
}
```

### النتيجة المتوقعة

إذا كان `page1.tif` يحتوي على النص *“Hello, Aspose OCR!”*، ستظهر النتيجة في وحدة التحكم كالتالي:

```
Hello, Aspose OCR!
```

إذا كانت الصورة مشوشة، قد ترى فواصل أسطر إضافية أو أحرف غير مُعترف بها—قم بضبط `Options` للمحرك (مثلًا `engine.Options.DetectLanguage = true`) لتحسين الدقة.

---

## المشكلات الشائعة عند تحميل الصورة للـ OCR

1. **مسار الملف غير صحيح** – الخطأ المطبعي يؤدي إلى `FileNotFoundException`. تحقق من المسار أو استخدم `Path.Combine` لضمان السلامة عبر الأنظمة.  
2. **صيغة غير مدعومة** – Aspose OCR يدعم PNG، JPEG، BMP، وTIFF. محاولة معالجة PDF مباشرة ستؤدي إلى `UnsupportedFormatException`. قم بالتحويل أولاً إذا لزم الأمر.  
3. **حجم الصورة كبير** – ملفات TIFF ذات الدقة العالية قد تستهلك الذاكرة. فكر في تقليل الدقة باستخدام `engine.Options.Dpi = 300` قبل التعرف.

---

## التعمق أكثر: تعديل إعدادات التعرف

Aspose.OCR يأتي مع مجموعة من الخيارات التي يمكنك تعديلها:

```csharp
engine.Options.Language = Language.English;      // Force English if you know the language
engine.Options.Dpi = 200;                       // Reduce DPI for faster processing
engine.Options.IsAutoRotate = true;            // Auto‑rotate skewed pages
```

جرّب هذه الخيارات لتحقيق توازن بين السرعة والدقة.

---

## مثال كامل قابل للتنفيذ (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل الذي يمكنك وضعه في مشروع وحدة تحكم جديد. يتضمن الإعدادات الاختيارية التي نوقشت أعلاه.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static async Task Main()
    {
        // Create the OCR engine
        var engine = new OcrEngine();

        // Optional: fine‑tune recognition
        engine.Options.Language = Language.English;
        engine.Options.Dpi = 200;
        engine.Options.IsAutoRotate = true;

        // Load the image (replace with your actual path)
        engine.Image = ImageStream.FromFile(@"./page1.tif");

        // Run OCR asynchronously
        string extractedText = await engine.RecognizeAsync();

        // Show the result
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

احفظ الملف باسم `Program.cs`، شغّل `dotnet add package Aspose.OCR`، ثم `dotnet run`. يجب أن ترى النص المستخرج يُطبع في وحدة التحكم.

---

## ملخص

لقد أوضحنا للتو **كيفية استخراج نص OCR** من صورة TIFF باستخدام Aspose OCR في C#. الخطوات—تهيئة المحرك، تحميل الصورة للـ OCR، التعرف على النص من TIF بشكل غير متزامن، وإخراج النتيجة—تغطي دورة الحياة الكاملة لاستخراج النص من ملفات الصور.

إذا كنت مستعدًا للانتقال إلى ما هو أكثر من النص العادي، استكشف `PdfConverter` من Aspose لدمج ناتج OCR في ملفات PDF قابلة للبحث، أو استخدم `engine.Options` للتعامل مع مستندات متعددة اللغات.

---

## ما التالي؟

- **معالجة دفعات:** تكرار عبر مجلد من ملفات TIFF وتخزين كل نتيجة في قاعدة بيانات.  
- **معالجة مسبقة للصور:** استخدم `System.Drawing` أو `ImageSharp` لتنظيف المسحات المشوشة قبل تمريرها إلى محرك OCR.  
- **دمج مع ASP.NET Core:** أنشئ نقطة نهاية تستقبل صورة مرفوعة وتعيد النص المعترف به كـ JSON.

لا تتردد في التجربة، وكسر الأشياء، ثم العودة إلى هذا الدليل لتحديث معلوماتك. إذا واجهت أي صعوبات، فإن وثائق Aspose OCR تُعد رفيقًا موثوقًا، لكن النمط الأساسي يبقى نفسه: **استخراج النص من الصورة**، **تحميل الصورة للـ OCR**، **التعرف على النص من TIF**، ومعالجة النتيجة.

برمجة سعيدة، ولتكن صورك دائمًا واضحة كالبلور!

## دروس ذات صلة

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}