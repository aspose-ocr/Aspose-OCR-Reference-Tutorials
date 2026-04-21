---
category: general
date: 2026-03-04
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلّم كيفية تحميل الصورة
  للتعرف الضوئي على الأحرف (OCR) والتعرف على النص من ملفات TIFF بكفاءة.
draft: false
keywords:
- extract text from image
- load image for ocr
- recognize text from tiff
- Aspose OCR C#
- GPU OCR engine
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR في C#. يوضح هذا الدليل
  كيفية تحميل الصورة للتعرف الضوئي على الأحرف (OCR) والتعرف على النص من ملفات TIFF
  باستخدام محرك GPU.
og_title: استخراج النص من الصورة باستخدام Aspose OCR – دليل C#
tags:
- OCR
- C#
- Aspose
- GPU
title: استخراج النص من الصورة باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة باستخدام Aspose OCR – دليل C# كامل

هل احتجت يوماً إلى **استخراج النص من الصورة** لكنك لم تكن متأكدًا أي مكتبة ستوفر لك السرعة والدقة معًا؟ لست وحدك—فالكثير من المطورين يواجهون هذه المشكلة عند التعامل مع ملفات PDF الممسوحة أو أرشيفات TIFF. الخبر السار هو أن Aspose OCR، مع محرك مدعوم بالـ GPU، يجعل العملية بأكملها تبدو سهلة.

في هذا الدرس سنوضح لك بالضبط كيف **تحمّل الصورة لـ OCR**، وكيفية إعداد محرك GPU، وأخيرًا **التعرف على النص من ملفات TIFF** في بضع أسطر فقط. في النهاية ستحصل على تطبيق Console قابل للتنفيذ يطبع النص المستخرج على الشاشة، وستفهم “السبب” وراء كل خطوة.

## ما ستتعلمه

- كيفية تثبيت وإضافة مرجع حزمة NuGet الخاصة بـ Aspose.OCR.  
- لماذا يمكن لـ `GpuOcrEngine` المدعوم بالـ GPU أن يقلل بشكل كبير من زمن المعالجة.  
- الطريقة الصحيحة **لتحميل الصورة لـ OCR** باستخدام `ImageInfo`.  
- كيفية ضبط إعدادات اللغة وحدود الذاكرة.  
- كيف **تتعرف على النص من TIFF** وتتعامل مع المشكلات الشائعة.

لا تحتاج إلى خبرة سابقة مع Aspose؛ معرفة أساسية بـ C# و .NET كافية. لنبدأ.

---

## الخطوة 1: استخراج النص من الصورة – تهيئة محرك OCR على الـ GPU

أول ما نحتاجه هو محرك OCR يستطيع فعلاً قراءة البكسلات. تقدم Aspose محرك `GpuOcrEngine` الذي يوزع الحمل الثقيل على بطاقة الرسوميات الخاصة بك. هذا مفيد بشكل خاص عندما يكون لديك العشرات من ملفات TIFF عالية الدقة في قائمة الانتظار.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Create a GPU‑enabled OCR engine.
// Setting GpuMemoryLimit helps avoid out‑of‑memory crashes on modest GPUs.
GpuOcrEngine ocrEngine = new GpuOcrEngine
{
    GpuMemoryLimit = 1024 // limit to 1024 MB
};
```

**لماذا هذا مهم:**  
محرك يعمل على الـ CPU فقط سيقوم بمسح كل بكسل بالتتابع، ما قد يكون بطيئًا جدًا للصور الكبيرة. من خلال تحديد حد لذاكرة الـ GPU، تحافظ على خفة العملية مع الاستفادة من تحسين الأداء.

> **نصيحة احترافية:** إذا كنت تعمل على خادم بدون GPU، استخدم `OcrEngine` بدلاً منه—واجهة البرمجة (API) هي نفسها، فقط غير اسم الفئة.

---

## الخطوة 2: تحميل الصورة لـ OCR – تحضير ملف TIFF

الآن بعد أن أصبح المحرك جاهزًا، علينا **تحميل الصورة لـ OCR**. طريقة `ImageInfo.Load` من Aspose تدعم مجموعة واسعة من الصيغ، بما فيها ملفات TIFF متعددة الصفحات. وجهها إلى ملفك ودع المكتبة تتولى الباقي.

```csharp
// Replace the path with the location of your TIFF file.
string imagePath = @"YOUR_DIRECTORY/english_page.tif";

// Load the image into an ImageInfo object.
// ImageInfo abstracts away format specifics, giving you a uniform API.
ImageInfo image = ImageInfo.Load(imagePath);
```

**حالة حافة:**  
إذا كان ملف TIFF يحتوي على عدة صفحات، يمكنك التجول عبر `image.Pages` ومعالجة كل صفحة على حدة. بالنسبة لمعظم المسحات ذات الصفحة الواحدة، السطر أعلاه يكفي.

---

## الخطوة 3: التعرف على النص من TIFF – تنفيذ OCR

مع الصورة في الذاكرة والمحرك مهيأ، نصل أخيرًا إلى **التعرف على النص من TIFF**. تُعيد طريقة `Recognize` كائن `OcrResult` يحتوي على السلسلة المستخرجة، درجات الثقة، وحتى إطارات الحدود إذا احتجت إليها لاحقًا.

```csharp
// Set the language you expect in the image.
// English is the default, but you can combine languages like Language.English | Language.Spanish.
ocrEngine.Language = Language.English;

// Run the OCR process.
OcrResult ocrResult = ocrEngine.Recognize(image);
```

**لماذا اللغة مهمة:**  
تحديد اللغة الصحيحة يحسن الدقة بشكل كبير لأن المحرك يستطيع تطبيق القواميس والنماذج الخاصة بتلك اللغة.

---

## الخطوة 4: إخراج النص المستخرج

الخطوة الأخيرة بسيطة—اكتب النتيجة إلى الـ console أو ملف أو قاعدة بيانات. هنا سنبقيها بسيطة ونعرض النص على الشاشة.

```csharp
// Print the recognized text.
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrResult.Text);
```

**الناتج المتوقع:**  
إذا كان `english_page.tif` يحتوي على فقرة مطبوعة، سترى شيئًا مثل:

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

إذا واجه الـ OCR صعوبة، قد يحتوي النص على أحرف غريبة؛ تعديل `GpuMemoryLimit` أو توفير صورة مصدر ذات دقة أعلى عادةً ما يساعد.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل المستقل الذي يمكنك نسخه ولصقه في مشروع Console App جديد. يُجمع مع .NET 6 أو أحدث.

```csharp
// ------------------------------------------------------------
// Complete C# program to extract text from image using Aspose OCR.
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize GPU OCR engine with a memory cap.
        GpuOcrEngine ocrEngine = new GpuOcrEngine
        {
            GpuMemoryLimit = 1024 // MB
        };

        // 2️⃣ Choose the language for recognition.
        ocrEngine.Language = Language.English;

        // 3️⃣ Load the image you want to process.
        // Make sure the path points to a valid TIFF file.
        string imagePath = @"YOUR_DIRECTORY/english_page.tif";
        ImageInfo image = ImageInfo.Load(imagePath);

        // 4️⃣ Perform OCR – this returns the recognized text.
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Display the result.
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);

        // Keep the console window open when debugging.
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

احفظ الملف، شغّل `dotnet run`، وسترى الـ console يطبع المحتوى المستخرج. بسيط، أليس كذلك؟

---

## أسئلة شائعة وحالات حافة

**ماذا لو كانت صورتي PNG أو JPEG بدلاً من TIFF؟**  
`ImageInfo.Load` تعمل مع أي صيغة نقطية تقريبًا، لذا يمكنك تغيير الامتداد ويبقى باقي الكود كما هو. لا تحتاج إلى أي تغييرات إضافية.

**الـ OCR يعطيني أحرف مشوهة—ما الذي يجب أن أتحقق منه؟**  
1. تأكد من دقة الصورة (300 dpi أو أعلى هي المثالية).  
2. تأكد من ضبط `Language` الصحيح؛ اللغة غير المتطابقة تقلل من دعم القاموس.  
3. زد `GpuMemoryLimit` إذا كانت الصورة كبيرة جدًا؛ قد يكون المحرك يحد من نفسه.

**هل يمكنني معالجة ملفات متعددة دفعة واحدة؟**  
بالتأكيد. ضع خطوات التحميل والتعرف داخل حلقة `foreach (var file in Directory.GetFiles(...))`. تذكر تحرير كل `ImageInfo` إذا كنت تعالج مئات الملفات لتحرير الموارد الأصلية.

**هل أحتاج إلى GPU لتشغيل هذا الكود؟**  
لا. إذا لم يتوفر GPU متوافق، استبدل `GpuOcrEngine` بـ `OcrEngine` العادي. استدعاءات الـ API (`Recognize`, `Language`, إلخ) تبقى دون تغيير.

---

## نصائح الأداء – الحصول على أقصى استفادة من GPU OCR

- **إعادة استخدام المحرك:** إنشاء `GpuOcrEngine` جديد لكل صورة يضيف عبئًا. أنشئه مرة واحدة وأعد استخدامه عبر العديد من الملفات.  
- **المعالجة الدفعية:** حمّل عدة صور في الذاكرة، ثم استدعِ `Recognize` بشكل متسلسل؛ سيبقى الـ GPU "دافئًا" ويعالج أسرع.  
- **ضبط حد الذاكرة:** على الأجهزة التي تمتلك 4 GB VRAM، حد 1024 MB آمن. على الأجهزة المتقدمة يمكنك رفعه إلى 4096 MB للدفعات الأكبر.

---

## الخلاصة

لقد تعلمت الآن كيفية **استخراج النص من الصورة** باستخدام محرك GPU الخاص بـ Aspose OCR، وكيفية **تحميل الصورة لـ OCR** بشكل صحيح، وكيفية **التعرف على النص من TIFF** في تطبيق Console C# نظيف وجاهز للإنتاج. الكود قابل للتنفيذ بالكامل، والشروحات تغطي كلًا من “كيف” و “لماذا”، ولديك الآن أساس قوي للتعامل مع سيناريوهات OCR أكثر تعقيدًا—مثل المستندات متعددة اللغات أو تدفقات الكاميرا في الوقت الفعلي.

هل أنت مستعد للتحدي التالي؟ جرّب توسيع العينة لكتابة الناتج إلى ملف CSV، أو جرب بيانات `BoundingBox` لتسليط الضوء على الكلمات المعترف بها في الصورة الأصلية. الاحتمالات لا حصر لها، وزيادة الأداء بفضل تسريع الـ GPU ستحافظ على سرعة خطوط عملك.

إذا وجدت هذا الدليل مفيدًا، أعطه نجمة على GitHub، شاركه مع زميل، أو اترك تعليقًا أدناه بنصائحك الخاصة. برمجة سعيدة!  

![extract text from image using Aspose OCR](placeholder.png){alt="استخراج النص من الصورة باستخدام Aspose OCR"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}