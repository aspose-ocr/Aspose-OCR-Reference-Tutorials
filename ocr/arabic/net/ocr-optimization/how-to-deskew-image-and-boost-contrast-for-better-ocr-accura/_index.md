---
category: general
date: 2025-12-30
description: كيفية تصحيح انحراف الصورة بسرعة وتعلم كيفية تعزيز التباين أثناء استخراج
  النص من الصورة لتحسين دقة التعرف الضوئي على الأحرف.
draft: false
keywords:
- how to deskew image
- how to boost contrast
- extract text from image
- recognize text image
- improve ocr accuracy
language: ar
og_description: كيفية تصحيح ميل الصورة بسرعة وتعلم كيفية تعزيز التباين أثناء استخراج
  النص من الصورة لتحسين دقة التعرف الضوئي على الأحرف.
og_title: كيفية تصحيح انحراف الصورة وتعزيز التباين لتحسين دقة التعرف الضوئي على الأحرف
tags:
- OCR
- C#
- Image Processing
title: كيفية تصحيح ميل الصورة وتعزيز التباين لتحسين دقة التعرف الضوئي على الأحرف
url: /ar/net/ocr-optimization/how-to-deskew-image-and-boost-contrast-for-better-ocr-accura/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيف تُصحّح انحراف الصورة وتزيد التباين لتحسين دقة OCR

هل تساءلت يومًا **كيف تُصحّح انحراف الصورة** التي تأتي من الماسح الضوئي أو الهاتف الذكي؟  
أنت لست وحدك—معظم المطورين يواجهون هذه المشكلة عندما تكون الصورة المصدر مائلة قليلًا أو مشوشة، وينتهي الأمر بأن يكون ناتج OCR فوضويًا.

الخبر السار هو أنه ببضع أسطر من C# يمكنك تعديل الصورة، تنظيف الخلفية، وحتى رفع التباين بحيث يقرأ المحرك النص كالمحترفين. في هذا الدليل سنوضح لك أيضًا **كيفية استخراج النص من الصورة** و**التعرف على محتوى صورة النص** باستخدام Aspose.OCR، مع الحفاظ على **تحسين دقة OCR** في المقام الأول.

## ما الذي ستحتاجه

- **.NET 6.0** أو أحدث (الكود يُجمّع أيضًا على .NET Framework 4.7+)
- حزمة NuGet **Aspose.OCR** (الإصدار 23.12 أو أحدث) – تثبيت عبر `dotnet add package Aspose.OCR`
- صورة تجريبية مائلة ومشوشة (مثال: `noisy_rotated.jpg`)
- Visual Studio، VS Code، أو أي بيئة تطوير تفضّلها

هذا كل ما تحتاجه—بدون مكتبات أصلية إضافية، ولا ربطات OpenCV ثقيلة. مجرد كود مُدار بالكامل.

---

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أولًا، أنشئ تطبيق console جديد وأدخل المساحات الاسمية المطلوبة إلى النطاق. هذه الخطوة هي الأساس لكل ما يلي.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later
        }
    }
}
```

**لماذا هذا مهم:**  
`Aspose.OCR` يزودك بفئة `OcrEngine`، بينما `Aspose.OCR.Filters` توفر فلاتر ما قبل المعالجة المفيدة مثل `DeskewFilter` و`ContrastBoostFilter`. استيرادها مسبقًا يبقي الكود منظمًا ويخبر المترجم بما نعتزم استخدامه.

---

## الخطوة 2: تهيئة محرك OCR وإضافة فلتر تصحيح الانحراف

الآن نطبق **كيفية تصحيح انحراف الصورة**. يقوم `DeskewFilter` تلقائيًا باكتشاف زاوية الدوران (حتى الحد الأقصى الذي تحدده) ويعيد تدوير البت ماب إلى الوضع الأفقي.

```csharp
// Inside Main()
var ocrEngine = new OcrEngine();

// Deskew: correct up to 15 degrees of rotation
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });
```

**ما الذي يحدث خلف الكواليس؟**  
يقوم الفلتر بمسح الصورة للعثور على أطول خط أفقي للنص، يقدّر الميل، ثم يطبق دورانًا عكسيًا. عبر تحديد `MaxAngle` إلى 15° نتجنب تصحيحًا مفرطًا للصور التي هي بالفعل مستقيمة.

> **نصيحة احترافية:** إذا كانت صورك المصدر قد تكون مقلوبة رأسًا على عقب، زد `MaxAngle` إلى 180°—سيتعرف الفلتر على الاتجاه الصحيح مهما كان.

---

## الخطوة 3: تقليل الضوضاء باستخدام فلتر Denoise

يمكن للمسح المشوش أن يخدع حتى أذكى محرك OCR. إضافة `DenoiseFilter` تُزيل البقع دون محو التفاصيل الدقيقة.

```csharp
// Denoise: strength ranges from 0 (off) to 1 (max)
ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });
```

**لماذا تحتاجه:**  
الضوضاء تُنشئ حواف زائفة يفسّرها خوارزم OCR كحروف. قيمة القوة `0.7` تُعد نقطة توازن لمعظم المستندات الممسوحة؛ يمكنك تعديلها حسب نظافة أو قذارة المدخلات.

---

## الخطوة 4: رفع التباين – “كيفية رفع التباين” عمليًا

هنا نجيب على الكلمة المفتاحية الثانوية **how to boost contrast**. يقوم `ContrastBoostFilter` بتضخيم الفارق بين النص الداكن والخلفية الفاتحة، مما يجعل الحروف بارزة.

```csharp
// Contrast boost: level > 1 increases contrast
ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });
```

**المنطق وراء ذلك:**  
التباين العالي يقلل من احتمال فقدان الخطوط الخفيفة. مستوى `1.3` يعمل جيدًا للمستندات التقليدية ذات النص الأسود على خلفية بيضاء؛ بالنسبة للصور الملونة قد تحتاج إلى `1.5` أو أكثر.

---

## الخطوة 5: تشغيل OCR واستخراج النص

بعد معالجة الصورة، نصل أخيرًا إلى **استخراج النص من الصورة** باستخدام طريقة `Recognize`. تُعيد الطريقة كائن `OcrResult` يحتوي على السلسلة الخام ودرجات الثقة.

```csharp
// Perform OCR on the prepared image
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/noisy_rotated.jpg");

// Output the recognized text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**ما ستحصل عليه:**  
`ocrResult.Text` يحمل النص العادي لكل ما تمكن المحرك من قراءته. إذا أردت معرفة الثقة على مستوى الكلمات، استكشف `ocrResult.Regions`—كل منطقة تتضمن خاصية `Confidence`.

---

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

فيما يلي البرنامج الكامل الذي يمكنك وضعه في `Program.cs`. تأكد من أن مسار الصورة يشير إلى ملف حقيقي على جهازك.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Deskew – correct up to 15° rotation
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });

            // 3️⃣ Denoise – smooth out speckles (strength 0.7)
            ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });

            // 4️⃣ Contrast boost – make text pop (level 1.3)
            ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });

            // 5️⃣ Recognize the image
            var imagePath = @"YOUR_DIRECTORY\noisy_rotated.jpg";
            var ocrResult = ocrEngine.Recognize(imagePath);

            // 6️⃣ Show the result
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**الناتج المتوقع (مثال):**

```
=== OCR Output ===
Invoice #12345
Date: 2024-09-30
Total Amount: $1,250.00
Thank you for your business!
```

إذا ظهر الناتج مشوشًا، أعد فحص جودة الصورة، عدّل `Strength` أو `Level`، أو زد `MaxAngle` لتصحيح أكثر عدوانية.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو كانت الصورة مقلوبة رأسًا على عقب؟

عيّن `MaxAngle = 180` في `DeskewFilter`. سيتعرف الفلتر على دوران 180° ويقلبها بشكل صحيح.

### مستنداتي ملونة (مثلاً نموذج ممسوح مع تظليل أزرق).

جرّب إضافة `ColorFilter` قبل رفع التباين، أو حوّل الصورة إلى تدرج رمادي يدويًا:

```csharp
ocrEngine.Filters.Add(new GrayscaleFilter());
```

### أحتاج إلى معالجة العديد من الملفات دفعة واحدة.

لفّ منطق OCR داخل حلقة `foreach` تتنقل عبر مجلد:

```csharp
foreach (var file in Directory.GetFiles(@"C:\Scans", "*.jpg"))
{
    var result = ocrEngine.Recognize(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), result.Text);
}
```

### كيف أعرف مستوى ثقة OCR؟

افحص `ocrResult.Regions`:

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"Text: {region.Text} – Confidence: {region.Confidence:P2}");
}
```

القيم الأعلى للثقة (قريبة من 100٪) عادةً ما تعني أن خطوات ما قبل المعالجة نجحت.

---

## نصائح لتعزيز دقة OCR

| النصيحة | لماذا تساعد |
|-----|--------------|
| **استخدام صيغ صور غير مضغوطة** (PNG, TIFF) | ضغط JPEG قد يطمس الحواف، مما يضر بالتعرف. |
| **الحفاظ على DPI 300+** | المزيد من البكسلات لكل حرف يزود المحرك ببيانات أكثر. |
| **قص الهوامش غير الضرورية** | يقلل الضوضاء ويسرّع المعالجة. |
| **تطبيق عتبة ثنائية** (أسود/أبيض) بعد رفع التباين للمستندات النصية النقية | يبسط الصورة إلى لونين، وهو ما تفضّله معظم محركات OCR. |
| **اختبار عينة صغيرة أولًا** | يتيح لك ضبط `Strength` و`Level` قبل التوسّع. |

---

## الخلاصة

استعرضنا **كيفية تصحيح انحراف الصورة**، **كيفية رفع التباين**، والمسار الكامل لـ **استخراج النص من الصورة** باستخدام Aspose.OCR. عبر ربط `DeskewFilter`، `DenoiseFilter`، و`ContrastBoostFilter` قبل استدعاء `Recognize`، ستلاحظ تحسنًا ملحوظًا في **تحسين دقة OCR** لمعظم المسحات الواقعية.

جرّب الكود، عدّل معلمات الفلاتر لتتناسب مع خصائص مستنداتك، وستتمكن من استخراج نص نظيف حتى من أكثر الصور فوضى. تريد المزيد؟ جرّب إضافة قيس مخصصة للغات، أو مرّر الناتج إلى مدقق إملائي للمعالجة اللاحقة.

برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة كالبلور!

--- 

![مثال على كيفية تصحيح انحراف الصورة](deskew_example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}