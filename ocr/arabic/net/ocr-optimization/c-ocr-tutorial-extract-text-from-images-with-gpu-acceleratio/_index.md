---
category: general
date: 2026-02-28
description: دروس C# OCR التي تُظهر كيفية التعرف على النص من الصورة، تحويل الصورة
  الممسوحة ضوئياً إلى نص، استخراج النص من ملف TIFF ومعالجة الصورة باستخدام وحدة معالجة
  الرسومات في دقائق.
draft: false
keywords:
- c# ocr tutorial
- recognize text from image
- convert scanned image to text
- extract text from tiff
- process image using gpu
language: ar
og_description: 'دورة C# OCR: تعلم كيفية التعرف على النص من الصورة، تحويل الصورة الممسوحة
  ضوئياً إلى نص، استخراج النص من ملفات TIFF ومعالجة الصورة باستخدام وحدة معالجة الرسومات
  (GPU) مع Aspose OCR.'
og_title: دليل c# OCR – استخراج النص بتسريع GPU
tags:
- OCR
- C#
- GPU processing
title: دروس OCR بلغة C# – استخراج النص من الصور باستخدام تسريع GPU
url: /ar/net/ocr-optimization/c-ocr-tutorial-extract-text-from-images-with-gpu-acceleratio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل c# OCR – استخراج النص من الصور باستخدام تسريع GPU

هل احتجت يومًا إلى **دليل c# OCR** يوصلك فعليًا من مسح ضبابي إلى نص قابل للتحرير دون أن تقص شعرك؟ لست وحدك. في العديد من المشاريع الواقعية ستجد نفسك تحدق في ملف TIFF ضخم، متسائلًا كيف **تتعرف على النص من الصورة** بسرعة ودقة.

الأخبار السارة؟ باستخدام محرك GPU الخاص بـ Aspose.OCR يمكنك **تحويل الصورة الممسوحة ضوئيًا إلى نص** في جزء صغير من الوقت الذي يستغرقه المعالج المركزي. في هذا الدليل سنستعرض كل خطوة، من تحميل ملف TIFF متعدد الميغابايت إلى طباعة النتيجة كنص عادي، مع الحفاظ على بساطة الشيفرة لتناسب عرضًا سريعًا أثناء استراحة القهوة.

> **ما ستحصل عليه:** تطبيق C# console كامل قابل للتنفيذ **يستخرج النص من TIFF**، يستخدم **معالجة الصورة باستخدام GPU**، ويطبع السلسلة المعترف بها إلى وحدة التحكم. لا خدمات خارجية، لا إعدادات مخفية—فقط شفرة .NET صافية.

## المتطلبات المسبقة

- .NET 6 SDK (أو أحدث) مثبت – بيئة تشغيل حديثة متعددة المنصات.
- Visual Studio 2022 أو VS Code – أي محرر يدعم C#.
- رخصة Aspose.OCR (أو نسخة تجريبية مجانية) – المكتبة تجارية، لكن النسخة التجريبية تكفي للتعلم.
- ملف TIFF كبير ممسوح ضوئيًا تريد اختباره – سمه `large_scan.tif` وضعه في مكان يمكن للتطبيق قراءته.

هذا كل شيء. لا حزم NuGet إضافية بخلاف `Aspose.OCR` و `Aspose.OCR.Gpu`.

## الخطوة 1 – إعداد المشروع وتثبيت Aspose OCR

```bash
dotnet new console -n GpuOcrDemo
cd GpuOcrDemo
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

> **نصيحة احترافية:** إذا كنت تستخدم جهازًا بدون GPU مخصص، فإن المكتبة ستعود بسلاسة إلى وضع CPU، لكنك لن ترى تسريع السرعة الذي نرغب به.

## الخطوة 2 – تهيئة محرك OCR وتمكين معالجة GPU

جوهر أي **دليل c# OCR** هو `OcrEngine`. من خلال ضبط `ProcessingMode` إلى `Gpu`، تخبر Aspose بأن يحمّل الأعمال الثقيلة إلى بطاقة الرسومات الخاصة بك.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System.Drawing;

class GpuOcrDemo
{
    static void Main()
    {
        // Step 2: Initialize the OCR engine and enable GPU processing
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu
        };
```

لماذا GPU؟ بطاقات GPU الحديثة تتفوق في عمليات البكسل المتوازية، وهو ما يحتاجه OCR عند مسح آلاف الأحرف عبر TIFF عالي الدقة. النتيجة هي انخفاض زمن الاستجابة وزيادة الإنتاجية، خاصةً للوظائف الدفعية.

## الخطوة 3 – تحميل صورة الإدخال (أي صيغة مدعومة)

يمكن لـ Aspose.OCR قراءة تقريبًا أي صيغة نقطية: TIFF، JPEG، PNG، BMP، وما إلى ذلك. هنا نقوم بتحميل TIFF لأنه صيغة شائعة للمستندات الممسوحة.

```csharp
        // Step 3: Load the input image (any supported format)
        using var image = Image.Load("YOUR_DIRECTORY/large_scan.tif");
```

> **ماذا لو كان لديك PDF؟** حوّل كل صفحة إلى صورة أولاً—يمكن لـ Aspose.PDF القيام بذلك، أو يمكنك استخدام أي محول مفتوح المصدر. محرك OCR يهتم فقط بالبيانات النقطية.

## الخطوة 4 – إجراء التعرف على OCR على الصورة المحملة

الآن يحدث السحر. تُعيد طريقة `Recognize` كائن `OcrResult` يحتوي على النص العادي، درجات الثقة، وحتى إحداثيات الصناديق المحيطة إذا احتجتها لاحقًا.

```csharp
        // Step 4: Perform OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);
```

إذا احتجت يومًا إلى **التعرف على النص من الصورة** بلغة معينة، اضبط `ocrEngine.Language` قبل استدعاء `Recognize`. اللغة الافتراضية هي الإنجليزية، لكن Aspose يدعم أكثر من 40 لغة.

## الخطوة 5 – إخراج النص العادي المعترف به

أخيرًا، اطبع النتيجة إلى وحدة التحكم. في تطبيق حقيقي قد تكتبها إلى قاعدة بيانات، ملف .txt، أو تمررها إلى خط أنابيب NLP لاحق.

```csharp
        // Step 5: Output the recognized plain‑text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج بصفحة مطبوعة واضحة يجب أن ينتج شيء مشابه لـ:

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

إذا كانت الصورة مشوشة، ستظل ترى سلسلة نصية—لكن مع أخطاء تعرّف أحيانًا. هنا يبرز دور **معالجة الصورة باستخدام GPU**: يمكنك إجراء معالجة مسبقة (تصحيح الميل، إزالة الضوضاء) على GPU قبل OCR، مما يحسن الدقة بشكل كبير.

## الخطوة 6 – اختياري: معالجة مسبقة لتعزيز الدقة

بينما يعمل **دليل c# OCR** الأساسي مباشرةً، بعض التعديلات غالبًا ما تُحدث فرقًا ملحوظًا:

```csharp
        // Optional: Apply basic image enhancements
        image = ImageProcessor.Binarize(image, threshold: 128);
        image = ImageProcessor.Deskew(image);
```

كل من `Binarize` و `Deskew` يتم تسريعهما على GPU عندما تكون في `ProcessingMode.Gpu`. خطوة التحويل إلى ثنائي تجعل الصورة بالأسود والأبيض النقي، مما يقلل كمية البيانات التي يجب على محرك OCR تحليلها.

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| **نفاد الذاكرة على ملفات TIFF الكبيرة** | ذاكرة GPU محدودة. | قسّم الصورة إلى مربعات (`Image.Split`) وعالج كل مربع على التوالي. |
| **اكتشاف لغة خاطئ** | اللغة الافتراضية هي الإنجليزية. | اضبط `ocrEngine.Language = Language.French;` (أو أي لغة مدعومة). |
| **عدم توافق برنامج تشغيل GPU** | برامج التشغيل القديمة لا توفر قدرات الحوسبة المطلوبة. | حدّث إلى أحدث برنامج تشغيل NVIDIA/AMD وتأكد من أن `ProcessingMode.Gpu` يُعيد `true` عبر `ocrEngine.IsGpuSupported`. |
| **نتيجة فارغة غير متوقعة** | لم يتم تحميل الصورة بشكل صحيح (مسار خاطئ). | استخدم مسارًا مطلقًا أو `Path.Combine(Environment.CurrentDirectory, "large_scan.tif")`. |

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل الذي يمكنك وضعه في `Program.cs`. يتضمن معالجة مسبقة اختيارية وتعاملًا قويًا مع الأخطاء.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Drawing;
using System.IO;

class GpuOcrDemo
{
    static void Main()
    {
        try
        {
            // 1️⃣ Initialize OCR engine with GPU acceleration
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = ProcessingMode.Gpu
            };

            // Verify GPU support (helps with debugging)
            Console.WriteLine($"GPU supported: {ocrEngine.IsGpuSupported}");

            // 2️⃣ Load the TIFF (adjust path as needed)
            string imagePath = Path.Combine(Environment.CurrentDirectory, "large_scan.tif");
            using var image = Image.Load(imagePath);

            // 3️⃣ (Optional) Pre‑process the image on the GPU
            var processed = ImageProcessor.Deskew(ImageProcessor.Binarize(image, 128));

            // 4️⃣ Run OCR
            var result = ocrEngine.Recognize(processed);

            // 5️⃣ Output the plain‑text
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(result.Text);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR: {ex.Message}");
        }
    }
}
```

**الناتج المتوقع في وحدة التحكم** (مقتطع للوجز):

```
GPU supported: True
=== OCR RESULT ===
[Your extracted text appears here]
```

شغّله باستخدام:

```bash
dotnet run
```

إذا تم إعداد كل شيء بشكل صحيح، سترى النص المخفي داخل ملف TIFF الخاص بك—بسرعة، بفضل معالجة GPU.

## توسيع الدليل

الآن بعد أن لديك **دليل c# OCR** قويًا، فكر في الخطوات التالية:

1. **معالجة دفعية** – تكرار عبر مجلد من ملفات TIFF، وتخزين كل نتيجة في ملف `.txt`.
2. **حزم اللغات** – إضافة دعم للإسبانية أو الصينية بتحميل ملفات اللغة المناسبة من Aspose.
3. **التكامل مع Azure Blob Storage** – سحب الصور من السحابة، تنفيذ OCR عليها، ثم إرجاع النص.
4. **معالجة لاحقة** – استخدام التعبيرات النمطية لاستخراج أرقام الفواتير، التواريخ، أو الإجماليات تلقائيًا.

كل من هذه الأفكار يبني على المفاهيم الأساسية التي غطيناها: **التعرف على النص من الصورة**، **تحويل الصورة الممسوحة ضوئيًا إلى نص**، **استخراج النص من TIFF**، و **معالجة الصورة باستخدام GPU**.

## الخلاصة

لقد انتهينا للتو من دليل **c# OCR** كامل المميزات يوضح لك كيفية **التعرف على النص من الصورة**، **تحويل الصورة الممسوحة ضوئيًا إلى نص**، و **استخراج النص من TIFF** مع **معالجة الصورة باستخدام GPU** لتحقيق أقصى سرعة. الشيفرة مستقلة، تعمل مع أي بيئة تشغيل .NET 6+، وتظهر كلًا من *كيفية* و *سبب* كل خطوة.

جرّبه مع مستنداتك الخاصة، جرب المعالجة المسبقة، وشاهد كيف يحول GPU مهمة OCR البطيئة إلى عملية سريعة كالصاعقة. عندما تكون مستعدًا، انتقل إلى وثائق Aspose لمزيد من التفاصيل حول دعم اللغات، تقييم الثقة، والتحليل المتقدم للتخطيط.

برمجة سعيدة، ولتكن خطوط أنابيب OCR الخاصة بك سريعة دائمًا!  

![مخطط يوضح تدفق دليل c# OCR الذي يحمل ملف TIFF، يعالج الصورة باستخدام GPU، ينفذ OCR، ويخرج النص](csharp-ocr-tutorial-diagram.png "مخطط دليل c# OCR – معالجة الصورة باستخدام GPU لاستخراج النص من TIFF")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}