---
category: general
date: 2026-02-20
description: معالجة مسبقة لتقنية OCR للصور باستخدام Aspose.OCR في C#. تعلم كيفية تطبيق
  مرشح المتوسط، تقليل ضوضاء الصورة، واستخراج النص من الصورة بكفاءة.
draft: false
keywords:
- preprocess image OCR
- apply median filter
- extract text image
- reduce image noise
- c# ocr example
language: ar
og_description: معالجة OCR للصور مسبقًا باستخدام Aspose.OCR. يوضح هذا الدرس كيفية
  تطبيق مرشح المتوسط، تقليل ضوضاء الصورة، واستخراج النص من الصورة باستخدام C#.
og_title: المعالجة المسبقة لتقنية OCR للصور في C# – دليل شامل
tags:
- OCR
- C#
- Image Processing
title: معالجة مسبقة لتقنية OCR للصور في C# – دليل كامل خطوة بخطوة
url: /ar/net/ocr-optimization/preprocess-image-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# معالجة ما قبل OCR للصور في C# – دليل خطوة بخطوة كامل

هل احتجت يومًا إلى **preprocess image OCR** لأن الصور الممسوحة ضوئيًا تعطي نصًا مشوشًا؟ لست وحدك. في العديد من المشاريع الواقعية—مثل الإيصالات، بطاقات الهوية، أو الملاحظات المكتوبة يدويًا—نادرًا ما تكون الصورة الخام جاهزة للتعرف الفوري. الخبر السار؟ بضع خطوات بسيطة للمعالجة المسبقة يمكنها تحسين الدقة بشكل كبير، ويمكنك تنفيذها كلها في C# باستخدام Aspose.OCR.

في هذا الدرس سنستعرض مثالًا عمليًا يوضح كيفية **apply median filter**، **reduce image noise**، وأخيرًا **extract text image** مع نتيجة نظيفة قابلة للقراءة. بنهاية الدرس ستحصل على تطبيق C# Console قابل للتنفيذ بالكامل يمكنك إدراجه في أي حل .NET. لا مراجع غامضة، فقط الشيفرة التي تحتاجها و"السبب" وراء كل سطر.

---

## ما ستحتاجه

- **Aspose.OCR for .NET** (أحدث نسخة وقت الكتابة، 23.12). يمكنك الحصول عليها عبر NuGet: `Install-Package Aspose.OCR`.
- .NET 6.0 أو أحدث (المثال يستخدم تطبيق console، لكن نفس المنطق يعمل في ASP.NET، WPF، إلخ).
- صورة نموذجية تحتاج إلى تنظيف—مثال، `skewed_photo.jpg`.  
- قليل من الخبرة في C#؛ المفاهيم بسيطة حتى للمطورين المبتدئين.

> **نصيحة احترافية:** إذا كنت تستخدم جهازًا مؤسسيًا، تأكد من أن مصدر NuGet مُعد للسماح بالحزم الخارجية، وإلا سيفشل التثبيت.

## الخطوة 1 – إنشاء مثيل محرك OCR  

أول شيء تقوم به هو إنشاء كائن `OcrEngine`. هذا الكائن يحتفظ بإعدادات التعرف وسيعالج لاحقًا الـ bitmap المُعالج مسبقًا.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image handling
using System;

class PreprocessExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is the core component that will read text.
        OcrEngine ocrEngine = new OcrEngine();

        // ... we’ll continue with loading and preprocessing the image below.
```

**لماذا؟**  
إنشاء المحرك مرة واحدة وإعادة استخدامه عبر صور متعددة يقلل من الحمل الزائد. كما يتيح لك تعديل اللغة أو أوضاع التعرف لاحقًا دون الحاجة لإعادة بناء خط الأنابيب بالكامل.

## الخطوة 2 – تحميل الصورة المصدر  

تحتاج إلى كائن `System.Drawing.Image` يشير إلى ملفك الخام. في مشروع حقيقي قد تقبل تدفقًا (stream)، لكن للتوضيح سنقرأ من القرص.

```csharp
        // Load the image that requires preprocessing.
        Image sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_photo.jpg");
```

> **ملاحظة:** استبدل `YOUR_DIRECTORY` بالمسار الفعلي للمجلد. إذا لم يُعثر على الملف، سيتم رمي استثناء `FileNotFoundException`—قم بالتقاطه إذا أردت معالجة الأخطاء برشاقة.

## الخطوة 3 – تصحيح الميل وتدوير الصورة  

معظم المستندات الممسوحة تكون مائلة قليلاً. مرشح `DeskewAndRotate` يكتشف زاوية الميل تلقائيًا ويُدوّر الصورة إلى وضعية عمودية.

```csharp
        // Correct orientation – crucial for accurate OCR.
        Image processedImage = sourceImage.Apply(Preprocess.DeskewAndRotate());
```

**لماذا هذا مهم؟**  
محركات OCR تفترض أن خطوط النص أفقية. حتى ميل بمقدار درجتين يمكن أن يقلل دقة التعرف بنسبة 15‑20 %. تصحيح الميل هو أرخص طريقة لتحقيق تحسين كبير.

## الخطوة 4 – تطبيق مرشح المتوسط لتقليل ضوضاء الصورة  

الضوضاء تظهر كبقع أو بكسلات عشوائية، خاصة في الصور ذات الإضاءة المنخفضة. مرشح المتوسط ينعّم هذه البقع مع الحفاظ على الحواف، وهذا ما نحتاجه قبل OCR.

```csharp
        // Reduce noise – radius of 2 is a good balance for most photos.
        processedImage = processedImage.Apply(Preprocess.MedianFilter(radius: 2));
```

**لماذا مرشح المتوسط؟**  
على عكس مرشح المتوسط الحسابي (mean)، مرشح المتوسط يستبدل كل بكسل بالقيمة المتوسطة لجيرانه. هذا يعني أن الضوضاء المعزولة تُقضى دون تمويه خطوط النص—تقنية كلاسيكية لـ **reduce image noise**.

## الخطوة 5 – تحسين التباين بالتمدد  

بعد إزالة الضوضاء، الخطوة التالية هي تعزيز الفرق بين النص والخلفية. تمطيط التباين يوزع شدة البكسلات عبر النطاق الكامل 0‑255.

```csharp
        // Stretch contrast to make dark text pop against a light background.
        processedImage = processedImage.Apply(Preprocess.ContrastStretch());
```

**لماذا التمدد؟**  
محركات OCR تعتمد على فصل واضح بين المقدمة والخلفية. إذا كانت الصورة باهتة، قد يعتبر المحرك النص خلفية. تمطيط التباين يحل ذلك دون الحاجة إلى تحديد عتبة يدويًا.

## الخطوة 6 – تنفيذ OCR على الصورة المعالجة مسبقًا  

الآن بعد أن أصبحت الصورة مستقيمة، نظيفة، وعالية التباين، نمررها إلى محرك OCR.

```csharp
        // Recognize the text from the cleaned image.
        string extractedText = ocrEngine.Recognize(processedImage);
```

**ما ستحصل عليه:**  
`extractedText` يحتوي على سلسلة Unicode الخام التي اكتشفها Aspose.OCR. يمكنك معالجة ما بعد ذلك (تقليم، تعبيرات regex، إلخ) إذا لزم الأمر.

## الخطوة 7 – إخراج النص المعترف به  

أخيرًا، اكتب النتيجة إلى الـ console أو ملف—حسب ما يناسب سير عملك.

```csharp
        // Show the result in the console.
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

### النتيجة المتوقعة

إذا كان `skewed_photo.jpg` يحتوي على العبارة “Hello World”، سترى شيئًا مثل:

```
=== Extracted Text ===
Hello World
```

إذا كانت الصورة لا تزال مشوشة، قد تلاحظ أحرفًا غير مفهومة—ارجع إلى الخطوة 4 وزد نصف قطر مرشح المتوسط، أو جرّب فلاتر إضافية مثل `GaussianBlur`.

## مثال كامل جاهز للتنفيذ (انسخه‑الصقه)

فيما يلي البرنامج الكامل، جاهز للترجمة. لا توجد أجزاء مفقودة—فقط استبدل مسار الملف.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;
using System;

class PreprocessExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image that needs preprocessing
        Image sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_photo.jpg");

        // Step 3: Deskew and rotate the image to correct orientation
        Image processedImage = sourceImage.Apply(Preprocess.DeskewAndRotate());

        // Step 4: Reduce noise with a median filter (radius = 2)
        processedImage = processedImage.Apply(Preprocess.MedianFilter(radius: 2));

        // Step 5: Enhance contrast using contrast stretching
        processedImage = processedImage.Apply(Preprocess.ContrastStretch());

        // Step 6: Perform OCR on the preprocessed image
        string extractedText = ocrEngine.Recognize(processedImage);

        // Step 7: Output the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

> **نصيحة لحالات الحافة:** إذا كانت صورتك تحتوي على نص ملون على خلفية ملونة، فكر في تحويلها إلى تدرج الرمادي قبل تطبيق `ContrastStretch`. يمكنك القيام بذلك باستخدام `Preprocess.Grayscale()` في خط الأنابيب.

## أسئلة شائعة وتنوعات  

### ماذا لو كانت الصورة مقلوبة رأسًا على عقب؟  
`DeskewAndRotate` يكتشف تلقائيًا دورانات 180 درجة، لكن يمكنك فرض دوران باستخدام `Preprocess.Rotate(angle: 180)` قبل تصحيح الميل.

### هل يمكنني تخطي مرشح المتوسط؟  
نعم، لكن من المحتمل أن تقل فوائد **reduce image noise**. في المسحات عالية الدقة قد يكون الفلتر غير ضروري؛ في صور الهواتف ذات الإضاءة المنخفضة، يكون عادةً أساسيًا.

### كيف يختلف هذا عن `Apply(Preprocess.Binarize())` البسيط؟  
التحويل إلى ثنائي (Binarization) يحول الصورة إلى أبيض وأسود نقي، مما قد يكون قاسيًا على الخطوط الرفيعة. نهجنا يحتفظ بتفاصيل التدرج الرمادي، ثم يمد التباين—غالبًا ما ينتج عنه نتائج أفضل للخطوط ذات الأحجام المختلطة.

### هل هناك طريقة لتطبيق **apply median filter** فقط على منطقة اهتمام؟  
`Apply` في Aspose.OCR يعمل على كامل الـ bitmap، لكن يمكنك قص الصورة أولاً (`sourceImage.Clone(new Rectangle(...), sourceImage.PixelFormat)`) ثم تطبيق الفلتر على تلك الصورة الفرعية.

## الخطوات التالية – ما بعد المعالجة الأساسية  

- **Language Packs:** إذا كنت بحاجة لاستخراج أحرف فرنسية أو يابانية، حمّل نموذج اللغة المناسب عبر `ocrEngine.Language = Language.French;`.
- **Custom Thresholding:** للمسحات ذات التباين المنخفض جدًا، جرّب `Preprocess.AdaptiveThreshold()` بعد مرشح المتوسط.
- **Batch Processing:** غلف الخطوات داخل حلقة `foreach (string file in Directory.GetFiles(...))` واكتب كل نتيجة إلى ملف `.txt`.
- **Performance Tuning:** أعد استخدام مثيل واحد من `OcrEngine` وخصص مسبقًا مخزن `Bitmap` لتجنب ارتفاعات GC عند معالجة آلاف الصور.

## الخلاصة  

لقد أظهرنا للتو كيفية **preprocess image OCR** في C# من البداية إلى النهاية: تحميل الصورة، تصحيح الميل، **apply median filter**، تعزيز التباين، وأخيرًا **extract text image** باستخدام Aspose.OCR. مقتطف الشيفرة الكامل جاهز للإدراج في أي مشروع، والتفسيرات تعطيك “السبب” وراء كل تحويل—حتى تتمكن من تعديل المعلمات وفقًا لحالاتك الخاصة.

جرّبه مع عدة صور مختلفة، العب بمدى الفلتر، وشاهد دقة التعرف ترتفع. عندما تشعر بالراحة، استكشف التعديلات المتقدمة المذكورة أعلاه، وستصبح الشخص المرجعي لخطوط OCR النظيفة في فريقك.

برمجة سعيدة، ولتكن OCR دائمًا تقرأ بنقاء! 

![مثال على preprocess image OCR](/images/preprocess-image-ocr.png "preprocess image OCR – قبل وبعد المعالجة")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}