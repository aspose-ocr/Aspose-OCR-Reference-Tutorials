---
category: general
date: 2026-04-29
description: كيفية تصحيح إمالة الصورة وزيادة دقة OCR باستخدام Aspose OCR – تعلم إزالة
  الضوضاء، تعزيز تباين الصورة، واستخراج النص من الصور.
draft: false
keywords:
- how to deskew image
- remove noise from image
- boost image contrast
- extract text from image
- improve ocr accuracy
language: ar
og_description: كيفية تصحيح ميل الصورة وتحسين دقة OCR. يوضح هذا الدرس كيفية إزالة
  الضوضاء من الصورة، وتعزيز تباين الصورة، واستخراج النص من الصورة باستخدام Aspose
  OCR.
og_title: كيفية تصحيح ميل الصورة – دليل Aspose OCR الكامل
tags:
- Aspose OCR
- C#
- Image preprocessing
title: كيفية تصحيح انحراف الصورة – دليل ما قبل معالجة Aspose OCR
url: /ar/net/ocr-optimization/how-to-deskew-image-aspose-ocr-preprocessing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح ميل الصورة – دليل Aspose OCR الكامل

هل تساءلت يوماً **عن كيفية تصحيح ميل الصورة** قبل تمريرها إلى محرك OCR؟ لست وحدك. المسح المائل أو الصورة الملتقطة بزاوية قد يفسد التعرف على النص، مما ينتج عنه مخرجات غير مفهومة.  

في هذا الدرس سنستعرض حلاً كاملاً من البداية إلى النهاية لا يقتصر فقط على **كيفية تصحيح ميل الصورة** بل يشمل أيضاً **إزالة الضوضاء من الصورة**، **زيادة تباين الصورة**، وأخيراً **استخراج النص من الصورة** باستخدام Aspose OCR. في النهاية ستعرف كيف **تحسين دقة OCR** دون الحاجة للغوص في الوثائق.

> **ما ستحصل عليه:** تطبيق C# console جاهز للتنفيذ، شرح واضح لكل خطوة من خطوات ما قبل المعالجة، وعدد من النصائح العملية التي يمكنك نسخها ولصقها في مشاريعك.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضاً مع .NET Core و .NET Framework)  
- حزمة NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- صورة نموذجية مائلة أو تحتوي على ضوضاء أو منخفضة التباين (مثال: `skewed_noisy.jpg`)  
- Visual Studio، VS Code، أو أي محرر C# تفضله  

لا توجد مكتبات أصلية إضافية مطلوبة – Aspose يتولى كل شيء داخل العملية.

---

## كيفية تصحيح ميل الصورة باستخدام Aspose OCR

أول ما نحتاجه هو مرشح تصحيح الميل الذي يضبط زاوية الدوران. Aspose OCR يضم `FilterDeskew`، الذي يحلل خطوط القاعدة للنص ويقوم بتدوير الصورة وفقاً لذلك.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that will later recognize text.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Build an image‑processing pipeline.
        //    The order matters: deskew → denoise → contrast boost.
        ImageProcessingPipeline processingPipeline = new ImageProcessingPipeline();
        processingPipeline.Add(new FilterDeskew());          // ✅ how to deskew image
        processingPipeline.Add(new FilterDenoise());         // ✅ remove noise from image
        processingPipeline.Add(new FilterContrastBoost());   // ✅ boost image contrast

        // 3️⃣ Load your source picture.
        var sourceImage = OcrEngine.LoadImage(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // 4️⃣ Apply the pipeline – the image is now straight, cleaner, and sharper.
        var processedImage = processingPipeline.Apply(sourceImage);

        // 5️⃣ Run OCR on the cleaned‑up bitmap.
        var ocrResult = ocrEngine.Recognize(processedImage);

        // 6️⃣ Print the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**لماذا نبدأ بتصحيح الميل:**  
إذا لم تكن خطوط النص أفقية، سيحاول محرك OCR تفسير الأحرف المائلة كرموز مختلفة، مما يقلل بشكل كبير من **تحسين دقة OCR**. تصحيح الميل يضبط خطوط القاعدة، مما يمنح المُعَرِّف سطحاً نظيفاً للعمل عليه.

> *نصيحة احترافية:* إذا كنت تعرف زاوية الدوران مسبقاً (مثلاً جميع المسحات بزاوية 90°)، يمكنك تخطي المرشح وتدوير الصورة يدوياً – هذا يوفر بعض الأداء.

---

## إزالة الضوضاء من الصورة – تنظيف المسح

تظهر الضوضاء كبقع سوداء أو بيضاء عشوائية (نمط “الملح والفلفل” الكلاسيكي) ويمكن أن تُربك تجزئة الأحرف. `FilterDenoise` يطبق مرشح متوسط يُنقِّي هذه البقع مع الحفاظ على الحواف.

```csharp
// Inside the pipeline we already added FilterDenoise.
// If you need a custom strength, you can instantiate it like:
var denoise = new FilterDenoise { Strength = 2 }; // 1‑3 are typical values
processingPipeline.Add(denoise);
```

**متى تضبط القوة:**  
- **Strength = 1** – ضوضاء خفيفة، معالجة سريعة.  
- **Strength = 3** – مسحات شديدة الضوضاء (مثل المستندات المرسلة بالفاكس).  

زيادة القوة بصورة مفرطة قد تُطمس الخطوط الرفيعة، مما قد *يضر* **تحسين دقة OCR**. جرّب قيمتين أو ثلاث على عينة تمثيلية.

---

## زيادة تباين الصورة – إبراز الأحرف الباهتة

الصور منخفضة التباين (مثل الإيصالات الباهتة) غالباً ما تجعل محرك OCR يتغاضى عن الأحرف الخفيفة. `FilterContrastBoost` يمدد المخطط اللوني بحيث تصبح البكسلات الداكنة أغمق والفاتحة أفتح.

```csharp
var contrast = new FilterContrastBoost { ContrastLevel = 1.5f }; // 1.0 = no change
processingPipeline.Add(contrast);
```

**لماذا التباين مهم:**  
التباين العالي يحسّن نسبة الإشارة إلى الضوضاء، مما يسهل على مُعرّف Aspose العصبي التمييز بين “I” و “l”. ومع ذلك، الزيادة المفرطة قد تشبع الصورة، فتتحول التدرجات السلسة إلى حواف صلبة تبدو كتشوهات. استهدف توازناً؛ 1.5‑2.0 قيمة جيدة للبدء.

---

## استخراج النص من الصورة – خطوة OCR النهائية

الآن بعد أن أصبحت الصورة مستقيمة، نظيفة، ومشرقة، يستطيع محرك OCR أداء مهمته. طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على النص الخام، درجات الثقة، وحتى إطارات الحدود إذا احتجت إليها.

```csharp
var ocrResult = ocrEngine.Recognize(processedImage);
Console.WriteLine(ocrResult.Text);
```

**نموذج الإخراج** (بافتراض أن الصورة الأصلية تحتوي على “Invoice #12345”):

```
=== OCR Output ===
Invoice #12345
Date: 04/28/2026
Total: $1,234.56
```

إذا لاحظت فقدان أحرف، أعد فحص سلسلة ما قبل المعالجة – ربما لا تزال الصورة تحتاج إلى تنقية أقوى أو مستوى تباين مختلف.  

> *سؤال شائع:* “ماذا لو أردت التعرف على لغة غير الإنجليزية؟”  
> فقط اضبط `ocrEngine.Language = Language.English;` إلى لغة مدعومة أخرى (مثل `Language.French`). خطوات ما قبل المعالجة تبقى كما هي.

---

## تحسين دقة OCR – تعديلات إضافية

حتى مع خط أنابيب مثالي، بعض الضوابط الإضافية يمكنها دفع **تحسين دقة OCR** إلى أعلى:

| النصيحة | متى تُستخدم | الطريقة |
|---------|-------------|----------|
| **التحويل إلى ثنائي** | مسحات داكنة جداً أو فاتحة جداً | `processingPipeline.Add(new FilterBinarize());` |
| **تغيير حجم الصورة** | خطوط صغيرة (<10 pt) | `processedImage = OcrEngine.Resize(processedImage, 2.0);` |
| **تحديد مجموعة الأحرف** | معرفة الأبجدية (أرقام فقط، إلخ) | `ocrEngine.Characters = "0123456789";` |
| **ملفات PDF متعددة الصفحات** | معالجة دفعة | حلقة تكرار على كل صفحة وإعادة استخدام نفس الخط الأنابيب. |

تذكر: كل مرشح إضافي يضيف وقت معالجة، لذا فعّل فقط ما تحتاجه فعلاً.

---

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج بالكامل، جاهز للترجمة. استبدل `YOUR_DIRECTORY` بالمجلد الذي يحتوي على `skewed_noisy.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Build preprocessing pipeline
        ImageProcessingPipeline pipeline = new ImageProcessingPipeline();
        pipeline.Add(new FilterDeskew());                     // how to deskew image
        pipeline.Add(new FilterDenoise { Strength = 2 });    // remove noise from image
        pipeline.Add(new FilterContrastBoost { ContrastLevel = 1.8f }); // boost image contrast

        // Load source image
        var sourcePath = @"YOUR_DIRECTORY/skewed_noisy.jpg";
        var sourceImage = OcrEngine.LoadImage(sourcePath);

        // Apply pipeline
        var cleanImage = pipeline.Apply(sourceImage);

        // Perform OCR
        var result = ocrEngine.Recognize(cleanImage);

        // Output
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

**النتيجة المتوقعة:** نص نظيف ومُستقيم يُطبع على وحدة التحكم، مع أخطاء أقل بكثير مقارنةً بتمرير الملف الأصلي مباشرة إلى `ocrEngine.Recognize`.

---

## الخلاصة

غطّينا **كيفية تصحيح ميل الصورة**، **إزالة الضوضاء من الصورة**، **زيادة تباين الصورة**، وأخيراً **استخراج النص من الصورة** باستخدام Aspose OCR. بربط هذه المرشحات ستحصل على قفزة ملحوظة في **تحسين دقة OCR**، خاصةً على المسحات منخفضة الجودة.

هل أنت مستعد للتحدي التالي؟ جرّب تمرير ملف PDF متعدد الصفحات عبر نفس الخط الأنابيب، أو جرب عتبات مخصصة للتحويل إلى ثنائي. المبادئ نفسها تنطبق – صَحِّح، نظّف، أضِئ، ثم تعرّف.

هل لديك أسئلة أو حالة خاصة غريبة؟ اترك تعليقاً، وسنساعدك على حلها معاً. برمجة سعيدة!  

![مثال على كيفية تصحيح ميل الصورة](deskew-example.png "مثال على كيفية تصحيح ميل الصورة")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}