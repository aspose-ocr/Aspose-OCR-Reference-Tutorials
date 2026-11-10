---
category: general
date: 2026-06-28
description: كيفية تصحيح ميل الصورة باستخدام Aspose.OCR. تعلّم تمهيد الصورة للتعرف
  الضوئي على الأحرف، تحسين دقة التعرف الضوئي، وتصحيح ميل الصورة الممسوحة ضوئياً مع
  مثال كامل بلغة C#.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- how to improve ocr
- deskew scanned image
language: ar
og_description: كيفية تصحيح انحراف الصورة باستخدام Aspose.OCR. يوضح لك هذا الدرس كيفية
  معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف، وزيادة الدقة، وتصحيح انحراف الصورة
  الممسوحة خطوة بخطوة.
og_title: كيفية تصحيح انحراف الصورة في C# – دليل Aspose.OCR الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  headline: How to Deskew Image in C# – Complete Aspose.OCR Guide
  type: TechArticle
- description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  name: How to Deskew Image in C# – Complete Aspose.OCR Guide
  steps:
  - name: Why a Deskew Filter First?
    text: 'When a document is rotated even a few degrees, the OCR engine misinterprets
      line baselines, leading to garbled output. The `DeskewFilter` automatically
      estimates the rotation angle (up to `MaxAngle` degrees) and rotates the bitmap
      back to a horizontal baseline. The returned `DeskewConfidence` tells '
  - name: 1️⃣ DeskewFilter (Primary Step)
    text: '- **What it does:** Detects the dominant text line direction and rotates
      the image. - **Why it matters:** A straight baseline maximizes character segmentation
      accuracy. - **Tip:** If your documents never exceed 10°, set `MaxAngle = 10`
      to speed up detection.'
  - name: 2️⃣ DenoiseFilter (Secondary Cleanup)
    text: '- **What it does:** Reduces random pixel noise that can appear after scanning.
      - **Why it matters:** Noise often creates false edges, confusing the OCR''s
      segmentation. - **Tip:** Adjust `Strength` between 0.3 (light) and 0.8 (aggressive)
      based on scan quality.'
  - name: 3️⃣ ContrastBoostFilter (Final Polish)
    text: '- **What it does:** Increases the difference between foreground text and
      background. - **Why it matters:** Low contrast can make faint characters invisible
      to the recognition engine. - **Tip:** A `Level` of 1.2 works for most black‑on‑white
      scans; for colored documents, experiment with values up to '
  type: HowTo
tags:
- OCR
- Aspose
- Image Processing
title: كيفية تصحيح انحراف الصورة في C# – دليل Aspose.OCR الكامل
url: /ar/net/ocr-optimization/how-to-deskew-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيف تقوم بتصحيح ميل الصورة في C# – دليل Aspose.OCR الكامل

هل تساءلت يومًا **كيف تصحح ميل ملفات الصورة** قبل تمريرها إلى محرك OCR؟ لست وحدك. غالبًا ما تصل المستندات الممسوحة ضوئيًا مائلة، وهذا الميل الصغير يمكن أن يضعف نتائج التعرف. الخبر السار؟ باستخدام Aspose.OCR يمكنك تعديل (تصحيح) وتنظيف الصور ببضع أسطر من C# فقط.

في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ **يعالج الصورة قبل OCR**، يضيف مرشح تصحيح الميل، ويظهر لك **كيفية تحسين دقة OCR**. في النهاية ستتمكن من **تصحيح ميل الصورة الممسوحة** تلقائيًا ورؤية درجات الثقة بنفسك.

> **ملاحظة:** يعمل الكود مع Aspose.OCR ≥ 22.10 و .NET 6+، لكن المفاهيم تنطبق على الإصدارات الأقدم أيضًا.

## ما الذي ستحتاجه

- **Aspose.OCR for .NET** (حزمة NuGet `Aspose.OCR`)
- ملف **TIFF** أو JPEG مائل تريد تصحيحه
- Visual Studio 2022 (أو أي بيئة تطوير C#)
- إلمام أساسي بـ C# وتطبيقات الكونسول

لا توجد مكتبات طرف ثالث إضافية مطلوبة؛ جميع خطوات المعالجة موجودة داخل Aspose.OCR.

---

## كيفية تصحيح ميل الصورة باستخدام Aspose.OCR

جوهر الحل هو **خط أنابيب الفلاتر**. فكر فيه كخط تجميع حيث ينظف كل مرشح مشكلة معينة: أولًا نصحح الميل، ثم نقلل الضوضاء، وأخيرًا نعزز التباين حتى يرى محرك OCR الأحرف بوضوح.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class DeskewExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var engine = new OcrEngine();

        // Step 2: Load the skewed image to be processed
        var img = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_doc.tif");

        // Step 3: Build a filter pipeline – deskew, then denoise, then boost contrast
        var pipeline = new OcrFilter[]
        {
            new DeskewFilter { MaxAngle = 30 },   // auto‑detect rotation up to 30°
            new DenoiseFilter { Strength = 0.5 },
            new ContrastBoostFilter { Level = 1.2 }
        };

        // Step 4: Apply the filters to the image before OCR
        var preprocessed = engine.ApplyFilters(img, pipeline);

        // Step 5: Perform OCR on the pre‑processed image
        var result = engine.Recognize(preprocessed);

        // Step 6: Output the deskew confidence and recognized text
        System.Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
        System.Console.WriteLine(result.Text);
    }
}
```

> **مثال على الصورة**  
> ![مثال على تصحيح ميل الصورة](/images/deskew-example.png "مثال على تصحيح ميل الصورة")

### لماذا نضع مرشح تصحيح الميل أولًا؟

عندما يتم تدوير المستند بضع درجات فقط، يخطئ محرك OCR في تفسير خطوط الأساس، مما يؤدي إلى مخرجات مشوشة. يقوم `DeskewFilter` تلقائيًا بتقدير زاوية الدوران (حتى `MaxAngle` درجة) ويعيد تدوير البت ماب إلى خط أفقي. تُظهر قيمة `DeskewConfidence` مدى ثقة الخوارزمية في التصحيح—مفيدة للتسجيل أو استراتيجيات الاحتياط.

---

## معالجة الصورة قبل OCR – بناء خط أنابيب الفلاتر

### 1️⃣ DeskewFilter (الخطوة الأساسية)

- **ما يفعله:** يكتشف اتجاه خط النص السائد ويدور الصورة.
- **لماذا هو مهم:** خط أساس مستقيم يزيد من دقة تجزئة الأحرف.
- **نصيحة:** إذا لم تتجاوز مستنداتك 10°، اضبط `MaxAngle = 10` لتسريع الكشف.

### 2️⃣ DenoiseFilter (تنظيف ثانوي)

- **ما يفعله:** يقلل الضوضاء العشوائية التي قد تظهر بعد المسح.
- **لماذا هو مهم:** الضوضاء غالبًا ما تُنشئ حواف زائفة، مما يربك تجزئة OCR.
- **نصيحة:** اضبط `Strength` بين 0.3 (خفيفة) و 0.8 (قوية) حسب جودة المسح.

### 3️⃣ ContrastBoostFilter (التلميع النهائي)

- **ما يفعله:** يزيد الفارق بين النص الأمامي والخلفية.
- **لماذا هو مهم:** التباين المنخفض قد يجعل الأحرف الباهتة غير مرئية لمحرك التعرف.
- **نصيحة:** قيمة `Level` بمقدار 1.2 تعمل لمعظم المسحات بالأبيض والأسود؛ بالنسبة للمستندات الملونة، جرّب قيمًا تصل إلى 2.0.

من خلال ربط هذه الفلاتر الثلاثة **تُعالج الصورة قبل OCR** بطريقة تعالج أكثر المشكلات شيوعًا: الميل، الضوضاء، وقلة التباين.

---

## كيفية تحسين دقة OCR باستخدام تصحيح الميل وإزالة الضوضاء

قد تتساءل: “إذا كان لدي بالفعل مرشح تصحيح الميل، لماذا أحتاج إلى إزالة الضوضاء وتعزيز التباين؟” الجواب يكمن في **التحسين المتراكم**. كل مرشح يعالج عيبًا مختلفًا، ومعًا يرفعون الثقة العامة.

#### اختبار واقعي

| الاختبار | دقة OCR الأصلية | بعد تصحيح الميل | بعد خط الأنابيب الكامل |
|----------|----------------|----------------|------------------------|
| فاتورة بسيطة (ميل 5°) | 78 % | 92 % | 96 % |
| مسح صحيفة قديمة (ميل 15°، حبيبي) | 61 % | 78 % | 88 % |
| نموذج منخفض التباين (بدون ميل) | 70 % | 71 % | 84 % |

*الأرقام توضيحية لكنها تعكس الزيادات النموذجية التي يبلغ عنها مستخدمو Aspose.*

**الخلاصة الرئيسية:** حتى إذا كان هدفك الأساسي هو **تصحيح ميل الصورة الممسوحة**، فإن إضافة خطوات إزالة الضوضاء وتعزيز التباين غالبًا ما ينتج عنه قفزة ملحوظة في جودة النص النهائي.

---

## تصحيح ميل الصورة الممسوحة: التحقق من النتائج

بعد تشغيل خط الأنابيب، ستحصل على معلومات مفيدة اثنتين:

```csharp
Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
Console.WriteLine(result.Text);
```

- **ثقة تصحيح الميل** (`result.DeskewConfidence`) هي نسبة مئوية. القيم فوق 90 % عادةً ما تعني أن الدوران تم تصحيحه بدقة.
- **النص المُعترف به** (`result.Text`) يتيح لك التحقق فورًا مما إذا كان الإخراج منطقيًا.

إذا كانت الثقة منخفضة (< 70 %)، ففكّر في:

1. **زيادة `MaxAngle`** – ربما يكون المستند مائلًا أكثر مما توقعت.
2. **إضافة `BinarizationFilter`** قبل تصحيح الميل لتبسيط الصورة.
3. **دوران الصورة يدويًا** باستخدام `OcrImage.Rotate(angle)` كخطة احتياطية.

---

## مثال كامل من البداية إلى النهاية (جاهز للتنفيذ)

فيما يلي **البرنامج الكامل المستقل** الذي يمكنك نسخه ولصقه في مشروع تطبيق كونسول جديد. تذكر استبدال `YOUR_DIRECTORY` بالمجلد الذي يحتوي على ملف TIFF المائل الخاص بك.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace DeskewDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize the OCR engine
            var engine = new OcrEngine();

            // 2️⃣ Load the image you want to straighten
            var imgPath = @"C:\Images\skewed_doc.tif"; // <-- update this path
            var img = OcrImage.FromFile(imgPath);

            // 3️⃣ Define the preprocessing pipeline
            var pipeline = new OcrFilter[]
            {
                new DeskewFilter { MaxAngle = 30 },   // auto‑detect up to 30°
                new DenoiseFilter { Strength = 0.5 }, // moderate noise reduction
                new ContrastBoostFilter { Level = 1.2 } // brighten the text
            };

            // 4️⃣ Apply the pipeline – this returns a new image instance
            var preprocessed = engine.ApplyFilters(img, pipeline);

            // 5️⃣ Run OCR on the cleaned‑up image
            var result = engine.Recognize(preprocessed);

            // 6️⃣ Show confidence and the extracted text
            Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(result.Text);
        }
    }
}
```

**المخرجات المتوقعة** (مع افتراض مسح نظيف إلى حد ما):

```
Deskew confidence: 96.45%
=== Recognized Text ===
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
...
```

إذا رأيت أحرفًا مشوشة، أعد مراجعة قوة الفلاتر أو أضف `BinarizationFilter` كما ذكرنا سابقًا.

---

## الأخطاء الشائعة والنصائح الاحترافية

- **خطأ:** استخدام ملف TIFF متعدد الصفحات. `OcrImage.FromFile` يقرأ الإطار الأول فقط. استخدم `OcrImage.FromMultiPageFile` إذا كنت بحاجة إلى جميع الصفحات.
- **خطأ:** نسيان تحرير `OcrEngine`. احزمها داخل كتلة `using` في الكود الإنتاجي لتحرير الموارد الأصلية.
- **نصيحة احترافية:** خزن خط الأنابيب مؤقتًا إذا كنت تعالج العديد من الصور بإعدادات متماثلة—يقلل ذلك من الحمل.
- **نصيحة احترافية:** سجّل `DeskewConfidence` في نظام مراقبة؛ الانخفاض المفاجئ قد يشير إلى تغير في معايرة الماسح.

---

## الخطوات التالية – توسيع سير العمل

الآن بعد أن عرفت **كيفية تصحيح ميل الصورة** و **معالجة الصورة قبل OCR**، يمكنك استكشاف:

- **المعالجة الدفعية** – تكرار عبر مجلد من ملفات PDF الممسوحة، تحويل كل صفحة إلى صورة، وتطبيق نفس خط الأنابيب.
- **دعم اللغات** – اضبط `engine.Language = OcrLanguage.English;` أو لغات أخرى لتحسين التعرف.
- **معالجة ما بعد OCR مخصصة** – استخدم تعبيرات عادية لتنظيف الأخطاء الشائعة في OCR (مثل “0” مقابل “O”).

كل من هذه المواضيع يرتبط بطبيعة الحال بالكلمات المفتاحية الثانوية **how to improve ocr** و **deskew scanned image**.

---

## الخاتمة

غطينا كل ما تحتاج معرفته حول **كيفية تصحيح ميل الصورة** باستخدام Aspose.OCR، من بناء خط أنابيب فلاتر قوي إلى التحقق من درجات الثقة. عبر **معالجة الصورة قبل OCR** باستخدام تصحيح الميل، إزالة الضوضاء، وتعزيز التباين، ستحقق تحسينًا ملحوظًا في نتائج **how to improve OCR**، خاصةً على المسحات المائلة أو الضوضائية.

جرّب ذلك على مجموعة مستنداتك، عدّل معلمات الفلاتر، وشاهد دقة OCR ترتفع. هل لديك أسئلة أو ملف صعب يرفض الاستقامة؟ اترك تعليقًا أدناه—دعنا نحل المشكلة معًا. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}