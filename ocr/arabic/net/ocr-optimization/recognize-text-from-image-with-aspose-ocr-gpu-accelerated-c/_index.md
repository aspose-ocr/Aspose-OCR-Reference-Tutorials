---
category: general
date: 2026-01-13
description: تعلم كيفية التعرف على النص من الصورة واستخراج النص من الإيصال بسرعة باستخدام
  Aspose OCR. يتضمن خطوات تحميل الصورة للتعرف الضوئي على الأحرف وتعيين معرف جهاز GPU.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for ocr
- set gpu device id
language: ar
og_description: تعرّف على النص من الصورة فورًا باستخدام Aspose OCR. اتبع هذا الدليل
  خطوة بخطوة لتحميل الصورة للـ OCR، وتعيين معرف جهاز GPU، واستخراج النص من الإيصال.
og_title: التعرف على النص من الصورة – دليل C# الكامل مع تسريع GPU
tags:
- Aspose OCR
- C#
- GPU computing
title: التعرف على النص من الصورة باستخدام Aspose OCR – دليل C# المعجل بالمعالج الرسومي
url: /ar/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة – دليل C# الكامل مع تسريع GPU

هل احتجت يوماً إلى **التعرف على النص من الصورة** لكن وجدت نسخة المعالج المركزي بطيئة جداً؟ ربما تحاول **استخراج النص من إيصالات** والكمون يفسد تجربة المستخدم. الخبر السار هو أنك لست مضطراً للرضوخ إلى الأداء البطيء—حزمة Aspose OCR للـ GPU يمكنها تسريع العملية، والكود لا يتعدى بضع أسطر.

في هذا الدرس سنستعرض مثالاً كاملاً قابلاً للتنفيذ يوضح كيفية **تحميل الصورة للـ OCR**، ضبط الـ GPU باستخدام **set GPU device ID**، وأخيراً استرجاع النتيجة كنص عادي. بنهاية الدرس ستحصل على مقتطف جاهز للإدراج يعمل على أي جهاز Windows أو Linux حديث ببطاقة NVIDIA مدعومة.

---

## ما ستحتاجه

- **.NET 6+** (أو .NET Framework 4.7.2+) – الـ API يعمل مع كلا الإصدارين.  
- حزمة NuGet **Aspose.OCR** **بالإضافة إلى** الإضافة **Aspose.OCR.Gpu**.  
- بطاقة NVIDIA GPU بسعة ذاكرة لا تقل عن 2 GB VRAM (العرض التجريبي يحد الاستخدام بـ 1 GB).  
- صورة نموذجية، مثل إيصال ممسوح ضوئياً (`receipt.jpg`).

إذا كان لديك مشروع بالفعل، فقط نفّذ `dotnet add package Aspose.OCR` و `dotnet add package Aspose.OCR.Gpu`. لا تحتاج إلى مكتبات أصلية إضافية؛ الـ SDK يضم ملفات CUDA الثنائية المطلوبة.

---

## التنفيذ خطوة بخطوة

### ## كيفية التعرف على النص من الصورة باستخدام Aspose OCR وGPU

فيما يلي **البرنامج الكامل المستقل**. انسخه إلى مشروع Console جديد واضغط `Ctrl+F5`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑accelerated namespace

class GpuOcrDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize a GPU‑enabled OCR engine
        // -------------------------------------------------
        var ocrEngine = new GpuOcrEngine();

        // -------------------------------------------------
        // Step 2: (Optional) Select the GPU device and limit memory usage
        // -------------------------------------------------
        ocrEngine.DeviceId = 0;        // set GPU device ID – first GPU in the system
        ocrEngine.MaxMemoryMb = 1024;  // cap at 1 GB to avoid OOM on shared machines

        // -------------------------------------------------
        // Step 3: Load the image you want to recognize
        // -------------------------------------------------
        var receiptImage = OcrImage.FromFile(@"YOUR_DIRECTORY/receipt.jpg");

        // -------------------------------------------------
        // Step 4: Perform OCR – here we extract text from receipt (English)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);

        // -------------------------------------------------
        // Step 5: Output the recognized plain text
        // -------------------------------------------------
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

> **نصيحة محترف:** إذا كان جهازك يحتوي على عدة بطاقات GPU، غيّر `DeviceId` إلى `1` أو `2` إلخ لاختيار البطاقة الأقل انشغالاً. سيُظهر الـ SDK استثناء واضح `GpuDeviceNotFoundException` إذا كان المعرف خارج النطاق.

### ### الخطوة 1: تحميل الصورة للـ OCR

استدعاء `OcrImage.FromFile` يفعل أكثر من مجرد قراءة ملف bitmap—إنه يسبق الصورة بمعالجة (تصحيح الميل، تحويل إلى ثنائي) بناءً على خوارزميات داخلية. لهذا السبب **load image for OCR** خطوة منفصلة: يمكنك استبدالها بـ `MemoryStream` إذا كانت الصورة مخزنة في قاعدة بيانات.

```csharp
var receiptImage = OcrImage.FromFile(@"C:\Invoices\receipt.jpg");
```

إذا كنت بحاجة إلى **التعرف على النص من الصورة** الموجودة بالفعل في الذاكرة:

```csharp
using (var ms = new MemoryStream(File.ReadAllBytes(@"receipt.jpg")))
{
    var receiptImage = OcrImage.FromStream(ms);
}
```

### ### الخطوة 2: ضبط معرف جهاز GPU وحدود الذاكرة

موارد الـ GPU محدودة. من خلال إتاحة `DeviceId` و `MaxMemoryMb`، يتيح Aspose لك **set GPU device ID** بأمان، مما يمنع عملية واحدة من استهلاك كامل البطاقة.

```csharp
ocrEngine.DeviceId = 0;        // first GPU
ocrEngine.MaxMemoryMb = 1024; // 1 GB ceiling
```

إذا تجاوزت حد الذاكرة، سيقوم المحرك تلقائياً بالتحويل إلى ذاكرة النظام RAM، وهو أبطأ لكنه يمنع الأعطال.

### ### الخطوة 3: استخراج النص من الإيصال (التعرف على النص من الصورة)

طريقة `Recognize` تقوم بالعمل الشاق. يمكنك تمرير أي لغة يدعمها Aspose OCR؛ بالنسبة للإيصالات، الإنجليزية تعمل في معظم الحالات، لكن يمكنك أيضاً إضافة `OcrLanguage.Spanish` أو حزمة لغة مخصصة.

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);
Console.WriteLine(ocrResult.Text);
```

**الناتج المتوقع** (عينة):

```
Store: QuickMart
Date: 2025-12-01
Total: $23.45
Thank you for shopping!
```

---

## الاختلافات الشائعة والحالات الطرفية

| الحالة | ما الذي يجب تغييره | السبب |
|-----------|----------------|-----|
| **عدة إيصالات في صورة واحدة** | استدعِ `ocrEngine.Recognize` على كل منطقة مقصوصة (استخدم `OcrImage.Crop`) | تحسين الدقة لأن المحرك يتعامل مع مساحة أصغر وأكثر نظافة. |
| **مسحات منخفضة الدقة (<150 dpi)** | قم بزيادة الحجم مسبقاً باستخدام `receiptImage.Resize(2.0)` قبل التعرف | كثافة البكسل الأعلى تزود الـ GPU ببيانات أكثر. |
| **إيصالات غير إنجليزية** | مرّر `OcrLanguage.French` (أو ملف `.traineddata` مخصص) | النماذج الخاصة بالغة تقلل الإيجابيات الزائفة. |
| **GPU غير متاح** | استخدم نسخة احتياطية إلى `OcrEngine` (CPU) داخل كتلة try‑catch | يضمن أن التطبيق يظل يعمل على الخوادم بدون رسومات. |

```csharp
try
{
    var gpuEngine = new GpuOcrEngine();
    // configure GPU as shown earlier …
    var result = gpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
catch (GpuDeviceNotFoundException)
{
    // Graceful fallback
    var cpuEngine = new OcrEngine();
    var result = cpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
```

---

## نصائح لجعل الـ OCR جاهزاً للإنتاج

- **المعالجة الدفعية:** غلف حلقة التعرف داخل `Parallel.ForEach` لكن حدّد درجة التوازي بعدد تدفقات الـ GPU التي يمكنك تخصيصها (عادة 1‑2 لكل بطاقة).  
- **نظافة الذاكرة:** حرّص على التخلص من كائنات `OcrImage` فور الانتهاء (`receiptImage.Dispose()`)، خاصةً عند معالجة آلاف الإيصالات.  
- **التسجيل:** احفظ `ocrResult.Confidence` لكل سطر؛ القيم المنخفضة قد تستدعي مراجعة يدوية.  
- **الأمان:** عند التعامل مع إيصالات حساسة، احفظ ملفات الصور في مجلدات مؤقتة مشفّرة واحذفها بعد المعالجة.

---

## الخلاصة

أصبح لديك الآن **مثال كامل قابل للتنفيذ** يوضح كيفية **التعرف على النص من الصورة** باستخدام تسريع GPU من Aspose OCR، **تحميل الصورة للـ OCR**، **ضبط معرف جهاز GPU**، وأخيراً **استخراج النص من الإيصال** في بضع خطوات مختصرة. الكود جاهز للنسخ واللصق، والشروحات توفر لك السياق الكافي لتكييفه مع سيناريوهات متعددة اللغات، أو عدة بطاقات GPU، أو أحمال عالية.

هل أنت مستعد للتحدي التالي؟ جرّب تغذية تدفق فيديو مباشر إلى `GpuOcrEngine` للمسح الضوئي الفوري للإيصالات، أو دمج النتيجة مع واجهة برمجة تطبيقات المحاسبة. السماء هي الحد عندما تجمع بين OCR سريع على الـ GPU وتصميم C# نظيف.

*برمجة سعيدة، ولتكن OCR دائمًا سريعة!*

![التعرف على النص من الصورة توضيح تجريبي](placeholder-image.png "مثال على التعرف على النص من الصورة")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}