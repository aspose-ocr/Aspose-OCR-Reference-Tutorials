---
category: general
date: 2026-01-02
description: تشغيل OCR على PNG بسرعة باستخدام Aspose OCR ودعم GPU. تعلم كيفية التعرف
  على النص من الصورة، استخراج النص من الصورة وتحديد حد ذاكرة GPU.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: ar
og_description: تشغيل OCR على ملفات PNG بكفاءة باستخدام Aspose OCR وتسريع GPU. يوضح
  هذا الدرس كيفية التعرف على النص من الصورة، استخراج النص من الصورة والتحكم في استخدام
  ذاكرة GPU.
og_title: تشغيل OCR على PNG باستخدام GPU – دليل C# الكامل
tags:
- OCR
- C#
- GPU
title: تشغيل OCR على PNG باستخدام GPU – دليل C# الكامل
url: /ar/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل OCR على PNG باستخدام GPU – دليل C# كامل

هل احتجت يوماً إلى **تشغيل OCR على ملفات PNG** لكنك واجهت بطء الأداء؟ لست وحدك. في العديد من خطوط الأنابيب الواقعية، يمكن لملف PNG عالي الدقة أن يبطئ محرك OCR القائم على المعالج فقط، محولاً ما يجب أن يكون بحثًا سريعًا إلى انتظار يدوم دقيقة.  

الخبر السار هو أن Aspose OCR يأتي بامتدادات GPU تتيح لك **التعرف على النص من صورة** في جزء من الوقت. في هذا الدرس سنستعرض مثالًا عمليًا يوضح لك بالضبط كيفية **تشغيل OCR على PNG** باستخدام C#، وكيفية **استخراج النص من صورة**، وحتى كيفية **تحديد حد الذاكرة للـ GPU** لتبقى ضمن ميزانيتك المادية.

سنغطي أيضًا “كيف” و “لماذا” وراء كل خطوة، لتخرج بنموذج ذهني قوي—not مجرد مقتطف نسخ‑لصق.

## ما ستتعلمه

- المتطلبات المسبقة لاستخدام دعم GPU في Aspose OCR.  
- كيفية تحميل PNG إلى كائن `Bitmap` وإدخاله إلى محرك OCR.  
- كيفية تكوين `GpuDevice` و `GpuMemoryLimitMb` للحصول على أفضل أداء.  
- كيفية **التعرف على النص من صورة** واسترجاع النتيجة كنص عادي.  
- نصائح للتعامل مع الحالات الشائعة مثل بطاقات GPU ذات الذاكرة القليلة أو ملفات PNG متعددة الصفحات.  

بنهاية هذا الدليل ستتمكن من **تشغيل OCR على PNG** بسرعة GPU وستتحكم بثقة في حجم الذاكرة المستهلكة لمهام OCR الخاصة بك.

![مخطط يوضح تشغيل OCR على PNG مع تسريع GPU](run-ocr-on-png-diagram.png "مثال تشغيل OCR على PNG")

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

1. .NET 6.0 أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضًا).  
2. بطاقة NVIDIA GPU تدعم CUDA (المثال يستخدم الفهرس 0 للجهاز).  
3. حزمة NuGet `Aspose.OCR` وامتدادات GPU الخاصة بها (`Aspose.OCR.Extensions`).  
4. ملف PNG تجريبي (`input.png`) موجود في مجلد يمكنك الإشارة إليه من مشروعك.  

إذا كان أي من هذه غير مألوف لك، لا تقلق—سنذكر بدائل حيثما كان ذلك مناسبًا.

---

## الخطوة 1 – تثبيت Aspose OCR وامتدادات GPU

أولاً وقبل كل شيء. بدون المكتبات الصحيحة لن يتم تجميع باقي الكود.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

حزمة `Aspose.OCR.Extensions` تجلب ملفات CUDA الثنائية المطلوبة لتسريع GPU.  
*نصيحة احترافية:* إذا كنت على جهاز لا يحتوي على GPU، يمكنك ما زال تجميع المشروع؛ فقط اضبط `PreferGpu = false` لاحقًا.

---

## الخطوة 2 – تحميل PNG الذي تريد معالجته

الآن نقوم فعليًا **بتشغيل OCR على PNG** بتحميله إلى كائن `Bitmap`. هذه الخطوة بسيطة لكن تستحق ملاحظة سريعة: `Bitmap` يتوقع مسار ملف، لذا تأكد من أن المسار صحيح بالنسبة للملف التنفيذي.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

إذا كان حجم PNG كبيرًا بشكل غير عادي (مثلاً > 5000 بكسل على أحد الجوانب)، قد ترغب في تقليص حجمه أولاً لتجنب استنزاف ذاكرة GPU. هنا يصبح خيار **تحديد حد الذاكرة للـ GPU** مفيدًا لاحقًا.

---

## الخطوة 3 – إنشاء وتكوين محرك OCR لاستخدام GPU

هذا هو جوهر الدرس: تكوين محرك OCR **للتعرف على النص من صورة** باستخدام GPU. هناك خاصيتان أساسيتان:

- `GpuDevice` – يحدد أي جهاز CUDA يُستخدم.  
- `GpuMemoryLimitMb` – يحدد الحد الأقصى للذاكرة التي يمكن للمحرك حجزها على الـ GPU.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**لماذا نحدد حدًا للذاكرة؟** بعض بطاقات GPU تشارك الذاكرة مع الشاشة أو تشغل عدة أحمال عمل في آنٍ واحد. بتحديد الحد، تمنع حدوث تعطل بسبب نفاد الذاكرة، خاصةً عند معالجة العديد من ملفات PNG بالتوازي.

---

## الخطوة 4 – تعريف خيارات التعرف (اللغة وتفضيل GPU)

كائن `RecognitionOptions` يخبر المحرك أي لغة يبحث عنها وما إذا كان **يفضل GPU** حتى للصور الصغيرة. بالنسبة لمعظم المستندات الإنجليزية هذا كافٍ، لكن يمكنك استبدال `Language.English` بأي لغة مدعومة أخرى.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

إذا احتجت يومًا إلى **استخراج النص من صورة** بلغة غير الإنجليزية، فقط غير قيمة تعداد `Language`. المكتبة تدعم عشرات اللغات مباشرة.

---

## الخطوة 5 – تشغيل OCR واسترجاع النتيجة

بعد ربط كل شيء، الاستدعاء النهائي هو سطر واحد فقط يقوم فعليًا **بتشغيل OCR على PNG** ويعيد كائن نتيجة غني.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

كائن `OcrResult` يحتوي ليس فقط على النص العادي (`ocrResult.Text`) بل أيضًا على درجات الثقة، الصناديق المحيطة، وحتى الصورة الأصلية مع الكلمات المظللة—مفيد إذا أردت تصحيح الأخطاء أو تصور الاستخراج.

**الناتج المتوقع** (لملف PNG تجريبي يحتوي على “Hello World”):

```
=== OCR Output ===
Hello World
```

إذا ظهر النص مشوشًا، تحقق من أن PNG غير تالف وأن حد ذاكرة GPU ليس منخفضًا جدًا بالنسبة لحجم الصورة.

---

## الخطوة 6 – التعامل مع الحالات الخاصة ونصائح أفضل الممارسات

### بطاقات GPU ذات الذاكرة القليلة

إذا صادفت استثناءً مثل `CudaException: out of memory`، قلل قيمة `GpuMemoryLimitMb` أو قسّم PNG إلى بلاطات قبل المعالجة. يمكن تنفيذ التجزئة باستخدام `Graphics.DrawImage` على نسخة `Bitmap`.

### معالجة عدة PNGs دفعة واحدة

عند معالجة مجلد من PNGs، أعد استخدام نفس كائن `OcrEngine`—تهيئته مرة واحدة يوفر تبديلات سياق GPU.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### الرجوع إلى CPU

إذا لم يتوفر GPU، ما عليك سوى ضبط `PreferGpu = false`. سيعود المحرك تلقائيًا إلى CPU دون أي تعديل في الكود.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑ولصقه في مشروع وحدة تحكم جديد. يتضمن جميع الخطوات السابقة، بالإضافة إلى بعض فحوصات الأمان.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

احفظ الملف باسم `Program.cs`، شغّـل `dotnet run`، وسترى النص المستخرج يُطبع على وحدة التحكم.

---

## الخلاصة

لقد عرضنا كيف **تشغيل OCR على PNG** باستخدام امتدادات GPU في Aspose OCR، وكيف **التعرف على النص من صورة**، وكيف **استخراج النص من صورة** مع التحكم في **تحديد حد الذاكرة للـ GPU**. من خلال تكوين `GpuDevice` و `GpuMemoryLimitMb` تحافظ على تطبيقك سريعًا ومستقرًا، حتى على بطاقات GPU متوسطة.

من هنا يمكنك:

- تجربة لغات أخرى (`Language.French`, `Language.Spanish`).  
- دمج خطوة OCR في خط أنابيب معالجة مستندات أكبر.  
- إضافة معالجة لاحقة مثل التدقيق الإملائي أو استخراج الكيانات لتحسين النص الخام.  

تذكر، المفتاح ليس فقط الكود بل فهم سبب أهمية كل إعداد. عندما تعرف كيف **تحديد حد الذاكرة للـ GPU** ومتى تلجأ إلى CPU، ستبني حلول OCR قابلة للتوسع بسهولة.

هل لديك أسئلة حول حجم PNG معين، أو ملفات TIFF متعددة الصفحات، أو استكشاف أخطاء GPU؟ اترك تعليقًا أدناه، وتمنياتنا لك بالبرمجة السعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}