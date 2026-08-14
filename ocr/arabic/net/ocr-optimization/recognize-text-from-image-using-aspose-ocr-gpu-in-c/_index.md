---
category: general
date: 2026-02-20
description: تعرّف على النص من الصورة بسرعة باستخدام تسريع GPU في Aspose OCR. تعلّم
  كيفية استخراج النص من المسح الضوئي في C# مع مثال كامل قابل للتنفيذ.
draft: false
keywords:
- recognize text from image
- extract text from scan
- Aspose OCR GPU
- C# OCR tutorial
- image to text conversion
language: ar
og_description: التعرف على النص من الصورة باستخدام تسريع GPU. يوضح لك هذا البرنامج
  التعليمي كيفية استخراج النص من المسح الضوئي في C# باستخدام Aspose OCR، مع الشيفرة
  والنصائح.
og_title: التعرف على النص من الصورة باستخدام Aspose OCR GPU – دليل C#
tags:
- Aspose
- OCR
- C#
- GPU
title: التعرف على النص من الصورة باستخدام Aspose OCR GPU في C#
url: /ar/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu-in-c/
---

alt text is "recognize text from image example". Should translate alt text? Probably yes, it's text content. But must preserve image markdown format. So alt text becomes Arabic translation: "مثال على التعرف على النص من صورة". Keep URL unchanged.

Also translate table headers and cells.

Let's produce Arabic translation.

Be careful with direction: Arabic is RTL but markdown still left-to-right; we just write Arabic text.

Let's translate.

Start with shortcodes unchanged.

Then heading "# recognize text from image using Aspose OCR GPU in C#" translate: "# التعرف على النص من صورة باستخدام Aspose OCR GPU في C#"

Similarly other headings.

Now body paragraphs.

I'll translate naturally.

Let's craft.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من صورة باستخدام Aspose OCR GPU في C#

هل احتجت يومًا إلى **التعرف على النص من صورة** لكن الملف كان ضخمًا وتوقف المعالج عن العمل؟ ربما جرّبت مكتبة OCR تقليدية واستغرق الأمر وقتًا طويلاً، أو كانت النتائج غير دقيقة. الخبر السار؟ مع تسريع GPU في Aspose OCR يمكنك تحويل ملف TIFF الممسوح ضخم إلى نص نظيف قابل للبحث في ثوانٍ.

في هذا الدليل سنستعرض مثالًا كاملاً جاهزًا للنسخ واللصق يوضح لك كيفية **استخراج النص من ملفات المسح** على جهاز يدعم GPU. لا مراجع غامضة، فقط الشيفرة التي تحتاجها، سبب أهمية كل سطر، وبعض الملاحظات لتجنب الإحباط.

## ما الذي ستحتاجه

- **.NET 6+** (أو .NET Framework 4.7+ – تعمل الواجهة البرمجية بنفس الطريقة)
- حزمة **Aspose.OCR for .NET** عبر NuGet (الإصدار 23.12 أو أحدث)
- **GPU** يدعم CUDA (اختياري، لكنه يسرّع العملية بشكل ملحوظ)
- صورة ممسوحة بدقة عالية (مثال: `large_doc.tif`)

إذا لم يكن لديك GPU، سيعود المحرك تلقائيًا إلى المعالج المركزي – لذا يمكنك تشغيل المثال، لكن سيكون أبطأ قليلًا.

## الخطوة 1 – تثبيت حزمة Aspose.OCR

افتح الطرفية أو نافذة Package Manager Console ونفّذ:

```bash
dotnet add package Aspose.OCR
```

أو، في واجهة NuGet داخل Visual Studio، ابحث عن **Aspose.OCR** وانقر *Install*. سيؤدي ذلك إلى جلب مكتبة OCR الأساسية بالإضافة إلى التجميع الاختياري لتسريع GPU.

> **نصيحة احترافية:** بعد التثبيت، تحقق من وجود ملف `Aspose.OCR.Acceleration.dll` داخل مجلد `packages`. هذا الملف مطلوب لدعم GPU؛ إذا كنت تعمل على خادم بدون واجهة رسومية، يمكنك إهماله وستظل الشيفرة تُترجم.

## الخطوة 2 – تهيئة محرك OCR المدعوم بـ GPU

الفئة `GpuOcrEngine` تكتشف أي GPU متوافق تلقائيًا. إذا كان لديك أكثر من جهاز يمكنك اختيار واحد محدد، لكن معظم المطورين يتركونه يختار بنفسه.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration;   // <-- enables GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Create the OCR engine. It will look for a CUDA‑compatible GPU.
        GpuOcrEngine ocrEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Force a particular GPU device.
        // Uncomment the line below if you know the device ID you want to use.
        // ocrEngine.Device = GpuDevice.GetById(0);
```

**لماذا هذا مهم:** تهيئة محرك GPU مرة واحدة يقلل من الحمل الزائد. إذا قمت بإنشاء وتدمير المحرك داخل حلقة بشكل متكرر، ستفقد تحسينات الأداء.

## الخطوة 3 – تحميل الصورة الممسوحة بدقة عالية

يعمل Aspose OCR مع `System.Drawing.Image`. تأكد من أن مسار الملف يشير إلى صورة حقيقية؛ وإلا ستحصل على استثناء `FileNotFoundException`.

```csharp
        // Step 3: Load the image you want to process.
        // Replace YOUR_DIRECTORY with the actual folder on your machine.
        var scannedImage = Image.FromFile(@"YOUR_DIRECTORY/large_doc.tif");
```

> **حالة خاصة:** إذا كانت الصورة أكبر من 10 000 × 10 000 بكسل، فكر في تقليل حجمها أولًا. ذاكرة GPU محدودة، ومحاولة تحميل صورة ضخمة قد تؤدي إلى استثناء `OutOfMemoryException`.

## الخطوة 4 – تنفيذ OCR باستخدام إعدادات اللغة الافتراضية (Latin)

طريقة `Recognize` تُعيد سلسلة نصية عادية. يمكنك تمرير كائن `OcrOptions` إذا احتجت لغة مختلفة أو معالجة مسبقة مخصصة.

```csharp
        // Step 4: Run OCR. By default it assumes Latin script.
        string recognizedText = ocrEngine.Recognize(scannedImage);
```

**لماذا الإعداد الافتراضي يعمل:** معظم المستندات الممسوحة – العقود، الفواتير، التقارير – تستخدم أبجديات لاتينية. إذا كنت تحتاج إلى سيريالية، عربية أو صينية، عيّن `ocrEngine.Language = "ru"` (أو رمز ISO المناسب) قبل استدعاء `Recognize`.

## الخطوة 5 – عرض أو حفظ النص المستخرج

لإجراء فحص سريع سنكتب النتيجة إلى وحدة التحكم فقط. في تطبيق حقيقي قد تحفظها في قاعدة بيانات، ملف `.txt`، أو تُدخلها إلى فهرس بحث.

```csharp
        // Step 5: Output the OCR result.
        Console.WriteLine(recognizedText);

        // Optional: Save to a file.
        // File.WriteAllText(@"output.txt", recognizedText);
    }
}
```

### النتيجة المتوقعة

إذا كان `large_doc.tif` يحتوي على فقرة بسيطة مثل “Hello, world!”، ستظهر لك:

```
Hello, world!
```

في حالة المسحات متعددة الصفحات، يجمع المحرك النص بترتيب القراءة. يمكنك تقسيمه لاحقًا باستخدام فواصل الأسطر (`\n`) إذا احتجت إلى حدود الصفحات.

## معالجة المشكلات الشائعة

| المشكلة | العرض | الحل |
|--------|-------|------|
| **لم يتم اكتشاف GPU** | `ocrEngine.Device` يساوي `null` والمعالجة بطيئة. | ثبّت أحدث برنامج تشغيل NVIDIA ومجموعة أدوات CUDA (الإصدار 11+). تحقق باستخدام `nvidia-smi`. |
| **تأخير جمع القمامة** | ارتفاع مفاجئ في الذاكرة بعد معالجة العديد من الصور. | استدعِ `scannedImage.Dispose()` بعد OCR، أو ضع الصورة داخل كتلة `using`. |
| **لغة غير صحيحة** | ظهور رموز غير مفهومة للنص غير اللاتيني. | عيّن `ocrEngine.Language` إلى رمز ISO 639‑1 الصحيح قبل `Recognize`. |
| **ملفات ضخمة جدًا** | `OutOfMemoryException`. | قلل الأبعاد باستخدام `Image.GetThumbnailImage` أو قسّم المسح إلى قطع صغيرة. |

## مثال كامل جاهز للتنفيذ

فيما يلي البرنامج بالكامل – بما في ذلك توجيهات `using`، معالجة الأخطاء، وكتلة `using` منظمة للصورة:

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration; // GPU support

class GpuOcrDemo
{
    static void Main()
    {
        try
        {
            // Initialize the GPU‑accelerated OCR engine.
            GpuOcrEngine ocrEngine = new GpuOcrEngine();

            // OPTIONAL: Choose a specific GPU device.
            // ocrEngine.Device = GpuDevice.GetById(0);

            // Load the high‑resolution scanned image.
            string imagePath = @"YOUR_DIRECTORY/large_doc.tif";
            if (!File.Exists(imagePath))
                throw new FileNotFoundException($"Image not found: {imagePath}");

            using (Image scannedImage = Image.FromFile(imagePath))
            {
                // Perform OCR (defaults to Latin script).
                string text = ocrEngine.Recognize(scannedImage);

                // Output the extracted text.
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(text);

                // Save to a text file (optional).
                string outputPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(outputPath, text);
                Console.WriteLine($"Text saved to {outputPath}");
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### ما يفعله هذا الكود

1. **ينشئ** كائن `GpuOcrEngine` يختار أفضل GPU تلقائيًا.
2. **يحمّل** ملف TIFF داخل كتلة `using` لضمان تحرير الموارد.
3. **يستدعي** `Recognize` لتحويل البت ماب إلى سلسلة نصية.
4. **يكتب** النتيجة إلى كل من وحدة التحكم وملف `.txt` بجوار الصورة الأصلية.
5. **يمسك** أي استثناء ويطبع رسالة خطأ ودية.

## التوسع – من “التعرف على النص من صورة” إلى خطوط معالجة مستندات كاملة

الآن بعد أن أصبحت قادرًا على **استخراج النص من ملفات المسح**، فكر في الخطوات التالية:

- **معالجة دفعات:** كرّر العملية على مجلد من ملفات TIFF واجمع النتائج في فهرس بحث قابل للبحث.
- **اكتشاف اللغة:** استخدم `ocrEngine.DetectLanguage()` (إن كان متوفرًا) لتبديل اللغة تلقائيًا.
- **معالجة ما بعد OCR:** مرّر الناتج عبر مدقق إملائي أو مرشح regex لتنقية الأخطاء الشائعة.
- **التكامل مع Azure Cognitive Search:** ادفع النص المستخرج إلى فهرس سحابي قابل للبحث الفوري.

كل ما سبق يبني على النمط الأساسي الذي رأيته للتو – تهيئة مرة واحدة، تغذية الصور، جمع النص.

## الخلاصة

لقد تعلمت الآن كيفية **التعرف على النص من صورة** باستخدام محرك Aspose OCR المدعوم بـ GPU في C#. يوضح المثال الكامل القابل للتنفيذ كيفية إعداد المحرك، تحميل مسح عالي الدقة، تنفيذ OCR، ومعالجة الناتج. باتباع النصائح ومعالجة الحالات الخاصة المذكورة أعلاه، ستتجنب المشكلات الشائعة وتحصل على نتائج موثوقة سواءً كنت تعمل على حاسوب مطور أو خادم إنتاج.

هل أنت مستعد لتحويل المزيد من المسحات إلى بيانات قابلة للبحث؟ جرّب معالجة مجلد كامل، جرب لغات غير لاتينية، أو ادخل النتائج إلى محرك بحث نص كامل. السماء هي الحد، والكود الذي كتبته الآن هو الأساس المتين الذي تحتاجه.

برمجة سعيدة! 🚀

![مثال على التعرف على النص من صورة](/images/ocr-gpu

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}