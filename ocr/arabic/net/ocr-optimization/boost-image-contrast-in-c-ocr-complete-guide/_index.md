---
category: general
date: 2026-04-06
description: عزّز تباين الصورة وأزل ضوضاء الصورة لتحسين دقة OCR في C#. تعلم كيفية
  تحميل صورة OCR وكيفية تنفيذ OCR في C# باستخدام فلاتر Aspose OCR.
draft: false
keywords:
- boost image contrast
- remove image noise
- improve ocr accuracy
- load image ocr
- how to ocr c#
language: ar
og_description: عزّز تباين الصورة وأزل الضوضاء لتحسين دقة OCR في C#. يوضح هذا الدرس
  كيفية تحميل صورة OCR وكيفية تنفيذ OCR في C# باستخدام Aspose.
og_title: زيادة تباين الصورة في OCR باستخدام C# – دليل خطوة بخطوة
tags:
- OCR
- C#
- Image Processing
title: زيادة تباين الصورة في OCR باستخدام C# – دليل كامل
url: /ar/net/ocr-optimization/boost-image-contrast-in-c-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعزيز تباين الصورة في OCR باستخدام C# – دليل كامل

هل جربت يومًا **تعزيز تباين الصورة** على مسح غير ثابت فحصلت على نص مشوش؟ لست وحدك. في العديد من المشاريع الواقعية تكون الصورة مائلة، مليئة بالضوضاء، ومملة ببساطة، مما يجعل OCR يتعثر. الخبر السار؟ بعض الفلاتر الموضوعة بشكل صحيح يمكنها تحويل تلك الفوضى إلى نص نظيف وقابل للقراءة. في هذا الدرس سنستعرض خطوة بخطوة كيفية **تعزيز تباين الصورة**، **إزالة ضوضاء الصورة**، و**تحسين دقة OCR** باستخدام Aspose OCR في C#. في النهاية ستعرف كيف **تحمّل صورة OCR**، تشغل خط الأنابيب، وتجيب أخيرًا على السؤال القديم “**how to OCR C#**?” دون عناء.

سوف نغطي كل ما تحتاجه:

* إعداد محرك Aspose OCR
* إنشاء خط أنابيب الفلاتر (تصحيح الميل، إزالة الضوضاء، تعزيز التباين)
* تحميل صورة لـ OCR
* استخراج وطباعة النص المعترف به
* نصائح، مشاكل محتملة، وتنوعات قد تواجهها

لا روابط توثيق خارجية—فقط مثال مستقل قابل للتنفيذ يمكنك لصقه في Visual Studio ومشاهدة النتيجة.

## المتطلبات المسبقة – ما ستحتاجه قبل البدء

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6+ (or .NET Framework 4.6+) | Aspose.OCR يستهدف هذه البيئات |
| Aspose.OCR NuGet package (`Aspose.OCR`) | يوفر `OcrEngine` وفئات الفلاتر |
| A sample image (`noisy_rotated.jpg`) | يوضح تصحيح الميل، إزالة الضوضاء، وتعزيز التباين |
| Basic C# knowledge | حتى تتمكن من تعديل الكود لاحقًا |

إذا كان لديك مشروع بالفعل، فقط أضف حزمة NuGet:

```bash
dotnet add package Aspose.OCR
```

هذا كل شيء—لا ملفات DLL إضافية، ولا تبعيات أصلية.

## الخطوة 1: تهيئة محرك OCR (بدء تعزيز تباين الصورة)

إنشاء المحرك هو الأساس. فكر في `OcrEngine` كالعقل الذي سيقرأ الأحرف لاحقًا بعد أن نقوم بتنظيف الصورة.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **لماذا؟** يحتفظ المحرك بالإعدادات، إعدادات اللغة، وخط أنابيب الفلاتر الذي سنبنيه لاحقًا. بدون ذلك، لا شيء يعمل.

## الخطوة 2: بناء خط أنابيب الفلاتر – تصحيح الميل، إزالة الضوضاء، **تعزيز تباين الصورة**

يتم تطبيق الفلاتر بالترتيب الذي تضيفها به. هنا نقوم أولاً بتصحيح الصورة (deskew)، ثم نخفف البقع الحبيبية (denoise)، وأخيرًا نرفع التباين حتى تبرز الأحرف.

```csharp
// DeskewFilter – corrects rotation up to 5 degrees
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 5 });

// DenoiseFilter – reduces noise with moderate strength
ocrEngine.Filters.Add(new DenoiseFilter { Strength = 2 });

// ContrastBoostFilter – enhances contrast for better character detection
ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.5f });
```

### ما يفعله كل فلتر

* **DeskewFilter**: المسحات المائلة شائعة عندما يلتقط المستخدمون صورًا بهواتفهم. زاوية قصوى قدرها 5° تلتقط معظم الانحرافات العرضية.
* **DenoiseFilter**: المسحات من الكاميرات الرخيصة غالبًا ما تحتوي على حبيبات. القوة = 2 هي نقطة مثالية—كافية للتنعيم دون تشويش الحواف.
* **ContrastBoostFilter**: هنا نقوم **بتعزيز تباين الصورة**. بزيادة `Level` إلى `1.5f`، يصبح الحبر الداكن أغمق والخلفية أفتح، مما يحسن **دقة OCR** بشكل كبير.

> **نصيحة احترافية:** إذا كانت صور المصدر ذات تباين عالي بالفعل، قلل `Level` لتجنب القص.

## الخطوة 3: تحميل الصورة لـ OCR – **Load Image OCR** بسيط

الآن نقوم بتحميل الصورة إلى الذاكرة. استخدام `System.Drawing.Image.FromFile` يعمل لمعظم الصيغ الشائعة (JPG، PNG، BMP).

```csharp
// Replace with the path to your own image
string imagePath = @"YOUR_DIRECTORY/noisy_rotated.jpg";

using (var inputImage = Image.FromFile(imagePath))
{
    // The rest of the steps go inside this block
}
```

> **لماذا نستخدم كتلة `using`؟** يضمن تحرير مقبض الصورة بسرعة، مما يمنع مشاكل قفل الملفات على Windows.

## الخطوة 4: تشغيل التعرف – جوهر **How to OCR C#**

داخل كتلة `using` نستدعي `Recognize`. يقوم المحرك تلقائيًا بتشغيل خط أنابيب الفلاتر الذي قمنا بتكوينه مسبقًا.

```csharp
    // Recognize text from the image
    var ocrResult = ocrEngine.Recognize(inputImage);

    // Output the recognized text to the console
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
```

### النتيجة المتوقعة

إذا كانت الصورة المصدر تحتوي على العبارة “Hello World”، سيطبع الطرفية شيئًا مثل:

```
=== OCR Output ===
Hello World
```

إذا ظهر النص مشوشًا، تحقق مرة أخرى من إعدادات الفلاتر—ربما تحتاج الصورة إلى إزالة ضوضاء أقوى أو مستوى تباين أعلى.

## الخطوة 5: مثال كامل قابل للتنفيذ (جميع الخطوات مجمعة)

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في تطبيق وحدة تحكم جديد (`dotnet new console`). تأكد من أن مسار الصورة يشير إلى ملف حقيقي على القرص.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Build a filter pipeline to improve image quality
        //   • DeskewFilter – corrects rotation up to 5 degrees
        //   • DenoiseFilter – reduces noise with moderate strength
        //   • ContrastBoostFilter – enhances contrast for better character detection
        ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 5 });
        ocrEngine.Filters.Add(new DenoiseFilter { Strength = 2 });
        ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.5f });

        // Step 3: Load the image that needs OCR processing
        string imagePath = @"YOUR_DIRECTORY/noisy_rotated.jpg";
        using (var inputImage = Image.FromFile(imagePath))
        {
            // Step 4: Recognize text from the image
            var ocrResult = ocrEngine.Recognize(inputImage);

            // Step 5: Output the recognized text to the console
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

شغّل `dotnet run` وشاهد السحر يحدث. لقد **عززت تباين الصورة**، **أزلت ضوضاء الصورة**، و**حسّنت دقة OCR**—كل ذلك في بضع أسطر من C#.

## أسئلة شائعة وحالات خاصة

### 1. ماذا لو كانت صوري بصيغة PNG؟

`Image.FromFile` يدعم PNG مباشرةً. لا حاجة لتغيير الكود—فقط وجه `imagePath` إلى ملف PNG.

### 2. لا يزال النص غير واضح بعد الفلاتر. أي أفكار؟

* زيادة `ContrastBoostFilter.Level` إلى `2.0f` أو أعلى.
* رفع `DenoiseFilter.Strength` إلى `3` للمسحات ذات الحبيبات الكثيفة.
* إذا تجاوزت زاوية الميل 5°، قم بزيادة `DeskewFilter.MaxAngle` إلى `10`.

### 3. هل يمكنني معالجة عدة صور دفعة واحدة؟

بالطبع. غلف منطق التعرف داخل حلقة:

```csharp
foreach (var file in Directory.GetFiles(@"C:\Images", "*.jpg"))
{
    using var img = Image.FromFile(file);
    var result = ocrEngine.Recognize(img);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

المحرك يعيد استخدام نفس خط أنابيب الفلاتر، مما يوفر وقت التهيئة.

### 4. هل يدعم Aspose OCR لغات غير الإنجليزية؟

نعم. قم بتعيين اللغة قبل التعرف:

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, etc.
```

تأكد من تثبيت حزمة اللغة المناسبة (عادةً ما تكون مدمجة مع حزمة NuGet).

## نصائح الأداء – الحصول على أقصى استفادة من OCR الخاص بك

* **إعادة استخدام `OcrEngine`**: إن إنشاؤه مرة واحدة وإعادة استخدامه للعديد من الصور يقلل من الحمل الزائد.
* **تغيير حجم الصور الكبيرة**: إذا كان مصدر الصورة أكبر من 2000 بكسل عرضًا، قلل الحجم إلى حوالي 1200 بكسل قبل إرساله إلى المحرك. الصور الأصغر تعالج أسرع وغالبًا ما تعطي نفس الدقة بعد تعزيز التباين.
* **التوازي بأمان**: `OcrEngine` غير آمن للاستخدام المتعدد الخيوط، لكن يمكنك إنشاء مجموعة من المحركات وتخصيص كل منها إلى خيط منفصل.

## الخلاصة – ما أنجزناه

بدأنا بصورة JPEG غير واضحة ومائلة، ومن خلال خط أنابيب فلاتر مختصر، **عززنا تباين الصورة**، **أزلنا ضوضاء الصورة**، و**حسّنا دقة OCR**. يوضح الكود النهائي طريقة نظيفة لـ **load image OCR**، تشغيل التعرف، وطباعة النتيجة—مجيبًا على السؤال الكلاسيكي “**how to OCR C#**?” مرة واحدة وإلى الأبد.

ما الخطوات التالية؟ جرّب استبدال `ContrastBoostFilter` بـ `GammaCorrectionFilter` إذا كنت تحتاج إلى تحكم أدق، أو جرب **قواميس مخصصة للغة** لرفع الدقة أكثر. يمكنك أيضًا استكشاف حفظ الصورة المنقحة إلى القرص (`inputImage.Save("cleaned.png")`) قبل التعرف—مفيد للتصحيح.

لا تتردد في تعديل خط الأنابيب لبياناتك الخاصة، وبرمجة سعيدة! إذا واجهت أي مشاكل، اترك تعليقًا أدناه—دعنا نحلها معًا.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}