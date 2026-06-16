---
category: general
date: 2026-04-03
description: كيفية تصحيح ميل الصورة باستخدام Aspose OCR في C# – تعلم كيفية تمهيد الصورة
  للتعرف الضوئي على الأحرف، التعرف على النص من الصورة وتحسين دقة OCR في دقائق.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from image
- improve ocr accuracy
- load image for ocr
language: ar
og_description: كيفية تصحيح انحراف الصورة في C# باستخدام Aspose OCR. يوضح هذا الدليل
  كيفية إعداد الصورة مسبقًا للتعرف الضوئي على الأحرف، والتعرف على النص من الصورة،
  وتعزيز الدقة.
og_title: كيفية تصحيح انحراف الصورة باستخدام Aspose OCR – دليل C# الكامل
tags:
- Aspose OCR
- C#
- Image preprocessing
title: كيفية تصحيح انحراف الصورة باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/ocr-optimization/how-to-deskew-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح إمالة الصورة باستخدام Aspose OCR – دليل C# الكامل

هل تساءلت يومًا **كيفية تصحيح إمالة الصورة** قبل تمريرها إلى محرك OCR؟ لست وحدك—المسحات المائلة، الصور الملتقطة بزاوية، أو حتى ملفات PDF المائلة قليلاً يمكن أن تفسد أي مكتبة للتعرف على النص.  

في هذا الدليل خطوة بخطوة سنستعرض سير العمل بالكامل: من تحميل الصورة، مرورًا بـ **preprocess image for OCR** (تصحيح الإمالة، إزالة الضوضاء، تعزيز التباين، التدوير التلقائي)، وصولًا إلى **recognize text from image** باستخدام Aspose OCR، وأخيرًا بعض النصائح لـ **improve OCR accuracy**. في النهاية ستحصل على تطبيق C# Console جاهز للتشغيل يتعامل مع PNG مشوش ومائل كالمحترفين.

## ما ستحتاجه

- **.NET 6+** (أو .NET Framework 4.7.2 – الـ API يعمل بنفس الطريقة)
- **Aspose.OCR for .NET** حزمة NuGet (`Install-Package Aspose.OCR`)
- صورة نموذجية **مائلة** و**مشوشة** (مثال: `skewed_noisy.png`)
- Visual Studio، Rider، أو أي محرر تفضله – لا تحتاج إلى أدوات خاصة

> **Pro tip:** إذا لم يكن لديك عينة مائلة، فقط قم بتدوير لقطة شاشة نظيفة بزاوية 10‑15° في Paint وأضف قليلًا من ضوضاء “الملح والفلفل” باستخدام محرر صور. الكود سيعمل بنفس الطريقة.

الآن، لنبدأ.

## كيفية تصحيح إمالة الصورة وتعزيز دقة OCR

أول شيء تريد فعله هو إخبار `OcrEngine` الخاصة بـ Aspose بـ **deskew** للـ bitmap الوارد. المحرك يأتي مع فئة مدمجة `ImagePreprocessingOptions` تتيح لك تشغيل عدة ميزات تحسين الجودة مرة واحدة.

```csharp
using Aspose.OCR;
using System.Drawing;

/// <summary>
/// Demonstrates how to deskew image, denoise, boost contrast, and run OCR.
/// </summary>
class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing options
        ImagePreprocessingOptions opts = new ImagePreprocessingOptions
        {
            Deskew = true,          // <-- this is the key to how to deskew image
            Denoise = true,
            ContrastBoost = 30,    // increase contrast by 30 %
            AutoRotate = true
        };
        ocrEngine.PreprocessingOptions = opts;

        // 3️⃣ Load the image you want to process
        Image input = Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run OCR on the pre‑processed bitmap
        string text = ocrEngine.Recognize(input);

        // 5️⃣ Show the result
        System.Console.WriteLine(text);
    }
}
```

### لماذا هذا يعمل

- **Deskew = true** يخبر المحرك باكتشاف خط أساس النص وتدوير الصورة حتى يصبح الخط أفقيًا. بدون ذلك، حتى إمالة 5° قد تقلل الدقة بنسبة 15‑20 %.
- **Denoise** يزيل البقع العشوائية التي تظهر غالبًا بعد مسح المستندات منخفضة الدقة.
- **ContrastBoost** يعزز الفارق بين المقدمة (النص) والخلفية (الورق)، وهو أساسي لـ **improve OCR accuracy**.
- **AutoRotate** يتعامل مع الوضعية العمودية مقابل الأفقية تلقائيًا، مما يوفر عليك فحصًا يدويًا.

الكود أعلاه هو **مثال كامل وقابل للتنفيذ**—فقط استبدل `YOUR_DIRECTORY` بمسار ملفك واضغط F5.

## Preprocess Image for OCR – إزالة الضوضاء وتعزيز التباين

قد تتساءل إذا كنت بحاجة فعلاً إلى كل من إزالة الضوضاء وتعزيز التباين. الجواب المختصر: **نعم، في معظم الحالات الواقعية**. إليك نظرة سريعة:

| الميزة | ما تفعله | متى تكون مهمة |
|--------|----------|----------------|
| **Deskew** | يسطّح خطوط النص المائلة | نماذج مسح، لقطات من كاميرا الهاتف |
| **Denoise** | يزيل البكسلات المنعزلة | مسحات بإضاءة منخفضة، ماسحات رخيصة |
| **ContrastBoost** | يفتح النص الداكن ويغلق الخلفية | مستندات باهتة، حبر باهت |
| **AutoRotate** | يكتشف الوضعية العمودية مقابل الأفقية | ملفات PDF متعددة الصفحات ذات اتجاهات مختلطة |

إذا كنت تعالج مسحًا نقيًا ومُحاذيًا تمامًا، يمكنك إيقاف العلامات، لكن **preprocess image for OCR** هو الإعداد الافتراضي الآمن الذي نادرًا ما يضر.

## Recognize Text from Image – باستخدام Aspose OCR

بعد انتهاء خط أنابيب المعالجة المسبقة، يسلّم المحرك الـ bitmap المنظف إلى المعرّف الداخلي الخاص به. طريقة `Recognize` تُرجع سلسلة `string` عادية مع الحفاظ على فواصل الأسطر. يمكنك إجراء معالجة لاحقة للنتيجة (مثل قص الفراغات، تشغيل التدقيق الإملائي) إذا لزم الأمر.

```csharp
string recognizedText = ocrEngine.Recognize(inputImage);
Console.WriteLine("--- OCR RESULT ---");
Console.WriteLine(recognizedText);
```

### النتيجة المتوقعة

إذا كان `skewed_noisy.png` يحتوي على العبارة “Hello World!”، سيطبع الطرفية شيءً مثل:

```
--- OCR RESULT ---
Hello World!
```

حتى مع ضوضاء معتدلة، يجب أن ترى **دقة تتجاوز 95 %** بفضل خطوات المعالجة المسبقة التي فعلناها.

## Load Image for OCR – نصائح التعامل مع الملفات

السطر `Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png")` هو أبسط طريقة لـ **load image for OCR**، لكن هناك بعض التفاصيل التي تستحق الذكر:

1. **قفل الملفات** – `FromFile` يبقي مقبض الملف مفتوحًا حتى يتم التخلص من الـ `Image`. احرص على وضعه داخل كتلة `using` إذا كنت تخطط لحذف أو نقل الملف لاحقًا.
2. **الصيغ المدعومة** – Aspose OCR يقبل BMP، JPEG، PNG، TIFF، و GIF. إذا كان لديك ملفات PDF، استخرج كل صفحة كصورة أولًا (Aspose.PDF يمكنه المساعدة).
3. **استهلاك الذاكرة** – الصور الكبيرة (أكثر من 5 MP) قد تستهلك ذاكرة RAM كبيرة. فكر في تقليل الحجم باستخدام `Bitmap` قبل تمريره إلى المحرك إذا واجهت `OutOfMemoryException`.

```csharp
using (Image input = Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png"))
{
    string result = ocrEngine.Recognize(input);
    Console.WriteLine(result);
}
```

## Improve OCR Accuracy – نصائح من الواقع

حتى مع المعالجة التلقائية، لا تزال بعض الحالات الحدية تُعرّق محركات OCR. إليك استراتيجيات تم اختبارها يمكنك إضافتها إلى خط أنابيبك:

- **Binarize the image** (`opts.Binarization = true`) عندما تكون الخلفية غير متساوية.
- **Set language** (`ocrEngine.Language = Language.English`) لتقليل مجموعة الأحرف.
- **Increase DPI**: إذا كنت تتحكم بعملية المسح، استهدف على الأقل 300 dpi.
- **Crop margins**: أزل الحدود البيضاء الكبيرة؛ يمكن أن تُربك اكتشاف الخطوط.
- **Validate output**: استخدم التعابير النمطية للتحقق من التواريخ، الأرقام، أو الأنماط المعروفة، ثم ضع علامة على الأسطر ذات الثقة المنخفضة للمراجعة اليدوية.

> **Remember:** الهدف ليس فقط **recognize text from image**، بل القيام بذلك بثقة عبر مجموعة متنوعة من جودة المستندات.

## Full Working Example – جميع الخطوات في ملف واحد

فيما يلي البرنامج النهائي المتكامل الذي يمكنك نسخه ولصقه في مشروع Console جديد.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class DeskewOcrDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine engine = new OcrEngine();

        // Preprocess settings (deskew, denoise, contrast, auto‑rotate)
        engine.PreprocessingOptions = new ImagePreprocessingOptions
        {
            Deskew = true,
            Denoise = true,
            ContrastBoost = 30,
            AutoRotate = true
        };

        // Load image – make sure the path is correct
        const string imagePath = @"YOUR_DIRECTORY/skewed_noisy.png";

        // Using block prevents file‑handle leaks
        using (Image img = Image.FromFile(imagePath))
        {
            // Run OCR
            string text = engine.Recognize(img);

            // Output result
            Console.WriteLine("--- OCR RESULT ---");
            Console.WriteLine(text);
        }
    }
}
```

شغّل البرنامج، وسترى النص المنظف والمُصحح يُطبع في الطرفية. إذا استبدلت `skewed_noisy.png` بصورة نظيفة ومُستقيمة، ستكون النتيجة متماثلة—مع تحسين طفيف في الأداء لأن المحرك سيتخطى خطوة تصحيح الإمالة.

## الخلاصة

غطّينا **كيفية تصحيح إمالة الصورة** باستخدام Aspose OCR، وأظهرنا لك كيف **preprocess image for OCR**، وبيّنّا الطريقة الصحيحة لـ **load image for OCR**، وأخيرًا **recognize text from image** مع مراعاة **improve OCR accuracy**. المقتطف البرمجي الكامل جاهز للإدراج في أي مشروع .NET، والنصائح الإضافية تعطيك خارطة طريق للتعامل مع مدخلات أصعب.

هل أنت مستعد للتحدي التالي؟ جرّب ربط عدة صور معًا لإنشاء تدفق عمل OCR متعدد الصفحات، أو جرب حزم لغات مخصصة للمستندات غير الإنجليزية. مبادئ المعالجة المسبقة نفسها تُطبق—تصحيح الإمالة، إزالة الضوضاء، تعزيز التباين، ودع Aspose يتولى الجزء الصعب.

هل لديك أسئلة حول نوع ملف معين أو تحتاج مساعدة في تعديل قيمة `ContrastBoost`؟ اترك تعليقًا أدناه أو تفاعل في منتديات Aspose. برمجة سعيدة، ولتكن OCR دائمًا دقيقة!  

![مخطط يوضح الصورة الأصلية المائلة على اليسار والنتيجة المصححة والمُنظفة على اليمين](deskew-diagram.png "مخطط يوضح الصورة الأصلية المائلة والنتيجة المصححة – مثال على كيفية تصحيح إمالة الصورة")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}