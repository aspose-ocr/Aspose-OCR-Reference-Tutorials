---
category: general
date: 2026-01-10
description: كيفية تصحيح انحراف الصورة وتحسين نتائج OCR باستخدام Aspose.OCR. تعلم
  كيفية تمهيد الصورة للـ OCR، إزالة الضوضاء من المسح، والتعرف على النص من المسح.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from scan
- how to use ocr
- remove noise from scan
language: ar
og_description: كيفية تصحيح انحراف الصورة وزيادة دقة OCR. يوضح هذا الدليل كيفية إعداد
  الصورة مسبقًا للتعرف الضوئي على الأحرف، وإزالة الضوضاء من المسح، والتعرف على النص
  من المسح باستخدام Aspose.OCR.
og_title: كيفية تصحيح إمالة الصورة في C# – دليل شامل لمعالجة ما قبل التعرف الضوئي
  على الأحرف
tags:
- OCR
- C#
- Image Processing
title: كيفية تصحيح إمالة الصورة في C# – دليل شامل لمعالجة ما قبل OCR
url: /ar/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح ميل الصورة في C# – دليل شامل لمعالجة ما قبل OCR

هل تساءلت يومًا **كيف تصحح ميل الصورة** قبل تمريرها إلى محرك OCR؟ لست وحدك. غالبًا ما تكون المستندات الممسوحة ضوئيًا مائلة، أو مشوشة، أو ذات تباين منخفض، وهذا يعيق أي محاولة للتعرف على النص.  

في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ **يعالج الصورة من أجل OCR**، يزيل الضوضاء من المسح، وأخيرًا **يتعرف على النص من المسح** باستخدام مكتبة Aspose.OCR. في النهاية ستحصل على فكرة واضحة عن **كيفية استخدام OCR** في C# مع الحفاظ على شفرة مختصرة وبسيطة.

> **نصيحة محترف:** حتى دوران بسيط (5‑10°) يمكن أن يقلل من دقة OCR بنسبة 30 % أو أكثر. تصحيح الميل هو الخطوة الأولى التي لا يجب أن تتخطاها أبدًا.

---

## ما ستحتاجه

- **.NET 6+** (الكود يعمل أيضًا على .NET Framework، لكن .NET 6 هو الإصدار الحالي طويل الدعم)
- **Aspose.OCR for .NET** – يمكنك الحصول عليه من NuGet (`Install-Package Aspose.OCR`)
- عينة من ملفات TIFF/PNG/JPEG مائلة أو مشوشة (سنستخدم `noisy_rotated.tif` في المثال)
- أي بيئة تطوير تفضلها – Visual Studio، Rider، أو VS Code ستكفي

هذا كل شيء. لا مكتبات إضافية، ولا خدمات خارجية.

---

## الخطوة 1 – تحميل الصورة المصدر (لماذا هذا مهم)

قبل أن نتمكن من **تصحيح ميل الصورة**، نحتاج إلى قراءتها إلى كائن Aspose `ImageStream`. هذا الكائن يج abstracts عمليات I/O للملف ويعطي محرك OCR واجهة موحدة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the original scan – replace the path with your own file
var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");

// Quick sanity check – make sure the image loaded
if (sourceImage == null)
{
    Console.WriteLine("Failed to load the image. Check the path and file permissions.");
    return;
}
```

*لماذا التحميل أولًا؟* لأن جميع الفلاتر اللاحقة تعمل على صورة في الذاكرة. إذا تعذر قراءة الملف، سيفشل كامل خط الأنابيب.

---

## الخطوة 2 – بناء خط أنابيب المعالجة المسبقة (تصحيح الميل + إزالة الضوضاء + تحسين التباين)

عادةً ما يربط سير عمل OCR قوي عدة فلاتر معًا. هنا نُ **نعالج الصورة من أجل OCR**، والأهم من ذلك، **نوضح كيف نصحح ميل الصورة** تلقائيًا.

```csharp
// Create a pipeline that will run three filters in order
var preprocessPipeline = new PreprocessPipeline()
{
    // 1️⃣ DeskewFilter – detects rotation up to 30° and corrects it
    new DeskewFilter { MaxAngle = 30 },

    // 2️⃣ DenoiseFilter – smooths out speckles while keeping edges
    new DenoiseFilter { Strength = 0.8 },

    // 3️⃣ ContrastBoostFilter – makes faint characters pop
    new ContrastBoostFilter { Level = 1.3 }
};
```

**لماذا هذه الثلاثة؟**  
- **DeskewFilter** يحل مشكلة “كيف تصحح ميل الصورة” تلقائيًا؛ لا تحتاج لتخمين الزاوية.  
- **DenoiseFilter** يتعامل مع طلب “إزالة الضوضاء من المسح”، والذي قد يخلق حروفًا وهمية.  
- **ContrastBoostFilter** يساعد محرك OCR على تمييز النص الداكن عن الخلفية الفاتحة، وهو مشكلة شائعة عندما *تعالج الصورة من أجل OCR*.

---

## الخطوة 3 – تطبيق خط الأنابيب (رؤية التحول)

الآن نقوم فعليًا بتشغيل الفلاتر. الـ `processedImage` المرتجع هو ما سنمرره إلى محرك OCR.

```csharp
// Apply all filters – the result is a cleaned‑up bitmap
var processedImage = preprocessPipeline.Apply(sourceImage);

// Optional: Save the cleaned image for visual verification
processedImage.Save("cleaned_output.tif");
Console.WriteLine("Image preprocessing complete – cleaned_output.tif saved.");
```

إذا فتحت `cleaned_output.tif`، ستلاحظ أن النص أصبح مستقيمًا، أقل حبيبية، وبتباين أعلى. هذا الفحص البصري مفيد عندما *تزيل الضوضاء من المسح* وتريد التأكد من أن تصحيح الميل نجح.

---

## الخطوة 4 – إنشاء وتكوين محرك OCR (كيفية استخدام OCR)

مع صورة نظيفة في اليد، نقوم بإنشاء كائن `OcrEngine`. هذا هو جوهر **كيفية استخدام OCR** مع Aspose.

```csharp
// Initialize the OCR engine
var ocrEngine = new OcrEngine
{
    // Assign the pre‑processed image
    Image = processedImage,

    // Optional: Set language (English is default)
    // Language = Language.English,
    
    // Enable automatic page segmentation (helps with multi‑column scans)
    AutoPageSegmentation = true
};
```

*لماذا نضبط `AutoPageSegmentation`؟* لأن العديد من المسحات تحتوي على جداول أو أعمدة متعددة. تفعيل هذه الخاصية يسمح للمحرك بتقسيم الصفحة بذكاء، مما يحسن النتيجة النهائية لـ **التعرف على النص من المسح**.

---

## الخطوة 5 – تشغيل عملية التعرف (أخيرًا التعرف على النص)

الآن لحظة الحقيقة: نطلب من المحرك قراءة النص.

```csharp
// Kick off the OCR process
ocrEngine.Recognize();

// Retrieve the plain‑text result
string recognizedText = ocrEngine.Text;

// Show the output in the console
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

إذا سارت الأمور بسلاسة، سترى كتلة نصية نظيفة تتطابق مع المستند الأصلي. هذا هو ثمرة **تصحيح ميل الصورة**، **إزالة الضوضاء**، و**معالجة الصورة من أجل OCR** بشكل صحيح.

---

## الخطوة 6 – مثال كامل جاهز للتنفيذ (انسخه‑الصقه)

فيما يلي البرنامج الكامل، جاهز للترجمة. فقط غيّر مسار الملف وستكون جاهزًا.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");
        if (sourceImage == null)
        {
            Console.WriteLine("Unable to load image. Check the path.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Build the preprocessing pipeline
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
        {
            new DeskewFilter { MaxAngle = 30 },          // how to deskew image
            new DenoiseFilter { Strength = 0.8 },       // remove noise from scan
            new ContrastBoostFilter { Level = 1.3 }      // improves OCR accuracy
        };

        // -------------------------------------------------
        // 3️⃣ Apply the pipeline
        // -------------------------------------------------
        var processedImage = preprocessPipeline.Apply(sourceImage);
        processedImage.Save("cleaned_output.tif");
        Console.WriteLine("Preprocessing finished – cleaned_output.tif saved.");

        // -------------------------------------------------
        // 4️⃣ Configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Image = processedImage,
            AutoPageSegmentation = true   // how to use OCR effectively
        };

        // -------------------------------------------------
        // 5️⃣ Recognize text from scan
        // -------------------------------------------------
        ocrEngine.Recognize();
        string result = ocrEngine.Text;

        Console.WriteLine("\n=== Recognized Text ===");
        Console.WriteLine(result);
    }
}
```

**الناتج المتوقع** (مقتطع للختصر):

```
=== Recognized Text ===
This is a sample scanned document.
It contains several lines of text,
and the OCR engine has correctly read them.
```

إذا بدا الناتج مشوشًا، تحقق مرة أخرى أن الصورة المصدر ليست مائلة بأكثر من 30°، أو زد قيمة `DeskewFilter.MaxAngle`.

---

## الأسئلة المتكررة (حالات حافة وتنوعات)

| السؤال | الجواب |
|----------|--------|
| **ماذا لو كان مسحي مائلًا بزاوية 45°؟** | `DeskewFilter` يحد الزاوية بـ `MaxAngle`. قم بزيادة القيمة (مثلاً `MaxAngle = 60`) أو قم بــ pre‑rotate الصورة باستخدام مكتبة رسومية قبل تمريرها إلى خط الأنابيب. |
| **هل يمكنني معالجة ملفات PDF صفحة‑بصفحة؟** | نعم. حوّل كل صفحة PDF إلى صورة (مثلاً باستخدام `Aspose.Pdf`) وشغّل نفس خط الأنابيب على كل bitmap. |
| **مستندي بالفرنسية – هل يجب أن أغير شيئًا؟** | اضبط `ocrEngine.Language = Language.French;` أو حمّل حزمة لغة مخصصة. بقية خط الأنابيب يبقى كما هو. |
| **هل هناك طريقة للحفاظ على الدقة الأصلية؟** | `PreprocessPipeline` يعمل على الـ bitmap الأصلي، محافظًا على DPI. تجنّب استدعاء `ImageStream.Resize` إلا إذا كنت بحاجة لتقليل الحجم لأداء أفضل. |
| **كيف يؤثر تحسين التباين على المسحات الملونة؟** | `ContrastBoostFilter` يعمل على كل قناة؛ وهو آمن للصور الرمادية أو الملونة، لكن يمكنك أيضًا تحويلها إلى رمادية أولًا باستخدام `new GrayscaleFilter()`. |

---

## مثال صورة (مساعدة بصرية)

![مثال على كيفية تصحيح ميل الصورة](/images/deskew-example.png)

*الصورة تُظهر قبل/بعد مسح مائل 12° ومشوش تم تصحيح ميله وتنظيفه.*

---

## الخلاصة

لقد غطينا **كيفية تصحيح ميل الصورة** باستخدام Aspose.OCR، وعرضنا خط أنابيب كامل **معالجة الصورة من أجل OCR**، وأظهرنا كيفية **إزالة الضوضاء من المسح**، وأخيرًا **التعرف على النص من المسح** ببضع أسطر من C#. من خلال ربط `DeskewFilter` و`DenoiseFilter` و`ContrastBoostFilter` ستحصل على bitmap نظيف يسمح لمحرك OCR بأداء مهمته دون التعرض للعيوب.  

ما الخطوات التالية؟ جرّب تعديل قوة الفلاتر، أضف `BinarizationFilter` للحصول على مخرجات بالأبيض والأسود النقي، أو مرّر الصورة المنقاة إلى خط أنابيب NLP لاحق. النمط نفسه يعمل على الإيصالات، وجوازات السفر، والوثائق التاريخية على حد سواء.

هل لديك المزيد من الأسئلة حول **كيفية استخدام OCR** بلغات أو أطر عمل أخرى؟ اترك تعليقًا، ونتمنى لك برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}