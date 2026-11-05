---
category: general
date: 2026-03-26
description: تشغيل OCR على صورة باستخدام دعم GPU في Aspose OCR بلغة C#. تعلم كيفية
  تحميل الصورة للـ OCR، تعيين معرف جهاز GPU، واستخراج النص من الصورة بسرعة.
draft: false
keywords:
- run OCR on image
- extract text from image
- load image for OCR
- recognize text from document
- set GPU device ID
language: ar
og_description: تشغيل التعرف الضوئي على الحروف (OCR) على صورة باستخدام Aspose OCR
  GPU في C#. يوضح هذا الدليل كيفية تحميل الصورة للتعرف الضوئي على الحروف، وتعيين معرف
  جهاز GPU، واستخراج النص من الصورة بكفاءة.
og_title: تشغيل OCR على الصورة باستخدام GPU في C# – دليل كامل
tags:
- C#
- OCR
- GPU
- Aspose
title: تشغيل OCR على صورة باستخدام GPU في C# – دليل برمجة شامل
url: /ar/net/ocr-optimization/run-ocr-on-image-with-gpu-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل OCR على الصورة باستخدام GPU في C# – دليل برمجي كامل

هل احتجت يوماً إلى **run OCR on image** للملفات ولكن وجدت نسخة الـ CPU بطيئة للغاية؟ لست وحدك. في العديد من التطبيقات الواقعية—مثل ماسحات الفواتير أو أرشيفات المستندات الضخمة—العقبة هي محرك OCR نفسه.  

في هذا الدرس سنستعرض **مثالًا كاملاً قابلاً للتنفيذ** يوضح لك كيفية **load image for OCR**، واختيارياً **set GPU device ID**، وأخيراً **extract text from image** باستخدام واجهة Aspose OCR المتسارعة بالـ GPU. بنهاية الدرس ستكون قادرًا على **recognize text from document** للصور في جزء بسيط من الوقت الذي تستغرقه الطريقة المعتمدة على الـ CPU فقط.

## ما ستتعلمه

- كيفية تثبيت وإضافة مراجع حزم Aspose.OCR و Aspose.OCR.Gpu.  
- الخطوات الدقيقة **run OCR on image** مع تسريع الـ GPU.  
- لماذا اختيار **GPU device ID** الصحيح مهم في الأجهزة متعددة الـ GPU.  
- نصائح للتعامل مع الملفات الكبيرة، استراتيجيات fallback، والمشكلات الشائعة.  

### المتطلبات المسبقة

| المتطلب | السبب |
|-------------|--------|
| .NET 6.0 أو أحدث | ميزات لغة حديثة وأداء أفضل |
| Visual Studio 2022 (أو أي بيئة تطوير C#) | لتسهيل إعداد المشروع |
| بطاقة NVIDIA GPU تدعم CUDA (اختياري) | مطلوب فقط إذا أردت تسريع الـ GPU |
| حزم NuGet Aspose.OCR & Aspose.OCR.Gpu | توفر الفئة `GpuOcrEngine` |

إذا لم يكن لديك GPU، لا تقلق—الكود سيتحول تلقائيًا إلى محرك الـ CPU، وسنشرح ذلك لاحقًا.

---

## الخطوة 1: تثبيت حزم Aspose OCR

قبل أن تتمكن من **run OCR on image**، تحتاج إلى المكتبات. افتح الطرفية (أو Package Manager Console) ونفّذ:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

هاتان الحزمتان تجلبان محرك OCR الأساسي وإضافات الـ GPU. بعد التثبيت، ستظهر المراجع التالية في ملف `.csproj` الخاص بك:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
  <PackageReference Include="Aspose.OCR.Gpu" Version="23.10.0" />
</ItemGroup>
```

> **نصيحة محترف:** حافظ على توافق إصدارات الحزم؛ الإصدارات غير المتطابقة قد تتسبب بأخطاء وقت التشغيل.

---

## الخطوة 2: إنشاء محرك OCR مدعوم بالـ GPU

الآن بعد أن أصبحت المكتبات جاهزة، لنقم **run OCR on image** باستخدام الـ GPU. فئة `GpuOcrEngine` هي نقطة الدخول للمعالجة المتسارعة.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Namespace for GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Instantiate the GPU OCR engine
        var gpuEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Choose which GPU to use – 0 = first GPU
        // This is where the "set GPU device ID" keyword comes into play.
        gpuEngine.DeviceId = 0;

        // The rest of the workflow continues in the following steps...
```

**لماذا الـ GPU؟**  
نوى الـ GPU تتفوق في عمليات البكسل المتوازية، وهو ما يحتاجه OCR عند فحص مسحات عالية الدقة. بتعيين `DeviceId`، تخبر المكتبة أي بطاقة فعلية ستستخدمها—مفيد في محطات العمل التي تحتوي على عدة بطاقات GPU.

---

## الخطوة 3: تحميل الصورة لـ OCR

قبل التعرف، يجب **load image for OCR**. توفر Aspose طريقة ثابتة مريحة تدعم صيغًا متعددة (JPEG، PNG، TIFF، إلخ).

```csharp
        // Step 3: Load the image you want to recognize
        // Replace the path with your actual file location.
        var ocrImage = OcrImage.FromFile(@"C:\Images\large_document.jpg");

        // Quick sanity check – ensure the image was loaded.
        if (ocrImage == null)
        {
            Console.WriteLine("Failed to load image. Check the file path.");
            return;
        }
```

> **حالة حافة:** إذا كان حجم الصورة أكبر من 10 ميغابايت، فكر في تقليل الدقة أولاً لتجنب استنفاد ذاكرة الـ GPU. يمكنك فعل ذلك باستخدام `ocrImage.Resize(width, height)` قبل عملية التعرف.

---

## الخطوة 4: التعرف على النص من المستند

مع جاهزية المحرك وتحميل الصورة، حان الوقت **recognize text from document**. تُعيد طريقة `Recognize` كائن `OcrResult` يحتوي على النص العادي ومعلومات إضافية.

```csharp
        // Step 4: Run the OCR process on the image
        OcrResult ocrResult = gpuEngine.Recognize(ocrImage);

        // Verify that OCR succeeded
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("OCR failed or returned empty result.");
            return;
        }
```

**ما الذي يحدث في الخلفية؟**  
يقوم محرك الـ GPU بإرسال بيانات البكسل إلى نوى CUDA، التي تنفّذ التثبيت الثنائي، تجزئة الأحرف، والاستدلال عبر الشبكات العصبية—كل ذلك بالتوازي. لهذا يمكنك **run OCR on image** للملفات التي قد تستغرق ثوانٍ على الـ CPU.

---

## الخطوة 5: استخراج النص من الصورة وعرضه

أخيرًا، **extract text from image** وعرضه. يمكنك أيضًا كتابة النتيجة إلى ملف، قاعدة بيانات، أو تمريرها إلى خطوط معالجة لغة طبيعية لاحقة.

```csharp
        // Step 5: Output the recognized plain‑text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);

        // Optional: Save to a .txt file for later processing
        System.IO.File.WriteAllText(@"C:\Output\ocr_result.txt", ocrResult.Text);
    }
}
```

**الناتج المتوقع** (مقتطع للتوضيح):

```
=== OCR Result ===
Invoice #12345
Date: 03/15/2026
Total: $1,234.56
...
```

إذا نفّذت البرنامج ورأيت كتلة مشابهة، تهانينا—لقد نجحت في **run OCR on image** باستخدام تسريع الـ GPU!

---

## التعامل مع الحالات بدون GPU (Fallback)

ماذا لو كان الجهاز المستهدف لا يحتوي على GPU متوافق؟ سيتسبب مُنشئ `GpuOcrEngine` في رمي استثناء `GpuNotSupportedException`. لفّ عملية التهيئة داخل try‑catch وارجع إلى `OcrEngine` (CPU) كما يلي:

```csharp
        try
        {
            var gpuEngine = new GpuOcrEngine { DeviceId = 0 };
            // Continue with GPU workflow...
        }
        catch (GpuNotSupportedException)
        {
            Console.WriteLine("GPU not available – switching to CPU OCR.");
            var cpuEngine = new OcrEngine();
            OcrResult result = cpuEngine.Recognize(ocrImage);
            Console.WriteLine(result.Text);
        }
```

هذا النمط يضمن بقاء تطبيقك فعالًا بغض النظر عن العتاد، وهو اعتبار مهم للنشر السحابي.

---

## مثال كامل جاهز للتنفيذ (Copy‑Paste)

فيما يلي **البرنامج بالكامل**—بدون أجزاء مفقودة، فقط استبدل مسارات الملفات بما يناسبك.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Namespace for GPU support

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Create a GPU‑enabled OCR engine
        GpuOcrEngine gpuEngine;
        try
        {
            gpuEngine = new GpuOcrEngine { DeviceId = 0 }; // set GPU device ID
        }
        catch (GpuNotSupportedException)
        {
            Console.WriteLine("GPU not detected. Falling back to CPU engine.");
            var cpuEngine = new OcrEngine();
            RunCpuOcr(cpuEngine);
            return;
        }

        // 2️⃣ Load image for OCR
        var ocrImage = OcrImage.FromFile(@"C:\Images\large_document.jpg");
        if (ocrImage == null)
        {
            Console.WriteLine("Unable to load image – check the path.");
            return;
        }

        // 3️⃣ Recognize text from document
        OcrResult ocrResult = gpuEngine.Recognize(ocrImage);
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("OCR returned no text.");
            return;
        }

        // 4️⃣ Extract text from image and output
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        System.IO.File.WriteAllText(@"C:\Output\ocr_result.txt", ocrResult.Text);
    }

    // Helper for CPU fallback
    static void RunCpuOcr(OcrEngine cpuEngine)
    {
        var img = OcrImage.FromFile(@"C:\Images\large_document.jpg");
        var result = cpuEngine.Recognize(img);
        Console.WriteLine("=== CPU OCR Result ===");
        Console.WriteLine(result.Text);
    }
}
```

> **ملاحظة:** الكود أعلاه يقوم تلقائيًا **extracts text from image** ويكتب النتيجة إلى `ocr_result.txt`. عدّل المسارات حسب الحاجة.

---

## الأسئلة المتكررة والنصائح

| السؤال | الجواب |
|----------|--------|
| *هل أحتاج إلى برنامج تشغيل NVIDIA محدد؟* | نعم—يوصى بـ CUDA 11.x أو أحدث. راجع ملاحظات إصدار Aspose للتوافق الدقيق. |
| *هل يمكنني معالجة عدة صور بشكل متزامن؟* | بالتأكيد. غلف استدعاء OCR داخل حلقة `Parallel.ForEach`، لكن احرص على مراقبة حدود ذاكرة الـ GPU. |
| *ماذا لو كان ناتج OCR يحتوي على أحرف مشوهة؟* | جرّب تعديل ما قبل المعالجة: `ocrImage.Binarize()` أو `ocrImage.Deskew()` قبل التعرف. |
| *هل هناك طريقة لتقليل نموذج اللغة؟* | عيّن `gpuEngine.Language = OcrLanguage.English;` لتسريع المعالجة إذا كنت تحتاج الإنجليزية فقط. |

---

## الخلاصة

أصبح لديك الآن **حل كامل من البداية إلى النهاية** لـ **run OCR on image**. 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}