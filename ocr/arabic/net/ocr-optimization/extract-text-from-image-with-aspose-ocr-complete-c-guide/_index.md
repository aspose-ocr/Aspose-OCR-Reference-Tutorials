---
category: general
date: 2026-04-08
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية معالجة الصورة
  مسبقًا للتعرف الضوئي على الأحرف وكيفية معالجة الصورة مسبقًا لزيادة الدقة.
draft: false
keywords:
- extract text from image
- preprocess image for ocr
- how to preprocess image
- Aspose OCR C#
- image preprocessing techniques
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR في C#. يوضح هذا الدليل
  كيفية معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف وكيفية تحسين الصورة للحصول على
  أفضل النتائج.
og_title: استخراج النص من الصورة باستخدام Aspose OCR – دليل كامل بلغة C#
tags:
- C#
- OCR
- Aspose
- Image Processing
title: استخراج النص من الصورة باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة باستخدام Aspose OCR – دليل C# كامل

هل احتجت يومًا إلى **استخراج النص من الصورة** لكن النتائج كانت مليئة بالأخطاء؟ لست وحدك — فمعظم المطورين يواجهون هذه المشكلة عندما تكون الصورة الأصلية مائلة أو مشوشة أو ذات تباين منخفض. الخبر السار هو أن روتينًا بسيطًا للمعالجة المسبقة يمكنه تحويل لقطة غير مستقرة إلى مصدر نظيف لتقنية OCR، و Aspose OCR يجعل العملية سهلة للغاية.

في هذا الدرس سنستعرض مثالًا واقعيًا يوضح **كيفية معالجة الصورة مسبقًا لتقنية OCR** باستخدام الفلاتر المدمجة في Aspose OCR، ثم **استخراج النص من الصورة** ببضع أسطر من C#. في النهاية ستحصل على برنامج جاهز للتنفيذ، وتفهم لماذا كل فلتر مهم، وتعرف كيف تُعدل خط الأنابيب لحالاتك الخاصة.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+)
- حزمة NuGet الخاصة بـ Aspose.OCR (`Install-Package Aspose.OCR`)
- صورة نموذجية مائلة أو مشوشة أو ذات تباين منخفض (مثال: `skewed_noisy.jpg`)
- أي بيئة تطوير تفضلها — Visual Studio أو Rider أو VS Code تكفي

لا توجد مكتبات أصلية إضافية، ولا خدمات ويب، فقط C# عادي.

## الخطوة 1: إعداد محرك OCR – نقطة الانطلاق لاستخراج النص

أولًا، أنشئ كائن `OcrEngine` وحدد اللغة التي يبحث عنها. الإنجليزية هي الأكثر شيوعًا، لكن يمكنك استبدال `"en"` بـ `"fr"` أو `"de"` وما إلى ذلك.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void PreprocessAndOcr()
    {
        // 1️⃣ Initialize the OCR engine – this is where we define the language.
        var ocrEngine = new OcrEngine { Language = "en" };
```

**لماذا هذا مهم:** المحرك يحتفظ بالقواميس الداخلية والخوارزميات الخاصة بكل لغة. إذا تخطيت تحديد اللغة، فإن Aspose يستخدم الإنجليزية افتراضيًا، لكن الصراحة تُجنبك المفاجآت عندما تُغيّر اللغة لاحقًا.

## الخطوة 2: بناء خط أنابيب المعالجة المسبقة – كيفية معالجة الصورة للحصول على أفضل النتائج

الآن نضيف الفلاتر. فكر فيها كحزمة تحرير صور صغيرة تُنفّذ تلقائيًا قبل خطوة OCR. الفلاتر الثلاثة أدناه تغطي أكثر المشكلات شيوعًا:

| الفلتر | ما يُصلحه | متى يُستخدم |
|--------|-----------|--------------|
| `DeskewFilter` | يدور الصورة لتصبح أفقية | صور مأخوذة بزاوية |
| `DenoiseFilter` | يقلل البقع العشوائية والحبوب | صور إضاءة منخفضة أو مستندات ممسوحة |
| `ContrastStretchFilter` | يعزز التباين، مما يجعل النص الداكن يبرز | مطبوعات باهتة أو لقطات شاشة مبهتة |

```csharp
        // 2️⃣ Add preprocessing steps – this is the core of “how to preprocess image”.
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast
```

**نصيحة محترف:** الترتيب مهم. ابدأ بـ Deskew، ثم Denoise، وأخيرًا ContrastStretch. إذا غيرت الترتيب، قد تضخم الضوضاء بدلًا من إزالتها.

## الخطوة 3: تشغيل OCR – أخيرًا استخراج النص من الصورة

بعد تجهيز خط الأنابيب، أعطِ المحرك مسار الصورة. سيطبق Aspose الفلاتر تلقائيًا، ثم يُنفّذ خوارزمية التعرف.

```csharp
        // 3️⃣ Recognize text from the pre‑processed image.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");
```

إذا لم يُعثر على الملف، ستحصل على استثناء واضح `FileNotFoundException`. لهذا نوصي باستخدام المسارات المطلقة أثناء التطوير، ثم التحول إلى مسارات نسبية أو قيم إعدادات في بيئة الإنتاج.

## الخطوة 4: عرض النتيجة – شاهد ما تم الحصول عليه

كائن `OcrResult` يحتوي على النص الخام، درجات الثقة، وحتى إطارات الحدود لكل كلمة. لعرض سريع، سنطبع النص على وحدة التحكم فقط.

```csharp
        // 4️⃣ Output the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مثل:

```
=== OCR Output ===
Invoice Number: 2023-0456
Date: 03/15/2024
Total: $1,234.56
```

إذا كان الإخراج مشوشًا، تحقق مرة أخرى من جودة الصورة أو جرّب فلاتر إضافية (مثل `BinarizationFilter` للصور الثنائية).

## مثال كامل يعمل – انسخ‑الصق وشغّله

فيما يلي البرنامج الكامل المستقل. استبدل فقط `YOUR_DIRECTORY/skewed_noisy.jpg` بالمسار الفعلي لصورتك التجريبية.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void Main()
    {
        PreprocessAndOcr();
    }

    public static void PreprocessAndOcr()
    {
        // Step 1: Create OCR engine and set language
        var ocrEngine = new OcrEngine { Language = "en" };

        // Step 2: Build preprocessing pipeline
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast

        // Step 3: Recognize text from the pre‑processed image
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // Step 4: Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**الإخراج المتوقع** – ستطبع وحدة التحكم تمثيل النص العادي لما هو موجود في الصورة. إذا كانت الصورة تحتوي على لافتة بسيطة تقول “OpenAI”، فستظهر تلك الكلمة بالضبط، دون رموز إضافية.

## حالات خاصة وكيفية تعديل خط الأنابيب

### 1️⃣ صور داكنة جدًا

إذا لم يكن فلتر التباين كافيًا، أضف مسبقًا `BrightnessCorrectionFilter`:

```csharp
ocrEngine.Preprocess.Add(new BrightnessCorrectionFilter(30)); // increase brightness by 30%
```

### 2️⃣ مستندات متعددة اللغات

عيّن `Language = "en+fr"` (Aspose يدعم رموز اللغات مفصولة بفواصل) وأضف `LanguageDetectionFilter` إذا رغبت في أن يكتشف المحرك اللغة تلقائيًا.

### 3️⃣ ملفات PDF كبيرة تم تحويلها إلى صور

معالجة PDF مكون من ألف صفحة صورةً بصورة واحدة قد تكون بطيئة. استخدم `Parallel.ForEach` لتشغيل OCR على عدة صور في آنٍ واحد، لكن تذكر أن `OcrEngine` غير آمن للمتعدد الخيوط — أنشئ نسخة منفصلة لكل خيط.

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine { Language = "en" };
    // add same filters...
    var result = engine.RecognizeImage(path);
    // store result...
});
```

### 4️⃣ الحصول على إطارات الحدود

إذا كنت بحاجة إلى موقع كل كلمة (مثلاً للتظليل)، تفحص `ocrResult.Regions`. كل منطقة تحتوي على إحداثيات `Rectangle` يمكنك تمريرها إلى طبقة واجهة المستخدم.

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

## الأخطاء الشائعة (وكيفية تجنّبها)

- **تخطي خطوة Deskew** – حتى ميل بزاوية درجتين قد يقلل الثقة بنسبة 20 %. أضف دائمًا `DeskewFilter` عندما لا تكون الصورة محاذاة تمامًا.
- **استخدام JPEG مع ضغط عالي** – ضوضاء الضغط تشبه الضوضاء؛ استبدلها بـ PNG أو TIFF للحصول على OCR أفضل.
- **تثبيت المسارات صراحة** — المسارات النسبية تعمل محليًا، لكن في خطوط CI/CD ستحتاج لقراءة موقع الصورة من الإعدادات أو متغيرات البيئة.

## اختبار إعدادك

1. شغّل البرنامج باستخدام صورة نظيفة وعالية التباين. يجب أن تحصل على نص شبه مثالي.
2. استبدلها بصورة مشوشة ومائلة. تحقق من تحسين الإخراج بعد إضافة الفلاتر الثلاثة.
3. جرّب إزالة فلتر واحد في كل مرة لتلاحظ تأثيره — سيساعدك ذلك على فهم *لماذا* كل خطوة مهمة.

## الخلاصة

لقد أظهرنا للتو كيفية **استخراج النص من الصورة** باستخدام Aspose OCR، وأظهرنا طريقة عملية **لمعالجة الصورة مسبقًا لتقنية OCR** تعمل في معظم السيناريوهات الواقعية. بربط `DeskewFilter` و `DenoiseFilter` و `ContrastStretchFilter` تمنح المحرك لوحة نظيفة، مما يحسّن الدقة بشكل كبير.

من هنا يمكنك استكشاف فلاتر أكثر تقدمًا، معالجة مستندات متعددة الصفحات، أو دمج نتائج OCR في فهرس بحث. مهما كان اختيارك، فإن النمط الأساسي — التهيئة، المعالجة المسبقة، التعرف، والاستخدام — يبقى هو نفسه.

هل أنت مستعد للارتقاء؟ جرّب إضافة `BinarizationFilter` للمسحات بالأبيض والأسود، أو اربط الإخراج بقاعدة بيانات لإنشاء ملفات PDF قابلة للبحث. برمجة سعيدة، ولتُعيد كل صورة تُدخلها إلى Aspose نصًا واضحًا وقابلًا للقراءة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}