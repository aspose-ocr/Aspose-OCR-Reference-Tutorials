---
category: general
date: 2026-02-22
description: تحويل الصورة إلى نص باستخدام Aspose OCR في C#. تعلّم كيفية تسجيل وحدة
  اللغة، تحميل الصورة للتعرف الضوئي على الأحرف واستخراج النص من الصورة بما في ذلك
  دعم اللغة السيريالية.
draft: false
keywords:
- convert image to text
- extract text from image
- how to register module
- load image for ocr
- how to recognize cyrillic
language: ar
og_description: حوّل الصورة إلى نص على الفور. يوضح هذا الدليل كيفية تسجيل الوحدة،
  تحميل الصورة للتعرف الضوئي على الأحرف، واستخراج النص من الصورة، بما في ذلك التعرف
  على السيريلي.
og_title: تحويل الصورة إلى نص باستخدام Aspose OCR – دليل C# كامل
tags:
- Aspose OCR
- C#
- Image Processing
title: تحويل الصورة إلى نص باستخدام Aspose OCR – دليل خطوة بخطوة بلغة C#
url: /ar/net/text-recognition/convert-image-to-text-with-aspose-ocr-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصورة إلى نص باستخدام Aspose OCR – دليل خطوة‑بخطوة بلغة C#

هل احتجت يومًا إلى **تحويل الصورة إلى نص** لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك—فالكثير من المطورين يواجهون صعوبة عندما تحتوي الصورة على أحرف غير لاتينية مثل السيريلي. في هذا الدرس سنستعرض حلًا كاملاً جاهزًا للتنفيذ يوضح لك كيفية تسجيل وحدة لغة، تحميل صورة للـ OCR، وأخيرًا استخراج النص من الصورة باستخدام Aspose OCR لـ .NET.

سنغطي كل شيء بدءًا من تثبيت حزمة NuGet وحتى التعامل مع الحالات الخاصة مثل ملفات اللغة المفقودة. بنهاية هذا الدليل ستتمكن من **تحويل الصورة إلى نص** في بضع أسطر فقط من C# وستفهم *لماذا* كل خطوة مهمة.

## ما ستتعلمه

- كيف تقوم **بتسجيل وحدة اللغة السيريلي** حتى يتمكن محرك OCR من فهم النص.  
- الطريقة الصحيحة **لتحميل الصورة للـ OCR** باستخدام طريقة `Image.Load` الخاصة بـ Aspose.  
- كيف تضبط المحرك **للتعرف على السيريلي** ثم **استخراج النص من الصورة**.  
- نصائح لتجاوز المشكلات الشائعة مثل وحدات zip الفاسدة أو صيغ الصور غير المدعومة.  

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+).  
- Visual Studio 2022 (أو أي بيئة تطوير تدعم C#).  
- حزمة NuGet الخاصة بـ Aspose.OCR (`Install-Package Aspose.OCR`).  
- ملف zip للغة السيريلي (`cyrillic.zip`) وصورة نموذجية (`cyrillic_sample.jpg`).  

> **نصيحة احترافية:** احتفظ بوحدات اللغة في مجلد مخصص (مثال: `./ocr-modules/`) لتجنب الأخطاء المتعلقة بالمسارات.

---

## الخطوة 1: كيفية تسجيل الوحدة – إضافة دعم السيريلي

قبل أن يتمكن محرك OCR من قراءة الأحرف السيريلي يجب أن تخبره بمكان وجود بيانات اللغة. هذا هو جزء **كيفية تسجيل الوحدة** من العملية.

```csharp
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to the Cyrillic language module (ZIP file)
string languageModulePath = Path.Combine("ocr-modules", "cyrillic.zip");

// Read the ZIP file into a byte array
byte[] moduleBytes = File.ReadAllBytes(languageModulePath);

// Register the module with the OCR engine
OcrEngine.RegisterLanguageModule(Language.Cyrillic, moduleBytes);
```

**لماذا التسجيل؟**  
Aspose OCR يأتي بمجموعة افتراضية من اللغات اللاتينية لتقليل حجم المكتبة. من خلال تسجيل وحدة السيريلي تقوم بتمديد قاموس المحرك، مما يسمح له بربط الرموز بالحروف Unicode بشكل صحيح. تخطي هذه الخطوة يجعل المحرك يلجأ إلى التخمين، مما ينتج مخرجات مشوشة.

> **خطأ شائع:** استخدام مسار نسبي يشير إلى الدليل الخطأ. احرص دائمًا على بناء المسار باستخدام `Path.Combine` أو التحقق منه بـ `File.Exists` قبل استدعاء `RegisterLanguageModule`.

---

## الخطوة 2: تحميل الصورة للـ OCR – إعداد الإدخال

الآن بعد أن أصبحت اللغة جاهزة، نحتاج إلى جلب الصورة إلى الذاكرة. هذه هي خطوة **تحميل الصورة للـ OCR**.

```csharp
using Aspose.OCR;

// Ensure the image exists
string imagePath = Path.Combine("ocr-images", "cyrillic_sample.jpg");
if (!File.Exists(imagePath))
{
    Console.WriteLine($"Image not found: {imagePath}");
    return;
}

// Load the image – Aspose automatically detects format (JPEG, PNG, BMP, etc.)
Image inputImage = Image.Load(imagePath);
```

**لماذا التحميل بهذه الطريقة؟**  
`Image.Load` يخفف عنك اكتشاف الصيغة وتحويل مساحة الألوان، مما يمنحك كائن `Image` متسق بغض النظر عن نوع ملف المصدر. هذا يقلل من احتمال حدوث أخطاء *Unsupported format* التي غالبًا ما تعيق المطورين الجدد على OCR.

> **نصيحة:** إذا كنت بحاجة إلى معالجة مسبقة للصورة (مثل تصحيح الميل أو التحويل إلى ثنائي)، قم بذلك *قبل* استدعاء `Recognize`. Aspose يوفر أدوات `ImageProcessor` لهذا الغرض.

---

## الخطوة 3: تعيين اللغة وتحويل الصورة إلى نص

مع تسجيل الوحدة وتحميل الصورة، يمكننا أخيرًا **تحويل الصورة إلى نص**. هذه الخطوة تجيب أيضًا على **كيفية التعرف على السيريلي**.

```csharp
// Create an OCR engine instance and set its language to Cyrillic
var ocrEngine = new OcrEngine
{
    Language = Language.Cyrillic,
    // Optional: increase accuracy for noisy images
    // Settings = new OcrEngineSettings { EnableNoiseRemoval = true }
};

// Run the recognition process
OcrResult ocrResult = ocrEngine.Recognize(inputImage);
```

**لماذا تعيين اللغة صراحةً؟**  
حتى بعد التسجيل، يظل المحرك يستخدم اللغة الإنجليزية افتراضيًا. تحديد `Language.Cyrillic` يوجه المحرك لاستخدام القاموس المسجل حديثًا، مما يحسن الدقة بشكل كبير للخطوط السلافية.

> **حالة حافة:** إذا حاولت التعرف على صورة دون تعيين اللغة، سيعود Aspose إلى اللاتينية، مما ينتج أحرف غير قابلة للقراءة للنص السيريلي.

---

## الخطوة 4: استخراج النص من الصورة – الحصول على النتيجة

كائن `OcrResult` يحتوي على السلسلة الخام، درجات الثقة، وبيانات الموقع. في معظم السيناريوهات تحتاج فقط إلى النص العادي.

```csharp
// Display the recognized text in the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);

// Optional: check confidence (0‑100)
// Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
```

**لماذا فحص الثقة؟**  
مستوى الثقة يخبرك بمدى موثوقية نتيجة OCR. القيم فوق 80% عادةً ما تكون آمنة للمعالجة اللاحقة، بينما القيم الأقل قد تتطلب مراجعة يدوية أو معالجة مسبقة للصورة.

> **ماذا لو كان الناتج فارغًا؟**  
الأسباب الشائعة تشمل وحدة لغة غير صحيحة، صورة فاسدة، أو صورة ذات تباين منخفض جدًا. جرّب زيادة التباين أو استخدام `ImageProcessor.AdjustContrast` قبل التعرف.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للنسخ واللصق والذي يجمع جميع الخطوات معًا. احفظه باسم `Program.cs` وشغله من جذر مشروعك.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Register the Cyrillic language module
        // -------------------------------------------------
        string languageModulePath = Path.Combine("ocr-modules", "cyrillic.zip");
        if (!File.Exists(languageModulePath))
        {
            Console.WriteLine($"Language module not found: {languageModulePath}");
            return;
        }
        OcrEngine.RegisterLanguageModule(Language.Cyrillic, File.ReadAllBytes(languageModulePath));

        // -------------------------------------------------
        // Step 2: Load the image you want to convert
        // -------------------------------------------------
        string imagePath = Path.Combine("ocr-images", "cyrillic_sample.jpg");
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }
        Image inputImage = Image.Load(imagePath);

        // -------------------------------------------------
        // Step 3: Create OCR engine and set language
        // -------------------------------------------------
        var ocrEngine = new OcrEngine { Language = Language.Cyrillic };

        // -------------------------------------------------
        // Step 4: Recognize and extract text
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 5: Output the result
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**الناتج المتوقع**

```
=== OCR Result ===
Привет мир! Это пример текста на кириллице.
```

إذا رأيت نصًا غير مفهوم بدلاً من السيريلي، تحقق مرة أخرى من أن ملف `cyrillic.zip` يتطابق مع نسخة Aspose OCR التي قمت بتثبيتها وأن الصورة واضحة بما يكفي للتعرف.

---

## الأسئلة المتكررة (FAQ)

**س: هل يمكنني استخدام هذا النهج للغات أخرى؟**  
ج: بالتأكيد. استبدل `Language.Cyrillic` بالعدد المناسب (مثلًا `Language.Arabic`) وسجّل ملف ZIP المطابق.

**س: ما صيغ الصور المدعومة؟**  
ج: JPEG، PNG، BMP، TIFF، وGIF كلها مدعومة أصلاً بواسطة `Image.Load`. بالنسبة لملفات PDF تحتاج إلى Aspose.PDF، ثم تحويل الصفحات إلى صور قبل OCR.

**س: كيف أحسن الدقة في المسحات منخفضة الجودة؟**  
ج: عالج الصورة مسبقًا—طبق التحويل إلى ثنائي، تصحيح الميل، أو إزالة الضوضاء باستخدام `ImageProcessor`. كذلك، زد إعدادات `OcrEngineSettings` مثل `EnableNoiseRemoval` و `EnableTextSegmentation`.

**س: هل هناك طريقة للحصول على صندوق الإحاطة لكل كلمة؟**  
ج: نعم. يحتوي `OcrResult` على مجموعة `Regions` حيث يحمل كل منطقة بيانات `Location`. يمكنك التكرار عبر `ocrResult.Regions` لاستخراج الإحداثيات.

---

## الخلاصة

أظهرنا لك كيفية **تحويل الصورة إلى نص** باستخدام Aspose OCR، مع تغطية كل شيء من **كيفية تسجيل الوحدة** إلى **تحميل الصورة للـ OCR** وأخيرًا **استخراج النص من الصورة** مع **التعرف على السيريلي**. الشيفرة الكاملة أعلاه جاهزة للتنفيذ، والتفسيرات توضح لك *السبب* وراء كل سطر—حتى تتمكن من تعديل الحل للغات أخرى أو سير عمل أكثر تعقيدًا.

هل أنت مستعد للخطوة التالية؟ جرّب تجربة تحويل ملفات PDF متعددة الصفحات، دمج مخرجات OCR في فهرس بحث، أو الجمع بينها وبين Azure Cognitive Services لاكتشاف اللغة. السماء هي الحد عندما تتقن أساسيات تحويل الصورة إلى نص.

![مثال تحويل الصورة إلى نص](image-placeholder.png "تحويل الصورة إلى نص")

*برمجة سعيدة! إذا واجهت أي مشاكل، اترك تعليقًا أدناه وسنقوم بحلها معًا.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}