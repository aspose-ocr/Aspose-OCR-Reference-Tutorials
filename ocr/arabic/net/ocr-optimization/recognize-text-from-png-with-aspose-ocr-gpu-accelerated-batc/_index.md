---
category: general
date: 2026-04-01
description: تعلم كيفية التعرف على النص من ملفات PNG بسرعة عن طريق تعيين معرف جهاز
  GPU وتمكين تسريع GPU في Aspose OCR. دليل خطوة بخطوة بلغة C#.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: ar
og_description: التعرف على النص من ملفات PNG بسرعة عن طريق ضبط معرف جهاز GPU. اتبع
  هذا الدليل الكامل بلغة C# لتمكين تسريع GPU باستخدام Aspose OCR.
og_title: التعرف على النص من PNG – دليل Aspose OCR المعجل بوحدة معالجة الرسومات
tags:
- C#
- OCR
- GPU
- Aspose
title: التعرف على النص من ملف PNG باستخدام Aspose OCR – عرض تجريبي دفعي مُسرّع بالمعالج
  الرسومي
url: /ar/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من PNG – دليل كامل لمعالجة الدفعات باستخدام C# مع تسريع GPU

هل احتجت يومًا إلى **التعرف على النص من PNG** لكن وجدت العملية بطيئة جدًا؟ لست وحدك. يبدأ معظم المطورين بنداء OCR بسيط، ثم يحدقون في وحدة تحكم تتحرك ببطء كالسلحفاة عندما يحتوي مجلد على العشرات من لقطات الشاشة.  

الخبر السار؟ Aspose OCR يمكنه نقل العبء الثقيل إلى بطاقة الرسومات الخاصة بك، ومع بضع أسطر فقط يمكنك **تعيين معرف جهاز GPU** لاختيار بطاقة الـ GPU المحددة التي تريدها. في هذا الدليل سنستعرض مثالًا كاملًا قابلاً للتنفيذ يجلب كل ملفات PNG من مجلد، يُفعّل تسريع GPU، يختار أول GPU، ويطبع عدد الأحرف لكل ملف.

بنهاية الدليل ستحصل على برنامج مستقل يمكنك إدراجه في أي مشروع .NET، وستفهم لماذا تفعيل الـ GPU مهم، وكيفية التعامل مع الحالات الخاصة، وما الذي يمكن تعديله للحصول على أداء أفضل.

## ما ستحتاجه

- **.NET 6.0** أو أحدث (الكود يُجمّع مع .NET Core أيضًا).  
- حزمة NuGet **Aspose.OCR** – ثبّتها باستخدام `dotnet add package Aspose.OCR`.  
- جهاز يحتوي على GPU متوافق مع CUDA (عادةً NVIDIA) والسائق المناسب.  
- مجلد مليء بصور **PNG** التي تريد معالجتها.  

إذا كان أي من ذلك غير مألوف لك، لا تقلق. الخطوات أدناه تتضمن الأوامر الدقيقة التي تحتاجها، وسنناقش أيضًا ما يجب فعله عندما لا يتوفر GPU.

## الخطوة 1: تهيئة محرك OCR وتمكين تسريع GPU  

أول شيء عليك فعله هو إنشاء نسخة من `OcrEngine` وتفعيل دعم GPU. هذه العلامة تخبر Aspose باستخدام مكتبات CUDA الأصلية تحت الغطاء.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**لماذا هذا مهم:** بدون `UseGpuAcceleration`، تُعالج كل صورة على المعالج (CPU)، مما يجعل العملية أبطأ بكثير، خاصةً للصور PNG عالية الدقة. تفعيل العلامة أيضًا يجهّز المحرك لقبول جهاز GPU محدد لاحقًا.

## الخطوة 2: تعيين معرف جهاز GPU (اختياري لكن مُوصى به)  

إذا كان جهازك يحتوي على أكثر من GPU، يمكنك اختيار أيٍّ منها لاستخدامه. تبدأ معرفات الأجهزة من **0**، لذا `0` يختار أول GPU، `1` الثاني، وهكذا.

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**نصيحة احترافية:** عند التشغيل على خادم مشترك، تعيين معرف جهاز GPU صراحةً يمكن أن يمنع مهمتك من سرقة الموارد من عمليات أخرى. إذا حذفت هذا السطر، سيختار Aspose الجهاز الافتراضي، وهو عادةً مناسب لإعداد يحتوي على GPU واحد.

## الخطوة 3: جمع جميع ملفات PNG من مجلد الدفعة الخاص بك  

الخطوة التالية هي تحديد كل ملفات PNG التي تريد تشغيل OCR عليها. طريقة `Directory.GetFiles` تقوم بالعمل الشاق.

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**حالة خاصة:** إذا كان المجلد فارغًا، سيكون `imageFiles` مصفوفة فارغة. سنتعامل مع ذلك لاحقًا برسالة ودية.

## الخطوة 4: معالجة كل صورة وإخراج عدد الأحرف المعترف بها  

الآن الحلقة الأساسية. لكل صورة PNG نستدعي `Recognize`، ثم نطبع اسم الملف وطول النص المستخرج.

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**ما ستراه:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

إذا كانت الصورة لا تحتوي على نص، سيكون العد `0`. وهذا طبيعي تمامًا للقطات الشاشة التي هي رسومية بحتة.

## الخطوة 5: تشغيل البرنامج والتحقق من استخدام GPU  

قم بإنشاء الملف (`dotnet build`) وتشغيله (`dotnet run`). أثناء تمرير وحدة التحكم، يمكنك فتح أداة مراقبة GPU (مثل NVIDIA Smi) لرؤية ارتفاع مؤقت في استخدام GPU لكل صورة. إذا لم تر أي نشاط، تحقق مرة أخرى من:

1. تم تثبيت برنامج تشغيل CUDA.  
2. تم تعيين `UseGpuAcceleration` إلى `true`.  
3. معرف `GpuDeviceId` الصحيح يطابق GPU فعلي.

إذا لم يكن GPU متاحًا، سيعود Aspose تلقائيًا إلى المعالج (CPU)، لكنك ستفقد ميزة السرعة.

## تنوعات شائعة ونصائح

| الحالة | ما الذي يجب تغييره |
|-----------|----------------|
| **تنسيق صورة مختلف** (مثال: JPEG) | غيّر نمط البحث إلى `*.jpg` أو `*.*` وستظل Aspose تتعرف على النص. |
| **حجم الدفعة كبير** (آلاف الملفات) | عالجها على دفعات لتجنب ضغط الذاكرة: قسّم `imageFiles` إلى مصفوفات أصغر. |
| **تحتاج النص الفعلي، ليس فقط الطول** | استبدل `ocrResult.Text.Length` بـ `ocrResult.Text` في `WriteLine`. |
| **التشغيل على خادم بدون واجهة** | تأكد من أن الخادم يحتوي على برنامج تشغيل GPU؛ وإلا، عيّن `UseGpuAcceleration = false` لتجنب الأخطاء غير الضرورية. |
| **عدة GPUs، تريد موازنة الحمل** | استخدم حلقة لتعيين `ocrEngine.GpuDeviceId = i % gpuCount` داخل `foreach` لتدوير الأجهزة. |

## النتيجة المتوقعة والتحقق

عندما يعمل كل شيء، تطبع وحدة التحكم اسم كل ملف متبوعًا بعدد الأحرف، كما هو موضح سابقًا. للتحقق مرة أخرى من ناتج OCR الفعلي، يمكنك مؤقتًا إظهار النص:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

تذكر فقط إزالة أو التعليق على هذا السطر للدفعات الكبيرة؛ طباعة آلاف الأسطر قد تغمر الطرفية.

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

احفظ هذا كـ `GpuBatchDemo.cs`، شغّل `dotnet add package Aspose.OCR`، ثم `dotnet run`. يجب أن ترى عدد الأحرف يظهر تقريبًا فورًا لكل PNG، بفضل تسريع GPU.

## الخلاصة

أنت الآن تعرف كيف **تتعرف على النص من ملفات PNG** بفعالية من خلال تمكين تسريع GPU وتعيين **معرف جهاز GPU** صراحةً في Aspose OCR. البرنامج الكامل القابل للنسخ واللصق يتعامل مع اكتشاف المجلد، وفحص الحالات الخاصة، ويعطيك تغذية راجعة فورية حول أداء OCR.

الخطوات التالية؟ جرّب استبدال استدعاء `Recognize` بـ `ocrEngine.RecognizeAsync` إذا كنت تحتاج إلى معالجة غير متزامنة، أو جرب خيارات تمهيد الصور المختلفة (مثل التحويل إلى ثنائي) التي توفرها Aspose. يمكنك أيضًا توجيه نتائج OCR إلى قاعدة بيانات أو فهرس بحث للحصول على حل بحث نص كامل.

هل لديك أسئلة حول معالجة ملفات PDF متعددة الصفحات، أو تريد مقارنة Aspose OCR مع Tesseract؟ اترك تعليقًا أو استكشف دروسنا الأخرى حول **batch OCR C#**، **نصائح أداء OCR**، و **معالجة الصور المدفوعة بـ GPU**. برمجة سعيدة!  

![مخرجات وحدة التحكم تُظهر عدد الأحرف المعترف بها لملفات PNG – التعرف على النص من PNG باستخدام تسريع GPU](image-placeholder.png "مثال مخرجات التعرف على النص من PNG")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}