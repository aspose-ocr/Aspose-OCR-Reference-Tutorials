---
category: general
date: 2025-12-29
description: تعلم كيفية تصحيح انحراف الصورة، وإزالة الخلفية، واستخراج النص باستخدام
  Aspose OCR. كود C# خطوة بخطوة لمعالجة الصورة مسبقًا للتعرف الضوئي على الأحرف والتعرف
  على النص من الصورة.
draft: false
keywords:
- how to deskew image
- how to remove background
- how to extract text
- preprocess image for ocr
- recognize text from image
language: ar
og_description: كيفية تصحيح انحراف الصورة وزيادة دقة OCR. اتبع هذا الدليل لإزالة الخلفية،
  ومعالجة الصورة مسبقًا للتعرف الضوئي على الأحرف، والتعرف على النص من الصورة باستخدام
  Aspose.
og_title: كيفية تصحيح إمالة الصورة – درس تمهيدي لمعالجة OCR باستخدام C#
tags:
- Aspose OCR
- C#
- Image preprocessing
title: كيفية تصحيح انحراف الصورة – دليل C# الكامل لمعالجة ما قبل OCR
url: /ar/net/skew-angle-calculation/how-to-deskew-image-complete-c-guide-for-ocr-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح إمالة الصورة – دليل C# كامل لمعالجة ما قبل OCR

هل تساءلت يومًا **كيف تصحح إمالة الصورة** التي خرجت من الماسح الضوئي وكأنها بطاقة بريدية مائلة؟ لست وحدك. في العديد من المشاريع الواقعية تكون الصور المصدر مائلة، أو مشوشة، أو تعاني من خلفية غير متجانسة، وهذا يجعل OCR يواجه صعوبات.  

في هذا الدرس سنستعرض حلًا عمليًا لا يقتصر فقط على **كيفية تصحيح إمالة الصورة** بل يشمل أيضًا **كيفية إزالة الخلفية**، **كيفية استخراج النص**، وأخيرًا **التعرف على النص من الصورة** باستخدام Aspose OCR لـ .NET. في النهاية ستحصل على برنامج C# جاهز للتنفيذ يقوم بتهيئة الصورة لـ OCR ويعيد نصًا نظيفًا وقابلًا للبحث.

## ما الذي ستحتاجه

- .NET 6 SDK أو أحدث (الكود يعمل على .NET Core و .NET Framework على حد سواء)  
- Visual Studio 2022 (أو أي محرر تفضله)  
- حزمة NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- صورة نموذجية مائلة ومشوشة (مثال: `skewed_noisy.jpg`)  

هذا كل شيء—بدون مكتبات أصلية إضافية، ولا أدوات سطر أوامر معقدة. هيا نبدأ.

## الخطوة 1 – تحميل صورة الإدخال (بدء عملية تصحيح إمالة الصورة)

أول شيء يجب القيام به هو جلب الصورة إلى الذاكرة. طريقة `Image.Load` في Aspose OCR تقبل مسار الملف وتعيد كائن `Image` يمكنك معالجته.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class Program
{
    static void Main()
    {
        // Load the original photo that needs deskewing and cleaning
        Image originalImage = Image.Load("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **لماذا هذا مهم:** تحميل الصورة يمنحنا مقبضًا لتطبيق كل التحويلات اللاحقة، من تصحيح الإمالة إلى إزالة الخلفية.

## الخطوة 2 – تصحيح إمالة الصورة (كيفية تصحيح إمالة الصورة عمليًا)

تأتي Aspose OCR مع مرشح `Deskew` المفيد الذي يكتشف زاوية الميلان تلقائيًا حتى حد قابل للتكوين. هنا نسمح بحد أقصى **5°** لأن معظم المستندات الممسوحة لا تتجاوز ذلك.

```csharp
        // Auto‑detect and correct rotation up to 5 degrees
        Image deskewed = ImageFilters.Deskew(originalImage, angleThreshold: 5);
```

> **نصيحة احترافية:** إذا كانت مستنداتك مائلة بأكثر من 5°، زد قيمة `angleThreshold` إلى 10 أو 15. يظل الخوارزم سريعًا حتى مع الزوايا الأكبر.

## الخطوة 3 – إزالة الضوضاء من الصورة المصححة

الضوضاء هي القاتل الصامت لدقة OCR. تمريرة إزالة الضوضاء البسيطة تُنعّم البقع دون تشويش الأحرف الفعلية.

```csharp
        // Reduce random speckles and grain
        Image denoised = deskewed.Denoise();
```

> **ماذا يحدث خلف الكواليس؟** يطبق المرشح تمويهًا متوسطًا يحافظ على الحواف (الأحرف) بينما يخفّف البكسلات المعزولة.

## الخطوة 4 – إزالة الخلفية (كيفية إزالة الخلفية بفعالية)

خلفية فاتحة أو نمطية يمكن أن تُربك محرك OCR. طريقة `RemoveBackground` في Aspose OCR تعزل النص الأمامي.

```csharp
        // Strip away uneven lighting or paper texture
        Image processedImage = denoised.RemoveBackground();
```

> **لماذا نزيل الخلفية؟** بزيادة التباين بين النص والقماش، يستطيع المحرك تمييز الأحرف بشكل أكثر موثوقية، مما يحسّن مباشرةً نتائج **كيفية استخراج النص**.

## الخطوة 5 – تهيئة محرك OCR

الآن بعد أن أصبحت الصورة مستقيمة، نظيفة، وعالية التباين، نقوم بإنشاء محرك OCR. لا تحتاج إلى إعدادات إضافية للغات اللاتينية الأساسية، لكن يمكنك تغيير اللغة إذا لزم الأمر.

```csharp
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **ملاحظة:** يدعم Aspose OCR أكثر من 100 لغة. إذا كنت بحاجة إلى دعم متعدد اللغات، عيّن `ocrEngine.Language = OcrLanguage.YourLanguage;` قبل عملية التعرف.

## الخطوة 6 – التعرف على النص من الصورة (كيفية استخراج النص)

مع جاهزية المحرك، قدم له الصورة التي تمت معالجتها مسبقًا. طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على النص الخام ودرجات الثقة.

```csharp
        // Perform the actual OCR
        OcrResult ocrResult = ocrEngine.Recognize(processedImage);
```

> **نظرة على النتيجة:** `ocrResult.Text` يحمل السلسلة النصية، بينما `ocrResult.Confidence` (إن استدعيتَها) يُظهر مدى ثقة المحرك بكل سطر.

## الخطوة 7 – إخراج النص المُعترف به

أخيرًا، اطبع النص المستخرج على وحدة التحكم—أو احفظه في ملف، قاعدة بيانات، أو أي وسيلة تناسب سير عملك.

```csharp
        // Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

البرنامج الكامل الآن جاهز للتنفيذ. ابنِه وشغّله، وسترى نصًا نظيفًا وقابلًا للقراءة رغم أن الصورة الأصلية كانت مائلة ومشوشة.

![مثال على كيفية تصحيح إمالة الصورة](/images/deskew-demo.png "عرض توضيحي لكيفية تصحيح إمالة الصورة باستخدام Aspose OCR")

*تُظهر اللقطة أعلاه قبل وبعد تصحيح إمالة الصورة، موضحةً تأثير سلسلة المعالجة المسبقة.*

## الحالات الخاصة والأسئلة الشائعة

### ماذا لو كانت الصورة مائلة بأكثر من 5°؟
زد قيمة `angleThreshold` في استدعاء `Deskew`. سيستمر الخوارزم في اكتشاف الزاوية الصحيحة، فقط ضمن نافذة بحث أوسع.

### مستندي يحتوي على نص ملون—هل `RemoveBackground` يفسده؟
`RemoveBackground` يعمل على الإضاءة، لذا يُحوّل النص الملون إلى تدرج رمادي قبل التنظيف. إذا كنت بحاجة للحفاظ على اللون للمعالجة اللاحقة، تخطَّ هذه الخطوة واعتمد فقط على إزالة الضوضاء.

### كيف أتعامل مع ملفات PDF متعددة الصفحات؟
حوّل كل صفحة PDF إلى صورة (مثلاً باستخدام Aspose.PDF)، ثم مرّر كل صورة عبر نفس السلسلة. كرّر العملية على الصفحات وادمج سلاسل `ocrResult.Text`.

### هل يمكن تحسين الدقة للملاحظات المكتوبة يدويًا؟
فكّر في تمكين `ocrEngine.Options.UseNeuralNetwork = true;` (متوفر في إصدارات Aspose الأحدث) وزد دقة الصورة إلى ما لا يقل عن 300 dpi قبل المعالجة.

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي ملف المصدر الكامل مع جميع توجيهات `using` والتعليقات الضرورية. الصقه في مشروع وحدة تحكم جديد واضغط **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the original image (skewed, noisy, etc.)
            Image originalImage = Image.Load("YOUR_DIRECTORY/skewed_noisy.jpg");

            // 2️⃣ Deskew – auto‑detect tilt up to 5°
            Image deskewed = ImageFilters.Deskew(originalImage, angleThreshold: 5);

            // 3️⃣ Denoise – smooth out speckles
            Image denoised = deskewed.Denoise();

            // 4️⃣ Remove background – boost contrast
            Image processedImage = denoised.RemoveBackground();

            // 5️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 6️⃣ Recognize text from the cleaned image
            OcrResult ocrResult = ocrEngine.Recognize(processedImage);

            // 7️⃣ Output the extracted text
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**الناتج المتوقع** (مثال لفاتورة بسيطة):

```
=== OCR Output ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,250.00
Thank you for your business!
```

إذا ظهر الناتج مشوشًا، تحقق من وضوح الصورة الأصلية وأن زاوية الإمالة ليست أكبر من العتبة التي حددتها.

## الخلاصة

غطّينا **كيفية تصحيح إمالة الصورة** خطوة بخطوة، وأظهرنا **كيفية إزالة الخلفية**، وشرحنا **كيفية استخراج النص** عبر المعالجة المسبقة، وأخيرًا استخدمنا Aspose OCR لـ **التعرف على النص من الصورة**. كل ذلك في برنامج C# مختصر يمكنك توسيعه لمعالجة دفعات، تحويل PDF، أو دمجه في نظام إدارة مستندات أكبر.

هل أنت مستعد للتحدي التالي؟ جرّب تمرير مجلد من ملفات PDF الممسوحة عبر هذه السلسلة، أو جرب إعدادات إزالة الضوضاء المختلفة لترى كيف تؤثر على درجات الثقة. كلما لعبت بالإعدادات، كلما فهمت أفضل التوازن بين السرعة والدقة.

لديك أسئلة أو صورة صعبة لا تزال ترفض التعاون؟ اترك تعليقًا أدناه، ولنحل المشكلة معًا. برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة كالكريستال!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}