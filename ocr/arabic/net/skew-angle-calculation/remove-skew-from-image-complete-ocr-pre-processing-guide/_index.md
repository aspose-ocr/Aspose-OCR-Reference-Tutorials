---
category: general
date: 2026-02-14
description: تعلم كيفية إزالة الانحراف من الصورة، ومعالجة الصورة مسبقًا للتعرف الضوئي
  على الأحرف، وتقليل الضوضاء في الصورة، واستخراج النص من الصورة باستخدام Aspose OCR
  في C#.
draft: false
keywords:
- remove skew from image
- preprocess image for ocr
- reduce noise in image
- extract text from image
- recognize text from document
language: ar
og_description: إزالة الانحراف من الصورة، معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف
  واستخراج النص من الصورة من خلال دليل خطوة‑بخطوة بلغة C# باستخدام Aspose OCR.
og_title: إزالة الميل من الصورة – دليل شامل لمعالجة ما قبل التعرف الضوئي على الأحرف
tags:
- OCR
- CSharp
- ImageProcessing
title: إزالة الانحراف من الصورة – دليل شامل لمعالجة ما قبل التعرف الضوئي على الأحرف
url: /ar/net/skew-angle-calculation/remove-skew-from-image-complete-ocr-pre-processing-guide/
---

>}}

Make sure to keep them unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إزالة الانحراف من الصورة – دليل شامل لمعالجة ما قبل OCR

هل احتجت يومًا إلى **إزالة الانحراف من الصورة** قبل تمريرها إلى محرك OCR؟ لست الوحيد—فالمستندات الممسوحة ضوئيًا، وصور الإيصالات، أو لقطات الشاشة غالبًا ما تكون مائلة، وهذا الزاوية الصغيرة يمكن أن تعيق التعرف على النص.  

الأخبار السارة؟ باستخدام مجموعة قليلة من فلاتر Aspose OCR يمكنك تسوية الصورة، إزالة الضوضاء، تعزيز التباين، ثم **استخراج النص من الصورة** في خط أنابيب واحد سلس. في هذا الدليل سنستعرض العملية بالكامل، من تحميل صورة مائلة إلى **التعرف على النص من المستند** وطباعة النتيجة.

---

## ما ستقوم ببنائه

بنهاية هذا البرنامج التعليمي ستحصل على تطبيق وحدة تحكم C# جاهز للتشغيل يقوم بـ:

1. **إزالة الانحراف من الصورة** باستخدام `DeskewFilter`.
2. **تقليل الضوضاء في الصورة** باستخدام `DenoiseFilter`.
3. **معالجة الصورة مسبقًا لـ OCR** عن طريق تعزيز التباين.
4. **التعرف على النص من المستند** عبر `Engine` الخاص بـ Aspose OCR.
5. **استخراج النص من الصورة** وعرضه على وحدة التحكم.

بدون خدمات خارجية، فقط حزمة Aspose OCR NuGet وقليل من الأسطر البرمجية.

---

## المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضًا).  
- Visual Studio 2022 أو أي محرر تفضله.  
- Aspose.OCR لـ .NET مثبت (`dotnet add package Aspose.OCR`).  
- صورة نموذجية (`skewed_noisy.jpg`) موجودة في مجلد يمكنك الإشارة إليه.

إذا كان لديك كل ذلك، لنبدأ.

---

## الخطوة 1: تحميل الصورة المصدر

أول شيء نحتاجه هو `ImageStream` يشير إلى الملف الذي نريد تنظيفه.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the source image that needs cleaning
ImageStream sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **لماذا هذا مهم:** `ImageStream` يُجرد البت ماب الأساسي، مما يسمح للفلاتر في Aspose بالعمل دون الحاجة لإدارة بيانات البكسل الخام.

---

## الخطوة 2: بناء خط أنابيب المعالجة المسبقة (إزالة الانحراف وتقليل الضوضاء)

بدلاً من استدعاء كل فلتر على حدة، تتيح لك Aspose ربطهم في `ImageProcessingPipeline`. هذا يبقي الكود منظمًا ويضمن تنفيذ العمليات بالترتيب الصحيح.

```csharp
// Create a pipeline and add desired filters
var processingPipeline = new ImageProcessingPipeline()
    .AddFilter(new DeskewFilter())                     // Remove skew
    .AddFilter(new DenoiseFilter())                    // Reduce noise
    .AddFilter(new ContrastBoostFilter { Level = 30 });// Boost contrast (0‑100)
```

### لماذا الترتيب مهم

1. **Deskew أولاً** – تسوية الصورة قبل إزالة الضوضاء يمنع مرشح الضوضاء من اعتبار الحواف المائلة كعناصر غير مرغوب فيها.  
2. **Denoise ثانيًا** – بمجرد أن تكون الصورة مستوية، يمكن للخوارزمية التمييز بشكل أفضل بين الإشارة والحبوب.  
3. **Contrast boost أخيرًا** – تحسين التباين بعد أن تكون الصورة نظيفة يزيد من قابلية قراءة OCR دون تضخيم الضوضاء.

---

## الخطوة 3: تطبيق خط الأنابيب والحصول على صورة مُنظفة

الآن نقوم بتشغيل خط الأنابيب على الـ stream الأصلي.

```csharp
// Apply the pipeline to obtain a cleaned image
ImageStream cleanedImage = processingPipeline.Apply(sourceImage);
```

في هذه المرحلة تكون الصورة مُسطحة، خالية من الضوضاء، وتتمتع بتباين أعلى—مثالية لـ OCR.

---

## الخطوة 4: تهيئة محرك OCR والتعرف على النص

مع صورة نقية في المتناول يمكننا أخيرًا تمريرها إلى Aspose OCR.

```csharp
// Initialise the OCR engine
Engine ocrEngine = new Engine();

// Recognise text from the cleaned image
OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);
```

> **نصيحة:** إذا كنت بحاجة إلى ضبط خاص باللغة، فإن `Engine` يقبل خاصية `Language` (مثال: `ocrEngine.Language = Language.English;`). بالنسبة لمعظم المستندات اللاتينية الإعداد الافتراضي يكفي.

---

## الخطوة 5: عرض النص المستخرج

سطر `Console.WriteLine` بسيط يُظهر النتيجة.

```csharp
// Output the extracted text
Console.WriteLine(ocrResult.Text);
```

عند تشغيل البرنامج يجب أن ترى محتوى `skewed_noisy.jpg` النصي مطبوعًا في الطرفية—نظيفًا، واضحًا، وجاهزًا للمعالجة اللاحقة.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل جاهز للنسخ واللصق. احفظه باسم `Program.cs`، استبدل `YOUR_DIRECTORY` بالمسار الفعلي، ثم نفّذ `dotnet run`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the source image that needs cleaning
            ImageStream sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

            // Step 2: Create an image‑processing pipeline and add desired filters
            var processingPipeline = new ImageProcessingPipeline()
                .AddFilter(new DeskewFilter())                     // Remove skew
                .AddFilter(new DenoiseFilter())                    // Reduce noise
                .AddFilter(new ContrastBoostFilter { Level = 30 });// Boost contrast (0‑100)

            // Step 3: Apply the pipeline to obtain a cleaned image
            ImageStream cleanedImage = processingPipeline.Apply(sourceImage);

            // Step 4: Initialise the OCR engine and recognize text from the cleaned image
            Engine ocrEngine = new Engine();
            OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);

            // Step 5: Display the extracted text
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**الإخراج المتوقع** (مثال لإيصال بسيط):

```
=== Extracted Text ===
Store: Coffee Corner
Date: 02/12/2026
Item          Qty   Price
Latte          2    $5.80
Croissant      1    $2.50
Total                $8.30
```

إذا كان الإخراج مشوشًا، تحقق من صحة مسار الصورة وتأكد من أن الملف المصدر يحتوي فعلاً على نص قابل للقراءة.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو كانت الصورة مدورة 90° بدلاً من انحراف طفيف؟

`DeskewFilter` يتعامل مع الزوايا الصغيرة (±15°). للدوارات الكاملة، استدعِ `new RotateFilter { Angle = 90 }` قبل خطوة الـ deskew.

### صوري بصيغة PNG—هل يتغير شيء؟

لا. `ImageStream.FromFile` يكتشف الصيغة تلقائيًا، لذا PNG، JPEG، BMP أو TIFF تعمل بنفس الطريقة.

### كيف يمكنني تعديل قوة تقليل الضوضاء؟

`DenoiseFilter` يتيح خاصية `Strength` (0‑100). القيم الأعلى تزيل المزيد من الحبوب لكن قد تمحو التفاصيل الدقيقة. جرّب القيم بين 30‑50 للمستندات النصية الكثيفة.

### أحتاج إلى معالجة دفعة من الملفات—هل يمكن إعادة استخدام خط الأنابيب؟

بالتأكيد. أنشئ `processingPipeline` مرة واحدة، ثم كرّر عبر كل ملف:

```csharp
foreach (var path in Directory.GetFiles("batch_folder", "*.jpg"))
{
    var src = ImageStream.FromFile(path);
    var cleaned = processingPipeline.Apply(src);
    var result = ocrEngine.Recognize(cleaned);
    // Save or log result.Text
}
```

إعادة استخدام نفس كائن `Engine` أيضًا يحسن الأداء.

---

## نصائح احترافية لـ OCR جاهز للإنتاج

- **Cache the pipeline**: إنشاء الفلاتر بشكل متكرر قد يكون مكلفًا في سيناريوهات عالية الإنتاجية.  
- **Set OCR language**: `ocrEngine.Language = Language.Spanish;` للمستندات غير الإنجليزية.  
- **Handle empty results**: تحقق دائمًا من `ocrResult.Text?.Length > 0` قبل المتابعة.  
- **Log intermediate images**: حفظ `cleanedImage` إلى القرص (`cleanedImage.Save("debug.png");`) يساعدك على ضبط معلمات الفلتر بدقة.

---

## الخلاصة

أظهرنا كيف **نزيل الانحراف من الصورة**، **نقلل الضوضاء في الصورة**، و**نُعِدّ الصورة للـ OCR** باستخدام خط أنابيب الفلاتر القوي في Aspose OCR، ثم **نتعرف على النص من المستند** وأخيرًا **نستخرج النص من الصورة**. كامل سير العمل لا يتجاوز 50 سطرًا من C# ويسهل توسيعه لمعالجة دفعات، نماذج لغوية مخصصة، أو فلاتر إضافية.

هل أنت مستعد للخطوة التالية؟ جرّب إضافة `BinarizeFilter` للحصول على مخرجات أبيض‑أسود، أو جرب مستويات مختلفة من `ContrastBoostFilter` لترى كيف تؤثر على دقة التعرف. كلما لعبت أكثر مع خط الأنابيب، كلما فهمت أفضل كيف يساهم كل فلتر في الحصول على نتيجة OCR نظيفة.

برمجة سعيدة، ولتظل صورك دائمًا مستقيمة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}