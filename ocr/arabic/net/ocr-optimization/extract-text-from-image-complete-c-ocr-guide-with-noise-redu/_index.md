---
category: general
date: 2026-02-25
description: استخراج النص من الصورة باستخدام Aspose OCR. تعلم كيفية تحميل الصورة للتعرف
  الضوئي على الأحرف، وتطبيق تقليل الضوضاء، وتحسين دقة التعرف الضوئي على الأحرف من
  خلال المعالجة المسبقة.
draft: false
keywords:
- extract text from image
- apply noise reduction
- improve ocr accuracy
- load image for ocr
- preprocess ocr image
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR. يوضح هذا الدليل كيفية
  تحميل الصورة للتعرف الضوئي على الأحرف، وتطبيق تقليل الضوضاء، وتحسين دقة التعرف الضوئي
  على الأحرف عبر المعالجة المسبقة.
og_title: استخراج النص من الصورة – دليل OCR كامل بلغة C#
tags:
- OCR
- C#
- Aspose
title: استخراج النص من الصورة – دليل كامل لتقنية OCR بلغة C# مع تقليل الضوضاء
url: /ar/net/ocr-optimization/extract-text-from-image-complete-c-ocr-guide-with-noise-redu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة – دليل OCR كامل بلغة C#

هل احتجت يومًا إلى **استخراج النص من الصورة** لكن النتائج كانت مليئة بالأخطاء؟ ربما كانت الصورة مهتزة قليلاً، الخلفية صاخبة، أو النص مائلًا قليلًا. في تجربتي، تلك العيوب الصغيرة هي أكبر المذنبين وراء نتائج OCR الضعيفة. الخبر السار؟ مع بضع خطوات معالجة مسبقة—مثل تطبيق تقليل الضوضاء وتصحيح الميل—يمكنك تحسين **دقة OCR** بشكل كبير دون تعديل سطر واحد من كود التعرف.

في هذا الدرس سنستعرض مثالًا واقعيًا يوضح كيفية **تحميل الصورة لـ OCR**، ربط خط أنابيب **معالجة مسبقة لصورة OCR**، وأخيرًا استخراج نص نظيف باستخدام Aspose.OCR لـ .NET. بنهاية الدرس ستحصل على تطبيق C# Console جاهز للتنفيذ يتعامل مع الصور الض noisy، المائلة كالمحترفين.

## ما ستتعلمه

- كيفية تثبيت وإشارة إلى مكتبة Aspose.OCR.
- الكود الدقيق اللازم لـ **تحميل الصورة لـ OCR** من القرص.
- كيفية **تطبيق تقليل الضوضاء**، والحد العتبي التكيفي، وتصحيح الميل في مرشح واحد سلس.
- لماذا كل خطوة معالجة مسبقة مهمة لـ **تحسين دقة OCR**.
- الناتج المتوقع في وحدة التحكم وطريقة سريعة للتحقق من النتيجة.

> **نصيحة:** إذا كنت جديدًا على Aspose، فإن المكتبة تعمل مع .NET 6+، .NET Framework 4.6+، وحتى .NET Core. لا توجد تبعيات أصلية إضافية—فقط حزمة NuGet.

---

## المتطلبات المسبقة

| المتطلب | لماذا هو مهم |
|-------------|----------------|
| .NET 6 SDK (أو أحدث) | ميزات لغة حديثة وأداء أفضل. |
| Visual Studio 2022 (أو VS Code) | تصحيح سهل وIntelliSense مريح. |
| حزمة NuGet Aspose.OCR لـ .NET | توفر `OcrEngine`، `PreprocessFilter`، والأنواع المرتبطة. |
| صورة عينة (`noisy_skewed.jpg`) | توضح تأثير المعالجة المسبقة. |

إذا كان لديك مشروع بالفعل، فقط نفّذ الأمر `dotnet add package Aspose.OCR` لجلب المكتبة.

---

## الخطوة 1 – إنشاء مشروع وحدة تحكم جديد

أولًا، أنشئ تطبيق وحدة تحكم جديد لتبقى الأمثلة منظمة.

```bash
dotnet new console -n AsposeOcrDemo
cd AsposeOcrDemo
dotnet add package Aspose.OCR
```

هذا الأمر ينشئ ملف `Program.cs` ويضيف حزمة OCR. افتح المشروع في محرّكك المفضّل؛ سنستبدل طريقة `Main` المُولدة تلقائيًا بنسخة أكثر وصفًا.

---

## الخطوة 2 – تحميل الصورة لـ OCR

قبل أن يبدأ أي تعرّف، يحتاج المحرك إلى تدفق صورة. طريقة `ImageStream.FromFile` تتعامل مع معظم الصيغ الشائعة (JPG، PNG، BMP). لنغلفها في كتلة `using` حتى يتم تحرير مقبض الملف تلقائيًا.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 👉 Step 2: Load the raw image we want to process.
        // Replace the path with the location of your own test picture.
        ImageStream rawImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_skewed.jpg");

        // The rest of the pipeline follows…
        RunOcrPipeline(rawImage);
    }

    static void RunOcrPipeline(ImageStream rawImage)
    {
        // Placeholder – we’ll fill this in next.
    }
}
```

> **لماذا هو مهم:** تحميل الصورة بشكل صحيح هو الأساس. إذا كان مسار الملف خاطئًا، سيطرح المحرك استثناء `FileNotFoundException` ولن تصل أبدًا إلى مرحلة المعالجة المسبقة.

---

## الخطوة 3 – بناء مرشح معالجة مسبقة (تطبيق تقليل الضوضاء + المزيد)

الآن يأتي السحر. مرشح **معالجة مسبقة لصورة OCR** يتيح لك ربط عمليات متعددة بأسلوب سلس. إليك لماذا كل خطوة أساسية:

1. **Adaptive Threshold** – يحول الصورة إلى أبيض وأسود بناءً على التباين المحلي، مما يساعد محرك OCR على تمييز الأحرف عن الخلفية.
2. **Deskew** – يكتشف ويصحح أي دوران، مما يضمن أن خطوط النص أفقية. النص المائل غالبًا ما يؤدي إلى فقدان الأحرف.
3. **Noise Reduction** – يزيل البقع، الغبار، أو عيوب الضغط التي تظهر كبيكسلات عشوائية.

```csharp
static void RunOcrPipeline(ImageStream rawImage)
{
    // 👉 Step 3: Build a preprocessing filter that applies three operations.
    PreprocessFilter preprocessFilter = new PreprocessFilter()
        .ApplyAdaptiveThreshold()   // Enhance contrast for better binarization
        .ApplyDeskew()              // Correct any rotation in the image
        .ApplyNoiseReduction();     // Remove speckles and background noise

    // Execute the filter and get a cleaned image stream.
    ImageStream cleanedImage = preprocessFilter.Execute(rawImage);

    // Pass the cleaned image to the OCR engine.
    PerformRecognition(cleanedImage);
}
```

> **نصيحة احترافية:** يمكنك إعادة ترتيب الاستدعاءات، لكن الترتيب أعلاه (threshold → deskew → noise reduction) هو الأكثر فعالية عادةً لأنه يفصل أولاً المقدمة عن الخلفية، ثم يضبط النص، وأخيرًا ينظف أي بقايا.

---

## الخطوة 4 – تشغيل OCR وعرض النص المعترف به

مع صورة معالجة مسبقًا في المتناول، يقوم `OcrEngine` بالعمل الشاق. يختار المحرك تلقائيًا نموذج اللغة المناسب (الإنجليزية افتراضيًا) ما لم تحدد غير ذلك.

```csharp
static void PerformRecognition(ImageStream image)
{
    // 👉 Step 4: Create the OCR engine and assign the cleaned image.
    OcrEngine ocrEngine = new OcrEngine
    {
        Image = image
    };

    // Run the recognition process.
    OcrResult result = ocrEngine.Recognize();

    // Output the extracted text to the console.
    Console.WriteLine("=== Extracted Text ===");
    Console.WriteLine(result.Text);
}
```

عند تشغيل البرنامج (`dotnet run`)، يجب أن ترى شيئًا مثل:

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

إذا كانت الصورة الأصلية صاخبة، ستلاحظ عددًا أقل بكثير من الأحرف العشوائية مقارنةً بتشغيل OCR على الملف الخام.

---

## الخطوة 5 – مثال كامل قابل للتنفيذ

بدمج جميع القطع معًا، إليك **الكود الكامل** الذي يمكنك نسخه ولصقه في `Program.cs`. لا قطع مفقودة، ولا تبعيات مخفية.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Load the image you want to OCR.
        ImageStream rawImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_skewed.jpg");

        // Build and execute the preprocessing pipeline.
        PreprocessFilter preprocessFilter = new PreprocessFilter()
            .ApplyAdaptiveThreshold()
            .ApplyDeskew()
            .ApplyNoiseReduction();

        ImageStream cleanedImage = preprocessFilter.Execute(rawImage);

        // Run OCR on the cleaned image.
        OcrEngine ocrEngine = new OcrEngine
        {
            Image = cleanedImage
        };

        OcrResult result = ocrEngine.Recognize();

        // Show the extracted text.
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(result.Text);
    }
}
```

### النتيجة المتوقعة

إذا كانت الصورة المصدر تحتوي على الجملة *“The quick brown fox jumps over the lazy dog.”* فستظهر بالضبط تلك السطر مطبوعًا، دون رموز عشوائية أو أحرف مفقودة. هذا هو دليل **تحسين دقة OCR** بعد تطبيق تقليل الضوضاء وتصحيح الميل.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو كانت صورتي بصيغة مختلفة (مثلاً PNG)؟

`ImageStream.FromFile` يكتشف نوع الملف تلقائيًا، لذا يمكنك الإشارة إلى `.png` أو `.bmp` دون أي تغييرات في الكود.

### كيف أتعامل مع ملفات PDF متعددة الصفحات؟

يمكن لـ Aspose.OCR معالجة كل صفحة على حدة. قم بالتكرار عبر `PdfDocument.Pages`، حوّل كل صفحة إلى تدفق صورة، ثم مرّرها إلى نفس خط أنابيب المعالجة المسبقة.

### هل يمكنني تغيير نموذج اللغة؟

نعم. عيّن `ocrEngine.Language = OcrLanguage.Spanish;` (أو أي لغة مدعومة) قبل استدعاء `Recognize()`.

### ماذا لو كانت الصورة نظيفة بالفعل؟

يمكنك تخطي الخطوات التي لا تحتاجها. بالنسبة لوثيقة ممسوحة ضوئيًا بشكل مثالي، فقط استدعِ `ApplyAdaptiveThreshold()` أو حتى احذف الفلتر بالكامل—سيعمل OCR، رغم أنك قد تفقد بعض التحسينات الطفيفة.

---

## نصائح احترافية لـ OCR جاهز للإنتاج

- **معالجة دفعات:** غلف خط الأنابيب في `Parallel.ForEach` عند معالجة عشرات الصور للاستفادة من معالجات متعددة النوى.
- **إدارة الذاكرة:** حرّر كائنات `ImageStream` بعد الاستخدام (`rawImage.Dispose();`) لتحرير الموارد الأصلية بسرعة.
- **التسجيل:** احصل على `ocrResult.Text` مع اسم الملف الأصلي لتتبع المراجعة.
- **معالجة الأخطاء:** احطّ التدفق بالكامل بـ `try/catch` وسجّل تفاصيل `OcrException`؛ غالبًا ما تحتوي على تلميحات حول صيغ الصور غير المدعومة.

---

## الخلاصة

لقد **استخدمنا استخراج النص من الصورة** باستخدام Aspose.OCR، وأظهرنا كيفية **تحميل الصورة لـ OCR**، وأوضحنا لماذا **تطبيق تقليل الضوضاء** (بالإضافة إلى الحد العتبي وتصحيح الميل) هو السر وراء **تحسين دقة OCR**. الحل الكامل يندمج في ملف C# واحد سهل القراءة، ويمكنك إدراجه في أي مشروع .NET غدًا.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال اللغة، جرب فلاتر مخصصة، أو عالج دفعة من الفواتير الممسوحة عبر نفس الخط الأنابيب. المفاهيم التي تعلمتها—المعالجة المسبقة، تدفقات الصور النظيفة، ومعالجة الأخطاء القوية—تنطبق على جميع سيناريوهات OCR.

هل لديك أسئلة أو لاحظت حالة خاصة غريبة؟ اترك تعليقًا أدناه؛ يسعدني مساعدتك في تحسين سير العمل. ترميز سعيد، ولتكن OCR دائمًا واضحة كالكريستال!

![مخطط يوضح خط أنابيب معالجة OCR مسبقًا – استخراج النص من الصورة بعد تقليل الضوضاء، والحد العتبي التكيفي، وتصحيح الميل](extract-text-from-image-ocr-pipeline.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}